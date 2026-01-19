# Marketo Email Templates

A repository for building and managing Marketo email templates with HTML.

## Project Structure

```
├── templates/           # Complete email templates
│   ├── base-template.html
│   └── newsletter-template.html
├── modules/             # Reusable Marketo modules
│   ├── header.html
│   ├── footer.html
│   ├── content-blocks.html
│   └── cta-buttons.html
├── components/          # Shared components and styles
│   └── email-reset.css
├── assets/
│   └── images/          # Image assets
└── docs/                # Documentation
    └── marketo-syntax-reference.md
```

## Quick Start

1. Choose a template from `templates/` as your starting point
2. Copy modules from `modules/` into your template as needed
3. Customize variables in the `<head>` section
4. Edit content within `mktoText` and `mktoImg` elements
5. Test and upload to Marketo

## Templates

### Base Template (`base-template.html`)
A comprehensive starting template with:
- Color and font variables
- Header with logo
- Hero image section
- Main content area
- Two-column layout
- Footer with social icons

### Newsletter Template (`newsletter-template.html`)
A newsletter-focused template featuring:
- Featured article hero section
- Two-column article grid
- CTA banner
- Modern, card-based design

## Available Modules

### Headers (`modules/header.html`)
- Logo Only
- Logo with Navigation
- Minimal (white background)

### Footers (`modules/footer.html`)
- Full Footer with social icons
- Minimal Footer
- Dark Footer

### Content Blocks (`modules/content-blocks.html`)
- Single Column Text
- Single Column with Image
- Two Column Equal
- Three Column
- Image Left/Right layouts
- Quote/Testimonial
- Dividers and Spacers

### CTA Buttons (`modules/cta-buttons.html`)
- Primary Button (centered)
- Secondary Button (outlined)
- Dual Buttons
- CTA with Supporting Text
- Full-width Banner CTA
- Text Link CTA

## Marketo Syntax Quick Reference

### Variables (in `<head>`)
```html
<meta class="mktoColor" id="primaryColor" mktoName="Primary Color" default="#0066cc">
<meta class="mktoString" id="fontFamily" mktoName="Font Family" default="Arial, sans-serif">
<meta class="mktoBoolean" id="showSection" mktoName="Show Section" default="true" true_value="block" false_value="none">
```

### Editable Text
```html
<div class="mktoText" id="uniqueId" mktoName="Display Name">
    <p>Editable content here</p>
</div>
```

### Editable Images
```html
<div class="mktoImg" id="uniqueId" mktoName="Display Name" mktoImgWidth="600">
    <img src="placeholder.jpg" alt="Description">
</div>
```

### Modules
```html
<tr class="mktoModule" id="uniqueId" mktoName="Module Name">
    <td>Module content</td>
</tr>
```

### Common Tokens
- `{{lead.First Name}}` - Lead's first name
- `{{system.viewAsWebpageLink}}` - View in browser
- `{{system.unsubscribeLink}}` - Unsubscribe link
- `{{system.company}}` - Company name

See `docs/marketo-syntax-reference.md` for complete documentation.

## Best Practices

### Email-Specific CSS
- Always use inline styles (email clients have limited CSS support)
- Use tables for layout (flexbox/grid not supported)
- Include CSS reset for consistent rendering
- Test on multiple email clients

### Marketo-Specific
- Use unique IDs for all editable elements
- Provide clear, descriptive `mktoName` values
- Set sensible default values for variables
- Group related modules with consistent naming

### Responsive Design
- Use `max-width: 600px` for main container
- Include responsive media queries (for clients that support them)
- Use `class="stack-column"` for columns that should stack on mobile
- Test on both desktop and mobile

## Testing

Before uploading to Marketo:

1. **Validate HTML** - Ensure valid markup
2. **Check unique IDs** - All element IDs must be unique
3. **Test rendering** - Use tools like Litmus or Email on Acid
4. **Verify tokens** - Ensure all Marketo tokens are correct
5. **Preview in Marketo** - Test the editor functionality

## Uploading to Marketo

1. Go to **Design Studio** > **Email Templates**
2. Click **New** > **New Template**
3. Enter a name and paste your HTML code
4. Click **Create**
5. Preview and test all editable regions
6. Approve the template for use

## Resources

- [Marketo Email Template Syntax](https://experienceleague.adobe.com/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax.html)
- [Email Development Best Practices](https://www.campaignmonitor.com/dev-resources/guides/coding-html-emails/)
- [Can I Email](https://www.caniemail.com/) - Email client CSS support reference
