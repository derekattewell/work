# Templates

This directory contains complete, standalone Marketo email templates.

## When to Create a New Template

Create a new template when you need:
- A completely new email structure
- Different module arrangement than existing templates
- A specialized template for a specific campaign type
- A template with unique header/footer requirements

## When to Create a Module Instead

Create a module (in `modules/`) when you need:
- A new section type for an existing template
- A reusable component across multiple templates
- A variant of an existing module (e.g., different color scheme)

## Template Structure

Every template must include:

### 1. Required DOCTYPE and Namespaces

```html
<!doctype html>
<html lang="en" dir="auto" xmlns="http://www.w3.org/1999/xhtml" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
```

### 2. Head Section

- Meta tags (charset, viewport, IE compatibility)
- Office document settings (MSO conditional)
- Google Fonts loading (link + @import)
- MSO font-face declarations
- CSS resets and responsive styles
- Marketo variables

### 3. Body Structure

```html
<body style="margin:0;padding:24px 0;word-spacing:normal;background-color:#ededed">
  <div style="background-color:#ededed" lang="en" dir="auto">
    <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation">
      <tbody id="template" class="mktoContainer">
        <!-- Modules go here -->
      </tbody>
    </table>

    <!-- Footer (outside mktoContainer if fixed) -->
  </div>
</body>
```

### 4. Required Elements

- At least one header module
- Content modules as needed
- Footer with legal links and social icons

## Template Naming

Use descriptive names that indicate the template's purpose:

- `master.html` - Main template with all modules
- `newsletter.html` - Newsletter-specific layout
- `promotional.html` - Promotional email layout
- `transactional.html` - Transactional email layout

## Template Checklist

Before uploading to Marketo:

- [ ] All module IDs are unique
- [ ] All variable IDs are unique
- [ ] MSO conditionals are properly opened and closed
- [ ] Footer includes required legal links
- [ ] All images have alt attributes
- [ ] All external links use HTTPS
- [ ] All links have `target="_blank" rel="noopener"`
- [ ] Template validates as HTML
- [ ] Tested in Litmus/Email on Acid

## Reference

- **Functional guide:** `.claude/marketo-email-development.md`
- **Style guide:** `.claude/styles/v1.md` (or current version)
- **Module catalog:** `modules/README.md`
