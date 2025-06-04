# Zen Timer: Minimalist Meditation Timer

<img width="540" alt="PLAKAT" src="https://github.com/user-attachments/assets/d2ebba28-3c74-4e18-bda2-92050986cd28" />

## Project Overview

Zen Timer is a minimalist, elegant meditation timer designed for distraction-free meditation practice. With its clean black interface and large, easily visible timer display, it's perfect for meditation sessions of any length. The timer offers customizable presets, pinch-to-zoom functionality for perfect visibility, and a thoughtfully designed UI that fades away during meditation to minimize distractions.

## How to Use

### Basic Usage

1. **Set Time**: 
   - Use the slider to set minutes
   - Tap the circle input to enter a specific time
   - Or select a preset from the settings menu

2. **Start the Timer**:
   - Tap once on the timer display to start counting down
   - The interface elements will fade away, leaving only the timer visible

3. **During Meditation**:
   - The screen stays awake using wake lock (where supported)
   - Timer continues to count down in fullscreen mode
   - Audio signals mark significant events (start, finish)

4. **Stop/Reset**:
   - Tap once to stop the timer
   - Tap again to reset to your set time

### Features and Options

#### Timer Settings
- **Direct Input**: Tap the circle beneath the timer to manually enter time
- **Slider**: Quickly set minutes using the horizontal slider
- **Presets**: Save up to 7 custom time presets in the settings menu
- **Negative Timer**: Timer continues into negative time after reaching zero, indicated by yellow color

#### Display Options
- **Pinch to Zoom**: Adjust the font size using pinch gestures (109% expanded zoom range)
- **Auto-sizing**: Timer automatically adjusts to optimal size for your device
- **Orientation Support**: Adapts to both portrait and landscape orientations
- **Persistent Size**: Timer remembers your preferred zoom level between sessions

#### Interface Controls
- **Settings Menu**: Access by tapping the yellow circle at the bottom
- **Close Settings**: Tap the yellow circle in settings, or tap anywhere on the background
- **Fullscreen Mode**: Automatically enters fullscreen when timer starts

## Interface Behavior

### Main Screen
- **Timer Display**: Large, centered digits showing time in simplified format
- **Slider**: Below the timer for quick minute adjustments
- **Input Circle**: For precise manual time entry
- **Settings Button**: Yellow circle at bottom center to access presets

### Timer Display States
- **Idle**: Regular color (light gray), showing set time
- **Running**: Only the timer is visible, other elements fade out
- **Negative**: Timer text and controls turn yellow when counting below zero
- **Countdown**: Digits update every second during meditation

### Settings Panel
- **Presets Area**: Radio buttons with customizable time circles
- **Close Button**: Yellow circle at bottom center to exit settings
- **Background Close**: Tapping anywhere outside UI elements closes settings

## Program Architecture

### Core Modules

#### State Management
- `state` object manages all application state:
  - Timer values (current, master)
  - UI state (running, orientation, scale)
  - Interaction state (pinch gestures, input modes)
  - System features (wake lock, audio context)

#### Timer Engine
- `startTimer()`: Initializes countdown, requests wake lock, enters fullscreen
- `stopTimer()`: Halts countdown, exits fullscreen, shows UI elements
- `resetTimer()`: Resets display to master value, resets negative state
- `updateMasterValue()`: Central function to update time across all UI elements

#### UI Management
- `showUIElements()`: Makes control elements visible with proper styling
- `hideUIElements()`: Hides all controls during meditation
- `applyFadeOutTransition()`: Manages smooth transitions when timer starts
- `applyFadeInTransition()`: Controls smooth transitions when timer stops

#### Display Adaptation
- `adjustFontSize()`: Dynamically calculates optimal font size based on:
  - Current orientation (portrait/landscape)
  - Available screen space
  - User-defined scale factor
- `checkOrientation()`: Detects and responds to orientation changes
- `saveCurrentScale()` & `loadStoredScale()`: Persist user's zoom preference

#### Interaction Handlers
- Tap gestures: Single-tap control for start/stop/reset
- Pinch gestures: Zoom control for timer display
- Touch handlers: Settings menu interactions
- Input handling: Time entry via virtual keyboard

#### Audio Output
- `beep()`: Generates audio feedback using Web Audio API
- Different beep patterns signal different events:
  - Two beeps: Timer start
  - Three beeps: Timer reaches zero
  - One beep: Timer reset

#### Persistence Layer
- localStorage-based storage for:
  - Custom time presets
  - User's preferred font scale
  - Selected preset between sessions

#### Settings Management
- `createPresetsUI()`: Generates the preset interface
- `updatePreset()`: Updates stored preset values
- `selectPreset()`: Handles preset selection
- `loadPresets()` & `savePresets()`: Local storage operations

### Internal Logic Flow

1. **Initialization**
   - Load saved preferences (presets, scale)
   - Set up event listeners
   - Render initial UI state

2. **Interaction Cycle**
   - User sets time through slider, direct input or presets
   - Master value updated, reflected in all UI components
   - Display adapts to size, orientation, and user preferences

3. **Meditation Cycle**
   - Timer start triggers fullscreen, wake lock, UI fade-out
   - Countdown updates display every second
   - Audio signals mark start and completion
   - User tap stops timer, returns to interactive state

4. **Settings Management**
   - Settings panel provides preset management
   - Presets stored in localStorage
   - UI responds to pinch gestures for zooming
   - Multiple ways to close settings (yellow button, background tap)

5. **Adaptive Response**
   - Responsive to orientation changes
   - Persistent preferences between sessions
   - Wake lock management based on visibility
   - Audio context initialization on first user interaction

## Technical Implementation

- **Pure Vanilla JavaScript**: No external libraries or frameworks
- **Single-file Application**: HTML, CSS, and JavaScript combined
- **Responsive Design**: Works on any device size and orientation
- **Progressive Features**: Wake lock for screen-on, Web Audio API for sounds
- **Persistent Storage**: localStorage for user preferences

## Accessibility and UX

- **High Contrast**: Clear visual design with adequate contrast
- **Touch Optimized**: Large tap targets for mobile use
- **Minimal Distractions**: UI fades away during meditation
- **Intuitive Controls**: Simple tap and gesture-based interface
- **Audio Feedback**: Sound cues for timer events

This timer combines elegant minimalism with thoughtful functionality to create a distraction-free meditation experience that adapts to your needs.
