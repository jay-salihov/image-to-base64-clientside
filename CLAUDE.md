# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a client-side web application that converts images to base64 and decodes base64 back to images. All processing happens entirely in the browser using the FileReader API - no server-side processing or uploads occur.

## Architecture

**Single-file application**: The entire application is contained in `index.html` with embedded JavaScript. There is no build process, bundler, or external dependencies beyond CDN-loaded CSS frameworks.

**Key components**:
- DaisyUI 4.7.2 and Tailwind CSS 2.2.19 for styling (loaded via CDN)
- Dark theme enabled by default via `data-theme="dark"`
- Two main functional sections:
  1. Image to Base64 converter (lines 29-61)
  2. Base64 to Image decoder (lines 63-86)

**Core functionality**:
- Image encoding: Uses FileReader.readAsDataURL() to convert File objects to data URLs, then extracts base64 portion
- Image decoding: Accepts base64 strings (with or without data URL prefix), auto-detects image type from base64 headers (JPEG: `/9j/`, PNG: `iVBORw0KGg`, GIF: `R0lGOD`, WebP: `UklGR`)
- Progress animation: Custom gradient-based progress animation on buttons using requestAnimationFrame
- No external JavaScript files or build tools

## Development

**Running the application**:
```bash
# Serve locally with any HTTP server, for example:
python -m http.server 8000
# Then open http://localhost:8000
```

Or simply open `index.html` directly in a browser (file:// protocol works).

**Testing changes**:
- Edit `index.html` and refresh the browser
- No build or compilation step required

## Code Structure Notes

- Global state: `currentImageFile`, `currentBase64`, `currentDataUrl` (lines 101-103)
- Button color constants: `BUTTON_COLOR` and `BUTTON_DISABLED_COLOR` are set dynamically to support theme changes (lines 91-98)
- Minimum operation duration of 500ms enforced for UX purposes (lines 188, 275) with visual progress feedback
- Clipboard operations use deprecated `document.execCommand('copy')` - this still works but could be modernized to use the Clipboard API
