# Embodied Movement: Digital Responsive Interactions

Research exploring the democratization of artistic expression through motion-responsive technology. Developed at UC Berkeley's Berkeley Center for New Media (BCNM) under Dr. Kimiko Ryokai's INFO C262: Tangible User Interfaces course, this project investigates how to leverage unconvential input loops to make digital interfaces function as generative platforms for personal & collective emotional expression.

This research examines:
- How digital movement representation through intertial tracking creates new movement qualities when translated into media art
- How technological interfaces alter participants' spatial experiences
- How different kinesthetic tracking methods influence participants' affective responses through ludic, gesture-reactive visualization
- Methods for disrupting participants' daily repertoire of mobility through digital art

Our post-structural approach to interaction design is characterized by:
- Non-hierarchical interaction models
- Emphasis on emergent, participant-driven experiences
- Rejection of binary conceptualizations of "correct" interaction
- Prioritization of fluid, interpretative experiences

[📄 Read the Full Research Paper](https://github.com/jaredmantell/IntertialInterface/blob/main/Final%20Paper_Embodied%20Movement_Exploring%20Digital%20Responsive%20Interactions_Fall%202024_0.1-1.pdf)
![image](https://github.com/user-attachments/assets/036af8f7-d41c-4b75-a8ba-eb2add8f8d07)

## Overview

A motion-responsive visualization system that runs on RGB images and transforms physical movements into artistic expression. Features two interaction modes:
- **Exploratory Mode**: Designed for general users, enabling intuitive engagement
- **Advanced Mode**: Targeted at professional movement practitioners, providing detailed biomechanical feedback
![image](https://github.com/user-attachments/assets/e2718005-2a8b-483d-904b-c7b12f0ff2c8)

## System Architecture

### Motion Tracking
- MoveNet pose estimation with DepthAI hardware (OAK-1, OAK-D)
- Real-time movement tracking using Kinect Camera 
- Accelerometer (ADXL345) integration for precise motion data

### Visualization
- TouchDesigner for real-time visual feedback
- Point-cloud visualization system
- Gesture-reactive visual elements

## Installation

Install required Python packages:
python3 -m pip install -r requirements.txt

### Hardware Requirements
- Kinect Camera
- ADXL345 Accelerometer
- Arduino Nano
- DepthAI compatible device (OAK-1, OAK-D)

## Usage

Basic demo:
python3 demo.py

Command line arguments:
-e, --edge            Enable Edge processing mode
-m MODEL             Select model ('thunder'/'lightning')
-i INPUT             Input source ('rgb'/'rgb_laconic'/file path)
-f FPS               Set internal camera FPS

### Interactive Controls
| Key    | Function                |
|--------|------------------------|
| Space  | Pause                  |
| c      | Toggle crop region     |
| f      | Show/hide FPS         |
| q/ESC  | Exit                  |
![image](https://github.com/user-attachments/assets/876a0b4c-4ecc-4bd1-8976-f40865cf9ee6)

## Technical Implementation

The system uses two main classes:

# For Host mode:
from MovenetDepthai import MovenetDepthai
# For Edge mode:
from MovenetDepthaiEdge import MovenetDepthai

pose = MovenetDepthai(input_src="rgb", 
                     model="thunder",    
                     score_thresh=0.2)

renderer = MovenetRenderer(pose)

while True:
    frame, body = pose.next_frame()
    if frame is None: break
    frame = renderer.draw(frame, body)
    if renderer.waitKey(1) == 27:
        break

## Research Methods

Our approach leverages:

1. Multiple motion capture technologies
2. Real-time visualization systems
3. User-centered design principles
4. Speculative design methodology
5. Extensive scenario testing

## Project Structure
embodied-movement/
├── src/
│   ├── demo.py
│   ├── MovenetDepthai.py
│   ├── MovenetDepthaiEdge.py
│   └── MovenetRenderer.py
├── docs/
│   └── paper.pdf
└── examples/
    └── demo_scenarios/

## Citation

@inproceedings{thiel2024embodied,
  title={Embodied Movement: Exploring Digital Responsive Interactions},
  author={Thiel, Sonja and Jung, Gyuyeon and Mantell, Jared and Maldonado, Marissa and Bondi, Paloma},
  booktitle={UC Berkeley School of Information},
  year={2024}
}

## Research Team
- Sonja Thiel, UC Berkeley
- Gyuyeon Jung, UC Berkeley
- Jared Mantell, UC Berkeley
- Marissa Maldonado, UC Berkeley
- Paloma Bondi, UC Berkeley

## Acknowledgments
- Prof. Kimiko Ryokai, UC Berkeley
- Vivian Chan, UC Berkeley 
- Christopher Sakuma, University of Pennsylvania

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Credits
- Google Next-Generation Pose Detection with MoveNet and TensorFlow.js
- Katsuya Hyodo (Pinto) for model conversion expertise
