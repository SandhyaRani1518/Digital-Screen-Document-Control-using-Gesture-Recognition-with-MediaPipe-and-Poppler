# Gesture and Control Details

## Hand landmarks

The application reads three MediaPipe Hands landmarks:
- `INDEX_FINGER_TIP`
- `THUMB_TIP`
- `INDEX_FINGER_MCP`

## Drawing-mode condition

Drawing mode is enabled when both distance checks pass:
- Index fingertip to thumb tip: greater than 60 pixels.
- Index-finger MCP to index fingertip: greater than 50 pixels.

These values are configurable constants in the implementation. They were set for a 1280 × 720 reference display and may need adjustment for other camera resolutions or setups.

## On-screen controls

The interface defines six control areas near the top of the webcam frame:

| Control | Function |
|---|---|
| LEFT | Move to the previous PDF page |
| RIGHT | Move to the next PDF page |
| CLEAR | Clear annotations on the active page |
| BLUE | Select blue annotation strokes |
| RED | Select red annotation strokes |
| GREEN | Select green annotation strokes |

A one-second cooldown is applied after a control action to reduce accidental repeated activations.

## Annotation behavior

Each PDF page has three bounded point queues, one per drawing colour. A `None` point separates strokes. A moving-average window smooths points when the annotation overlay is rendered. Clearing resets the queues for the active page only.

Annotations are kept in memory for the current application session. They are not exported to the PDF or saved between runs.