# 🎙️ CSPML Voice-Activated Audio Processing System

A voice-activated audio processing system developed using **Python and Google Colab**. The system recognizes specific voice commands to control audio processing, performs noise reduction, and applies audio effects such as **Echo** and **Drum Beat** using impulse responses and convolution.

---

## 📌 Overview

This project demonstrates the practical implementation of **Digital Signal Processing (DSP)** and audio processing techniques in an interactive Google Colab environment.

The system captures audio through the microphone, recognizes the commands **"CSPML listen"** and **"CSPML stop"**, performs noise reduction, and allows the user to apply different audio effects.

The main processing stages are:

**Voice Command → Audio Recording → Noise Reduction → Effect Selection → Convolution → Audio Output**

---

## ✨ Features

- 🎤 Microphone audio recording
- 🗣️ Voice command recognition
- ▶️ **"CSPML listen"** command to activate the system
- ⏹️ **"CSPML stop"** command to stop processing
- 🔇 Frequency-domain noise reduction
- 🔁 Echo audio effect
- 🥁 Drum Beat audio effect
- 🎛️ Interactive effect selection using a dropdown GUI
- ⚡ Impulse-response based audio effects
- 🔄 FFT-based convolution
- 🔊 Processed audio playback

---

## 🎤 Microphone Input

The system captures audio directly from the user's microphone through the browser in Google Colab.

### Audio Configuration

| Parameter | Value |
|-----------|-------|
| Sampling Rate | 16 kHz |
| Channels | Mono |
| Test Recording Duration | 5 seconds |

The browser's microphone interface is used to record the audio, which is then processed in Python.

---

## 🗣️ Voice Command Recognition

The system uses speech recognition to detect specific commands.

### Supported Commands

```text
CSPML listen
CSPML stop
```

The recognized speech is normalized and checked against possible variations of the word **CSPML**.

The system also uses similarity matching to improve detection of words such as:

```text
listen
stop
CSPML
CSP ML
C S P M L
```

Speech recognition is performed using the Google speech recognition service with the language setting:

```text
en-IN
```

### System States

```text
"CSPML listen"
       ↓
    ACTIVE
       ↓
Audio Processing

"CSPML stop"
       ↓
     IDLE
       ↓
Processing Stopped
```

---

## 🔇 Noise Cancellation

The project includes a basic noise-reduction technique.

During noise estimation, the user is asked to remain silent for the first **1 second** of the recording. This portion is treated as the noise sample.

The noise is transformed into the frequency domain using the **Fast Fourier Transform (FFT)**.

### Processing Flow

```text
Microphone Audio
       ↓
Noise Sample
       ↓
FFT
       ↓
Noise Spectrum
       ↓
Noise Estimation
       ↓
Noise Reduction
       ↓
Inverse FFT
       ↓
Cleaned Audio
```

The project estimates the noise magnitude and suppresses low-level unwanted components while retaining the main audio signal.

---

## 🔊 Audio Effects

The project implements audio effects using **impulse responses and convolution**.

Two effects are provided:

1. 🔁 Echo
2. 🥁 Drum Beat

The basic principle is:

```text
Input Signal x[n]
       +
Impulse Response h[n]
       ↓
Convolution
       ↓
Output Signal y[n]
```

Mathematically:

```text
y[n] = x[n] * h[n]
```

where:

- `x[n]` = input audio signal
- `h[n]` = impulse response
- `y[n]` = processed audio signal

---

## 🔁 Echo Effect

The Echo effect is created using an impulse response containing an original impulse and a delayed impulse.

### Parameters

```text
Echo Delay = 0.3 seconds
Echo Gain  = 0.5
```

The impulse response can be represented conceptually as:

```text
h[n] = δ[n] + 0.5δ[n - delay]
```

The delay is converted from seconds into samples using the sampling rate.

The echo effect is then applied using FFT-based convolution:

```python
signal.fftconvolve()
```

### Processing

```text
Cleaned Audio
      ↓
Echo Impulse Response
      ↓
FFT Convolution
      ↓
Echo Audio
```

---

## 🥁 Drum Beat Effect

A simple drum-beat pattern is generated using an impulse response.

### Parameters

```text
Drum Duration = 1.0 second
Beat Interval = 0.25 second
```

Multiple impulses are placed at regular intervals to create the rhythmic pattern.

Different amplitudes are used for successive impulses to create variation in the drum pattern.

Example:

```text
Impulse 1 → 1.0
Impulse 2 → 0.7
Impulse 3 → 0.5
Impulse 4 → 0.7
```

The drum impulse response is then convolved with the cleaned audio.

```text
Cleaned Audio
      ↓
Drum Impulse Response
      ↓
FFT Convolution
      ↓
Drum Beat Effect
```

---

## 🎛️ Interactive Effect Selection

The project includes an interactive dropdown interface using `ipywidgets`.

Available options are:

```text
No Effect
Echo
Drum Beat
```

The user can select an effect from the dropdown, and the selected effect is applied to the processed audio.

---

## 🧠 Complete System Workflow

```text
                 🎤 MICROPHONE
                       │
                       ▼
                AUDIO RECORDING
                       │
                       ▼
              VOICE COMMAND CHECK
                       │
             ┌─────────┴─────────┐
             │                   │
       CSPML listen         CSPML stop
             │                   │
             ▼                   ▼
          ACTIVE                IDLE
             │
             ▼
       NOISE REDUCTION
             │
             ▼
      EFFECT SELECTION
             │
        ┌────┴─────┐
        │          │
      Echo      Drum Beat
        │          │
        └────┬─────┘
             │
             ▼
         CONVOLUTION
             │
             ▼
      PROCESSED AUDIO
             │
             ▼
        🔊 AUDIO OUTPUT
```

---

## 🧮 DSP Concepts Demonstrated

This project demonstrates several fundamental concepts related to digital signal processing and audio processing:

- Sampling
- Microphone audio acquisition
- Speech recognition
- Fast Fourier Transform (FFT)
- Inverse FFT
- Frequency-domain processing
- Noise estimation
- Noise reduction
- Impulse response
- Linear convolution
- FFT-based convolution
- Audio normalization
- Digital audio playback

---

## 🛠️ Technologies Used

### Programming Language

- Python

### Python Libraries

- NumPy
- SciPy
- SpeechRecognition
- IPywidgets
- IPython Display

### Platform

- Google Colab

### Additional Tool

- FFmpeg

FFmpeg is used to convert browser-recorded **WebM audio** into **WAV format** for further processing.

---

## 📊 Project Results

The notebook includes testing and demonstration of different stages of the system.

### 🎤 Microphone Recording

The microphone input is recorded through the browser and played back to verify successful audio capture.

### 🗣️ Voice Command Recognition

The system tests recognition of:

```text
CSPML listen
CSPML stop
```

### 🔇 Noise Cancellation

The original audio and noise-cancelled audio can be compared using the audio players provided in the notebook.

### 🔁 Echo Effect

The cleaned audio is processed using the Echo impulse response and convolution.

### 🥁 Drum Beat Effect

The cleaned audio is processed using the generated Drum Beat impulse response.

### 🎛️ Effect Selection

The interactive dropdown allows the user to select between:

```text
No Effect
Echo
Drum Beat
```

---

## 🖼️ Results Gallery

Add screenshots of the project outputs to the `images` folder and display them here.

### 🎤 Voice Command Detection

![Voice Command Detection](images/voice-command.png)

### 🔇 Noise Cancellation

![Noise Cancellation](images/noise-cancellation.png)

### 🔁 Echo Effect

![Echo Effect](images/echo-effect.png)

### 🥁 Drum Beat Effect

![Drum Beat Effect](images/drum-beat-effect.png)

### 🎛️ Effect Selection GUI

![Effect Selection GUI](images/effect-selection.png)

---

## 🎥 Project Demo

Add a GIF demonstrating the working system to the `images` folder.

![CSPML Audio Processing System Demo](images/system-demo.gif)

---

## ▶️ How to Run

### Step 1: Open the Notebook

Open the `.ipynb` file using **Google Colab**.

### Step 2: Run the Cells

Execute the notebook cells in sequence.

### Step 3: Allow Microphone Access

When the browser asks for microphone permission, select:

```text
Allow
```

### Step 4: Test the Microphone

Record a short sample and verify that the recorded audio can be played back.

### Step 5: Test Voice Commands

Speak one of the supported commands:

```text
CSPML listen
```

or

```text
CSPML stop
```

### Step 6: Estimate Noise

During the noise-estimation stage:

```text
First 1 second → Remain silent
Remaining time → Speak normally
```

The first second is used to estimate the background noise.

### Step 7: Select an Audio Effect

Use the interactive dropdown:

```text
No Effect
Echo
Drum Beat
```

### Step 8: Listen to the Processed Audio

The processed audio is generated and provided through the audio player in the notebook.

---

## 📁 Project Structure

```text
CSPML-Voice-Activated-Audio-Processing-System/
│
├── CSPML_Voice_Activated_Audio_Processing_System_in_Google_Colab.ipynb
│
├── README.md
│
└── images/
    ├── voice-command.png
    ├── noise-cancellation.png
    ├── echo-effect.png
    ├── drum-beat-effect.png
    ├── effect-selection.png
    └── system-demo.gif
```

---

## 🎯 Project Objective

The objective of this project is to demonstrate how **voice commands and digital signal-processing techniques** can be combined to create an interactive audio-processing system.

The project focuses on the practical implementation of:

```text
Voice Command Control
        +
Noise Reduction
        +
Impulse Responses
        +
Convolution
        +
Audio Processing
```

---

## 📚 Learning Outcomes

Through this project, the following concepts are practically demonstrated:

- Understanding microphone-based audio acquisition
- Working with sampled audio signals
- Applying FFT to audio signals
- Estimating and reducing background noise
- Understanding impulse responses
- Implementing audio effects through convolution
- Using FFT-based convolution
- Integrating speech recognition with signal processing
- Creating a simple interactive audio-processing interface in Google Colab

---

## 💡 Key Takeaway

This project demonstrates a practical combination of **Speech Recognition, Digital Signal Processing, and Audio Effects** in a single Python-based system.

It provides a simple platform for understanding how an input audio signal can be captured, analyzed, processed, modified, and played back using fundamental signal-processing techniques.

---

## 👨‍💻 Author

**AmarDeep Dwivedi**

M.Tech Research  
Electrical Engineering — CSPML  
IIT Dharwad

---

## ⭐ Project Highlights

```text
🎤 Voice-Activated
🔇 Noise Reduction
🔁 Echo Processing
🥁 Drum Beat Effect
⚡ FFT
🔄 Convolution
🎛️ Interactive GUI
☁️ Google Colab
🐍 Python
```
