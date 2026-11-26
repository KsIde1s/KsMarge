# KsMarge — local browser PDF merger

KsMarge is a minimal PDF merger built with React, TypeScript, Vite and `pdf-lib`.

## What it does

- Select or drag in multiple PDF files.
- Reorder files with drag and drop.
- Remove individual files or clear the list.
- Merge all pages into one PDF in the displayed order.
- Preview the merged PDF in the browser before downloading.
- Choose a custom output filename.
- Process files locally in the browser; no backend or account is used.

## Requirements

- Node.js 18+ (Node.js 20 LTS recommended)
- npm

## Run locally

```bash
npm install
npm run dev
```

Open the local development address shown in your terminal (usually http://localhost:8888).
## Create a production build

```bash
npm run build
npm run preview
```

The static production site is generated in `dist/` and can be hosted on any static web host.

## Architecture

```text
Browser
  ├── React UI
  │    ├── PDF file picker / drop zone
  │    ├── ordered file list (native HTML drag-and-drop)
  │    └── merge + download controls
  └── pdf-lib
       ├── reads each File as ArrayBuffer
       ├── copies pages in the chosen order
       └── serializes one merged PDF Blob
```

There is no API server, database, login, or file upload.

## Notes and limitations

- Files are processed in the browser and are not sent to an application server.
- The app keeps the original PDF page content rather than converting pages to images, so it avoids the quality loss associated with screenshot/raster-based merging.
- PDF merging is not a lossless preservation guarantee for every possible PDF feature. Encrypted/password-protected, malformed, or unusually complex PDFs may fail. Digital signatures in source PDFs should not be expected to remain valid after merging.
- "Unlimited" is constrained in practice by the device's available memory and browser limits. Very large PDFs may fail on low-memory devices.
- The app uses system fonts and makes no external network requests.
