# Marketo Email Templates

A repository for building and managing Marketo email templates with HTML.

## Project Structure

```
├── .claude/                    # Development guidelines
│   ├── marketo-email-development.md   # Functional best practices & Marketo syntax
│   └── style-guide.md                 # Brand style guidelines (WIP)
├── templates/                  # Complete email templates (to be created)
├── modules/                    # Reusable Marketo modules (to be created)
├── assets/
│   └── images/                 # Image assets
└── README.md
```

## Development Guidelines

### Skill Files (`.claude/`)

This repository uses skill files to maintain consistency when building email templates:

1. **`marketo-email-development.md`** - Comprehensive guide covering:
   - Document structure and required elements
   - Email client compatibility (Outlook, Gmail, Apple Mail, etc.)
   - MSO conditional comments for Outlook
   - CSS reset and client-specific fixes
   - Table-based layout patterns
   - Typography and web font loading
   - Image best practices
   - Bulletproof button patterns
   - Responsive design techniques
   - Marketo-specific syntax (modules, variables, editable regions)
   - Accessibility requirements
   - Security practices
   - Module naming conventions
   - Testing and validation checklist

2. **`style-guide.md`** - Brand style guidelines including:
   - Brand colors
   - Typography scale
   - Spacing system
   - Component styles
   - Image guidelines

## Key Technical Features

Based on our existing template architecture:

### Email Client Compatibility
- Full Outlook support via VML and MSO conditionals
- Gmail, Apple Mail, Yahoo Mail optimization
- Mobile-responsive design

### Marketo Integration
- Module-based architecture (`mktoModule`)
- Editable text regions (`mktoText`)
- Editable images (`mktoImg`)
- Template variables (`mktoString`, `mktoColor`, etc.)
- Module-scoped variables for repeatable sections

### Best Practices Implemented
- Bulletproof buttons that work in all clients
- Web fonts with proper fallbacks
- Accessibility compliance (ARIA, semantic structure)
- Security (rel="noopener", HTTPS only)
- 600px container width standard

## Quick Reference

### Standard Dimensions
- Container width: 600px
- Content padding: 24px 47px
- Button padding: 12px 22px
- Border radius: 5px (buttons), 20px (cards)

### Brand Colors
- SR Green: `#24842e`
- ITRG Blue: `#216aa5`
- Grey background: `#f6f6f6`
- Outer background: `#ededed`

### Font Stack
- Headings: `Montserrat, Helvetica, Arial, sans-serif`
- Body: `Roboto, Helvetica, Arial, sans-serif`

## Resources

- [Marketo Email Template Syntax](https://experienceleague.adobe.com/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax.html)
- [Can I Email](https://www.caniemail.com/) - Email client CSS support reference
- [Litmus](https://www.litmus.com/) - Email testing
