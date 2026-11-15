# Project Scope

## Implemented functionality

- Local PDF page rendering through `pdf2image` and Poppler.
- Webcam frame capture and processing through OpenCV.
- One-hand landmark tracking through MediaPipe Hands.
- Previous and next page controls.
- Freehand drawing using the index fingertip.
- Blue, red, and green annotation colours.
- Clearing annotations on the active page.
- Per-page annotation buffers held in memory during the current run.
- Moving-average stroke smoothing.
- Side-by-side webcam and PDF display.

## Current limitations

- Annotation strokes are not saved into the original PDF.
- Annotations are not saved or restored between application runs.
- PDF zoom and rotation are not implemented in the current code.
- Cloud storage, synchronization, and collaborative editing are not implemented.
- Gesture handling uses landmark-distance thresholds rather than a separately trained gesture-classification model.

## Note on project claims

This scope describes the behavior implemented in the current application. Ideas discussed as possible future enhancements should not be presented as completed features unless working code and test evidence are available.