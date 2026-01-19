# Marketo Email Templates

A repository for building and managing Marketo email templates with HTML.

## Project Structure

```
├── .claude/                           # Development guidelines
│   ├── marketo-email-development.md   # Functional best practices & Marketo syntax
│   └── styles/                        # Versioned style guides
│       ├── README.md                  # How to use style versions
│       └── v1.md                      # Style guide v1 (active)
├── templates/                         # Complete email templates
│   └── README.md                      # Template guidelines
├── modules/                           # Standalone modules for insertion
│   ├── README.md                      # Module guidelines
│   ├── headers/                       # Header modules
│   ├── content/                       # Content/typography modules
│   ├── buttons/                       # CTA button modules
│   ├── layouts/                       # Multi-column layouts
│   └── utility/                       # Spacers, dividers
├── assets/
│   └── images/                        # Image assets
└── README.md
```

## Workflow: Templates vs Modules

| Task | What to Create | Location |
|------|----------------|----------|
| Brand new email structure | Complete template | `templates/` |
| New section for existing template | Standalone module | `modules/` |
| Reusable component | Standalone module | `modules/` |
| Variant of existing module | Standalone module | `modules/` |

### Creating a New Template

1. Reference `.claude/marketo-email-development.md` for technical requirements
2. Reference `.claude/styles/v1.md` (or specified version) for visual styles
3. Save complete template in `templates/`

### Creating a New Module

1. Reference the development guide for module structure requirements
2. Reference the style guide for component styles
3. Save module in appropriate category folder under `modules/`
4. Add required variables documentation

See `modules/README.md` for detailed module creation guidelines.

## Development System

### 1. Functional Development Guide

**File:** `.claude/marketo-email-development.md`

Covers all technical aspects:
- Document structure and required elements
- Email client compatibility (Outlook, Gmail, Apple Mail, etc.)
- MSO conditional comments for Outlook
- CSS reset and client-specific fixes
- Table-based layout patterns
- Marketo-specific syntax
- Creating modules vs templates
- Accessibility and security
- Testing and validation

### 2. Style Guides (Versioned)

**Directory:** `.claude/styles/`

Visual style definitions:
- Brand colors and usage
- Typography scale
- Spacing system
- Layout grid
- Component styles
- Module catalog

## Style Guide Versions

| Version | File | Status | Description |
|---------|------|--------|-------------|
| v1 | `styles/v1.md` | **Active** | Initial version from existing SR/ITRG template |

### Creating New Versions

To iterate on styles:

> "Create style guide v2 based on v1 with [your changes]"

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
