# Embodied Movement: Digital Responsive Interactions

Research exploring human movement and digital interaction through tangible user interfaces, developed at UC Berkeley School of Information. This project investigates how digital systems can translate physical movement into meaningful sensory experiences.

[📄 Read the Full Research Paper](https://github.com/jaredmantell/IntertialInterface/blob/main/Final%20Paper_Embodied%20Movement_Exploring%20Digital%20Responsive%20Interactions_Fall%202024_0.1-1.pdf)

![Demo](img/demo.gif)

## Overview

A motion-responsive visualization system that runs on RGB images and transforms physical movements into artistic expression. Features two interaction modes:
- **Exploratory Mode**: Designed for general users, enabling intuitive engagement
- **Advanced Mode**: Targeted at professional movement practitioners, providing detailed biomechanical feedback

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
