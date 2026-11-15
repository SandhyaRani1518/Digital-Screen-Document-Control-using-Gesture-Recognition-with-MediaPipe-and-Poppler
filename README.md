# Digital Screen Document Control Using Gesture Recognition

A webcam-based, touchless PDF interaction prototype that lets a user navigate document pages and add simple on-screen annotations using hand tracking.

## Overview

The application combines MediaPipe Hands, OpenCV, and Poppler-based PDF rendering. A webcam captures the user's hand, MediaPipe detects hand landmarks, and the application uses fingertip position and landmark distances to trigger document controls and freehand drawing.

The PDF is displayed beside the webcam feed. Annotation strokes are drawn over the rendered page, with a separate in-memory annotation buffer for each page while the application is running.

## Features implemented in the supplied Python source

- Render a multi-page PDF into images using `pdf2image` and Poppler.
- Track one hand using MediaPipe Hands.
- Navigate to the previous or next PDF page using on-screen LEFT and RIGHT control areas.
- Draw on the active page using the index fingertip.
- Select blue, red, or green annotation strokes.
- Clear annotations on the active page.
- Keep page-specific annotation buffers during the current run.
- Smooth drawing paths with a moving-average window.
- Display the webcam and PDF page side by side.

## How it works

```text
PDF file -> pdf2image / Poppler -> Rendered PDF pages
                                      |
Webcam -> OpenCV -> MediaPipe Hands -> Hand landmarks
                                      |
                          Fingertip position and distances
                                      |
                         Page / colour / clear controls
                                      |
                                Drawing mode
                                      |
                       Per-page annotation buffers
                                      |
                         Smoothed annotation overlay
                                      |
                      Side-by-side PDF + webcam display
```

## Technology stack

- **Python** — application logic
- **MediaPipe Hands** — real-time hand landmark tracking
- **OpenCV** — webcam capture, interface rendering, and drawing
- **NumPy** — image and coordinate calculations
- **pdf2image** — PDF page conversion
- **Poppler** — PDF rendering backend

## Gesture and control mapping

| On-screen control / movement | Action |
|---|---|
| LEFT | Previous PDF page |
| RIGHT | Next PDF page |
| CLEAR | Clear annotations on the current page |
| BLUE / RED / GREEN | Choose the annotation colour |
| Index fingertip moved in drawing mode | Add a freehand annotation stroke |

The supplied implementation determines drawing mode using distances between the index fingertip, thumb tip, and index-finger MCP landmark. It uses threshold-based interaction logic rather than a separately trained gesture-classification model.

## Project scope and limitations

- Annotations are held in memory only for the current application session.
- The supplied source does not write annotations back into the original PDF.
- The supplied source does not implement persistent annotation storage, zoom, cloud synchronization, or multi-user collaboration.
- Gesture responsiveness can vary with lighting, camera position, webcam quality, and threshold settings.
- No performance or accuracy figures are claimed by this overview; measured results require a documented and repeatable test procedure.

## Public repository scope

This repository is a **public project overview**. It contains the project explanation and high-level design notes, not the original implementation source, full academic paper, abstract, or team documents.

## Project areas

- `docs/architecture.md` — component architecture and data flow
- `docs/controls.md` — hand landmarks, thresholds, and controls
- `docs/project-scope.md` — included functionality and current boundaries

## Credits and permissions

The underlying project was developed as a collaborative academic project. This overview intentionally omits personal contact details and does not redistribute team documents. Before publishing implementation files, screenshots, or publication material, confirm that you have permission to share them and that any co-authors' rights and privacy are respected.

## License

No reuse license is granted by this overview. Add a license only after confirming the relevant ownership and permissions.
