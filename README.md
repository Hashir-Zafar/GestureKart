🚗 GestureKart

**AI-Powered Gesture-Controlled Traffic Safety Simulator**

An interactive 3D web game where players navigate realistic urban traffic scenarios using **physical body gestures** tracked via webcam. Built for [Hackathon Name] to revolutionize traffic rule education in Pakistan.

🎮 Features

- **Gesture Controls**: Steer by leaning, brake by raising your hand
- **Real-Time Pose Detection**: Powered by MediaPipe Pose Landmarker
- **3D Environment**: Immersive road simulation with Three.js/React Three Fiber
- **Traffic Rule Enforcement**: Red light violations, lane discipline tracking
- **Civic Driving Score**: Downloadable performance report card (PDF/Image)
- **60 FPS Performance**: Smooth, lag-free gesture recognition

🕹️ How to Play

1. **Allow webcam access** when prompted
2. **Lean left/right** → Steer your vehicle
3. **Raise right hand above head** → Stop at red signals
4. **Adjust hand distance** → Control speed (optional)
5. Complete the course and download your **Civic Score Card**

🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Gesture Detection** | MediaPipe Pose Landmarker |
| **3D Graphics** | Three.js / React Three Fiber |
| **Frontend** | React.js, Vite |
| **Styling** | CSS3, Tailwind (optional) |
| **Deployment** | Vercel (HTTPS required for webcam) |

🚀 Quick Start

Prerequisites
- Node.js 16+ installed
- Webcam-enabled device
- Modern browser (Chrome/Edge recommended)

Installation

```bash
# Clone the repository
git clone https://github.com/[your-username]/gesturekart.git

# Navigate to project folder
cd gesturekart

# Install dependencies
npm install

# Start development server
npm run dev
