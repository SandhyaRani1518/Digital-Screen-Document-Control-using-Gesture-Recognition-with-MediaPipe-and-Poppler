# System Architecture

## Main components

### 1. PDF rendering

The application converts a multi-page PDF into images using `pdf2image`, which invokes Poppler. The rendered pages are stored in memory and the active page is shown beside the webcam view.

### 2. Webcam and hand tracking

OpenCV captures webcam frames and mirrors the view. MediaPipe Hands processes each frame and supplies hand landmarks. The supplied implementation tracks one hand.

### 3. Interaction logic

The application reads three landmarks:

- Index fingertip
- Thumb tip
- Index-finger MCP

It calculates distances between the fingertip and the other two landmarks. The resulting threshold checks determine whether the pointer is in drawing mode. The fingertip position is also checked against the on-screen control areas.

### 4. Page and annotation state

The application maintains the current PDF page, selected annotation colour, and a bounded annotation queue for each page and colour. A clear action resets the active page's queues.

### 5. Rendering and display

Annotation points are smoothed with a moving-average window and drawn onto a copy of the active PDF page. The annotated page and webcam frame are resized and combined into a side-by-side OpenCV window.

## Data flow

```text
PDF -> pdf2image / Poppler -> page images
                                  |
Webcam -> OpenCV -> MediaPipe Hands -> landmarks
                                  |
                     fingertip / distance checks
                         |                 |
                         v                 v
                 control selection    drawing mode
                         |                 |
                         v                 v
                  page / colour      annotation points
                    / clear                 |
                         |                 v
                         +------> per-page annotation queues
                                           |
                                           v
                                  smoothed drawing overlay
                                           |
                                           v
                                  combined display window
```

## Runtime behavior

The application reads frames continuously until the user presses `q` in the display window. A cooldown is applied to page, colour, and clear control actions to reduce repeated activations.

## Design boundaries

The supplied code does not persist annotations, modify the source PDF, or provide zoom, cloud synchronization, or collaborative editing.
