# JTAG TAP Controller Visualization Tool

An interactive web-based visualization tool for the JTAG TAP (Test Access Port) Controller State Machine with modern UI, responsive design, real-time signal controls, waveform display, register tracking, and sample vector playback.

![JTAG TAP Controller Tool](https://img.shields.io/badge/Status-Complete-green) ![License](https://img.shields.io/badge/License-Educational-blue) ![Browser](https://img.shields.io/badge/Browser-Compatible-orange)

## 🎬 Live Demo

**Try it now**: Simply download and open `index.html` in your browser - no installation required!

### What You'll See

- **Interactive State Diagram**: Official JTAG TAP Controller state diagram with real-time highlighting
- **Live Signal Controls**: Click buttons or use keyboard shortcuts to control TMS, TCK, TDI
- **Real-time Waveforms**: Watch digital signals change with mouse hover information
- **Register Updates**: See IR, DR, and TDO capture registers update in real-time
- **Sample Vectors**: Try built-in examples or create your own test sequences

### First Steps

1. **Open** `index.html` in any modern browser
2. **Click** the TCK button (or press 'C') to see state transitions
3. **Try** the "Reset Sequence" sample vector to see automated operation
4. **Hover** over waveforms to see signal timing information
5. **Experiment** with custom vectors in the text area

## 🌟 Features

### 🎯 Core JTAG Functionality

- **Complete IEEE 1149.1 Implementation**: Full 16-state JTAG TAP Controller state machine
- **Official State Diagram**: Uses the authentic JTAG state diagram SVG from Wikimedia Commons
- **Real-time State Transitions**: Live highlighting of current state with proper timing
- **Signal Control**: Interactive TMS, TCK, TDI controls with immediate visual feedback
- **Register Operations**: Complete shift register implementation with proper data flow

### 📊 Advanced Visualization

- **Interactive Waveform Display**: Real-time digital signal timing with mouse controls
- **Signal History**: Scrollable waveform showing last 100+ signal transitions
- **Time Markers**: Accurate time scale with interactive cursor and hover information
- **Color-coded Signals**: TMS (red), TCK (green), TDI (blue), TDO (orange)
- **Crosshair Cursor**: Mouse hover shows exact signal values and timing information

### 🎮 Enhanced User Interaction

- **Multiple Input Methods**:
  - Mouse: Click signal controls to toggle values
  - Keyboard Shortcuts: `T` (TMS), `C` (TCK), `D` (TDI), `X` (Clear)
  - Arrow Keys: Left/Right to adjust playback speed
- **Speed Control**: Draggable slider with 0.25x to 4x speed options
- **Interactive Waveforms**: Hover for signal values, click for precise timing
- **Auto-logging**: Automatic capture of TMS,TDI values on TCK rising edge

### 🔧 Register Tracking & Data Capture

- **5-bit Instruction Register (IR)**: Enhanced from 4-bit with proper masking (0x1F)
- **8-bit Data Register (DR)**: Complete shift register implementation
- **32-bit TDO Capture Register**: Automatic capture of shifted TDO data
- **Dual Display Formats**: Both hexadecimal and binary representations
- **Real-time Updates**: Registers update during shift operations with visual feedback

### 🎬 Sample Vectors & Automation

- **Built-in Sample Vectors**:
  - **Reset Sequence**: Proper TAP controller reset demonstration
  - **DR Shift (0xA5)**: Data register shift operation example
  - **IR Load (0x1F)**: 5-bit instruction register loading
- **Custom Vector Support**: Load your own JTAG test sequences
- **Animated Playback**: Step-by-step execution with configurable speed
- **Vector Format**: Simple TMS,TDI comma-separated format with comments

### 📱 Modern Design & Accessibility

- **Responsive Layout**: Optimized for desktop, tablet, and mobile devices
- **Single Viewport Design**: No scrolling required, fits all content
- **Modern UI**: Clean interface with subtle shadows and hover effects
- **Professional Styling**: CSS Grid layout with proper spacing and typography
- **AI Attribution**: Modern gradient logo with hover animations

## 🚀 Quick Start

### 1. No Installation Required

Simply open the HTML file in any modern web browser:

```bash
# Open directly in browser
open index.html

# Or serve locally if needed
python3 -m http.server 8000
# Then navigate to http://localhost:8000
```

### 2. Basic Usage

1. **Signal Control**:
   - Click TMS, TCK, TDI buttons or use keyboard shortcuts (T, C, D)
   - Watch state diagram highlight current state in real-time

2. **Observe State Transitions**:
   - Toggle TCK (clock) to advance through states
   - TMS value determines state transition path

3. **Monitor Registers**:
   - View IR (5-bit) and DR (8-bit) values in hex and binary
   - Watch TDO Capture Register accumulate shifted data

4. **Interactive Waveforms**:
   - Hover mouse over waveforms to see signal values
   - Use speed slider or arrow keys to control playback rate
   - Clear history with 'X' key or Clear button

### 3. Try Sample Vectors

- **Reset Sequence**: Click to see proper TAP controller reset
- **DR Shift (0xA5)**: Demonstrates shifting 0xA5 into data register
- **IR Load (0x1F)**: Shows loading 0x1F into 5-bit instruction register
- **Custom Vectors**: Create your own test sequences

## 📁 File Structure

```text
├── index.html           # Complete application (HTML + CSS + JavaScript)
├── jtag-diagram.svg     # Official JTAG state diagram from Wikimedia
├── README.md           # This comprehensive documentation
├── spec.md             # Original specification document
└── test.html           # Register testing utilities
```

## 🔄 JTAG State Machine Implementation

Complete IEEE 1149.1 JTAG TAP Controller with all 16 states:

### Test Logic States

- **Test-Logic-Reset**: Default reset state (TMS=1 for 5+ cycles)
- **Run-Test/Idle**: Idle state for test operations

### Data Register (DR) Path

- **Select-DR-Scan**: Enter DR path (TMS=1 from Run-Test/Idle)
- **Capture-DR**: Load parallel data into shift register
- **Shift-DR**: Serial shift operation (TDI → DR → TDO)
- **Exit1-DR**: Prepare to exit or pause shifting
- **Pause-DR**: Temporarily halt shifting operation
- **Exit2-DR**: Resume from pause state
- **Update-DR**: Transfer shifted data to output latches

### Instruction Register (IR) Path

- **Select-IR-Scan**: Enter IR path (TMS=1 from Select-DR-Scan)
- **Capture-IR**: Load instruction register for shifting
- **Shift-IR**: Serial shift operation (TDI → IR → TDO)
- **Exit1-IR**: Prepare to exit or pause shifting
- **Pause-IR**: Temporarily halt shifting operation
- **Exit2-IR**: Resume from pause state
- **Update-IR**: Transfer shifted instruction to decoder

## 📝 Custom Vector Format

Create your own JTAG test sequences:

```text
# Comments start with #
# Format: TMS,TDI (one value per line)
# Example: Reset sequence
1,0    # TMS=1, TDI=0 (moving toward reset)
1,0    # Continue reset
1,0    # Continue reset
1,0    # Continue reset
1,0    # Ensure in Test-Logic-Reset
0,0    # TMS=0, go to Run-Test/Idle

# Example: Enter Shift-DR and shift one bit
1,0    # Select-DR-Scan
0,0    # Capture-DR
0,1    # Shift-DR with TDI=1
1,0    # Exit1-DR
1,0    # Update-DR
0,0    # Run-Test/Idle
```

## ⚙️ Technical Implementation

### Signal Timing & State Machine

- **Clock Edge Sensitivity**: State transitions on TCK rising edge (0→1)
- **TMS Sampling**: TMS value sampled on TCK rising edge determines next state
- **Shift Operations**: TDI shifts into registers during Shift-DR/Shift-IR states
- **TDO Output**: Register MSB appears on TDO during shift operations
- **Proper Direction**: TDI → LSB, shift left, MSB → TDO

### Register Architecture

- **Data Register (DR)**: 8-bit shift register with parallel load/update
- **Instruction Register (IR)**: 5-bit shift register with 0x1F mask
- **TDO Capture**: 32-bit register automatically captures shifted TDO data
- **Update Latches**: Separate output latches updated on Update-DR/Update-IR

### Waveform Engine

- **Signal History**: Maintains chronological record of all signal changes
- **Interactive Display**: Mouse hover shows exact values and timing
- **Auto-scaling**: Time axis adjusts to show relevant signal history
- **Color Coding**: Distinct colors for easy signal identification
- **Performance**: Optimized canvas rendering for smooth real-time updates

### Auto-logging System

- **TCK Edge Detection**: Monitors for rising edge transitions (0→1)
- **Automatic Capture**: Records TMS,TDI values on each TCK rising edge
- **Format Compatibility**: Generated logs can be used as custom vectors
- **Real-time Display**: Shows captured vectors in custom vector text area

## 🌐 Browser Compatibility

Tested and optimized for modern browsers:

- ✅ **Chrome/Chromium 90+**: Full feature support
- ✅ **Firefox 88+**: Complete compatibility
- ✅ **Safari 14+**: All features working
- ✅ **Edge 90+**: Full functionality
- ✅ **Mobile Browsers**: Responsive design works on iOS/Android

## 🎓 Educational Applications

Perfect for learning and teaching:

### Learning JTAG

- **Visual Learning**: See exactly how TAP controller state machine works
- **Interactive Exploration**: Experiment with different signal combinations
- **Timing Understanding**: Observe relationship between signals and state changes
- **Register Operations**: Learn how data flows through JTAG scan chains

### Teaching Aid

- **Classroom Demonstrations**: Project tool for live JTAG instruction
- **Assignment Tool**: Students can create and test their own vectors
- **Concept Reinforcement**: Visual feedback reinforces theoretical concepts
- **Standards Compliance**: Based on actual IEEE 1149.1 specification

### Development & Debugging

- **Sequence Verification**: Test JTAG sequences before hardware implementation
- **Timing Analysis**: Understand signal timing requirements
- **Protocol Understanding**: Learn proper JTAG scan chain operations
- **Vector Generation**: Create test vectors for hardware validation

## 📋 Sample Vector Examples

### Complete Reset Sequence

```text
# Comprehensive reset (works from any state)
1,0  # Ensure moving toward Test-Logic-Reset
1,0  # Continue reset
1,0  # Continue reset
1,0  # Continue reset
1,0  # Definitely in Test-Logic-Reset
0,0  # Move to Run-Test/Idle
```

### Data Register Shift (0xA5 = 10100101)

```text
# Navigate to DR path
1,0  # Select-DR-Scan
0,0  # Capture-DR

# Shift 0xA5 (LSB first: 10100101)
0,1  # Shift bit 0 (1)
0,0  # Shift bit 1 (0)
0,1  # Shift bit 2 (1)
0,0  # Shift bit 3 (0)
0,0  # Shift bit 4 (0)
0,1  # Shift bit 5 (1)
0,0  # Shift bit 6 (0)
1,1  # Shift bit 7 (1) and exit to Exit1-DR

# Complete operation
1,0  # Update-DR
0,0  # Return to Run-Test/Idle
```

### Instruction Register Load (0x1F = 11111)

```text
# Navigate to IR path
1,0  # Select-DR-Scan
1,0  # Select-IR-Scan
0,0  # Capture-IR

# Shift 0x1F (LSB first: 11111)
0,1  # Shift bit 0 (1)
0,1  # Shift bit 1 (1)
0,1  # Shift bit 2 (1)
0,1  # Shift bit 3 (1)
1,1  # Shift bit 4 (1) and exit to Exit1-IR

# Complete operation
1,0  # Update-IR
0,0  # Return to Run-Test/Idle
```

## 🔗 References & Standards

- **[IEEE 1149.1 Standard](https://standards.ieee.org/standard/1149_1-2013.html)**: Official JTAG specification
- **[JTAG Wikipedia](https://en.wikipedia.org/wiki/JTAG)**: Comprehensive JTAG overview
- **[State Diagram Source](https://commons.wikimedia.org/wiki/File:JTAG_TAP_Controller_State_Diagram.svg)**: Official Wikimedia diagram
- **[Boundary Scan Tutorial](https://www.corelis.com/education/tutorials/jtag-tutorial/)**: Additional JTAG learning resources

## 🏗️ Development Notes

### Performance Optimizations

- **Canvas Rendering**: Optimized waveform drawing for 60fps performance
- **Memory Management**: Efficient signal history storage and cleanup
- **Event Handling**: Debounced user input for smooth interaction
- **Mobile Optimization**: Touch-friendly controls and responsive layout

### Code Architecture

- **Modern JavaScript**: ES6+ features with clean, maintainable code structure
- **CSS Grid/Flexbox**: Modern layout techniques for responsive design
- **Modular Design**: Separated concerns for state machine, UI, and waveforms
- **Error Handling**: Robust input validation and graceful error recovery

## 📄 License

This educational tool is provided under the following terms:

- **Educational Use**: Free for learning, teaching, and non-commercial research
- **Open Source**: Source code available for inspection and modification
- **Attribution**: JTAG state diagram from Wikimedia Commons (unmodified)
- **Standards Compliance**: Implementation follows IEEE 1149.1 specification

---

**⚠️ Important**: This implementation is for educational and development purposes. For production JTAG applications, always consult the official IEEE 1149.1 standard and device-specific documentation.

**🤖 AI-Assisted Development**: This tool was developed with AI assistance to ensure accuracy and completeness in JTAG implementation and modern web development practices.
