# Embodied Movement: Digital Responsive Interactions

Research exploring novel methods of of artistic expression through motion-responsive technology. Developed at UC Berkeley's Berkeley Center for New Media (BCNM) under Dr. Kimiko Ryokai's INFO C262: Tangible User Interfaces course, this project investigates how to leverage unconventional input loops to make digital interfaces function as generative platforms for personal & collective emotional expression.

[📄 Read the Full Research Paper](https://github.com/jaredmantell/IntertialInterface/blob/main/Final%20Paper_Embodied%20Movement_Exploring%20Digital%20Responsive%20Interactions_Fall%202024_0.1-1.pdf)

![Demo](img/dance.gif)

## Research Focus
This research examines:
- How digital movement representation through inertial tracking creates new movement qualities when translated into media art
- How technological interfaces alter participants' spatial experiences, particularly focusing on flow states and collective movement patterns
- How different kinesthetic tracking methods influence participants' affective responses through ludic, gesture-reactive visualization
- Methods for disrupting participants' daily repertoire of mobility through digital art
- Exploration of non-verbal engagement with media in public and private spaces

Our post-structural approach to interaction design is characterized by:
- Non-hierarchical interaction models emphasizing emergent experiences
- Emphasis on flowing, participant-driven experiences that break traditional structures
- Rejection of binary conceptualizations of "correct" interaction
- Integration of vulnerability and collective expression through movement
- Prioritization of fluid, interpretative experiences over prescriptive interactions

## Overview
A motion-responsive visualization system that runs on RGB images and transforms physical movements into artistic expression. Features two interaction modes:
- **Exploratory Mode**: Designed for general users, enabling intuitive engagement with flowing visuals
- **Advanced Mode**: Targeted at professional movement practitioners, providing detailed biomechanical feedback

![Professional Dancers Scenario](https://github.com/user-attachments/assets/036af8f7-d41c-4b75-a8ba-eb2add8f8d07)

![Casual Users Scenario](https://github.com/user-attachments/assets/e2718005-2a8b-483d-904b-c7b12f0ff2c8)

## System Architecture

### Motion Tracking
- MoveNet pose estimation with DepthAI hardware (OAK-1, OAK-D)
- Real-time movement tracking using Kinect Camera 
- Accelerometer (ADXL345) integration for precise motion data
- Multi-person tracking capabilities for collective interaction
- Edge detection and gesture recognition systems

![Edge Detection Method](https://github.com/user-attachments/assets/876a0b4c-4ecc-4bd1-8976-f40865cf9ee6)

### Visualization
- TouchDesigner for real-time visual feedback
- Point-cloud visualization with reactive harmonics
- Gesture-reactive visual elements including:
  - Seed, period, and amplitude modulation
  - Dynamic roughness and exponent mapping
  - Real-time color theory integration
  - Fluid design approaches aligning with breaking structure
- Support for both single and multi-user interactions
- Real-time average value computation for group movement visualization

## Technical Implementation

### Installation
python3 -m pip install -r requirements.txt

### Hardware Requirements
- Kinect Camera
- ADXL345 Accelerometer 
- Arduino Nano
- DepthAI compatible device (OAK-1, OAK-D)
- Optional: LED lighting for ambient feedback
- Projection system for visual output

### Basic Usage
python3 demo.py

### Command Line Arguments
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

### Implementation Example
from MovenetDepthai import MovenetDepthai
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

## Architecture: Host mode vs Edge mode
The cropping algorithm determines from the body detected in frame N, on which region of frame N+1 the inference will run. The mode (Host or Edge) describes where this algorithm runs:
- In Host mode, the cropping algorithm runs on the host CPU. Only this mode allows images or video files as input. The flow of information between the host and the device is bi-directional: in particular, the host sends frames or cropping instructions to the device.
- In Edge mode, the cropping algorithm runs on the MyriadX. So, in this mode, all the functional bricks of MoveNet (inference, determination of the cropping region for next frame, cropping) are executed on the device. The only information exchanged are the body keypoints and optionally the camera video frame.

Note: in either mode, when using the color camera, you can choose to disable the sending of the video frame to the host, by specifying "rgb_laconic" instead of "rgb" as input source.

![Architecture](img/movenet_nodes.png)

## Research Methods
Our approach leverages:
1. Multiple motion capture technologies
2. Real-time visualization systems
3. User-centered design principles
4. Speculative design methodology
5. Extensive scenario testing
6. IDEO Model Cards for scenario development
7. Tarot Cards of Tech for obstacle anticipation
8. Body storming and interactive prototyping

## Project Structure
embodied-movement/ —— src/ | —— demo.py | —— MovenetDepthai.py | —— MovenetDepthaiEdge.py | —— MovenetRenderer.py
                   |—— docs/ | —— paper.pdf
                   └—— examples/ └—— demo_scenarios/

## Artistic Inspirations
- "The Inheritance" (2015) - Movement in large spaces and aesthetics of wide-ranging movements
- "Farbklangschichten" - Kinesthetic experiences with colors and sounds
- "Colored Shadows" - Movement representation through dancing shadows
- "The Treachery of Sanctuary" (2012) - Interactive shadow transformation

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
