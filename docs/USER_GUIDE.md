# LINKGRID User Guide

This guide covers setup, configuration, features, and troubleshooting for **LINKGRID**, a client-side utility for creating custom QR codes and short links.

---

## Table of Contents

1. [Quick Start & Setup](#quick-start--setup)
2. [Input & Normalization](#input--normalization)
3. [Operation Modes](#operation-modes)
   - [QR Code Mode](#1-qr-code-mode)
   - [Short Link Mode](#2-short-link-mode)
   - [Both (Hybrid) Mode](#3-both-mode)
4. [Customization Options](#customization-options)
   - [Module & Field Colors](#module--field-colors)
   - [Output Size & Scaling](#output-size--scaling)
   - [Logo Embedding & Favicon Sync](#logo-embedding--favicon-sync)
5. [Exporting & Sharing](#exporting--sharing)
6. [Authentication (Optional)](#authentication-optional)
7. [Browser Compatibility](#browser-compatibility)
8. [Troubleshooting](#troubleshooting)

---

## Quick Start & Setup

LINKGRID requires no build tools, compilers, or backend dependencies.

### Option A: Direct Browser Launch
1. Download or clone the repository.
2. Double-click [index.html](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/index.html) to open it in your default web browser.

### Option B: Local Static Server (Recommended)
Running through a local web server is recommended to ensure full support for the modern Web Clipboard API and Firebase Auth popups:
```bash
# Python 3
python -m http.server 8000

# Node.js (npx)
npx serve .
```
Navigate to `http://localhost:8000` in your browser.

---

## Input & Normalization

Enter any text or link into the **Source link** input field:
- **Standard URLs:** `https://example.com/page`, `example.com`
- **Wi-Fi Strings:** `WIFI:T:WPA;S:NetworkName;P:Password;;`
- **Contact Cards (vCard):** `BEGIN:VCARD...`
- **Plain Text:** Any text string

### Automatic URL Normalization
If an input does not begin with a protocol scheme (e.g. `https://`, `http://`, `ftp://`), LINKGRID automatically prepends `https://` during processing. You can trigger generation by clicking **Build it** or pressing the `Enter` key.

---

## Operation Modes

Select your target mode using the mode selector tabs:

### 1. QR Code Mode
- **Behavior:** Generates a custom QR code completely inside your browser.
- **Privacy:** 100% client-side. No input data is sent to external servers.
- **Controls Displayed:** Color pickers, Output Size slider, and Logo upload field.

### 2. Short Link Mode
- **Behavior:** Sends the normalized URL to the external public shortener service ([SmolURL](https://smolurl.com)) and generates a shortened URL.
- **Privacy Notice:** The URL string leaves your browser and is sent to `https://smolurl.com/api/links`.
- **Controls Displayed:** Displays a dedicated short link display box with a **Copy** button. Color, size, and logo controls are hidden.

### 3. Both Mode
- **Behavior:** First requests a shortened URL via SmolURL, then automatically generates a custom QR code that encodes the newly created short link.
- **Controls Displayed:** Displays both the short link copy interface and the QR preview canvas with download capabilities.

---

## Customization Options

### Module & Field Colors
- **Module Color:** Controls the foreground color of the QR code data dots/modules (defaults to `#0b0d0c`).
- **Field Color:** Controls the background color of the QR code canvas and quiet zone (defaults to `#f3f1e9`).

> [!TIP]
> Ensure high contrast between the module color and field color (e.g., dark modules on a light background). Inverting colors or choosing low-contrast tones can prevent smartphone camera scanners from recognizing the code.

### Output Size & Scaling
- **Slider Range:** Adjust from `160px` up to `480px` (default: `240px`).
- **Pixel-Perfect Scaling:** To eliminate blurry, anti-aliased module edges, LINKGRID computes an integer multiplier based on the QR version and standard 4-module quiet zone margin:
  $$\text{Multiplier} = \max\left(1, \text{round}\left(\frac{\text{Requested Size}}{\text{Total Modules}}\right)\right)$$
  The export canvas snaps precisely to whole pixels. The final exported resolution may vary slightly from the slider label to guarantee crisp edges.

### Logo Embedding & Favicon Sync
- **Uploading an Image:** Click the **Logo (optional)** file selector and select any standard image file (`.png`, `.jpg`, `.svg`, `.webp`).
- **Automatic Error Correction Upgrade:** Adding a logo automatically raises the QR code error correction from **Level M** (~15% recovery capacity) to **Level H** (~30% recovery capacity) to preserve scan integrity.
- **Module-Aligned Cutout:** A centered background box is drawn with dimensions matching an exact integer multiple of QR modules (~30% width), ensuring modules are replaced cleanly.
- **Dynamic Favicon:** When a logo is active, LINKGRID automatically sets your browser tab's favicon to the uploaded logo.
- **Clear Button:** Click **Clear** next to the logo input to remove the logo and restore the default LINKGRID favicon.

---

## Exporting & Sharing

- **Download PNG:** When a QR code is rendered, click **Download PNG** to save `linkgrid-qr.png` to your device.
- **Copy Short Link:** In "Short link" or "Both" mode, click **Copy** next to the short link. The button temporarily displays "Copied" upon success.

---

## Authentication (Optional)

LINKGRID contains an optional Google Sign-In module implemented via Firebase v10.13.0:
- Clicking **Sign In** initiates a Google OAuth popup flow.
- When signed in, the header displays your Google user avatar, display name, and a **Sign Out** button.
- **Configuration:** To link the authentication system to your own Firebase project, configure the `firebaseConfig` object located near the bottom of [index.html](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/index.html).

---

## Browser Compatibility

LINKGRID relies on modern, standard web APIs supported by all current browsers:

| Browser | Minimum Recommended Version |
| :--- | :--- |
| **Google Chrome / Chromium** | Version 66+ |
| **Mozilla Firefox** | Version 63+ |
| **Apple Safari** | Version 13.1+ |
| **Microsoft Edge** | Version 79+ |
| **Mobile Browsers (iOS Safari, Android Chrome)** | Modern versions |

Required API features:
- HTML5 Canvas (`CanvasRenderingContext2D`)
- FileReader API (`readAsDataURL`)
- Asynchronous Fetch API (`window.fetch`)
- Async Clipboard API (`navigator.clipboard.writeText`)
- ES6+ JavaScript (Async/Await, Arrow functions, Modules)

---

## Troubleshooting

### 1. "Could not reach the shortening service — try again, or switch to QR only."
- **Cause:** The external SmolURL service (`smolurl.com`) may be temporarily offline, rate-limiting requests, or blocked by network firewalls.
- **Remedy:** Switch the mode tab to **QR code** mode. QR code generation operates completely offline and client-side without relying on external services.

### 2. Copy Button Does Not Copy to Clipboard
- **Cause:** Modern browsers restrict `navigator.clipboard` access to secure contexts (`https://` or `http://localhost`). Opening files via direct `file:///` paths may be blocked by browser security sandboxes.
- **Remedy:** Run LINKGRID via a local web server (e.g., `python -m http.server 8000`) or deploy to an HTTPS host.

### 3. QR Code Will Not Scan
- **Low Contrast:** Check your module and field color choices. QR scanners expect high contrast (dark foreground against light background).
- **Logo Too Complex or Obscuring Modules:** When encoding very long URLs, QR code modules become smaller and denser. Try shortening the URL first or testing without an embedded logo.

### 4. Firebase Sign-In Error
- **Cause:** If running on a local port not authorized in the Firebase Console (Authorized Domains list), the OAuth popup will reject authentication.
- **Remedy:** Add your host (`localhost`, `127.0.0.1`, or your custom domain) to **Authentication -> Settings -> Authorized Domains** in your Firebase Console.
