# Gesture-Based PDF Navigation and Annotation

A webcam-based document interaction prototype that lets users move through PDF pages and add on-screen annotations using hand movements.

## Overview

The application uses MediaPipe Hands to track hand landmarks, OpenCV to capture and process webcam frames, and pdf2image with Poppler to render PDF pages. The index fingertip acts as the pointer for document controls and freehand drawing.

The PDF page and webcam feed appear side by side. Annotation strokes are drawn over a copy of the rendered page and are kept separately for each page during the current session.

## Features

- Render multi-page PDF documents as images.
- Track one hand in real time using MediaPipe Hands.
- Navigate to the previous or next page using on-screen controls.
- Draw freehand annotations using the index fingertip.
- Choose blue, red, or green annotation colours.
- Clear annotations from the active page.
- Maintain separate in-memory annotation points for each PDF page.
- Smooth drawing paths using a moving-average window.
- Display the PDF and webcam feed side by side.

## How it works

```text
PDF document -> pdf2image / Poppler -> Rendered pages
                                           |
Webcam -> OpenCV -> MediaPipe Hands -> Hand landmarks
                                           |
                               Fingertip position and distances
                                           |
                              Page / colour / clear controls
                                           |
                                     Drawing mode
                                           |
                              Per-page annotation points
                                           |
                               Smoothed drawing overlay
                                           |
                             Combined PDF + webcam view
```

## Technology stack

- **Python** — application logic
- **MediaPipe Hands** — hand landmark tracking
- **OpenCV** — webcam capture, image processing, and drawing
- **NumPy** — image and coordinate calculations
- **pdf2image** — PDF page conversion
- **Poppler** — PDF rendering utilities

## Gesture and control mapping

| Control or movement | Action |
|---|---|
| LEFT | Go to the previous PDF page |
| RIGHT | Go to the next PDF page |
| CLEAR | Remove annotations from the active page |
| BLUE / RED / GREEN | Select the annotation colour |
| Index fingertip in drawing mode | Add a freehand annotation stroke |

Drawing mode is based on distances between the index fingertip, thumb tip, and index-finger MCP landmark. The current implementation uses threshold-based interaction logic; it does not use a separately trained gesture-classification model. It uses MediaPipe's legacy Solutions API (`mp.solutions.hands`), which Google no longer supports as of March 1, 2023. Migrating to the MediaPipe Hand Landmarker task is a recommended future maintenance step. See the [MediaPipe migration and legacy-solutions guide](https://ai.google.dev/edge/mediapipe/solutions/guide).

## Current scope and limitations

- Annotations remain in memory during the current application session.
- The application draws over a rendered page; it does not save annotations into the original PDF.
- Annotation data is not restored after the application closes.
- The current implementation does not include PDF zoom, cloud synchronization, or multi-user collaboration.
- Gesture responsiveness can vary with lighting, camera position, webcam quality, and threshold settings.
- No measured accuracy or performance figures are stated here. Any such figures should be supported by a repeatable test procedure.

## Repository contents

This repository provides a public project overview and design notes. It does not contain the original implementation files or the complete academic paper.

- `docs/architecture.md` — system components and data flow
- `docs/controls.md` — hand landmarks, thresholds, and controls
- `docs/project-scope.md` — implemented features and limitations
- `docs/references.md` — official library documentation and API status

## References

Technical documentation for the libraries and tools used in this project is listed in [`docs/references.md`](docs/references.md). These links are background references for the dependencies; the project-specific workflow and controls are described from the application's own implementation.

## Project acknowledgement

This project was developed collaboratively as an academic project.

## License and reuse

This repository does not currently include a separate open-source license. GitHub's terms allow other GitHub users to view and fork public repositories through GitHub. That platform permission is not the same as a general project license granting additional reuse rights elsewhere. Because this was collaborative work, check with the other contributors before adding a license or granting broader permission to copy, modify, or redistribute the project materials. See [GitHub's guide to repository licensing](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository) for an explanation of what the absence of a license means.