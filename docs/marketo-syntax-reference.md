# Marketo Email Template Syntax Reference

This document covers all the Marketo-specific syntax and elements you'll need when building email templates.

## Variables

Variables allow marketers to customize template elements without editing code.

### Color Variables
```html
<meta class="mktoColor" id="primaryColor" mktoName="Primary Color" default="#0066cc">
```

### String Variables
```html
<meta class="mktoString" id="fontFamily" mktoName="Font Family" default="Arial, sans-serif">
```

### Number Variables
```html
<meta class="mktoNumber" id="fontSize" mktoName="Font Size" default="16" min="10" max="24" units="px">
```

### Boolean Variables
```html
<meta class="mktoBoolean" id="showSection" mktoName="Show Section" default="true" true_value="block" false_value="none">
```

**Usage in CSS/HTML:**
```html
<div style="display: ${showSection};">Content here</div>
```

### Image Variables
```html
<meta class="mktoImage" id="heroImage" mktoName="Hero Image" default="https://example.com/default.jpg">
```

## Editable Elements

### Editable Text (mktoText)
```html
<div class="mktoText" id="uniqueTextId" mktoName="Display Name in Editor">
    <p>Default editable content</p>
</div>
```

**Important Rules:**
- Each `id` must be unique within the template
- `mktoName` is what appears in the Marketo editor
- Can contain any HTML content

### Editable Images (mktoImg)
```html
<div class="mktoImg" id="uniqueImageId" mktoName="Display Name" mktoImgWidth="600">
    <img src="https://placeholder.com/600x300" alt="Description">
</div>
```

**Attributes:**
- `mktoImgWidth` - Constrains the image width in the editor
- `mktoImgHeight` - Constrains the image height (optional)
- `mktoLockImgSize` - Prevents resizing when set to "true"
- `mktoLockImgStyle` - Prevents style editing when set to "true"

### Rich Text Areas
```html
<div class="mktoText" id="richContent" mktoName="Rich Content Area">
    <h2>Heading</h2>
    <p>Paragraph with <strong>bold</strong> and <em>italic</em> text.</p>
</div>
```

## Modules

Modules are repeatable, reorderable sections that marketers can add/remove.

### Basic Module
```html
<tr class="mktoModule" id="uniqueModuleId" mktoName="Module Display Name">
    <td>Module content here</td>
</tr>
```

### Module Attributes
- `mktoAddByDefault="false"` - Module won't appear by default
- `mktoActive="false"` - Module is inactive by default

### Example Module with All Options
```html
<tr class="mktoModule" id="contentModule" mktoName="Content Block" mktoAddByDefault="true">
    <td style="padding: 20px;">
        <div class="mktoText" id="moduleHeading" mktoName="Heading">
            <h2>Section Title</h2>
        </div>
        <div class="mktoText" id="moduleBody" mktoName="Body Content">
            <p>Your content here.</p>
        </div>
    </td>
</tr>
```

## Snippets

Include dynamic content from Marketo Snippets:

```html
<div class="mktoSnippet" id="snippetId" mktoName="Snippet Name">
    <!-- Fallback content if snippet not selected -->
    <p>Default content</p>
</div>
```

## System Tokens

Marketo provides system tokens for common dynamic content:

### Company/Subscription Info
- `{{system.company}}` - Company name
- `{{system.address}}` - Company address
- `{{system.currentYear}}` - Current year

### Email Links
- `{{system.viewAsWebpageLink}}` - View in browser URL
- `{{system.unsubscribeLink}}` - Unsubscribe URL
- `{{system.forwardToFriendLink}}` - Forward to friend URL

### Lead/Person Tokens
- `{{lead.First Name}}` - First name
- `{{lead.Last Name}}` - Last name
- `{{lead.Email Address}}` - Email address
- `{{lead.Company Name}}` - Company name

### Usage Example
```html
<p>Hello {{lead.First Name:default=there}},</p>
<p>&copy; {{system.currentYear}} {{system.company}}</p>
```

**Default Values:**
```html
{{lead.First Name:default=Friend}}
```

## Email-Specific Meta Tags

Required meta tags for proper email rendering:

```html
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>${emailSubject}</title>
```

The `${emailSubject}` token automatically pulls the email subject line.

## Best Practices

### 1. Unique IDs
Every editable element needs a unique ID:
```html
<!-- Good -->
<div class="mktoText" id="heroHeading">...</div>
<div class="mktoText" id="bodyContent">...</div>

<!-- Bad - duplicate IDs -->
<div class="mktoText" id="content">...</div>
<div class="mktoText" id="content">...</div>
```

### 2. Descriptive mktoName Values
Use clear, descriptive names for the editor:
```html
<!-- Good -->
mktoName="Hero Section Headline"
mktoName="Footer Company Address"

<!-- Not ideal -->
mktoName="Text 1"
mktoName="Content"
```

### 3. Module Organization
Group related modules with consistent naming:
```html
<tr class="mktoModule" id="header1" mktoName="Header - Logo Only">
<tr class="mktoModule" id="header2" mktoName="Header - Logo with Nav">
<tr class="mktoModule" id="content1" mktoName="Content - Single Column">
<tr class="mktoModule" id="content2" mktoName="Content - Two Column">
```

### 4. Variable Placement
Place all variable declarations in the `<head>`:
```html
<head>
    <meta class="mktoColor" id="primaryColor" mktoName="Primary Color" default="#0066cc">
    <meta class="mktoString" id="fontFamily" mktoName="Font Family" default="Arial, sans-serif">
    <!-- ... other variables ... -->
</head>
```

### 5. Inline Styles
Email clients have limited CSS support. Always use inline styles:
```html
<!-- Good -->
<p style="margin: 0; font-size: 16px; color: #333333;">Text</p>

<!-- Won't work reliably -->
<p class="body-text">Text</p>
```

## Validation Checklist

Before uploading to Marketo:

- [ ] All element IDs are unique
- [ ] All mktoText/mktoImg/mktoModule elements have valid IDs
- [ ] Variables have appropriate default values
- [ ] System tokens are correctly formatted
- [ ] Inline styles are used throughout
- [ ] Images have alt attributes
- [ ] Links use `href` attributes (not JavaScript)
- [ ] Template validates as HTML
