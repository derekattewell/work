# Marketo Email Template Development Guide

This document contains all functional best practices, rendering techniques, security practices, and Marketo-specific syntax for building email templates. Reference this guide when creating or modifying any email template.

---

## Table of Contents

1. [Document Structure](#document-structure)
2. [Email Client Compatibility](#email-client-compatibility)
3. [Outlook & Microsoft Conditional Comments](#outlook--microsoft-conditional-comments)
4. [CSS Reset & Client Fixes](#css-reset--client-fixes)
5. [Table-Based Layout](#table-based-layout)
6. [Typography & Fonts](#typography--fonts)
7. [Images](#images)
8. [Buttons](#buttons)
9. [Responsive Design](#responsive-design)
10. [Marketo Syntax](#marketo-syntax)
11. [Accessibility](#accessibility)
12. [Security Practices](#security-practices)
13. [Module Naming Conventions](#module-naming-conventions)
14. [Testing & Validation](#testing--validation)

---

## Document Structure

### Required DOCTYPE and HTML Tag

Always start templates with the proper DOCTYPE and HTML tag including XML namespaces for VML (required for Outlook):

```html
<!doctype html>
<html lang="en" dir="auto" xmlns="http://www.w3.org/1999/xhtml" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
```

**Key attributes:**
- `lang="en"` - Required for accessibility and screen readers
- `dir="auto"` - Allows automatic text direction detection
- `xmlns:v` and `xmlns:o` - Required for VML support in Outlook

### Head Section Requirements

```html
<head>
  <title>Template Name</title>
  <!--[if !mso]><!-->
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <!--<![endif]-->
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">

  <!-- CSS styles here -->

  <!-- Marketo variables here -->
</head>
```

### Body Structure

```html
<body style="margin:0;padding:24px 0;word-spacing:normal;background-color:#ededed">
  <div style="background-color:#ededed" lang="en" dir="auto">
    <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation">
      <tbody id="template" class="mktoContainer">
        <!-- Modules go here -->
      </tbody>
    </table>
  </div>
</body>
```

---

## Email Client Compatibility

### Supported Email Clients (Priority Order)

1. **Outlook (Windows)** - Desktop versions 2013, 2016, 2019, 2021, Microsoft 365
2. **Outlook (Mac)** - Latest versions
3. **Apple Mail** - iOS and macOS
4. **Gmail** - Web, iOS, Android
5. **Yahoo Mail** - Web and mobile
6. **Outlook.com** - Web interface
7. **Samsung Mail** - Android
8. **Other mobile clients**

### Client-Specific Considerations

| Client | Key Issues | Solutions |
|--------|-----------|-----------|
| Outlook (Windows) | Uses Word rendering engine, no CSS3, limited padding support | Use VML, MSO conditionals, `mso-padding-alt` |
| Gmail | Strips `<style>` in some contexts, aggressive CSS filtering | Inline all critical styles |
| Apple Mail | Generally good support | Standard practices work |
| Yahoo | Attribute selectors issues | Use class-based selectors |

---

## Outlook & Microsoft Conditional Comments

### Basic MSO Conditional Syntax

```html
<!--[if mso | IE]>
  <!-- Outlook-only code -->
<![endif]-->

<!--[if !mso]><!-->
  <!-- Non-Outlook code -->
<!--<![endif]-->

<!--[if lte mso 11]>
  <!-- Outlook 2003 and earlier -->
<![endif]-->
```

### Required Office Document Settings

Include this in the `<head>` inside MSO conditionals to ensure proper rendering:

```html
<!--[if mso]>
  <noscript>
    <xml>
      <o:OfficeDocumentSettings>
        <o:AllowPNG/>
        <o:PixelsPerInch>96</o:PixelsPerInch>
      </o:OfficeDocumentSettings>
    </xml>
  </noscript>
<![endif]-->
```

**Purpose:**
- `<o:AllowPNG/>` - Enables PNG support in older Outlook versions
- `<o:PixelsPerInch>96</o:PixelsPerInch>` - Prevents DPI scaling issues on high-DPI displays

### Outlook Column Width Fix

```html
<!--[if lte mso 11]>
  <style type="text/css">
    .mj-outlook-group-fix { width:100% !important; }
  </style>
<![endif]-->
```

### Outlook Table Wrappers

When creating multi-column layouts, wrap content in MSO-specific tables:

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="module-name-outlook" role="presentation" style="width:600px;" width="600" bgcolor="#FFFFFF" ><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly;"><![endif]-->

<div class="module-name" style="background:#fff;background-color:#fff;margin:0 auto;max-width:600px">
  <!-- Content -->
</div>

<!--[if mso | IE]></td></tr></table><![endif]-->
```

### Outlook Column Structure

```html
<!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:253px;" ><![endif]-->

<div class="mj-column-per-50 mj-outlook-group-fix" style="font-size:0;text-align:left;direction:ltr;display:inline-block;vertical-align:top;width:100%">
  <!-- Column content -->
</div>

<!--[if mso | IE]></td><td class="" style="vertical-align:top;width:253px;" ><![endif]-->

<div class="mj-column-per-50 mj-outlook-group-fix" style="font-size:0;text-align:left;direction:ltr;display:inline-block;vertical-align:top;width:100%">
  <!-- Column content -->
</div>

<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## CSS Reset & Client Fixes

### Required Reset Styles

Include these in a `<style>` block in the `<head>`:

```css
/* Outlook link padding fix */
#outlook a {
  padding: 0;
}

/* Base resets */
body {
  margin: 0;
  padding: 0;
  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
}

/* Table resets */
table, td {
  border-collapse: collapse;
  mso-table-lspace: 0;
  mso-table-rspace: 0;
}

/* Image resets */
img {
  border: 0;
  height: auto;
  line-height: 100%;
  outline: 0;
  text-decoration: none;
  -ms-interpolation-mode: bicubic;
}

/* Paragraph display fix */
p {
  display: block;
  margin: 13px 0;
}
```

### Explanation of Key Properties

| Property | Purpose |
|----------|---------|
| `-webkit-text-size-adjust: 100%` | Prevents iOS from resizing text |
| `-ms-text-size-adjust: 100%` | Prevents Windows Mobile from resizing text |
| `mso-table-lspace: 0` | Removes left spacing on tables in Outlook |
| `mso-table-rspace: 0` | Removes right spacing on tables in Outlook |
| `-ms-interpolation-mode: bicubic` | Improves image scaling in IE |

---

## Table-Based Layout

### Core Principles

1. **Always use tables for layout** - CSS-based layouts (flexbox, grid) are not supported in Outlook
2. **Use `role="presentation"`** - Required for accessibility on layout tables
3. **Reset all table attributes** - Always include `border="0" cellpadding="0" cellspacing="0"`

### Standard Table Template

```html
<table border="0" cellpadding="0" cellspacing="0" role="presentation" style="border-collapse:collapse;border-spacing:0" width="100%">
  <tbody>
    <tr>
      <td style="vertical-align:top;padding:0">
        <!-- Content -->
      </td>
    </tr>
  </tbody>
</table>
```

### Container Width

- **Maximum width**: 600px (standard for email)
- **Always center**: Use `align="center"` and `margin:0 auto`

```html
<table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="width:100%;max-width:600px">
```

### Nested Table Structure

Follow this nesting pattern for proper rendering:

```
Table (container)
└── tbody
    └── tr
        └── td (with padding)
            └── Table (content)
                └── tbody
                    └── tr
                        └── td
                            └── Content
```

---

## Typography & Fonts

### Web Font Loading

Load web fonts for non-MSO clients using both `<link>` and `@import` for maximum compatibility:

```html
<!--[if !mso]><!-->
<link href="https://fonts.googleapis.com/css?family=Roboto:400,500,700,italic&display=swap" rel="stylesheet" type="text/css">
<link href="https://fonts.googleapis.com/css?family=Montserrat:300,400,500,700,italic&display=swap" rel="stylesheet" type="text/css">
<style type="text/css">
  @import url(https://fonts.googleapis.com/css?family=Roboto:400,500,700,italic&display=swap);
  @import url(https://fonts.googleapis.com/css?family=Montserrat:300,400,500,700,italic&display=swap);
</style>
<!--<![endif]-->
```

### Font Embedding for Outlook

Embed `@font-face` declarations inside MSO conditionals:

```html
<!--[if mso]>
<style>
  @font-face {
    font-family: 'Montserrat';
    font-style: normal;
    font-weight: 400;
    font-display: swap;
    src: url(https://fonts.gstatic.com/s/montserrat/v25/JTUSjIg1_i6t8kCHKm459WlhyyTh89Y.woff2) format('woff2');
    unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+0304, U+0308, U+0329, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
  }
  /* Include all weights and styles needed */
</style>
<![endif]-->
```

### Font Stack Requirements

**Always include fallback fonts:**

```css
/* Headings */
font-family: Montserrat, Helvetica, Arial, sans-serif;

/* Body text */
font-family: Roboto, Helvetica, Arial, sans-serif;

/* System font stack (for parent containers) */
font-family: Montserrat, -apple-system, BlinkMacSystemFont, Segoe UI, Helvetica, Arial, sans-serif;
```

### Inline Font Styles

Always apply font styles inline on the element:

```html
<p style="font-family:Roboto,Helvetica,Arial,sans-serif;margin:0;line-height:1.45">
  Content here
</p>
```

---

## Images

### Required Image Attributes

Every `<img>` tag must include:

```html
<img
  alt="Descriptive alt text"
  src="https://example.com/image.png"
  srcset="https://example.com/image.svg"
  style="border:0;display:block;outline:0;text-decoration:none;height:auto;width:100%;font-size:13px"
  width="150"
  height="auto"
>
```

### Attribute Explanations

| Attribute | Purpose |
|-----------|---------|
| `alt` | **Required** - Accessibility and fallback text |
| `src` | Primary image (PNG/JPG for Outlook compatibility) |
| `srcset` | SVG version for modern clients |
| `width` | Explicit width prevents layout shifts |
| `height="auto"` | Maintains aspect ratio |
| `border:0` | Removes link borders in older clients |
| `display:block` | Removes bottom gap in email clients |
| `font-size:13px` | Fallback text size if image doesn't load |

### Retina/High-DPI Images

Provide 2x images and constrain with width:

```html
<img
  src="https://example.com/image-2x.png"
  width="150"
  style="width:150px;max-width:100%"
>
```

### Image Links

Wrap images in links with proper attributes:

```html
<a href="https://example.com" target="_blank" rel="noopener" style="color:inherit">
  <img alt="Description" src="image.png" style="...">
</a>
```

### Marketo Editable Images

```html
<div id="unique-image-id" class="mktoImg" mktoName="Display Name" mktoLockImgStyle="true" mktoImgLink="${variable-href}" mktoImgLinkTarget="_blank" mktoImgWidth="496" mktoImgHeight="auto">
  <img alt="" src="placeholder.png" style="border:0;border-radius:20px;display:block;outline:0;text-decoration:none;height:auto;width:100%;font-size:13px">
</div>
```

---

## Buttons

### Bulletproof Button Pattern

This pattern works across all email clients including Outlook:

```html
<table border="0" cellpadding="0" cellspacing="0" role="presentation" style="border-collapse:separate;line-height:100%">
  <tbody>
    <tr>
      <td align="center" bgcolor="#24842E" role="presentation" style="border:solid 1px #24842e;border-radius:5px;cursor:auto;mso-padding-alt:12px 22px;background:#24842e" valign="middle">
        <a href="${button-href}" style="display:inline-block;background:#24842e;color:#fff;font-family:Montserrat,Helvetica,Arial,sans-serif;font-size:16px;font-weight:700;line-height:120%;margin:0;text-decoration:none;text-transform:none;padding:12px 22px;mso-padding-alt:0;border-radius:5px" target="_blank">
          ${button-text}
        </a>
      </td>
    </tr>
  </tbody>
</table>
```

### Key Button Properties

| Property | Location | Purpose |
|----------|----------|---------|
| `bgcolor` | `<td>` attribute | Background color for Outlook |
| `background` | `<td>` style | Background color for other clients |
| `background` | `<a>` style | Ensures clickable area is colored |
| `mso-padding-alt` | `<td>` style | Padding for Outlook (td level) |
| `mso-padding-alt:0` | `<a>` style | Resets padding on anchor for Outlook |
| `border-collapse:separate` | `<table>` style | Required for border-radius |
| `border` | `<td>` style | Adds border for outline buttons |

### Outline Button Variant

```html
<td align="center" bgcolor="#FFFFFF" role="presentation" style="border:solid 1px #24842e;border-radius:5px;cursor:auto;mso-padding-alt:12px 22px;background:#fff" valign="middle">
  <a href="${href}" style="display:inline-block;background:#fff;color:#24842e;font-family:Montserrat,Helvetica,Arial,sans-serif;font-size:16px;font-weight:700;line-height:120%;margin:0;text-decoration:none;text-transform:none;padding:12px 22px;mso-padding-alt:0;border-radius:5px" target="_blank">
    Button Text
  </a>
</td>
```

---

## Responsive Design

### Media Query Breakpoints

```css
/* Desktop and above */
@media only screen and (min-width:480px) {
  .mj-column-per-50 { width:50%!important; max-width:50% }
  .mj-column-per-100 { width:100%!important; max-width:100% }
  /* Add other column widths as needed */
}

/* Mobile */
@media only screen and (max-width:479px) {
  table.mj-full-width-mobile { width:100%!important }
  td.mj-full-width-mobile { width:auto!important }
}
```

### Firefox-Specific Media Queries

```css
@media screen and (min-width:480px) {
  .moz-text-html .mj-column-per-50 { width:50%!important; max-width:50% }
}
```

### Column Width Classes

Define percentage-based column classes:

```css
.mj-column-per-16 { width:16%!important; max-width:16% }
.mj-column-per-33 { width:33%!important; max-width:33% }
.mj-column-per-34 { width:34%!important; max-width:34% }
.mj-column-per-49 { width:49%!important; max-width:49% }
.mj-column-per-50 { width:50%!important; max-width:50% }
.mj-column-per-65 { width:65%!important; max-width:65% }
.mj-column-per-84 { width:84%!important; max-width:84% }
.mj-column-per-100 { width:100%!important; max-width:100% }
```

### Responsive Column Pattern

```html
<div class="mj-column-per-50 mj-outlook-group-fix" style="font-size:0;text-align:left;direction:ltr;display:inline-block;vertical-align:top;width:100%">
  <!-- Column content -->
</div>
```

**Key styles:**
- `font-size:0` - Removes whitespace between inline-block elements
- `display:inline-block` - Allows columns to sit side by side
- `width:100%` - Default mobile width, overridden by media query

---

## Marketo Syntax

### Container (Required)

The main `<tbody>` must be a Marketo container:

```html
<tbody id="template" class="mktoContainer">
  <!-- Modules go here -->
</tbody>
```

### Modules

Modules are repeatable, reorderable sections:

```html
<tr class="mktoModule" id="unique-module-id" mktoname="Display Name in Editor">
  <td>
    <!-- Module content -->
  </td>
</tr>
```

**Rules:**
- `id` must be unique across the entire template
- `mktoname` is what users see in the Marketo editor
- Modules must be direct children of the mktoContainer

### Editable Text

```html
<div style="font-family:..." id="unique-text-id" class="mktoText" mktoname="Display Name">
  <p style="...">Editable content</p>
</div>
```

### Editable Images

```html
<div id="unique-img-id" class="mktoImg" mktoName="Display Name" mktoLockImgStyle="true" mktoImgLink="${link-variable}" mktoImgLinkTarget="_blank" mktoImgWidth="496" mktoImgHeight="auto">
  <img alt="" src="placeholder.png" style="...">
</div>
```

**Attributes:**
- `mktoLockImgStyle="true"` - Prevents style modifications
- `mktoImgLink` - Makes image clickable (use variable for editability)
- `mktoImgLinkTarget` - Link target (`_blank` for new window)
- `mktoImgWidth` / `mktoImgHeight` - Constrain dimensions

### Variables

Define in `<head>` as meta tags:

```html
<!-- Global variable -->
<meta id="copyright-year" class="mktoString" mktoname="Copyright year" default="2025">

<!-- Module-scoped variable -->
<meta id="button__button-href" class="mktoString" mktoname="Button Link" default="#" mktomodulescope="true">
<meta id="button__button" class="mktoString" mktoname="Button Text" default="Button" mktomodulescope="true">
```

**Variable types:**
- `mktoString` - Text input
- `mktoColor` - Color picker
- `mktoNumber` - Numeric input
- `mktoBoolean` - Toggle

**Using variables:**
```html
<!-- In text/attributes -->
${variable-id}

<!-- In href -->
href="${button__button-href}"
```

### Module-Scoped Variables

Use `mktomodulescope="true"` when variables should be unique per module instance:

```html
<meta id="module-name__variable" class="mktoString" mktoname="Display Name" default="value" mktomodulescope="true">
```

### Naming Convention for Variables

Follow this pattern: `module-id__element-name`

```
button__button-href     → Button module, button href
button__button          → Button module, button text
section-grey__title     → Section grey module, title
```

---

## Accessibility

### Required Practices

1. **Table role**: Always use `role="presentation"` on layout tables
   ```html
   <table role="presentation" ...>
   ```

2. **Language**: Include `lang` attribute on `<html>` and content `<div>`
   ```html
   <html lang="en">
   <div lang="en" dir="auto">
   ```

3. **Alt text**: Every image must have `alt` attribute (can be empty for decorative images)
   ```html
   <img alt="Description of image" ...>
   <img alt="" ...> <!-- Decorative only -->
   ```

4. **Navigation labels**: Use `aria-label` on navigation elements
   ```html
   <nav aria-label="Links">
   ```

5. **Hidden decorators**: Use `aria-hidden` for decorative elements
   ```html
   <span aria-hidden="true">&nbsp;|&nbsp;</span>
   ```

6. **Semantic structure**: Use proper heading hierarchy (h1, h2, h3, etc.)

7. **Color contrast**: Ensure 4.5:1 minimum contrast ratio for text

8. **Link text**: Use descriptive link text, not "click here"

---

## Security Practices

### Link Security

Always use `rel="noopener"` on external links with `target="_blank"`:

```html
<a href="https://example.com" target="_blank" rel="noopener">Link</a>
```

**Why:** Prevents the opened page from accessing `window.opener`, which could be used for phishing attacks.

### HTTPS Only

All external resources must use HTTPS:
- Images
- Fonts
- Tracking pixels
- Any external URLs

### No JavaScript

Never include JavaScript in email templates:
- Email clients block or strip JavaScript
- Can trigger spam filters
- Security risk

### UTM Parameters

Include tracking parameters on all links:

```html
<a href="https://example.com?utm_source=marketo&utm_medium=email">
```

### Content Security

- Never include sensitive data in templates
- Don't expose internal URLs or API endpoints
- Sanitize any dynamic content

---

## Module Naming Conventions

### ID Naming Pattern

Use BEM-like naming:

```
module-name                     → Base module
module-name--variant           → Module variant (--SR, --ITRG, --grey)
module-name__element           → Element within module
module-name--variant__element  → Element in variant
```

### Examples

```
header-sr                       → SR header module
header-itrg                     → ITRG header module
typography--grey               → Typography with grey background
typography--grey__title--SR    → SR title in grey typography
section-grey-with-button       → Grey section with button
two-col-text-then-button--ITRG → ITRG variant of 2-col module
```

### mktoname Guidelines

- Use clear, human-readable names
- Include context: "Title (SR)", "Button Link"
- Be consistent across similar modules
- Match the purpose, not the technical name

---

## Testing & Validation

### Pre-Upload Checklist

- [ ] All IDs are unique
- [ ] All mktoText/mktoImg/mktoModule have valid IDs
- [ ] Variables have appropriate default values
- [ ] All images have alt attributes
- [ ] All external links use HTTPS
- [ ] All links have `target="_blank" rel="noopener"`
- [ ] MSO conditionals are properly closed
- [ ] Tables have `role="presentation"`
- [ ] Font fallbacks are in place
- [ ] Buttons use bulletproof pattern

### Testing Tools

1. **Litmus** - Cross-client testing
2. **Email on Acid** - Cross-client testing
3. **Marketo Preview** - Test within Marketo
4. **W3C Validator** - HTML validation

### Client Testing Priority

Test in this order:
1. Outlook (Windows) - Most problematic
2. Gmail (Web)
3. Apple Mail (iOS)
4. Outlook (Mac)
5. Yahoo Mail
6. Mobile Gmail

### Common Issues to Check

| Issue | Clients Affected | Solution |
|-------|-----------------|----------|
| Broken layout | Outlook | Use MSO conditionals |
| Missing background colors | Outlook | Use `bgcolor` attribute |
| Button padding wrong | Outlook | Use `mso-padding-alt` |
| Images not showing | Gmail | Ensure HTTPS, check alt |
| Fonts not rendering | Outlook | Include embedded @font-face |
| Columns not stacking | Mobile | Check media queries |

---

## Quick Reference

### Standard Dimensions

- **Container width**: 600px
- **Content padding**: 24px 47px or 24px 52px
- **Inner column padding**: 0 5px
- **Button padding**: 12px 22px
- **Border radius**: 5px (buttons), 20px (cards/images)

### Standard Spacing

- **Module spacing**: 24px vertical
- **Element spacing**: 16-24px
- **Footer top padding**: 48px

### Font Sizes

- H1: 40px, weight 700, line-height 1.2
- H2: 28px, weight 300, line-height 1.35
- H3: 20px, weight 500, line-height 1.35
- H4: 16px, weight 700, line-height 1.35
- H5/H6: 14px, weight 500, line-height 1.35
- Body: 16px, weight 400, line-height 1.45
- Disclaimer: 12px, italic, line-height 1.45
- Footer: 12px, line-height 1.35

### Line Heights

- Headings: 1.2 - 1.35
- Body text: 1.45
- List items: 1.5
- Buttons: 120% (1.2)

---

## File Organization

```
project/
├── .claude/
│   ├── marketo-email-development.md  (this file)
│   └── style-guide.md                (brand styles)
├── templates/                         (complete templates)
├── modules/                           (reusable modules)
├── components/                        (shared elements)
├── assets/
│   └── images/
└── docs/                             (additional documentation)
```
