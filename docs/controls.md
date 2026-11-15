# Gesture and Control Details

## Hand landmarks used

The source reads the following MediaPipe Hands landmarks:

- `INDEX_FINGER_TIP`
- `THUMB_TIP`
- `INDEX_FINGER_MCP`

## Drawing-mode condition

Drawing mode is enabled when both distance checks pass:

- Index fingertip to thumb tip is greater than 60 pixels.
- Index-finger MCP to index fingertip is greater than 50 pixels.

These thresholds are constants in the supplied source and are based on its 1280 × 720 reference coordinate system. They may need adjustment for different camera resolutions or setups.

## On-screen controls

The interface defines six control areas near the top of the webcam frame:

| Control | Function |
|---|---|
| LEFT | Move to the previous PDF page |
| RIGHT | Move to the next PDF page |
| CLEAR | Clear the active page's annotations |
| BLUE | Select blue annotation strokes |
| RED | Select red annotation strokes |
| GREEN | Select green annotation strokes |

The source uses a one-second cooldown after a control action.

## Annotation behavior

Each PDF page has three bounded point queues, one per drawing colour. A `None` point separates strokes. A moving-average window smooths the points when the annotation overlay is rendered. Clearing resets the queues for the active page only.

Annotations are stored in memory for the active application session. They are not exported to the PDF or saved between runs.
