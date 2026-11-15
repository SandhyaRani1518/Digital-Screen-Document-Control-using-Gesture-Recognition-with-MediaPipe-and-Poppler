# Technical References

This page lists official documentation for the libraries and tools used by the gesture-based PDF navigation and annotation prototype. These sources explain the underlying tools; the project-specific feature descriptions and workflow are based on the application's own implementation.

1. **Google AI Edge / MediaPipe — MediaPipe Hands (Legacy Solutions API).**
   https://github.com/google-ai-edge/mediapipe/blob/master/docs/solutions/hands.md
   Relevant to the application's use of `mp.solutions.hands`, hand landmarks, and the MediaPipe Python Solutions API.

2. **OpenCV — OpenCV-Python Tutorials.**
   https://docs.opencv.org/5.0/py_tutorials/py_tutorials.html
   Background documentation for image processing, webcam capture, displaying images, and drawing with OpenCV.

3. **Belval — pdf2image documentation.**
   https://pdf2image.readthedocs.io/en/stable/
   Documents the Python interface used to convert PDF pages into images.

4. **Poppler — PDF rendering library and utilities.**
   https://poppler.freedesktop.org/
   Project documentation and downloads for the PDF rendering utilities used by pdf2image.

5. **NumPy — Official documentation.**
   https://numpy.org/doc/stable/
   Reference for array operations and numerical processing used in the application.

6. **GitHub Docs — Licensing a repository.**
   https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
   Explains the difference between a public repository and a repository that includes an explicit open-source license.

## Attribution note

Library names and links are included to acknowledge the external tools and provide readers with their official documentation. The project overview does not reproduce text or source code from these documentation pages.