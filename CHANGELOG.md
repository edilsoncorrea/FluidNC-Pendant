# Changelog

## [Enhanced 3-Axis Control] - 2026-02-09

### Added
- **Independent Z-axis joystick control** via analog input on GPIO 39
- `readJSZ()` function for smooth Z-axis reading with hysteresis
- Z-axis calibration during startup for improved accuracy
- Display command definitions (TFT_SLPIN, TFT_DISPOFF) for ST7789

### Changed
- **Simultaneous 3-axis jogging**: X, Y, and Z axes now operate independently and simultaneously
- Joystick control logic: removed toggle between XY-plane and Z-axis modes
- Red button behavior: always activates XYZ mode instead of toggling between XY and Z
- Visual feedback: all axes highlighted when available (no more mode-dependent colors)
- Jog command format: updated to support 3D movement `$J=G21G91X%fY%fZ%fF%d`

### Improved
- **Better ergonomics**: no need to switch modes - all 3 axes respond immediately
- **Smoother operation**: independent axis control allows diagonal movements in 3D space
- **User experience**: simplified interface without mode switching

### Technical Details
- Z-axis connected to GPIO 39 (analog input)
- Calibration uses 100-sample averaging for all axes (X, Y, Z)
- Hysteresis implementation prevents jitter on all three axes
- Maintains compatibility with original FluidNC-Pendant hardware

### Migration Notes
If upgrading from the original version:
- Ensure GPIO 39 is connected to your Z-axis joystick potentiometer
- The red button no longer toggles modes - it now serves as XYZ axis selector
- All three axes respond simultaneously to joystick input
