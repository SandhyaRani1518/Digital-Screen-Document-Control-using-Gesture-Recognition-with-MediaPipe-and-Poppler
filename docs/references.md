# Technical References

This page lists official documentation for the libraries and tools used by the project. These sources describe the underlying dependencies; the project-specific workflow and controls are documented from the application's implementation.

1. **MediaPipe Hands — Legacy Solutions API.**
   https://github.com/google-ai-edge/mediapipe/blob/master/docs/solutions/hands.md
   The project uses the legacy Python API `mp.solutions.hands` for real-time hand landmark tracking.

2. **MediaPipe Solutions guide — legacy status and migration.**
   https://ai.google.dev/edge/mediapipe/solutions/guide
   Google states that support for MediaPipe Legacy Solutions ended on March 1, 2023. The guide identifies Hand Landmarker as the upgraded solution for hand landmark detection. Migration is a future maintenance task for this project.

3. **MediaPipe Hand Landmarker — Python guide.**
   https://developers.google.com/edge/mediapipe/solutions/vision/hand_landmarker/python
   Current task-based API documentation for a future migration from the legacy Hands API.

4. **OpenCV-Python tutorials.**
   https://docs.opencv.org/4.13.0/d6/d00/tutorial_py_root.html
   Background documentation for image processing, webcam/video capture, display windows, and drawing operations.

5. **pdf2image documentation.**
   https://pdf2image.readthedocs.io/en/stable/
   Documents the Python interface used to convert PDF pages into images.

6. **Poppler project.**
   https://poppler.freedesktop.org/
   Project site for the PDF rendering utilities used by pdf2image.

7. **NumPy documentation.**
   https://numpy.org/doc/stable/
   Reference for array operations and numerical processing used in the application.

8. **GitHub Docs — licensing a repository.**
   https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
   Explains the role of an explicit open-source license and the implications of publishing a repository without one.

## Attribution note

These links acknowledge the external tools and provide their official technical documentation. They are not sources for the project's own code.