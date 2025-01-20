# How to Show Uploaded Image Preview in DocType

Frappe allows you to display a preview of uploaded images in a DocType form. Follow these steps to enable image previews:

---

## Step 1: Add an Image Field
1. Open the DocType configuration in the **Developer** module.
2. Add a new field with the following properties:
   - **Label**: Image
   - **Fieldtype**: Image
   - **Options**: Specify the fieldname of the image file (e.g., `attach_image`).

Example:
```json
{
    "fieldname": "image",
    "label": "Image",
    "fieldtype": "Image",
    "options": "attach_image"
}
```

---

## Step 2: Add an Attachment Field
1. Add another field to handle the image upload:
   - **Label**: Attach Image
   - **Fieldtype**: Attach

Example:
```json
{
    "fieldname": "attach_image",
    "label": "Attach Image",
    "fieldtype": "Attach"
}
```

---

## Step 3: Test the Setup
1. Navigate to the DocType form.
2. Upload an image using the **Attach Image** field.
3. The uploaded image will be displayed in the **Image** field as a preview.

---

By adding these fields, you can ensure a smooth user experience with real-time image previews in your DocType forms.
