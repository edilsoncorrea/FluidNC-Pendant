# FluidNC-Pendant - Enhanced 3-Axis Control

> **⚡ Enhanced fork** with simultaneous 3-axis joystick control for improved ergonomics and workflow

Work originated from https://github.com/gjkrediet/Fluid-controller and enhanced by [AC8L](https://github.com/AC8L/FluidNC-Pendant)

<img src="https://github.com/AC8L/FluidNC-Pendant/blob/main/Photos/Front.jpeg" width=50% height=50%>

The original design by gjkrediet was intended for bluetooth, this design is for Wi-Fi version of the FluidNC. Pendant communicates with the controller through Websocket protocol on TCP port 81.

## ✨ Key Enhancements in This Fork

### 🎮 **Simultaneous 3-Axis Control**
This fork adds **independent Z-axis control** to the analog joystick, enabling true 3D jogging without mode switching.

**What's New:**
- ✅ Joystick simultaneously controls all 3 axes (X, Y, Z)
- ✅ No mode switching required - instant 3D movement
- ✅ Intuitive diagonal movements in 3D space
- ✅ Simplified button interface
- ✅ Better ergonomics and workflow efficiency

**Previous behavior:**
- Joystick controlled X/Y axes only
- Required pressing RED button to toggle between XY-plane and Z-axis modes

**Enhanced behavior:**
- All three axes respond simultaneously to joystick input
- True 3D control for natural, fluid movements
- RED button simplified to XYZ mode selector

# PCB
PCB was redesigned to hold all components to be soldered into it except the battery and power switch.
GRBL files are included for online order as well as schematics.

## Front of the PCB with soldered components
<img src="https://github.com/AC8L/FluidNC-Pendant/blob/main/Photos/PCB_Mounted.jpeg" width=50% height=50%>

## Back of the PCB
<img src="https://github.com/AC8L/FluidNC-Pendant/blob/main/Photos/PCB_Back.jpeg" width=50% height=50%>

## JST 2.0 soldered to the power switch and JST that comes with TTGO
<img src="https://github.com/AC8L/FluidNC-Pendant/blob/main/Photos/JST_and_Switch_On_Lid.jpeg" width=50% height=50%>

## Battery is fixed behind PCB with a Kapton tape
<img src="https://github.com/AC8L/FluidNC-Pendant/blob/main/Photos/LiPo_Kapton.jpeg" width=50% height=50%>

# 3D printed case
Lid was slightly modified to hold new PCB and power switch. Depending on which tactile switches were used - 3D printed buttons can be vertically scaled/reduced in the slicer.

# Firmware
Development was migrated from Arduino IDE into the PlatformIO to have stricter control over library versioning.

## Installation instructions:
1. Clone git repo: 
   ```bash
   git clone https://github.com/edilsoncorrea/FluidNC-Pendant.git
   cd FluidNC-Pendant
   ```
2. Copy/rename sample_Config.h to Config.h
   ```bash
   cp src/sample_Config.h src/Config.h
   ```
3. Enter your WiFi SSID information and FluidNC hostname/port in `src/Config.h`
4. Open project in Visual Studio Code with PlatformIO extension
5. Wait until Visual Studio Code pulls down all depending libraries
6. Overwrite content of `.pio/libdeps/esp32dev/TFT_eSPI/User_Setup.h` with the content of `src/User_Setup.h.TFT_eSPI`
7. Overwrite the content of `.pio/libdeps/esp32dev/TFT_eSPI/User_Setup_Select.h` with the content of `src/User_Setup_Select.h.TFT_eSPI`
8. Now firmware will compile and you should be able to program the TTGO T Display

### Quick Compilation
```bash
pio run                    # Compile
pio run --target upload    # Upload to device
```

## Hardware Requirements

### Enhanced 3-Axis Version
- **Z-axis connection:** GPIO 39 (analog joystick potentiometer)
- Compatible with original TTGO T-Display PCB
- All other connections remain the same

# Operations

## Button Functions

### Red Button
- **Normal press:** XYZ mode selector (all axes active)
- **When FluidNC is in ALARM mode:** Sends UNLOCK command
- **During RUN:** Hold/Resume cycle control
- **Long press:** Puts pendant into sleep mode
- **When in sleep mode:** Wakes pendant up

### Optical Rotator
- **Default mode:** Adjusts jog speed
- **When pressed:** Enters Menu mode
- **In Menu:** Scroll through options by rotating, select by clicking
- **Menu functions:** Homing, brightness adjustment, spindle control, and more

### Joystick (Enhanced 3-Axis)
- **X-axis:** Left/Right movement
- **Y-axis:** Forward/Backward movement  
- **Z-axis:** Up/Down movement (NEW!)
- **All three axes work simultaneously** for true 3D control

### Green Button
- **Press:** Opens rotary encoder function selector
- **Allows changing:** What parameter the rotator controls (X, Y, Z axis, spindle speed, jog speed, etc.)
- **Press again:** Confirms selection

### Yellow Button
- **Normal press:** Sends abort command to the CNC
- **Long press:** Reset controller

## 📊 Comparison Table

| Feature | Original Version | Enhanced Version |
|---------|-----------------|------------------|
| Joystick control | XY or Z (toggle) | XYZ simultaneous |
| Mode switching | Required | Not needed |
| 3D diagonal jogs | ❌ | ✅ |
| RED button | XY/Z toggle | XYZ selector |
| Workflow | Multi-step | Direct & intuitive |

## Network Configuration

The pendant connects to FluidNC via WiFi and WebSocket:

- **WiFi settings:** Configure in `src/Config.h`
- **FluidNC discovery:** Uses mDNS (`fluidnc.local` by default)
- **Alternative:** Can use direct IP address if mDNS doesn't work
- **Port:** WebSocket on port 81 (default)

**Example Config.h:**
```cpp
const char *ssid = "YourWiFiNetwork";
const char *password = "YourPassword";
const char *fluidnc_host = "fluidnc.local";  // or "192.168.1.100"
const uint16_t fluidnc_port = 81;
```

## 🙏 Credits

Based on excellent work by:
- [gjkrediet/Fluid-controller](https://github.com/gjkrediet/Fluid-controller) - Original Bluetooth design
- [AC8L/FluidNC-Pendant](https://github.com/AC8L/FluidNC-Pendant) - WiFi version

## 📝 Changelog

See [CHANGELOG.md](CHANGELOG.md) for detailed version history.

## 📄 License

Inherits license from original project.
