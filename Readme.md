# Intelligent Multi-Agent System for Automated Pothole and Road Damage Detection

An AI-powered road inspection system that detects potholes and road damage from images using **YOLOv8** and provides intelligent analysis through a **LangGraph + Ollama** agent.

---

## Features

- Detect potholes and road surface damage from uploaded images
- Bounding-box visualization of detected defects
- Severity assessment and damage analysis
- AI-powered explanations and recommendations
- Web-based interface built with Flask
- Multi-agent workflow using LangGraph

---

## Prerequisites

Before running the project, ensure you have:

- Python 3.10+
- Git
- Ollama (for AI analysis)
- A trained YOLO model (`pothole_best_final.pt`)

---

## Project Setup

### 1. Create a Virtual Environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

---

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

If `requirements.txt` is missing:

```bash
pip install flask ultralytics opencv-python-headless pillow numpy langgraph langchain-ollama
```

---

## Ollama Setup

### Install Ollama

Download and install:

https://ollama.com

### Pull the Required Model

Check `agent.py` for the configured model.

Example:

```bash
ollama pull gemma4:31b-cloud
```

or

```bash
ollama pull llama3
```

### Start Ollama

```bash
ollama serve
```

Keep this terminal running.

---

## YOLO Model Setup

Place the trained model file in the project root:

```text
pothole_best_final.pt
```

Example structure:

```text
project/
│
├── app.py
├── agent.py
├── pothole_best_final.pt
├── static/
├── templates/
└── dataset/
```

---

## Run the Application

Start the Flask server:

```bash
python app.py
```

You should see output similar to:

```text
* Running on http://127.0.0.1:5000
```

---

## Access the Web Interface

Open your browser and visit:

```text
http://localhost:5000
```

---

## How to Use

1. Open the web application.
2. Upload a road image.
3. The YOLO model detects potholes and road damage.
4. Detection results are displayed with bounding boxes.
5. The AI agent generates:
   - Damage analysis
   - Severity assessment
   - Road maintenance recommendations

---

## Troubleshooting

### Ollama Connection Error

Verify Ollama is running:

```bash
ollama serve
```

### Model Not Found

Ensure:

```text
pothole_best_final.pt
```

exists in the project directory.

### Missing Dependencies

Reinstall packages:

```bash
pip install -r requirements.txt
```

or

```bash
pip install flask ultralytics opencv-python-headless pillow numpy langgraph langchain-ollama
```

---

## Railway Docker Deployment

This project includes a `Dockerfile` for Railway. Railway will provide a `PORT`
environment variable automatically, and the Flask app now binds to that port.

### Deploy Steps

1. Push the project to GitHub.
2. Create a new Railway project from the GitHub repository.
3. Railway should detect the `Dockerfile` automatically.
4. Deploy the service.

### Local Docker Test

```bash
docker build -t pothole-detection .
docker run --rm -p 5000:5000 -e PORT=5000 pothole-detection
```

Then open:

```text
http://localhost:5000
```

> Note: the `/chat` endpoint requires an Ollama server and model to be reachable
> from the deployed container. The image detection UI can still run without
> Ollama.

---

## Tech Stack

- Flask
- YOLOv8 (Ultralytics)
- OpenCV
- LangGraph
- LangChain
- Ollama
- Python

---

## Quick Start

```bash
# Create environment
python -m venv venv

# Activate environment
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start Ollama
ollama serve

# Run application
python app.py
```

Then open:

```text
http://localhost:5000
```

and start uploading road images for pothole detection.
