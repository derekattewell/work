# Marketo Email Templates

A repository for building and managing Marketo email templates with HTML.

## Project Structure

```
├── .claude/                           # Development guidelines
│   ├── marketo-email-development.md   # Functional best practices & Marketo syntax
│   └── styles/                        # Versioned style guides
│       ├── README.md                  # How to use style versions
│       └── v1.md                      # Style guide v1 (active)
├── templates/                         # Complete email templates (to be created)
├── modules/                           # Reusable Marketo modules (to be created)
├── assets/
│   └── images/                        # Image assets
└── README.md
```

## Development System

This repository uses a two-part guide system:

### 1. Functional Development Guide (`.claude/marketo-email-development.md`)

Covers all technical aspects of email development:
- Document structure and required elements
- Email client compatibility (Outlook, Gmail, Apple Mail, etc.)
- MSO conditional comments for Outlook
- CSS reset and client-specific fixes
- Table-based layout patterns
- Typography and web font loading
- Image best practices
- Bulletproof button patterns
- Responsive design techniques
- Marketo-specific syntax
- Accessibility requirements
- Security practices
- Testing and validation checklist

### 2. Style Guides (`.claude/styles/`)

Versioned visual style definitions:
- Brand colors and usage
- Typography scale (fonts, sizes, weights)
- Spacing system
- Layout grid and column widths
- Border radius values
- Component styles (buttons, dividers, etc.)
- Module catalog
- Image assets and URLs

## Style Guide Versions

| Version | File | Status | Description |
|---------|------|--------|-------------|
| v1 | `styles/v1.md` | **Active** | Initial version from existing SR/ITRG template |

### Creating New Versions

To iterate on styles, request a new version:

> "Create style guide v2 based on v1 with [your changes]"

Previous versions are preserved for reference or rollback.

## Quick Reference (from v1)

### Brand Colors
- SR Green: `#24842e`
- ITRG Blue: `#216aa5`
- Grey background: `#f6f6f6`
- Outer background: `#ededed`

### Typography
- Headings: `Montserrat, Helvetica, Arial, sans-serif`
- Body: `Roboto, Helvetica, Arial, sans-serif`

### Dimensions
- Container width: 600px
- Content padding: 24px 47px
- Button padding: 12px 22px
- Border radius: 5px (buttons), 20px (cards)

## Resources

- [Marketo Email Template Syntax](https://experienceleague.adobe.com/docs/marketo/using/product-docs/email-marketing/general/email-editor-2/email-template-syntax.html)
- [Can I Email](https://www.caniemail.com/) - Email client CSS support reference
- [Litmus](https://www.litmus.com/) - Email testing
