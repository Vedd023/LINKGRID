# Known Issues & Technical Considerations

This document records architectural nuances, external service dependencies, and operational considerations verified directly against the LINKGRID implementation.

---

## 1. External URL Shortening Availability (SmolURL)

- **Behavior:** The "Short link" and "Both" modes make an asynchronous `fetch` POST request to `https://smolurl.com/api/links`.
- **Limitation:** If `smolurl.com` is unreachable, rate-limited, blocked by adblockers/network firewalls, or experiences downtime, URL shortening will fail.
- **Handling:** The application catches the exception and displays an inline alert:
  > *"Could not reach the shortening service — try again, or switch to QR only."*
- **Workaround:** Switch to **QR code** mode. Pure QR generation is performed entirely on the client side without contacting external servers.

---

## 2. CDN Script Tag vs. Bundled Local `qr.js`

- **Observation:** [index.html](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/index.html) (line 10) loads the QR generator from Cloudflare cdnjs:
  ```html
  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
  ```
  Although a standalone minified copy is provided in the repository as [qr.js](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/qr.js), `index.html` does not reference `./qr.js` by default.
- **Impact:** If `index.html` is opened in a completely air-gapped/offline environment or in an environment where `cdnjs.cloudflare.com` is blocked, the `QRCode` library will fail to load.
- **Workaround:** For completely offline usage, change line 10 in `index.html` to `<script src="qr.js"></script>`.

---

## 3. Pixel-Perfect Dimension Snapping (Integer Multipliers)

- **Behavior:** The size slider permits selections between `160px` and `480px` in increments of `20px`. However, the rendering pipeline enforces crisp nearest-neighbor rasterization:
  ```javascript
  const marginModules = 4;
  const totalModules = modules + marginModules * 2;
  let mult = Math.round(requestedSize / totalModules);
  if (mult < 1) mult = 1;
  const fullSize = totalModules * mult;
  ```
- **Impact:** The resulting exported PNG dimensions (`fullSize`) will snap to exact integer multiples of the QR grid. The actual image pixel dimensions may therefore differ slightly from the slider readout (for example, exporting at 232px or 261px instead of exactly 240px). This is intentional to prevent blurry, anti-aliased module borders.

---

## 4. Clipboard API Restrictions on `file://` Origins

- **Behavior:** The **Copy** button for short links invokes `navigator.clipboard.writeText(text)`.
- **Limitation:** Modern browser security policies restrict clipboard access to secure origins (`https://` or `http://localhost`). When opening `index.html` directly from the local disk using the `file:///` protocol, some browsers (including Firefox and Safari) may disallow clipboard writes without an explicit permission prompt.
- **Workaround:** Run the application via a local development web server (e.g. `python -m http.server 8000` or `npx serve .`).

---

## 5. QR Readability with Low Contrast or Dense Data

- **Behavior:** Custom module and field color pickers allow any 24-bit hex color.
- **Limitation:** 
  - Selecting low-contrast color pairs (e.g., light gray modules on a white field, or dark blue modules on a black field) will result in QR codes that standard optical barcode scanners cannot decode.
  - Encoding exceptionally long URLs results in high-density QR versions with very small module dimensions. In "Both" mode, shortening the URL first avoids excessive data density and significantly improves readability.

---

## 6. Standalone `dashboard.html` File

- **Observation:** The repository includes [dashboard.html](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/dashboard.html), an admin dashboard interface titled "CMSolutions — Main Dashboard".
- **Status:** This file is currently unlinked from [index.html](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/index.html) and functions as an independent, standalone page.
