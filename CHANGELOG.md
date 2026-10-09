# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.0] - 2026-10-09

### Added
- **Client-Side QR Code Engine:** Integrated `qrcodejs` for generating standard QR codes directly in the browser canvas.
- **Color Customization:** Configurable module (foreground) and field (background) color selectors with real-time picker inputs.
- **Crisp Integer Module Scaling:** Dynamic pixel-perfect scaling algorithm utilizing standard 4-module quiet zones and nearest-neighbor integer multipliers to eliminate blurry sub-pixel antialiasing.
- **Logo Embedding:**
  - File picker support for embedding custom logos in the center of QR codes.
  - Automatic error correction level upgrade from Level M (~15%) to Level H (~30%) when a logo is attached.
  - Module-aligned background clearing square to maintain structural QR integrity.
  - Proportional logo scaling capped at 80% of the center clearing square.
  - Real-time browser favicon synchronization reflecting the active logo, with complete restoration on clear.
- **External URL Shortening:** Public URL shortening integration via the SmolURL API (`smolurl.com`).
- **Flexible Modes:**
  - `QR code`: Pure client-side QR code generator.
  - `Short link`: Standalone URL shortener with copyable output.
  - `Both`: Hybrid flow that shortens a URL and generates a QR code pointing directly to the shortened address.
- **Export & Utility Tools:**
  - One-click PNG image download (`linkgrid-qr.png`).
  - One-click clipboard copy for short links with visual confirmation.
  - Automatic URL normalization prepending `https://` if protocol scheme is omitted.
- **Optional Firebase Authentication:** Integrated Google Sign-In interface via Firebase v10.13.0 modular SDK with avatar and user status display.
- **Visual Interface:** Responsive dark-console interface featuring ambient animated gradients, scanline animations, glassmorphism containers, and accessible `prefers-reduced-motion` overrides.
