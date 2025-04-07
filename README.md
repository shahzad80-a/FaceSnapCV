FaceSnapCV is a Python-based project that uses OpenCV and Mediapipe to detect faces and facial landmarks in real-time via webcam. It can serve as a starting point for face recognition, emotion detection, or AR filters.


---

Key Features:

Real-time webcam face detection

Facial landmarks visualization

Lightweight and easy to extend

Built with OpenCV and Mediapipe



---

Code (main.py):

import cv2
import mediapipe as mp

# Initialize Mediapipe face mesh
mp_face_mesh = mp.solutions.face_mesh
face_mesh = mp_face_mesh.FaceMesh(static_image_mode=False, max_num_faces=1)
mp_drawing = mp.solutions.drawing_utils

# OpenCV video capture
cap = cv2.VideoCapture(0)

while cap.isOpened():
    success, frame = cap.read()
    if not success:
        break

    # Flip the frame for natural interaction
    frame = cv2.flip(frame, 1)
    rgb_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    
    # Process the frame
    result = face_mesh.process(rgb_frame)

    # Draw face landmarks
    if result.multi_face_landmarks:
        for face_landmarks in result.multi_face_landmarks:
            mp_drawing.draw_landmarks(
                frame,
                face_landmarks,
                mp_face_mesh.FACEMESH_CONTOURS,
                mp_drawing.DrawingSpec(color=(0, 255, 0), thickness=1, circle_radius=1),
                mp_drawing.DrawingSpec(color=(0, 0, 255), thickness=1)
            )

    cv2.imshow('FaceSnapCV - Press Q to Quit', frame)

    if cv2.waitKey(5) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()


---

Requirements (requirements.txt):

opencv-python
mediapipe

