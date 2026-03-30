# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

Static landing page for importing 4 IT emergency contacts via QR code at a dental conference ("Digitale Prophylaxe", Alpha Omega 2026). The core challenge: iOS Safari only imports the first contact from a multi-vCard file, so the page uses platform detection to work around this.

## Architecture

- **Pure static site** — single `index.html`, no build step, no dependencies
- **`vcf/`** — individual `.vcf` files per contact + one combined `alle-kontakte.vcf`
- **Platform strategy**: iOS opens individual `.vcf` files via `window.location.href` (hands off to Contacts app); Android/Desktop triggers a Blob download of the combined multi-vCard
- **QR code** (`qr-code.png`, `qr-code.svg`) points to the GitHub Pages URL

## Local Development

```bash
# Serve locally (any static server works)
python3 -m http.server 8000
# Then open http://localhost:8000
```

iOS testing requires the page to be served over HTTPS or via a tunnel (e.g. `npx localtunnel`).

## Deployment

Hosted on GitHub Pages. Push to `main` branch auto-deploys.

## Regenerating the QR Code

If the URL changes, regenerate with:
```bash
python3 -c "
import qrcode, qrcode.image.svg
url = 'https://NEW-URL-HERE/'
qr = qrcode.QRCode(error_correction=qrcode.constants.ERROR_CORRECT_M, box_size=20, border=2)
qr.add_data(url); qr.make(fit=True)
qr.make_image(fill_color='#082540', back_color='#FFFFFF').save('qr-code.png')
qr2 = qrcode.QRCode(error_correction=qrcode.constants.ERROR_CORRECT_M, box_size=20, border=2)
qr2.add_data(url); qr2.make(fit=True)
qr2.make_image(image_factory=qrcode.image.svg.SvgPathImage).save('qr-code.svg')
"
```

## CI Colors

- Primary: `#082540` (dark blue)
- Accent: `#4B91B9` (light blue)
- Background: `#EAF5FA`
