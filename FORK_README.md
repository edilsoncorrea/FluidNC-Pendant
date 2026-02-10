# FluidNC-Pendant - Enhanced 3-Axis Version

Fork of [AC8L/FluidNC-Pendant](https://github.com/AC8L/FluidNC-Pendant) with improved 3-axis joystick control.

## ✨ Key Enhancements

### 🎮 **Simultaneous 3-Axis Control**
This fork adds **independent Z-axis control** to the analog joystick, enabling true 3D jogging without mode switching.

**Original behavior:**
- Joystick controlled X/Y axes
- Red button toggled between XY-plane and Z-axis modes
- Required switching to move Z axis

**Enhanced behavior:**
- Joystick simultaneously controls all 3 axes (X, Y, Z)
- No mode switching required
- Intuitive diagonal movements in 3D space
- Red button simplified to XYZ mode selector

## 📋 Changes from Original

### Hardware
- **Z-axis input:** GPIO 39 (analog joystick potentiometer)
- Compatible with original TTGO T-Display PCB

### Software Modifications
- Added `readJSZ()` function with hysteresis
- Independent 3-axis jog command: `$J=G21G91X%fY%fZ%fF%d`
- Calibration for all three axes during startup
- Simplified button logic (removed XY/Z toggle)
- Updated visual feedback (all axes always active)

### Files Modified
- `src/Pendant.h` - Added PIN_JSZ, calibrateZ, display commands
- `src/Joystick.h` - Implemented readJSZ(), simultaneous 3-axis logic
- `src/Setup.h` - Z-axis calibration
- `src/TFT_Draw.h` - Updated visual indicators
- `src/ButtonHandlers.h` - Simplified red button behavior

## 🚀 Getting Started

Follow the original [installation instructions](README.md), ensuring GPIO 39 is connected to your Z-axis joystick potentiometer.

### Compilation
```powershell
pio run
```

### Upload
```powershell
pio run --target upload
```

## 🎯 Usage

### Joystick Operation
- **X-axis:** Left/Right movement
- **Y-axis:** Forward/Backward movement  
- **Z-axis:** Up/Down movement (NEW!)
- All three axes work simultaneously

### Buttons
- **Green:** Menu / Rotary encoder function selector
- **Red:** XYZ mode / Unlock on ALARM / Hold/Resume during run
- **Yellow:** Abort / Reset (long press)
- **Rotary Encoder:** Jog speed, spindle control, axis selection

## 📊 Improvements Summary

| Feature | Original | Enhanced |
|---------|----------|----------|
| Joystick axes | 2 (XY or Z) | 3 (XYZ simultaneous) |
| Mode switching | Required | Not needed |
| Diagonal 3D jogs | ❌ | ✅ |
| Red button | XY/Z toggle | XYZ selector |
| User experience | Multi-step | Direct |

## 🙏 Credits

Based on the excellent work by:
- [AC8L/FluidNC-Pendant](https://github.com/AC8L/FluidNC-Pendant) - WiFi version
- [gjkrediet/Fluid-controller](https://github.com/gjkrediet/Fluid-controller) - Original Bluetooth design

## 📄 License

Inherits license from original project.

## 🔧 Contributing

Improvements and bug reports welcome! Please open an issue or pull request.

---

**Note:** This is an enhanced fork. For the official version with Bluetooth support and original functionality, see [AC8L/FluidNC-Pendant](https://github.com/AC8L/FluidNC-Pendant).
