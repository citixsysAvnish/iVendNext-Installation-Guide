# iVendNext Environment Setup Guide

Stack: Ubuntu 24.04, Python 3.12, Node 24.21.0, MariaDB 10.11, Redis 7.0, bench 5.25.9, Frappe framework v15 (iVendNext fork).

## 1. Prerequisites

Install system dependencies (Python 3.12, MariaDB, Redis, Node via nvm, yarn, wkhtmltopdf) and `frappe-bench`:

```bash
pip install frappe-bench
```

## 2. Initialize the bench (pulls the iVendNext framework fork, not vanilla Frappe)

```bash
bench init ivendnext-bench --frappe-branch release_1.0_unencrypted \
    --frappe-path https://github.com/ivendnext/iVendFramework.git
cd ivendnext-bench
```

## 3. Get the iVendNext apps (all pinned to `release_1.0_unencrypted`)

```bash
bench get-app erpnext https://github.com/ivendnext/iVendNext.git --branch release_1.0_unencrypted
bench get-app hw_integration https://github.com/ivendnext/hw_integration.git --branch release_1.0_unencrypted
bench get-app ivend_loyality https://github.com/ivendnext/ivend_loyality.git --branch release_1.0_unencrypted
bench get-app ivendnext_pos https://github.com/ivendnext/iVend-POS.git --branch release_1.0_unencrypted
```

Note the repo/app name mismatches: `erpnext` app ↔ `iVendNext.git` repo, `ivendnext_pos` app ↔ `iVend-POS.git` repo.

## 4. Create the site

```bash
bench new-site ivendnext.local --db-type mariadb
```

This prompts for/creates the MariaDB root password and a per-site DB password (stored in `sites/ivendnext.local/site_config.json`, not recoverable later if lost).

## 5. Install apps in dependency order

```bash
bench --site ivendnext.local install-app erpnext
bench --site ivendnext.local install-app hw_integration
bench --site ivendnext.local install-app ivend_loyality
bench --site ivendnext.local install-app ivendnext_pos
```

## 6. Set the default site and dev config

```bash
bench use ivendnext.local
bench set-config -g developer_mode 1
```

## 7. Map the hostname locally

Add to `/etc/hosts`:

```
127.0.0.1 ivendnext.local
```

## 8. Set ports / webserver config (as needed)

`sites/common_site_config.json` in this bench uses:

- `webserver_port`: 8001
- `socketio_port`: 9001
- `redis_cache`: `redis://127.0.0.1:1101`
- `redis_queue`: `redis://127.0.0.1:1301`

Adjust with `bench set-config` if the defaults (8000/9000/13000s) conflict with something else on the box.

## 9. Start the bench

```bash
bench start
```

This runs (via Procfile/honcho): web (`bench serve --port 8001`), socketio, redis_cache, redis_queue, scheduler, watcher (esbuild), and a worker.

## 10. Verify

```bash
curl -H "Host: ivendnext.local" http://127.0.0.1:8001/
```

Should return `200`. **Important:** the site must be accessed by hostname (`http://ivendnext.local:8001`), not by raw IP — Frappe routes by `Host` header, and hitting `127.0.0.1` directly returns 404 unless `serve_default_site` is set.

## 11. Log in

Default user is **Administrator**; set/reset its password with:

```bash
bench --site ivendnext.local set-admin-password <password>
```

## Restoring a database backup

```bash
# Always snapshot the current DB first
bench --site ivendnext.local backup

# Restore the target backup
bench --site ivendnext.local restore /path/to/backup-database.sql.gz --mariadb-root-password '<root-password>'
```

If restore fails partway with a MySQL syntax error, check the archive isn't truncated before assuming a data issue:

```bash
gunzip -t /path/to/backup-database.sql.gz
```

If it reports "unexpected end of file", the transfer was incomplete — re-download the file rather than debugging SQL. If a restore fails partway, the site DB is left in an inconsistent state; restore the pre-restore backup taken above to recover.
