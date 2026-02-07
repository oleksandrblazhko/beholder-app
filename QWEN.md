# Beholder Application - Development Context

## Project Overview

Beholder is a computer vision (CV) toolkit for building tangible controllers for interactive computer systems. It enables designers to build physical inputs that are instrumented with CV markers. By observing the properties of these markers, a CV system can detect physical interactions that occur. Beholder provides a software editor that maps CV marker behavior to keyboard events, connecting CV-driven tangible controllers to any software that responds to keyboard input.

The application is built as an Electron app using Cycle.js (functional reactive programming framework) with TypeScript. It integrates native components for computer vision processing and keyboard emulation.

## Architecture

### Frontend (Interface/)
- **Framework**: Cycle.js with TypeScript
- **State Management**: Custom command reducer pattern with undo/redo functionality
- **UI Components**: Custom node-based visual programming interface
- **Build Tool**: esbuild for bundling TypeScript to JavaScript

### Backend (Native/)
- **Computer Vision**: OpenCV-based marker detection (LocalMarkerDetection)
- **Keyboard Emulation**: Native modules for simulating keyboard events
- **Mobile Integration**: UDP-based communication for mobile sources

### Key Components

1. **Node System**: Visual programming interface with various node types:
   - Detection Panel (root panel for all nodes)
   - Detect Marker (captures marker values)
   - Number (integer value nodes)
   - Key Press/Tap (keyboard event triggers)
   - Logic Gates (NOT, AND, OR, comparison gates)
   - Specialized triggers (value change, angle change)

2. **Native Drivers**: Bridge between frontend and native functionality:
   - WebcamDetectionDriver: Manages camera feed and marker detection
   - ProgramDriver: Executes the node graph and handles keyboard events

3. **State Management**: Command-based reducer with undo/redo support

## Building and Running

### Prerequisites
- Node.js
- OpenCV 4.7 (with environment variables configured)

### Setup Commands
```bash
# Install JavaScript dependencies
npm install

# Build the JavaScript codebase
npm run build

# Start the application
npm start

# Development mode (auto-rebuilds on changes)
npm run dev
# Then in separate terminal:
npm start
```

### Platform-Specific Setup
**Windows:**
- Install OpenCV 4.7 from official installer
- Add OpenCV to system PATH
- Replace Native folder with Windows binaries

**Mac:**
- Install OpenCV via Homebrew: `brew install opencv`
- Replace Native folder with Mac binaries

## Development Conventions

### Code Structure
- **Interface/**: Contains all frontend code (Cycle.js components, state management)
- **Native/**: Contains native modules for computer vision and keyboard emulation
- **Interface/Components/**: Reusable UI components
- **Interface/StateManagement/**: Command reducer and undo/redo logic
- **Interface/NativeDrivers/**: Bridges to native functionality

### Framework Patterns
- **Cycle.js**: Functional reactive programming with streams (xstream)
- **Command Pattern**: Actions are dispatched to a central reducer
- **Node-based UI**: Visual programming interface with draggable, connectable nodes
- **Immutable Updates**: State changes happen through command reducer

### Testing
- No explicit test files found in the repository
- Manual testing through the visual interface

## Key Technologies

- **Electron**: Cross-platform desktop application framework
- **Cycle.js**: Functional and reactive JavaScript framework
- **xstream**: Reactive stream library
- **Ramda**: Functional programming utility library
- **TypeScript**: Typed superset of JavaScript
- **esbuild**: Fast JavaScript bundler
- **OpenCV**: Computer vision library for marker detection
- **Native Modules**: C++ bindings for system-level operations

## Project Status

The project is in early development stage (version 0.0.2) and focuses on providing a visual programming interface for connecting computer vision marker detection to keyboard events. The system allows users to create complex interaction patterns by connecting different types of nodes in a graph-based interface.

## Common Development Tasks

1. **Adding new node types**: Extend the CreateNode module and add to NodePalette
2. **Modifying detection algorithms**: Update native LocalMarkerDetection module
3. **Extending keyboard mapping**: Update key mapping utilities in NativeDrivers/Utils/
4. **Customizing UI**: Modify CSS in Assets/Styles/ and components in Components/

## Troubleshooting

- Camera feed issues: Terminate and restart the app
- Native module errors: Ensure OpenCV is properly installed and in PATH
- Marker detection problems: Check lighting conditions and marker visibility