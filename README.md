# Embodied Movement: Digital Responsive Interactions

Research exploring the democratization of artistic expression through motion-responsive technology. Developed at UC Berkeley's Berkeley Center for New Media (BCNM) under Dr. Kimiko Ryokai's INFO C262: Tangible User Interfaces course, this project investigates how to leverage unconventional input loops to make digital interfaces function as generative platforms for personal & collective emotional expression.

[📄 Read the Full Research Paper](https://github.com/jaredmantell/IntertialInterface/blob/main/Final%20Paper_Embodied%20Movement_Exploring%20Digital%20Responsive%20Interactions_Fall%202024_0.1-1.pdf)

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

## System Architecture

### Motion Tracking
- MoveNet pose estimation with DepthAI hardware (OAK-1, OAK-D)
- Real-time movement tracking using Kinect Camera 
- Accelerometer (ADXL345) integration for precise motion data
- Multi-person tracking capabilities for collective interaction
- Edge detection and gesture recognition systems

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

## Environment Considerations
The system has been tested in various contexts:
- Indoor studio spaces
- Public areas (coffee shops, student unions)
- Performance venues
- Campus outdoor spaces
- Gallery installations

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

## Artistic Inspirations
- "The Inheritance" (2015) - Movement in large spaces
- "Farbklangschichten" - Kinesthetic color experiences
- "Colored Shadows" - Movement representation
- "The Treachery of Sanctuary" (2012) - Motion tracking artistry

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
