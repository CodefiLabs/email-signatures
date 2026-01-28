# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML email signature generator for Codefi team members. Hosted via GitHub Pages at signature.codefiworks.com.

## Architecture

- `index.html` - Main page containing all employee signatures with copy-to-clipboard functionality
- `email/img/` - Portrait photos and icons (logo, social icons, contact icons)
- `email/img/template.html` - Reference template for creating new signatures

## Adding a New Signature

1. Add the employee's portrait image (130x130px PNG) to `email/img/`
2. Commit the image to get a permanent GitHub raw URL with commit hash
3. Copy an existing signature block in `index.html` and update:
   - Portrait image URL (use raw GitHub URL with commit hash for stability)
   - Name, title, email, phone (if applicable)
   - Increment the signature index in the `id="signature_N"` and `onclick="copySignature(N)"`
4. The phone field is optional - some signatures include it, some don't

## Image URL Pattern

Images use raw GitHub URLs with commit hashes for version stability:
```
https://raw.githubusercontent.com/CodefiLabs/email-signatures/{COMMIT_HASH}/email/img/{filename}.png
```

## Brand Colors

- Primary teal: `#007E7A` / `#007F7B`
- Green separator: `#73bf48`
- Dark gray text: `#58595B`

## Logo/Social Icons Spacing (IMPORTANT)

The inner table containing the Codefi logo and social icons must NOT have `width="100%"`. This causes inconsistent spacing based on the length of the name/title/email content above it.

**Correct:**
```html
<table cellspacing="0" cellpadding="0" border="0">
```

**Incorrect (causes extra space after logo):**
```html
<table width="100%" cellspacing="0" cellpadding="0" border="0">
```

The logo cell should have a fixed width matching the logo image:
```html
<td width="84" height="45" style="width: 84px;">
```

When adding new signatures, always copy from an existing signature that has correct spacing (no `width="100%"` on the inner table).
