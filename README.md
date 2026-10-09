# LINKGRID

**LINKGRID** is a lightning-fast, client-side tool that transforms any URL into beautiful, highly customizable QR codes and short links—all right from your browser. 

## Features

- **Client-Side Generation:** Your data stays in your browser. QR codes are rendered instantly on the client side without needing a backend server (except for the third-party shortlink request).
- **Custom QR Codes:**
  - **Color Customization:** Fine-tune both the module color (foreground) and field color (background) to match your brand.
  - **Dynamic Logo Embedding:** Upload a logo to automatically embed it perfectly in the center of your QR code with pixel-perfect module alignment and dynamic scaling.
  - **Adjustable Size:** Control the export resolution of your QR code up to 480px.
- **Instant Short Links:** Convert long URLs into concise short links using an integrated public shortening service.
- **Hybrid Mode:** Generate a short link and immediately create a QR code that points to it.
- **Dynamic Favicon:** The website's favicon dynamically updates to match your uploaded logo.
- **Download Ready:** Export your crisp, perfectly scaled QR codes as PNG files with a single click.

## Quick Start

Since LINKGRID is entirely client-side, you don't need any complex build steps or dependencies to get it running.

1. Clone or download this repository.
2. Open `index.html` in any modern web browser.
3. Paste a link and start building!

## How to Use

1. **Paste a Link:** Enter any valid URL, contact card string, or text into the input field.
2. **Select Output Mode:** 
   - **QR Code:** Generates a custom QR code.
   - **Short Link:** Shortens the URL.
   - **Both:** Shortens the URL and generates a QR code pointing to the new short link.
3. **Customize (QR Mode):**
   - Pick your desired **module** and **field** colors.
   - Use the slider to set the **Output Size**.
   - (Optional) **Upload a Logo**: Select an image file. LINKGRID will automatically switch to High Error Correction mode and seamlessly embed the logo with perfect QR module alignment.
4. **Build & Export:** Click **Build it**. You can then copy the short link or click **Download PNG** to save your new QR code.

## Technologies Used

- **HTML5 & CSS3:** For a sleek, modern, and responsive interface featuring a minimal console aesthetic.
- **Vanilla JavaScript:** For dynamic UI updates, file processing, and API handling.
- **qrcodejs:** A lightweight, client-side QR code generation library (included locally as `qr.js`).
