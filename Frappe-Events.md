# Frappe Framework Extensibility Guide

Frappe Framework provides an extensibility mechanism using events, allowing developers to hook into various points of the framework's lifecycle. This makes it easier to customize and extend Frappe-based applications without modifying the core code. Here’s an overview of Frappe's extensibility events:

---

## 1. DocType Events
DocType events are triggered at different stages of a document's lifecycle. Define these hooks in the `hooks.py` file of your app.

### Examples of DocType Events:
- **Before Save** (`before_save`)
- **After Save** (`after_save`)
- **Before Insert** (`before_insert`)
- **After Insert** (`after_insert`)
- **On Update** (`on_update`)
- **On Cancel** (`on_cancel`)
- **On Trash** (`on_trash`)

### Example in `hooks.py`:
```python
# hooks.py
doc_events = {
    "Sales Invoice": {
        "on_submit": "my_app.events.sales_invoice_on_submit",
        "before_save": "my_app.events.sales_invoice_before_save"
    }
}
```

### Example Event Handler in `events.py`:
```python
# events.py
def sales_invoice_on_submit(doc, method):
    # Perform actions after Sales Invoice submission
    frappe.msgprint(f"Sales Invoice {doc.name} has been submitted!")

def sales_invoice_before_save(doc, method):
    # Perform actions before Sales Invoice is saved
    if not doc.customer:
        frappe.throw("Customer is required!")
```

---

## 2. Custom Scripts
Custom scripts add client-side logic for specific forms or DocTypes.

### Client Events:
Triggered by form interactions on the client side.

### Supported Events:
- `onload`
- `refresh`
- `validate`
- `before_save`
- `after_save`

### Example Custom Script (Client-Side):
```javascript
// Custom Script for Sales Invoice
frappe.ui.form.on('Sales Invoice', {
    refresh: function(frm) {
        frappe.msgprint(`Welcome to Sales Invoice: ${frm.doc.name}`);
    },
    validate: function(frm) {
        if (!frm.doc.customer) {
            frappe.throw('Customer is mandatory!');
        }
    }
});
```

---

## 3. Scheduler Events
Frappe provides scheduled tasks that run at specific intervals, defined in `hooks.py`.

### Example in `hooks.py`:
```python
# hooks.py
scheduler_events = {
    "all": [
        "my_app.tasks.all"
    ],
    "daily": [
        "my_app.tasks.daily"
    ],
    "hourly": [
        "my_app.tasks.hourly"
    ],
    "weekly": [
        "my_app.tasks.weekly"
    ],
    "monthly": [
        "my_app.tasks.monthly"
    ]
}
```

### Example Task Function in `tasks.py`:
```python
# tasks.py
def daily():
    frappe.log_error("Daily task executed", "Scheduler Log")

def weekly():
    frappe.log_error("Weekly task executed", "Scheduler Log")
```

---

## 4. Web and API Hooks
Extend or override web requests and API endpoints.

### Override Whitelisted Methods:
```python
# hooks.py
override_whitelisted_methods = {
    "frappe.desk.doctype.event.event.get_events": "my_app.event.get_events"
}
```

### Custom Implementation in `event.py`:
```python
# event.py
def get_events(start, end, filters=None):
    # Custom logic to fetch events
    return []
```

---

## 5. Override Standard Doctype Classes
Replace the default server-side class of a DocType with your own.

### Example in `hooks.py`:
```python
# hooks.py
override_doctype_class = {
    "ToDo": "my_app.overrides.CustomToDo"
}
```

### Custom Class Implementation:
```python
# overrides.py
class CustomToDo(ToDo):
    def before_save(self):
        frappe.msgprint("This is a custom ToDo behavior!")
```

---

## 6. Custom Jinja Filters
Add custom Jinja filters for templates.

### Example in `hooks.py`:
```python
# hooks.py
jinja = {
    "methods": "my_app.utils.custom_filters"
}
```

### Custom Filter Implementation:
```python
# utils.py
def custom_uppercase(value):
    return value.upper()
```

### Usage in Jinja Template:
```jinja
{{ "hello" | custom_uppercase }}
```

---

## 7. Permissions Events
Define custom permission rules for DocTypes.

### Example in `hooks.py`:
```python
# hooks.py
permission_query_conditions = {
    "Task": "my_app.permissions.get_permission_query_conditions"
}

has_permission = {
    "Task": "my_app.permissions.has_permission"
}
```

### Custom Logic in `permissions.py`:
```python
# permissions.py
def get_permission_query_conditions(user):
    if not user == "Administrator":
        return "owner = '{0}'".format(user)

def has_permission(doc, user):
    return doc.owner == user
```

---

## 8. Page and Report Extensions
Extend or override specific Page or Report behaviors.

### Override Page Scripts:
```python
# hooks.py
page_js = {"dashboard": "public/js/dashboard.js"}
```

### Override Report Scripts:
```python
# hooks.py
report_js = {"Sales Register": "public/js/sales_register.js"}
```

---

## 9. Custom App-Specific Events
Create your own event-driven architecture using Frappe’s `publish_realtime` API.

### Publishing an Event:
```python
# Example in Python
frappe.publish_realtime("event_name", {"message": "Hello, World!"})
```

### Listening to an Event (Client-Side):
```javascript
// Example in JavaScript
frappe.realtime.on("event_name", (data) => {
    console.log(data.message);
});
```

---

These extensibility options make Frappe powerful and adaptable to a wide range of use cases. Let me know if you'd like to explore any of these topics in more detail!
