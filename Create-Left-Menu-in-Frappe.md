# How to Create a Left Menu in Frappe

Creating a custom left menu in Frappe enhances the user experience by providing easy navigation to specific modules or pages. Follow these steps to create a left menu:

---

## Step 1: Identify the Module or App
Determine which module or app the left menu will be associated with.

---

## Step 2: Modify the `config` File
1. Navigate to the `config` folder in your custom app.
2. Open or create a `desktop.py` file.
3. Define the menu items using the following structure:

Example:
```python
# desktop.py
from frappe import _

def get_data():
    return [
        {
            "module_name": "My Module",
            "color": "blue",
            "icon": "octicon octicon-file-directory",
            "type": "module",
            "label": _("My Module"),
            "items": [
                {
                    "type": "doctype",
                    "name": "Customer Feedback",
                    "label": _("Customer Feedback"),
                    "description": _("Manage customer feedback records")
                },
                {
                    "type": "page",
                    "name": "custom-dashboard",
                    "label": _("Custom Dashboard"),
                    "description": _("View custom dashboards")
                }
            ]
        }
    ]
```

---

## Step 3: Reload the App
1. Run the following command to apply changes:
   ```bash
   bench clear-cache
   bench restart
   ```
2. Refresh the browser to see the updated left menu.

---

## Step 4: Test the Menu
1. Open the module from the desk.
2. Verify that the left menu displays the configured items.
3. Check if the links navigate to the correct pages or DocTypes.

---

Creating a left menu helps organize content and improves navigation, ensuring a better user experience.
