# Third-Party Notices & Attribution

This document lists the third-party libraries, fonts, and external services utilized in the LINKGRID codebase, along with their respective licensing terms and attribution notices.

---

## 1. JavaScript Libraries

### QRCode.js (`qr.js`)
- **Project:** [QRCode.js](https://github.com/davidshimjs/qrcodejs)
- **Author:** Shim Sangmin (davidshimjs)
- **Included as:** 
  - Local minified file: [qr.js](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/qr.js)
  - CDN reference: `https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js` in [index.html](file:///c:/Users/Ved%20Dixit/OneDrive/Desktop/LINKGRID/index.html)
- **License:** MIT License
- **Copyright:** (c) 2012 davidshimjs

```text
The MIT License (MIT)

Copyright (c) 2012 davidshimjs

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```

---

### Firebase Web SDK (`v10.13.0`)
- **Project:** [Firebase JavaScript SDK](https://github.com/firebase/firebase-js-sdk)
- **Provider:** Google LLC
- **Included as:** Remote ES module imports via `https://www.gstatic.com/firebasejs/10.13.0/`
  - `firebase-app.js`
  - `firebase-auth.js`
- **License:** Apache License 2.0
- **Copyright:** Copyright 2024 Google LLC

Licensed under the Apache License, Version 2.0; you may not use this file except in compliance with the License. You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

---

## 2. Fonts

The typography in LINKGRID is served via Google Fonts CDN under the **SIL Open Font License, Version 1.1**.

### Playfair Display
- **Designer:** Claus Eggers Sørensen
- **License:** SIL Open Font License 1.1
- **Source:** [Google Fonts - Playfair Display](https://fonts.google.com/specimen/Playfair+Display)

### Space Mono
- **Designer:** Colophon Foundry
- **License:** SIL Open Font License 1.1
- **Source:** [Google Fonts - Space Mono](https://fonts.google.com/specimen/Space+Mono)

### Inter *(used in `dashboard.html`)*
- **Designer:** Rasmus Andersson
- **License:** SIL Open Font License 1.1
- **Source:** [Google Fonts - Inter](https://fonts.google.com/specimen/Inter)

---

## 3. External Web Services

### SmolURL API
- **Endpoint:** `https://smolurl.com/api/links`
- **Service Provider:** SmolURL ([smolurl.com](https://smolurl.com))
- **Role:** Handles URL shortening in "Short link" and "Both" modes via asynchronous HTTPS POST requests.
- **Usage Notice:** SmolURL is an independent, external web service. Availability, rate limits, latency, and retention are governed by SmolURL's service policies. LINKGRID does not operate, control, or host this service.
