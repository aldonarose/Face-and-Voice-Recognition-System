# Face and Voice Recognition System

This project is a multi-modal biometric security system that utilizes both face and voice recognition to authenticate users. It features a user-friendly graphical interface to enroll new users by capturing their facial features and a voice sample. Subsequently, it can recognize enrolled users by comparing their live face and voice data against the stored biometric records.
## Table of Contents
* [Features](#features)
* [Technologies Used](#technologies-used)
* [How It Works](#how-it-works)
* [Installation](#installation)
* [Usage](#usage)
## Features
* **Dual-Factor Authentication**: Leverages both facial patterns and voice characteristics for a more secure and reliable user verification process.
* **User-Friendly GUI**: A clean and intuitive graphical user interface built with Tkinter for easy interaction.
* **Simple Enrollment**: A straightforward process to register new users by capturing their face and a short voice sample.
* **Real-time Recognition**: Performs authentication on-the-fly using live data from your webcam and microphone.
## Technologies Used
* **Python**: Core programming language.
* **OpenCV**: For real-time camera access and image processing.
* **face_recognition**: For state-of-the-art face detection and recognition based on dlib's models.
* **librosa & NumPy**: For audio processing, feature extraction (MFCCs), and numerical operations.
* **sounddevice & soundfile**: For recording and handling audio files from the microphone.
* **Tkinter**: For the graphical user interface (GUI).
## How It Works
The system's logic is divided into two main components: enrollment and recognition.
### Enrollment
When a new user is enrolled, the system captures their biometrics in two stages:
* **Face Capture**: The user's face is captured via webcam. The face_recognition library then processes this image to generate a unique 128-dimension facial embedding (a vector of numbers representing the face).
  
* **Voice Capture**: The user records a 3-second audio clip. From this clip, the system uses librosa to extract the ***Mel-Frequency Cepstral Coefficients (MFCCs)***, which are a robust representation of the vocal characteristics. The mean of these coefficients is taken to create a feature vector for the user's voice.

This biometric data (file paths to the face image and voice recording) is then stored in a enrolled_data.json file, mapped to the user's name.
### Recognition
To recognize a user, the system follows a similar process to capture new face and voice samples. It then computes the facial embedding and voice MFCCs for this new data. These are compared against the stored data for all enrolled users using the Euclidean distance:
* A lower face distance signifies a closer facial match.
* A lower voice distance signifies a closer voice match.

A match is confirmed only if both the face distance is below a threshold of 0.6 and the voice distance is below a threshold of 150. The system identifies the user with the lowest combined distance scores as the best match.
## Installation
1. Clone the repository:
```
git clone https://github.com/aldonarose/face-and-voice-recognition-system.git
cd face-and-voice-recognition-system
```
2. Install the required libraries:
```
pip install opencv-python face_recognition sounddevice soundfile librosa numpy
```
## Usage
This application uses a graphical user interface for all operations.
1. Run the main script from your terminal:
```
python "face_and_voice_recognition.ipynb"
```
2. The main application window will open, presenting two options:
  * Enroll New User
  * Recognize User
### Enrolling a New User
1. Click the Enroll New User button.
2. Enter your name in the dialog box that appears and click OK.
3. A camera window will open. Position your face clearly and press the SPACE key to capture the image.
4. A message box will then instruct you to record your voice. Click OK and speak clearly into your microphone for 3 seconds.
5. Once completed, a confirmation message will show that the user has been enrolled successfully.
### Recognizing a User
1. Click the Recognize User button.
2. The camera window will open. Position your face and press the SPACE key.
3. You will be prompted to record your voice. Click OK and speak for 3 seconds.
4. The system will process the inputs and display the recognition result in a message box, either identifying the matched user along with the distance scores or indicating that no match was found.
