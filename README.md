# Invisible Threads: Pulse-Activated WebAR Installation

Interactive art meets biometric detection. An immersive web-based augmented reality experience that reveals landscape paintings in response to your heartbeat. Part of the SAIS v1.0 research project from AATC Expedition Olympus.

**Status:** Complete | **License:** CC BY-NC 4.0 | **File Size:** 23.3 MB

---

## Quick Start

No installation required. Just open in a modern web browser:

1. Download invisible_threads_complete.html
2. Double-click to open
3. Click "Simulate Pulse" (already active)
4. Watch the paintings respond to your heartbeat
5. Click Day 1-7 buttons to switch paintings

Deploy to Netlify, GitHub Pages, or any static host for a live demo.

---

## About

### The Mission

Invisible Threads captures the human dimension of deep space analog missions. During AATC Expedition Olympus (May 2-10, 2026), an 11-member crew experienced documented peaks in cognitive workload and stress around the mission's 75% mark, known as the "Three-Quarter Phenomenon."

This artwork translates that data into an interactive experience:
- 8 oil paintings, one per mission day
- Real-time pulse detection using rPPG technology
- Dynamic visual activation as heart rate changes
- Interactive WebAR at Venice's Palazzo Pisani Revedin

### The Science

The installations use remote photoplethysmography (rPPG), a contactless technique that extracts heart rate from your smartphone camera. Your pulse becomes the brushstroke—as stress rises, the hidden landscapes beneath the overlays emerge.

**Mission Days:**

| Day | Theme | State | Animation |
|-----|-------|-------|-----------|
| 1-2 | Arrival & Settlement | High energy | Lightning + clouds |
| 3-5 | Routine Operations | Steady state | Golden spirals |
| 6 | The Peak | Maximum stress | Intense chaos |
| 7-8 | Release & Return | Calm resolution | Mirror reflections |

---

## Features

### Interactive Elements

- Pulse Simulation Mode: Immediate demo without camera
- Camera Detection Mode: Real-time heart rate extraction
- 8 High-Resolution Paintings: Embedded landscapes, always ready
- Live Metrics Display: BPM, signal quality, psychological state
- Snapshot Download: Capture the moment your heart revealed the art

### Technical Highlights

- Zero External Dependencies: All images embedded as Base64
- Responsive Design: Works on desktop, tablet, mobile
- Offline Ready: No internet needed after load
- Dual Canvas Rendering: Landscape and animation layers
- Smooth BPM-Driven Transitions: Pulse modulates opacity and animation speed
- Self-Contained: Single 23.3 MB HTML file

---

## How to Use

### Simulation Mode (Default)

1. Open invisible_threads_complete.html
2. Watch your simulated heart rate fluctuate (60-120 BPM)
3. Click Day 1-7 buttons to explore each mission phase
4. Notice the landscape reveals as pulse rises

What you will see:
- Calm (less than 65 BPM): Landscape at 60% opacity, soft color gradient
- Moderate (65-85 BPM): Landscape brightens to 75%, overlays activate
- Turbulent (greater than 85 BPM): Landscape nearly fully visible, intense animations

### Camera Mode (Real Pulse Detection)

1. Click "Camera Detection"
2. Allow camera access when prompted
3. Position your face in the center (good lighting helps)
4. Wait 10-15 seconds for rPPG calibration
5. Your real heart rate controls the visualization

Tips:
- Bright lighting improves accuracy
- Keep face steady 15-20 cm from camera
- Works best with calm, measured breathing
- Signal quality indicator shows detection confidence

### Controls

| Button | Function |
|--------|----------|
| Simulate Pulse | Use synthetic BPM variation |
| Camera Detection | Enable real rPPG heart rate |
| Pause Animation | Freeze the visual effects |
| Reset | Return to baseline state |
| Download | Save PNG snapshot |
| Day 1-7 | Switch between mission phases |

---

## Technical Stack

### Core Technologies

- Canvas Rendering: HTML5 2D context for real-time animation
- Remote Photoplethysmography (rPPG): JavaScript implementation of red-channel pulse detection
- Image Processing: Face ROI extraction, signal filtering
- Dual-Layer Architecture: Separate canvases for background and animation
- Base64 Encoding: All 7 paintings embedded (no external requests)

### JavaScript

- Vanilla JS only (no dependencies)

### Browser Support

| Browser | Support |
|---------|---------|
| Chrome/Edge | Full support |
| Firefox | Full support |
| Safari | Full support (camera requires HTTPS) |
| Mobile Safari | Limited (camera access on iOS 14.5+) |

---

## Data and Metrics

### Displayed in Real-Time

- Heart Rate (BPM): Detected or simulated
- Signal Quality: Confidence in rPPG reading (%)
- Psychological State: Calm / Moderate / Turbulent
- Landscape Activation: Current opacity (0-100%)

### No Data Collection

- Video is processed locally in your browser
- No frames stored or transmitted
- No biometric data saved
- Camera access can be revoked anytime

---

## Landscape Opacity Model

Each painting has a base visibility that increases with pulse:

Landscape Opacity = Base Opacity + (Normalized BPM x 0.35)

Base Opacity by Day:
- Days 1-2, 4-5: 60% (atmospheric, clear presence)
- Day 3: 65% (spiral harmony, visible)
- Day 6 (Peak): 55% (emphasize chaos, not the calm landscape)
- Days 7-8: 70% (peaceful, already prominent)

Maximum Opacity: 100% at turbulent heart rate (90+ BPM)

---

## Deployment

### Local Testing

No build step needed. Simply open the HTML file in a browser.

### Netlify (Recommended)

1. Create new site from this repo
2. Deploy main branch
3. Netlify automatically serves the HTML
4. Share URL with visitors

### GitHub Pages

Push to gh-pages branch and enable Pages in Settings. URL: https://username.github.io/invisible-threads

### Vercel

Run "vercel deploy" - auto-deploys on push with single-file HTML support.

### Self-Hosted

Copy the HTML file to any web server, or test locally with Python:

  python3 -m http.server 8000

Then visit http://localhost:8000

### Exhibition Setup (Palazzo Pisani, Venice)

- Deploy to private server or CDN
- Display on public screen or iPad stations
- Visitors scan QR code and open in their phone camera
- Real-time rPPG detection powers the interaction

---

## File Structure

```
invisible_threads_complete.html        # Single self-contained file
├── HTML Markup                         # Canvas, buttons, overlay info
├── Embedded Styles (23 KB)            # CSS for responsive layout
├── Embedded Images (23.3 MB total)    # 7 paintings as Base64
│   ├── Day 1: Stormy arrival
│   ├── Day 2: Settlement
│   ├── Day 3: Routine spirals
│   ├── Day 4: Midpoint momentum
│   ├── Day 5: Rising stress
│   ├── Day 6: Peak turbulence
│   └── Day 7: Release calm
└── JavaScript Logic (~6 KB)           # Animation, rPPG, rendering
    ├── Initialization and canvases
    ├── Pulse simulation
    ├── rPPG detection (camera mode)
    ├── Painting state updates
    ├── Animation rendering (lightning, spirals, mirrors)
    └── Download and control handlers
```

---

## rPPG Algorithm Details

### How It Works

1. Video Capture: 160x120 px face video from camera
2. ROI Extraction: 80x60 px central face region
3. Red Channel Analysis: Extract intensity per frame
4. Peak Detection: Count local maxima in rolling 20-frame buffer
5. BPM Calculation: (peaks / 20) x 60 x 12.5 FPS
6. Validation: Reject readings outside 40-180 BPM range

### Accuracy

- Not clinical-grade: rudimentary heuristic, not validated
- Visually effective: sufficient for art interaction
- Works in diverse lighting: robust red-channel method
- Sensitive to motion: keep face still for best results

For clinical use, integrate with certified pulse oximeter or FDA-approved rPPG SDK.

---

## Customization

### Change Landscape Visibility

Edit the baseOpacity values in the PAINTINGS array:

```javascript
{
  day: 1,
  title: "The Arrival",
  baseOpacity: 0.6,  // Change this (0.0 to 1.0)
  // ...
}
```

- 0.3 = Subtle, mostly hidden
- 0.6 = Balanced (current default)
- 0.9 = Dominant, almost fully visible

### Change Animation Types

Swap animation types in the animationType field:

```javascript
animationType: "lightning-clouds"  // Options:
                                   // "spiral-golden"
                                   // "mirror-calm"
```

### Add 8th Painting (Day 8: Return)

1. Encode your 8th painting as Base64
2. Add to PAINTING_IMAGES
3. Already have 8 paintings in PAINTINGS array - no code change needed

### Modify Color Palettes

Each painting has a palette array (3 gradient colors):

```javascript
palette: ["#1a0033", "#3d1a5c", "#661099"]  // Purple tones
// Change to your colors in hex format
```

---

## Research Background

### SAIS v1.0 System

Invisible Threads is a companion to SAIS v1.0, a 5-layer hybrid autonomous decision architecture for deep space exploration, developed during Expedition Olympus.

SAIS Layers:
1. Fuzzy Logic Safety Guardian: Deterministic constraints (0.15W)
2. ML Ensemble: Anomaly detection (1.80W)
3. Bayesian Diagnostic: Probabilistic fault reasoning (0.20W)
4. Orchestrator: Decision synthesis (0.15W)
5. LLM Fallback: Llama 3.2:1b offline SOP access (variable)

Total Power: 2.3W (Layers 1-4), peak 15W with Layer 5

For the full technical paper: https://github.com/kristina-mitrovic/sais-v1

### Three-Quarter Phenomenon

NASA-TLX crew workload data from the 8-day mission showed a significant peak on Day 6 (75% mission mark):

| Day | Workload Score | Observation |
|-----|----------------|-------------|
| 1-2 | 43-47 | High motivation, adjustment |
| 3-5 | 47-53 | Routine, steady |
| 6 | 57 | Peak stress, interpersonal friction |
| 7-8 | 44-50 | Relief, re-entry boost |

This pattern informed the intensity scaling of animations across mission days.

---

## What Happens on Day 6

Day 6 (The Peak) is visually distinct:

- Base landscape opacity: 55% (lower than other days)
- Animation type: Lightning and chaos
- Color palette: Deep reds and burgundies
- Psychological trigger: Requires highest stress to fully reveal the landscape

Why? At peak mission stress, the chaotic overlays dominate. Only by achieving turbulent heart rate (90+ BPM) does the landscape fully emerge—a metaphor for clarity emerging from crisis.

---

## License

Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)

You are free to:
- Share: Copy and redistribute in any medium
- Adapt: Remix, transform, and build upon
- Display: Exhibit in galleries, museums, web

With conditions:
- Attribution: Credit the author (Kristina Mitrovic)
- Non-Commercial: Not for commercial use without permission

For commercial licensing or exhibition inquiries, contact the author.

---

## Credits

Author: Kristina Mitrovic
Role: Commander EXP106CDR, AATC Expedition Olympus
Affiliation: University of Nis, Mälardalen University, University of Milan
Institution: Analog Astronaut Training Center (AATC), Austria

Technologies and Inspiration:
- Remote Photoplethysmography research (Poh et al., 2010)
- NASA-TLX workload assessment framework
- Canvas 2D API for real-time rendering
- Base64 encoding for zero-dependency deployment

---

## Known Limitations

### rPPG Accuracy

- Rudimentary algorithm: peak counting over red channel
- Not clinically validated: use certified sensors for medical decisions
- Motion-sensitive: works best with still face
- Lighting-dependent: bright, even lighting improves accuracy

### Browser Support

- Camera access requires HTTPS (except localhost)
- Safari on iOS requires iOS 14.5+ (privacy-protected rPPG)
- File size is 23.3 MB (all images embedded for offline support)

### Simulation Mode

The synthetic BPM variation is intentionally simple (sine wave with noise). Real rPPG will show more complex patterns.

---

## Future Roadmap

- Real-time BPM logging to JSON (post-mission analysis)
- Multi-visitor queue system for exhibition
- Sound design (heartbeat audio synthesis)
- Integration with certified medical-grade pulse oximeter
- Customizable painting mapping per installation
- WebGL optimization for mobile
- PWA mode for offline installation on tablets
- QR code linking for exhibition kiosks

---

## How to Cite

```
@software{mitrovic2026invisible,
  author = {Mitrovic, Kristina},
  title = {Invisible Threads: Pulse-Activated WebAR Installation},
  year = {2026},
  publisher = {AATC Expedition Olympus},
  url = {https://github.com/kristina-mitrovic/invisible-threads}
}
```

---

## Support and Questions

- Issues: Open a GitHub issue for bugs or feature requests
- Exhibitions: Contact for Venice installation or tour
- Research: Questions about SAIS v1.0 or rPPG implementation
- Collaboration: Interested in adaptations or partnerships

---

## Demo

Quick walkthrough (60 seconds):
1. Open app and see calm state (60% landscape visible)
2. Simulate pulse rising and watch landscape brighten
3. Hit peak stress and landscape fully reveals
4. Switch to Day 6 to see the chaos and intensity
5. Download snapshot to save the moment

---

## Thank You

Special thanks to:
- The 11 analog astronauts of AATC Expedition Olympus
- The Analog Astronaut Training Center, Austria
- Palazzo Pisani Revedin, Venice (exhibition venue)
- Remote photoplethysmography pioneers

"The journey to Mars will be defined by the speed of light, but it will be sustained by the intelligence we carry with us."

---

Made with care during 8 days in analog isolation.
May 2-10, 2026 | Rzepiennik Suchy, Poland
