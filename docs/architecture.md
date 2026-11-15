# System Architecture

## Main components

### 1. PDF rendering

The application converts a multi-page PDF into images using `pdf2image`, which calls Poppler utilities. The rendered pages are held in memory, and the active page is displayed beside the webcam feed.

### 2. Webcam and hand tracking

OpenCV captures and mirrors webcam frames. MediaPipe Hands processes each frame and returns hand landmarks. The current application tracks one hand.

### 3. Interaction logic

The application uses three hand landmarks:
- Index fingertip
- Thumb tip
- Index-finger MCP (metacarpophalangeal joint)

It calculates the distances between the index fingertip and the other two landmarks. Threshold checks determine whether drawing mode is active. The fingertip position is also checked against the on-screen control areas.

### 4. Page and annotation state

The application stores the active PDF page, the selected annotation colour, and a bounded point queue for each page and colour. The CLEAR control resets the queues for the active page.

### 5. Rendering and display

Annotation points are smoothed with a moving-average window and drawn on a copy of the active PDF page. The annotated page and webcam frame are resized and combined in a side-by-side OpenCV window.

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

The application processes webcam frames continuously until the user presses `q` in the display window. A cooldown helps prevent repeated activation of page, colour, and clear controls.

## Design boundaries

Annotations are temporary and are not written back into the original PDF. The current implementation does not provide persistent annotation storage, zoom, cloud synchronization, or collaborative editing.