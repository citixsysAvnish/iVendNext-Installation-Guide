# Getting Started with Frappe Development

## Prerequisites
Ensure your system meets the following requirements:

### Supported Operating Systems
- Linux
- macOS
- WSL (Windows Subsystem for Linux)

### Software Requirements
- Python 3.10 or later  
- Node.js (v16 or later)
- npm or yarn (Node.js package manager)
- Redis (for caching and real-time updates)
- MariaDB 10.6 or later
- wkhtmltopdf (optional, for PDF generation)
- Yarn (for JavaScript dependencies)

### Package Managers
- `pip` (Python package manager)
- `virtualenv` (for environment isolation)

---

## Step 1: Install Bench
Bench is a command-line tool for managing Frappe apps and sites.

### Install Bench
```bash
pip install frappe-bench
```

### Verify Installation
```bash
bench --version
```

---

## Step 2: Initialize a Bench Directory
Create a directory for the Frappe project:

```bash
bench init my-bench --frappe-branch version-14
cd my-bench
```

Replace `version-14` with the desired Frappe branch.

---

## Step 3: Create a New Site
A "site" is where the app runs within the Frappe framework.

```bash
bench new-site mysite.localhost
```

- Enter the **MySQL root password** when prompted.
- Set an admin password for the site.

---

## Step 4: Install Frappe Apps
Install apps (such as ERPNext or custom apps) on the site.

```bash
bench get-app erpnext --branch version-14
bench --site mysite.localhost install-app erpnext
```

---

## Step 5: Start the Development Server
Run the development server to access the site.

```bash
bench start
```

Open a browser and go to `http://localhost:8000`.

---

## Step 6: Create a Custom App (Optional)
To build a custom application:

1. Create a new app:
   ```bash
   bench new-app my_custom_app
   ```

2. Install the app on the site:
   ```bash
   bench --site mysite.localhost install-app my_custom_app
   ```

---

## Step 7: Explore Frappe Development
Start customizing and extending the application:

1. **DocTypes**: For database models and business logic.
2. **Custom Scripts**: For client-side interactions.
3. **Hooks**: To integrate events and lifecycle methods.
4. **Web Pages**: For frontend content.
5. **APIs**: Utilize built-in REST and GraphQL capabilities.

---

## Development Tips
- Use `bench console` for interactive Python debugging.
- Run `bench build` to recompile assets after modifying JavaScript or CSS files.
- Use `bench migrate` to apply changes after modifying DocTypes or schemas.
