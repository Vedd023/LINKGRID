# Contributing to LINKGRID

Thank you for your interest in contributing to LINKGRID! LINKGRID is built as a lightweight, zero-build, client-side web application using vanilla HTML5, CSS3, and modern JavaScript.

## Guiding Principles

- **Zero-Build Simplicity:** Keep the project accessible without mandatory bundlers, build steps, or package management overhead.
- **Client-Side Privacy:** QR generation and logo composite processing must remain 100% client-side. No user input or uploaded images should be sent across the network.
- **Visual Polish:** Maintain the curated retro-futuristic dark console design aesthetic and responsive layout.

## Development Workflow

1. **Fork and Clone**:
   ```bash
   git clone https://github.com/Vedd023/LINKGRID.git
   cd LINKGRID
   ```

2. **Run Locally**:
   Because LINKGRID has no build pipeline, you can run it immediately:
   - Double-click or open `index.html` in your web browser, or
   - Serve the directory using any local development server (recommended for testing clipboard and authentication APIs):
     ```bash
     # Using Python
     python -m http.server 8000

     # Or using Node.js / npx
     npx serve .
     ```
   - Access the app at `http://localhost:8000` or `http://localhost:3000`.

3. **Making Changes**:
   - Keep modifications focused and documented.
   - Test across major desktop and mobile browsers (Chrome, Firefox, Safari, Edge).
   - Ensure QR readability using a physical smartphone camera or standard QR scanner app after making adjustments to rendering logic.

## Submitting a Pull Request

1. Create a descriptive branch from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```
2. Commit your changes with clear, concise commit messages.
3. Push to your fork and submit a Pull Request against the `main` branch.
4. Provide a clear summary in your PR describing:
   - The motivation for the change.
   - Any visual or behavioral changes (with screenshots if applicable).
   - Verification steps taken.
