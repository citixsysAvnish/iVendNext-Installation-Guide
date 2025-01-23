# Complete List of Bench Commands

## **Setup & Configuration**

| Command                                     | Description                                                |
|---------------------------------------------|------------------------------------------------------------|
| `bench init <folder_name>`                  | Initialize a new bench instance.                          |
| `bench new-site <site_name>`                | Create a new site.                                         |
| `bench use <site_name>`                     | Set the default site for the bench.                       |
| `bench set-config <key> <value>`            | Set configuration options (e.g., developer mode).          |
| `bench get-config <key>`                    | Get the value of a configuration option.                  |
| `bench setup requirements`                  | Install Python and Node.js dependencies.                  |
| `bench setup supervisor`                    | Setup supervisor for process management.                  |
| `bench setup nginx`                         | Generate NGINX configuration.                             |
| `bench setup redis`                         | Configure Redis caching.                                   |

---

## **Development Commands**

| Command                                     | Description                                                |
|---------------------------------------------|------------------------------------------------------------|
| `bench start`                               | Start development server.                                  |
| `bench migrate`                             | Apply schema changes for all sites.                       |
| `bench update`                              | Update apps and dependencies.                             |
| `bench build`                               | Build JS and CSS assets for all apps.                     |
| `bench watch`                               | Watch and compile assets on file changes.                 |
| `bench backup`                              | Take a backup of the site database and files.             |
| `bench restore <sql_file>`                  | Restore a site from a SQL backup file.                    |
| `bench reinstall`                           | Reinstall the site (erases all data).                     |
| `bench reload-doc <module> <doctype> <name>`| Reload a specific DocType or module.                      |

---

## **App Management**

| Command                                     | Description                                                |
|---------------------------------------------|------------------------------------------------------------|
| `bench get-app <app_name>`                  | Clone an app from GitHub.                                  |
| `bench new-app <app_name>`                  | Create a new app.                                          |
| `bench install-app <app_name>`              | Install an app on the current site.                       |
| `bench uninstall-app <app_name>`            | Uninstall an app from the current site.                   |
| `bench remove-app <app_name>`               | Remove an app entirely from the bench.                    |
| `bench export-fixtures`                     | Export fixtures for a custom app.                         |
| `bench import-fixtures`                     | Import fixtures for a custom app.                         |

---

## **Site Management**

| Command                                     | Description                                                |
|---------------------------------------------|------------------------------------------------------------|
| `bench --site <site_name> execute <method>` | Execute Python method for a site.                         |
| `bench --site <site_name> clear-cache`      | Clear cache for the site.                                  |
| `bench --site <site_name> clear-website-cache`| Clear website cache for the site.                        |
| `bench --site <site_name> backup`           | Backup a specific site.                                    |
| `bench --site <site_name> migrate`          | Apply schema changes for a specific site.                 |
| `bench --site <site_name> set-maintenance-mode on/off` | Enable or disable maintenance mode.                      |

---

## **Testing**

| Command                                     | Description                                                |
|---------------------------------------------|------------------------------------------------------------|
| `bench run-tests`                           | Run tests for all apps.                                    |
| `bench run-tests --doctype <doctype>`       | Run tests for a specific DocType.                         |
| `bench run-tests --app <app_name>`          | Run tests for a specific app.                             |
| `bench --site <site_name> run-tests`        | Run tests for a specific site.                            |

---

## **Asset Management**

| Command                                     | Description                                                |
|---------------------------------------------|------------------------------------------------------------|
| `bench build`                               | Build JS and CSS assets for all apps.                     |
| `bench watch`                               | Watch and build assets on file changes.                   |
| `bench clear-cache`                         | Clear cache for all sites.                                |
| `bench clear-website-cache`                 | Clear website cache for all sites.                        |
| `bench setup requirements`                  | Install required Node.js and Python packages.             |

---

## **Utility Commands**

| Command                                     | Description                                                |
|---------------------------------------------|------------------------------------------------------------|
| `bench version`                             | Show the current version of Bench.                        |
| `bench console`                             | Start a Python shell with Frappe environment loaded.       |
| `bench doctor`                              | Check system status and report errors.                    |
| `bench show-config`                         | Display the configuration settings.                       |
| `bench shell`                               | Open the shell for database access.                       |
| `bench restart`                             | Restart bench processes.                                   |

---

## **Common Scenarios**

| Task                                        | Command                                                    |
|---------------------------------------------|------------------------------------------------------------|
| **Create a new app**                        | `bench new-app <app_name>`                                 |
| **Install an app**                          | `bench install-app <app_name>`                             |
| **Export custom fields/fixtures**           | `bench export-fixtures`                                    |
| **Run Frappe in developer mode**            | `bench set-config developer_mode 1`                        |
| **Backup a specific site**                  | `bench --site <site_name> backup`                          |
| **Restore a site from a SQL backup**        | `bench --site <site_name> restore <sql_file>`              |

---

This list includes most of the essential commands for managing Frappe/ERPNext environments. For additional commands or detailed usage, refer to the official documentation or run `bench --help`. 
