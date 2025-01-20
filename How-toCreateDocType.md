# How to Create a DocType in Frappe

A **DocType** in Frappe is a fundamental building block for defining database tables, business logic, and forms. Follow these steps to create a new DocType in Frappe.

---

## Step 1: Open the Frappe Developer Module
1. Log in to your Frappe/ERPNext site as an Administrator or a user with Developer permissions.
2. Navigate to the **Developer** module in the sidebar.
3. Select **DocType** from the list.

---

## Step 2: Create a New DocType
1. Click the **New** button in the DocType list view.
2. Fill in the required fields:
   - **Name**: Enter a name for the DocType (e.g., `Customer Feedback`).
   - **Module**: Select the module where the DocType will belong.
   - **Is Custom?**: Enable this if the DocType is specific to your custom app.
3. Configure additional options as needed:
   - **Allow Import**: Enable if you want to allow data import for this DocType.
   - **Track Changes**: Enable if you want to maintain a log of changes.
   - **Has Attachments**: Enable to allow file attachments.

---

## Step 3: Define Fields
1. In the **Fields** table, define the fields for the DocType.
   - **Label**: The display name of the field.
   - **Fieldname**: Automatically generated from the label but can be customized.
   - **Fieldtype**: Choose the field type (e.g., `Data`, `Date`, `Select`, `Table`).
   - **Options**: Configure specific options (e.g., for `Select`, provide comma-separated values).
   - **Mandatory**: Mark fields that are required.
2. Repeat for all the fields you need.

---

## Step 4: Configure Permissions
1. Scroll to the **Role Permissions** section.
2. Add roles and define their permissions (e.g., Read, Write, Create, Delete).
3. Fine-tune permissions based on your application’s needs.

---

## Step 5: Save and Publish
1. Click **Save** to save the new DocType.
2. If required, enable the **Custom** option or publish the DocType to make it available for use.

---

## Step 6: Customize the DocType (Optional)
You can further enhance the DocType by adding:

- **Custom Scripts**: For client-side logic.
- **Hooks**: To execute server-side code during lifecycle events (e.g., before save, after submit).
- **Workflows**: For approval processes and task management.

---

## Step 7: Add the DocType to a Module
1. Open the `desktop.py` file of your app.
2. Add the DocType to the module's configuration to make it visible on the desk.

Example:
```python
# desktop.py
module_page = {
    "label": "My Module",
    "icon": "octicon octicon-file-directory",
    "items": [
        {
            "type": "doctype",
            "name": "Customer Feedback",
            "label": "Customer Feedback",
            "description": "Manage customer feedback."
        }
    ]
}
```

---

## Step 8: Test the DocType
1. Navigate to the newly created DocType from the desk.
2. Create a new record and ensure the fields, permissions, and logic work as expected.

---

Following these steps will help you create and configure a new DocType in Frappe successfully. Let me know if additional details are needed!
