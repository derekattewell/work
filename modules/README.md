# Modules

This directory contains standalone Marketo modules that can be inserted into existing templates.

## When to Use Modules vs Templates

| Use Case | What to Create | Location |
|----------|----------------|----------|
| Building a brand new email structure | Complete template | `templates/` |
| Adding a new section type to existing template | Standalone module | `modules/` |
| Creating a reusable component | Standalone module | `modules/` |
| One-off email with unique structure | Complete template | `templates/` |

## Directory Structure

```
modules/
├── headers/      # Header modules (logos, navigation)
├── content/      # Text, typography, sections
├── buttons/      # CTA button variations
├── layouts/      # Multi-column layouts, image+text combos
├── utility/      # Spacers, dividers, utility elements
└── README.md     # This file
```

## Module Requirements

Every module must:

1. **Be a complete `<tr>` element** with `mktoModule` class
2. **Have a unique ID** that won't conflict with existing modules
3. **Include `mktoname`** for the Marketo editor display name
4. **Be self-contained** - no dependencies on external CSS or other modules

### Module Template

```html
<tr class="mktoModule" id="unique-module-id" mktoname="Display Name in Editor">
  <td>
    <!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="unique-module-id-outlook" role="presentation" style="width:600px;" width="600" bgcolor="#FFFFFF" ><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly;"><![endif]-->

    <div class="unique-module-id" style="background:#fff;background-color:#fff;margin:0 auto;max-width:600px">
      <!-- Module content here -->
    </div>

    <!--[if mso | IE]></td></tr></table><![endif]-->
  </td>
</tr>
```

## Naming Conventions

### Module IDs

Follow this pattern: `[category]-[description]` or `[category]-[description]--[variant]`

**Examples:**
- `content-single-column`
- `content-single-column--grey`
- `layout-two-col-image-left`
- `button-primary--sr`
- `button-primary--itrg`

### File Names

Match the module ID: `[module-id].html`

**Examples:**
- `content-single-column.html`
- `layout-two-col-image-left.html`
- `button-primary--sr.html`

## Adding a Module to Existing Template

1. **Copy the module code** from the `.html` file
2. **Paste into the template** inside the `<tbody class="mktoContainer">` element
3. **Ensure no ID conflicts** with existing modules
4. **Add any required variables** to the template's `<head>` section

### Variable Scoping

For module-specific variables, use `mktomodulescope="true"`:

```html
<meta id="module-id__variable-name" class="mktoString" mktoname="Display Name" default="value" mktomodulescope="true">
```

This allows the same module to be used multiple times with different values.

## Testing Modules

### Standalone Testing

Create a minimal test template:

```html
<!doctype html>
<html lang="en" dir="auto" xmlns="http://www.w3.org/1999/xhtml" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
<head>
  <!-- Required head content -->
  <!-- Module variables -->
</head>
<body style="margin:0;padding:24px 0;background-color:#ededed">
  <div style="background-color:#ededed">
    <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation">
      <tbody class="mktoContainer">
        <!-- Paste module here for testing -->
      </tbody>
    </table>
  </div>
</body>
</html>
```

### Integration Testing

After adding to the main template:
1. Upload to Marketo
2. Verify module appears in editor
3. Test all editable regions
4. Check rendering in email clients

## Existing Module Categories (from v1 Style Guide)

Reference `.claude/styles/v1.md` for the complete module catalog with IDs and descriptions.

### Headers
- `header-sr` - SoftwareReviews primary
- `header-itrg` - Info-Tech primary
- `header-advisory` - Advisory centered

### Content
- `typography` - Full typography showcase
- `typography--grey` - Grey background variant
- `typography-SR` - SR green background
- `typography-ITRG` - ITRG blue background
- `section-grey` - Grey section without button
- `section-grey-with-button` - Grey section with CTA

### Buttons
- `button` - Primary SR green
- `button-blue` - Primary ITRG blue
- `two-col-buttons` - Dual buttons (SR)
- `two-col-buttons-blue` - Dual buttons (ITRG)

### Layouts
- `two-col-text-then-image` - Text left, image right
- `two-col-image-then-text` - Image left, text right
- `two-col-title-then-image` - Title left, image right
- `three-col-numbers-vertical` - Step indicators

### Utility
- `spacer` - Transparent spacing
- `hr-0` - Section divider
