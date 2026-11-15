# Project Scope

## Included in the supplied implementation

- Local PDF page rendering through `pdf2image` and Poppler.
- Webcam frame capture through OpenCV.
- One-hand landmark tracking through MediaPipe Hands.
- Previous / next page controls.
- Freehand drawing using the index fingertip.
- Blue, red, and green annotation colours.
- Clearing annotations on the current page.
- Per-page annotation buffers held in memory during the current run.
- Moving-average stroke smoothing.
- Side-by-side webcam and PDF display.

## Not included in the supplied implementation

- Saving annotation strokes to the PDF.
- Saving or restoring annotations between application runs.
- Zooming or rotating PDF pages.
- Cloud storage or synchronization.
- Multi-user or real-time collaborative editing.
- A separately trained gesture classification model.

## Publication note

This document describes the functionality present in the supplied Python source. Features mentioned as possible extensions in project materials should not be presented as implemented unless separate working code and test evidence are available.
