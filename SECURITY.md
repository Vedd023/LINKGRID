# Security Policy

## Overview

LINKGRID is designed primarily as a client-side web application. Most operations—including QR code generation, logo composite rendering, image scaling, and PNG file export—occur entirely within the user's browser without transferring input text or image files to an application backend.

## Scope & Data Flow

When evaluating security or reporting vulnerabilities, please note the differing data flows across application features:

| Feature | Execution Environment | Network Exposure |
| :--- | :--- | :--- |
| **QR Code Generation** | Browser (Client-side) | None. Data is rendered directly onto an HTML5 canvas. |
| **Logo Embedding** | Browser (Client-side) | None. Processed via local `FileReader` as an in-memory data URL. |
| **PNG Export** | Browser (Client-side) | None. Generated via local canvas `toDataURL('image/png')`. |
| **Short Link Generation** | External Third-Party API | The input URL is transmitted via HTTPS POST to `https://smolurl.com/api/links`. |
| **User Authentication** | External Third-Party Service | Google Sign-in facilitated via Google Firebase Authentication SDK. |

### Important Security Considerations

1. **Third-Party URL Shortener (`smolurl.com`)**:
   - In "Short link" and "Both" modes, URLs submitted to LINKGRID are sent across the network to the external public shortener service `smolurl.com`.
   - Avoid submitting sensitive, private, or confidential URLs (such as URLs containing authorization tokens, private keys, or internal network addresses) to the shortener.
   - For sensitive payloads, use the pure **QR code** mode, where no data leaves your browser.

2. **Client-Side Authentication Config**:
   - The repository contains client-facing configuration identifiers for Firebase. Firebase client configurations (API keys, project IDs) are public identifiers by design in client-side web applications; however, backend access control depends on Firebase Console rules and authorized domain restrictions.

## Reporting a Vulnerability

If you discover a security issue or vulnerability within LINKGRID:

1. **Do not create public GitHub issues** to report potential security vulnerabilities.
2. Please report the issue privately to the repository maintainer by opening a private security advisory on GitHub via the repository's **Security** tab (`https://github.com/Vedd023/LINKGRID/security/advisories/new`), or by contacting the maintainer directly via their GitHub profile ([@Vedd023](https://github.com/Vedd023)).
3. Please include:
   - A description of the vulnerability and its potential impact.
   - Step-by-step reproduction instructions or a minimal proof of concept.
   - Affected browser(s) and environment details.

Reports will be acknowledged promptly, investigated, and addressed in a future update.
