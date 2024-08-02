# pythonOpenCV5HandJoints
This project senses the hand signal through the webcam
DOCUMENTATION
import cv2: This imports the OpenCV library, which is used for computer vision tasks.
import mediapipe as mp: This imports the MediaPipe library and assigns it the alias mp. MediaPipe is used for hand tracking and other computer vision tasks.
mp_hands = mp.solutions.hands: This assigns the hand tracking solution from MediaPipe to mp_hands.
mp_drawing = mp.solutions.drawing_utils: This assigns the drawing utilities from MediaPipe to mp_drawing. These utilities help in drawing landmarks and connections on the detected hand.
cap = cv2.VideoCapture(0): This initializes the webcam for capturing video. 0 usually refers to the default webcam of the laptop
with mp_hands.Hands(...) as hands: This initializes the hand tracking model with specific parameters and assigns it to hands.
static_image_mode=False: This parameter indicates that the input images are not static. The model will treat the input as a video stream.
max_num_hands=1: This sets the maximum number of hands to detect.
min_detection_confidence=0.7: This sets the minimum confidence value for the hand detection to be considered successful.
min_tracking_confidence=0.7: This sets the minimum confidence value for the hand landmarks to be considered successfully tracked.
while cap.isOpened():: This loop runs as long as the webcam is open
success, image = cap.read(): This captures a frame from the webcam. success is a boolean indicating if the frame was captured successfully, and image is the captured frame.
if not success:: This checks if the frame was not captured successfully.
print("Ignoring empty camera frame."): This prints a message if the frame was not captured successfully.
continue: This skips the rest of the loop and continues to the next iteration if the frame was not captured successfully.
image = cv2.flip(image, 1): This flips the image horizontally to provide a mirror view (selfie-view).
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB): This converts the image from BGR color space (used by OpenCV) to RGB color space (used by MediaPipe).
image.flags.writeable = False: This marks the image as not writable to improve performance by passing it by reference.
results = hands.process(image): This processes the image to detect hands and returns the results.
image.flags.writeable = True: This marks the image as writable again.
image = cv2.cvtColor(image, cv2.COLOR_RGB2BGR): This converts the image back to BGR color space for display using OpenCV.
if results.multi_hand_landmarks:: This checks if any hand landmarks were detected.
for hand_landmarks in results.multi_hand_landmarks:: This iterates through each detected hand's landmarks.
for landmark in hand_landmarks.landmark:: This iterates through each landmark in the detected hand.
x = int(landmark.x * image.shape[1]): This calculates the x-coordinate of the landmark in pixel space.
y = int(landmark.y * image.shape[0]): This calculates the y-coordinate of the landmark in pixel space.
cv2.circle(image, (x, y), 5, (255, 0, 0), -1): This draws a blue circle at the landmark position on the image.
mp_drawing.draw_landmarks(...): This uses MediaPipe's drawing utilities to draw the landmarks and connections on the hand.
image: The image to draw on.
hand_landmarks: The landmarks to draw.
mp_hands.HAND_CONNECTIONS: The connections between the landmarks to draw.
mp_drawing.DrawingSpec(color=(0, 0, 255), thickness=2, circle_radius=2): The drawing specification for the landmarks.
mp_drawing.DrawingSpec(color=(0, 255, 0), thickness=2, circle_radius=2): The drawing specification for the connections.
cv2.imshow('Hand Tracking', image): This displays the image with the hand tracking annotations in a window named 'Hand Tracking'.
if cv2.waitKey(5) & 0xFF == 27:: This waits for 5 milliseconds for a key press. If the 'Esc' key (key code 27) is pressed, it breaks the loop.
cap.release(): This releases the webcam.
cv2.destroyAllWindows(): This closes all OpenCV windows.
This coverS all the lines of the code. If there are any issues, let me know!
