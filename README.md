<p align="center">
  <img src="./img.png" alt="Project Banner" width="100%">
</p>

# [VIRTUAL MOUSE] 🎯

## Basic Details

### Team Name: [Syntax Squad]

### Team Members
- Member 1: [Farhana Sherin E] - [NSS College Of Engineering Palakkad]
- Member 2: [Jinsha Mol C T] - [NSS College Of Engineering Palakkad]

### Hosted Project Link
[mention your project hosted link here]

### Project Description
[A computer vision-based mouse control system that enables users to interact with computers using hand movements. The project detects hand landmarks, calculates angles and distances between fingers, and converts gestures into system commands for touchless interaction.]

### The Problem statement
[Physical interaction with devices can be inconvenient, unhygienic, and inaccessible in certain environments like hospitals, public kiosks, and presentations. Traditional input devices such as keyboards and mice also limit natural human-computer interaction.]

### The Solution
[The system uses computer vision and machine learning techniques to detect hand gestures using a webcam. It calculates angles and distances between hand landmarks and maps gestures to computer control actions, enabling hands-free device operation.]

---

## Technical Details

### Technologies/Components Used

**For Software:**
- Languages used: [Python]
- Frameworks used: OpenCV-based vision pipeline]
- Libraries used: [OpenCV,MediaPipe(for hand landmark detection),Numpy,PyAutoGUI,pynput]
- Tools used: [VS Code,Git,GitHub,Webcam]

**For Hardware:**
- Main components: [List main components]
- Specifications: [Technical specifications]
- Tools required: [List tools needed]

---

## Features

List the key features of your project:
- Real-time hand tracking: [Detects hand landmarks using computer vision]
- Gesture Recognition: [Identifies gestures using angle and distance calculation.]
- Touchless Interaction: [Enables hands-free system control-Cursor move,Left Click,Right Click,Double Click,ScreenShot]
- Lightweight & Low Cost: [Works using a standard webcam]

---

## Implementation

### For Software:

#### Installation
```bash
[pip install opencv-python mediapipe pyautogui numpy pynput]
```

#### Run
```bash
[python main.py]
```

### For Hardware:

#### Components Required
[List all components needed with specifications]

#### Circuit Setup
[Explain how to set up the circuit]

---

## Project Documentation

### For Software:

#### Screenshots (Add at least 3)

![[Screenshot1](https://drive.google.com/file/d/1387kCticlnWRwPRr2zazhgDzoedTxQp1/view?usp=drivesdk)](hand detection)
*This is how the hand is detected by using webcam*

![[Screenshot2](https://drive.google.com/file/d/19pbt9wIombIojhHRAHryi7FmEEs9lfYE/view?usp=drivesdk)](Right click)
*The right-click gesture enables users to perform the mouse right-click action using hand movements. When the system detects a specific finger position pattern, it interprets the gesture and triggers the right mouse button automatically. This allows users to open context menus and perform secondary actions without using a physical mouse.
*

![[Screenshot3](https://drive.google.com/file/d/1qchDCGgpgiIhKfGN8t8y4rFHtgWXwy7C/view?usp=drivesdk)](Left click)
*The **Left Click** is triggered when the index finger folds (angle < 50°) while the middle finger remains extended and the thumb-index distance is high. Once these conditions are met, the system uses the `pynput` controller to execute a press and release sequence on the left mouse button. A green "Left Click" label is then displayed on the screen to provide immediate visual feedback to the user.*

![[Screenshot4](https://drive.google.com/file/d/1KyGUM0HSbe2YxTyxten4tJQmFiQVz6zd/view?usp=drivesdk))](ScreenShot taken)
*The Screenshot function is activated by a "pinch" gesture, where the distance between the thumb and index finger drops below 50 units while both the index and middle fingers are folded. Upon detection, the system captures the screen using pyautogui, saves the file with a unique random identifier, and displays a "Screenshot Taken" alert on the interface.*

![[Screenshot5](https://drive.google.com/file/d/1WQ4ZHJTw4JFtpzIAajsq7ihaHCkKI1Va/view?usp=drivesdk))](Double click)
*The Double Click gesture is recognized when both the index and middle fingers are folded simultaneously (both angles < 50°) while maintaining a high thumb-index distance. Under these specific geometric conditions, the system invokes pyautogui.doubleClick() to simulate a rapid two-tap sequence. To assist the user, a yellow "Double Click" overlay is rendered on the live video feed.*

![[Screenshot6](https://drive.google.com/file/d/1FDxPs8pHTwq2RXiYr2HOetOwRxTLWA4L/view?usp=drivesdk))](Cursor move)
*The Cursor Move function is the primary navigation mode, activated when the system detects a "navigation pose" characterized by a folded thumb-index distance (distance < 50) while the index finger itself remains extended (angle > 90°). The system captures the normalized coordinates of the index finger tip and maps them directly to your monitor's pixel resolution using linear interpolation.s*

#### Diagrams

**System Architecture:**

![Architecture Diagram](![WhatsApp Image 2026-02-14 at 8 26 30 AM](https://github.com/user-attachments/assets/453ce2e7-d35c-4fbb-9766-f66eabccde8b)

)
*1. System Components & Layers

The architecture is divided into three logical tiers:
A. Perception Layer (Data Ingestion)

    Webcam Module: Captures the video stream. This is the "eye" of the system.

    Preprocessing Unit: Standardizes the frame.

        Flipping: Since webcams are usually front-facing, we mirror the image so that moving your hand to the left moves the cursor to the left.

        Color Conversion: Changes BGR (OpenCV default) to RGB (MediaPipe/AI default).

B. Intelligence Layer (The "Brain")

    Hand Tracking Engine: Uses a pre-trained ML model (like MediaPipe) to identify 21 3D landmarks (joints).

    Coordinate Translator: Maps the 2D coordinates from the webcam resolution (e.g., 640x480) to the user's screen resolution (e.g., 1920x1080).

    Heuristic Logic Engine: This is where the "Rules" live.

        Rule 1: If Index and Middle fingers are close → Left Click.

        Rule 2: If Index is up and Middle is down → Mouse Move.

C. Execution Layer (System Integration)

    Command Mapper: Translates the logic result into a specific function call.

    OS Driver Interface: Uses system libraries to inject mouse/keyboard events directly into the Operating System's event queue.

2. Data Flow (The "Journey of a Click")

    Stream: The webcam sends a Raw Frame Matrix to the Python environment.

    Detection: The ML model outputs a List of Coordinates (x,y,z for 21 points).

    Calculation: The system calculates the Euclidean Distance between point 8 (Index Tip) and point 12 (Middle Tip).
    d=(x2​−x1​)2+(y2​−y1​)2​

    Decision: If d<threshold, a "Click" signal is generated.

    Interrupt: The OS receives a virtual click event at the current x,y position.

3. Tech Stack Interaction
Component	Technology	Role
Language	Python	The glue that connects all modules.
Computer Vision	OpenCV	Handles video capture, frame flipping, and UI overlays.
Machine Learning	MediaPipe	High-speed hand landmark detection (uses On-Device ML).
Math Engine	NumPy / Math	Performs vector calculations for finger distances/angles.
OS Automation	PyAutoGUI / pynput	Controls the hardware mouse and keyboard via software.
Summary Table
Step	Data Form	Process
Input	Pixels (RGB)	cv2.VideoCapture()
Processing	Landmarks (X, Y)	mp.hands.Hands()
Logic	Boolean (True/False)	Distance Thresholding
Output	Win32/X11 Event	pyautogui.click()*

**Application Workflow:**

![Workflow](![WhatsApp Image 2026-02-14 at 8 44 30 AM](https://github.com/user-attachments/assets/9aa63a6b-d7dd-4b02-adee-b4b9c2d1024e)
)
*Initialization & Ingestion: The process begins by initializing the software environment (OpenCV, MediaPipe) and capturing live frames from the webcam.

The Detection Gate: This is a critical decision point. The system uses a hand-tracking model to scan the frame. If no hand is detected, it enters a "No" loop, discarding the current frame and moving to the next to optimize processing.

Data Conversion (Landmarks): Once a hand is confirmed, the system extracts 21 key landmarks. This stage effectively translates a physical hand into a mathematical coordinate system (x,y,z points).

Gesture Recognition Logic: The system interprets the landmarks. It calculates spatial relationships—such as the distance between the index and thumb—to determine if the user is performing a specific "gesture" rather than just moving their hand.

Execution & Loop: The recognized gesture is mapped to a system command (like a Left Click). After the action is executed, the system checks for an exit signal. If none is found, it loops back to the webcam capture to process the next millisecond of movement.*

---

### For Hardware:

#### Schematic & Circuit

![Circuit](Add your circuit diagram here)
*Add caption explaining connections*

![Schematic](Add your schematic diagram here)
*Add caption explaining the schematic*

#### Build Photos

![Team](Add photo of your team here)

![Components](Add photo of your components here)
*List out all components shown*

![Build](Add photos of build process here)
*Explain the build steps*

![Final](Add photo of final product here)
*Explain the final build*

---

## Additional Documentation

### For Web Projects with Backend:

#### API Documentation

**Base URL:** `https://api.yourproject.com`

##### Endpoints

**GET /api/endpoint**
- **Description:** [What it does]
- **Parameters:**
  - `param1` (string): [Description]
  - `param2` (integer): [Description]
- **Response:**
```json
{
  "status": "success",
  "data": {}
}
```

**POST /api/endpoint**
- **Description:** [What it does]
- **Request Body:**
```json
{
  "field1": "value1",
  "field2": "value2"
}
```
- **Response:**
```json
{
  "status": "success",
  "message": "Operation completed"
}
```

[Add more endpoints as needed...]

---

### For Mobile Apps:

#### App Flow Diagram

![App Flow](docs/app-flow.png)
*Explain the user flow through your application*

#### Installation Guide

**For Android (APK):**
1. Download the APK from [Release Link]
2. Enable "Install from Unknown Sources" in your device settings:
   - Go to Settings > Security
   - Enable "Unknown Sources"
3. Open the downloaded APK file
4. Follow the installation prompts
5. Open the app and enjoy!

**For iOS (IPA) - TestFlight:**
1. Download TestFlight from the App Store
2. Open this TestFlight link: [Your TestFlight Link]
3. Click "Install" or "Accept"
4. Wait for the app to install
5. Open the app from your home screen

**Building from Source:**
```bash
# For Android
flutter build apk
# or
./gradlew assembleDebug

# For iOS
flutter build ios
# or
xcodebuild -workspace App.xcworkspace -scheme App -configuration Debug
```

---

### For Hardware Projects:

#### Bill of Materials (BOM)

| Component | Quantity | Specifications | Price | Link/Source |
|-----------|----------|----------------|-------|-------------|
| Arduino Uno | 1 | ATmega328P, 16MHz | ₹450 | [Link] |
| LED | 5 | Red, 5mm, 20mA | ₹5 each | [Link] |
| Resistor | 5 | 220Ω, 1/4W | ₹1 each | [Link] |
| Breadboard | 1 | 830 points | ₹100 | [Link] |
| Jumper Wires | 20 | Male-to-Male | ₹50 | [Link] |
| [Add more...] | | | | |

**Total Estimated Cost:** ₹[Amount]

#### Assembly Instructions

**Step 1: Prepare Components**
1. Gather all components listed in the BOM
2. Check component specifications
3. Prepare your workspace
![Step 1](images/assembly-step1.jpg)
*Caption: All components laid out*

**Step 2: Build the Power Supply**
1. Connect the power rails on the breadboard
2. Connect Arduino 5V to breadboard positive rail
3. Connect Arduino GND to breadboard negative rail
![Step 2](images/assembly-step2.jpg)
*Caption: Power connections completed*

**Step 3: Add Components**
1. Place LEDs on breadboard
2. Connect resistors in series with LEDs
3. Connect LED cathodes to GND
4. Connect LED anodes to Arduino digital pins (2-6)
![Step 3](images/assembly-step3.jpg)
*Caption: LED circuit assembled*

**Step 4: [Continue for all steps...]**

**Final Assembly:**
![Final Build](images/final-build.jpg)
*Caption: Completed project ready for testing*

---

### For Scripts/CLI Tools:

#### Command Reference

**Basic Usage:**
```bash
python script.py [options] [arguments]
```

**Available Commands:**
- `command1 [args]` - Description of what command1 does
- `command2 [args]` - Description of what command2 does
- `command3 [args]` - Description of what command3 does

**Options:**
- `-h, --help` - Show help message and exit
- `-v, --verbose` - Enable verbose output
- `-o, --output FILE` - Specify output file path
- `-c, --config FILE` - Specify configuration file
- `--version` - Show version information

**Examples:**

```bash
# Example 1: Basic usage
python script.py input.txt

# Example 2: With verbose output
python script.py -v input.txt

# Example 3: Specify output file
python script.py -o output.txt input.txt

# Example 4: Using configuration
python script.py -c config.json --verbose input.txt
```

#### Demo Output

**Example 1: Basic Processing**

**Input:**
```
This is a sample input file
with multiple lines of text
for demonstration purposes
```

**Command:**
```bash
python script.py sample.txt
```

**Output:**
```
Processing: sample.txt
Lines processed: 3
Characters counted: 86
Status: Success
Output saved to: output.txt
```

**Example 2: Advanced Usage**

**Input:**
```json
{
  "name": "test",
  "value": 123
}
```

**Command:**
```bash
python script.py -v --format json data.json
```

**Output:**
```
[VERBOSE] Loading configuration...
[VERBOSE] Parsing JSON input...
[VERBOSE] Processing data...
{
  "status": "success",
  "processed": true,
  "result": {
    "name": "test",
    "value": 123,
    "timestamp": "2024-02-07T10:30:00"
  }
}
[VERBOSE] Operation completed in 0.23s
```

---

## Project Demo

### Video
[Add your demo video link here - YouTube, Google Drive, etc.]

*Touchless Navigation: Move the mouse cursor by hovering your index finger in the air.

    Intuitive Click Actions: * Left Click: Triggered by folding the index finger while keeping the middle finger extended.

        Right Click: Triggered by folding the middle finger while keeping the index finger extended.

        Double Click: Triggered by folding both the index and middle fingers simultaneously.

    System Integration: Built-in support for capturing screenshots using a specific "pinch" gesture (low distance between thumb and index).

    Visual Feedback: On-screen text overlays provide real-time confirmation of the detected gesture (e.g., "Left Click" or "Screenshot Taken").

User Flow

    Initialization: The system activates the webcam and loads the MediaPipe Hand tracking model.

    Hand Capture: The user places their hand within the camera's field of view. The frame is mirrored (flipped) to ensure that moving the hand right moves the cursor right.

    Real-Time Tracking: The system identifies 21 key hand landmarks and draws a skeleton overlay on the user's hand for visual tracking.

    Gesture Detection: * If the thumb and index finger are close, the system enters Movement Mode, mapping the index tip's position to the screen coordinates.

        If specific finger angles or distances are met, the corresponding Mouse Event (Click/Screenshot) is triggered.

    Execution: The system uses OS-level controllers to execute the command immediately on the computer.

Technical Highlights
1. Computer Vision Pipeline

The project utilizes MediaPipe Hands, a high-fidelity hand and finger tracking solution. It uses machine learning to infer 21 3D landmarks of a hand from just a single frame.
2. Angle & Distance Heuristics

Instead of complex deep learning classifiers for gestures, this project uses Geometric Heuristics:

    Angle Calculation: Uses np.arctan2 to calculate the joint angles between three landmarks (e.g., the knuckle, middle joint, and fingertip).

    Euclidean Distance: Uses np.hypot to measure the gap between the thumb and index finger to distinguish between navigation and clicking modes.
    L=((x2​−x1​)2+(y2​−y1​)2)^(1/2)​

3. Coordinate Mapping & Interpolation

Because webcam resolutions (often 640x480) differ from screen resolutions (e.g., 1920x1080), the system performs Linear Interpolation. The np.interp function is used to scale normalized landmark coordinates (0 to 1) to specific pixel values suitable for pyautogui or pynput execution.
4. Multi-Library Tech Stack

    OpenCV: Handles video stream acquisition and UI rendering.

    PyAutoGUI & Pynput: Provide the "System Mouse Controller" functionality to interact with the OS.

    NumPy: Powers the high-speed mathematical calculations required for real-time responsiveness.*

### Additional Demos
[Add any extra demo materials/links - Live site, APK download, online demo, etc.]

---

## AI Tools Used (Optional - For Transparency Bonus)

If you used AI tools during development, document them here for transparency:

**Tool Used:** [ChatGPT,Gemini]

**Purpose:** [What you used it for]
-ChatGPT : "For error detection and Syntax"
-Gemini: "flow chart"
- Example: "Code review and optimization suggestions"

**Key Prompts Used:**
- "Create a REST API endpoint for user authentication"
- "Debug this async function that's causing race conditions"
- "Optimize this database query for better performance"

**Percentage of AI-generated code:** [10%]

**Human Contributions:**
- Architecture design and planning
- Custom business logic implementation
- Integration and testing
- UI/UX design decisions

*Note: Proper documentation of AI usage demonstrates transparency and earns bonus points in evaluation!*

---

## Team Contributions

- [Farhana Sherin E]: [openCv,Flow chart,Architecture,pyautogui]
- [Jinsha Mol C T]: [Mediapipe,README.md,main function]
- [Name 3]: [Specific contributions - e.g., UI/UX design, Testing, Documentation, etc.]

---

## License

This project is licensed under the [LICENSE_NAME] License - see the [LICENSE](LICENSE) file for details.

**Common License Options:**
- MIT License (Permissive, widely used)
- Apache 2.0 (Permissive with patent grant)
- GPL v3 (Copyleft, requires derivative works to be open source)

---

Made with ❤️ at TinkerHub
