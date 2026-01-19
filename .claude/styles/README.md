# Style Guide Versions

This directory contains versioned style guides for email template development. Each version is a complete style definition that can be used independently.

## How to Use

When building a template, specify which style guide version to use:

> "Build an email template using **style guide v1**"

Or when iterating:

> "Create a new style guide v2 based on v1 but with [changes]"

## Available Versions

| Version | File | Description | Status |
|---------|------|-------------|--------|
| v1 | `v1.md` | Initial version extracted from existing SR/ITRG template | Available |
| v2 | `v2.md` | Floating elements aesthetic with pill buttons and generous spacing | **Active** |

## Creating New Versions

When creating a new style guide version:

1. **Copy the previous version** as a starting point
2. **Document all changes** in the changelog section
3. **Update the version number** and date at the top
4. **Keep previous versions** for reference/rollback

### Naming Convention

- `v1.md` - First version
- `v2.md` - Second iteration
- `v3.md` - Third iteration
- etc.

### What to Include in a Style Guide

Each style guide should define:

- Brand variants and when to use them
- Complete color palette with hex values
- Typography scale (fonts, sizes, weights, line heights)
- Spacing system (padding, margins, gaps)
- Layout grid (container widths, column percentages)
- Border radius values
- Component styles (buttons, dividers, images)
- Module catalog (available modules and their purposes)
- Image assets and URLs
- Footer content and links
- Marketo variables

## Switching Between Versions

To switch which style guide is active for new template development:

1. Reference the desired version in your request
2. Or update this README to mark a different version as "Active"

## Version History

| Date | Version | Changes |
|------|---------|---------|
| Jan 2026 | v1 | Initial extraction from production template |
| Jan 2026 | v2 | Floating elements aesthetic, pill buttons, larger typography, generous spacing |
