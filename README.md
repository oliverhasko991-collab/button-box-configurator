# ⚡ Arduino Button Box Configurator

**Build your own DCS flight simulator button box without writing a single line of code!**

A web-based tool to configure Arduino boards as button boxes for flight simulators like DCS World. Simply select your components, assign keys, and download ready-to-use Arduino code.

🔗 **[Try it now!](https://oliverhasko991-collab.github.io/button-box-configurator/button-box-configurator-updated.html)**

---

## ✨ Features

- 🎮 **No coding required** - Visual configuration interface
- 🔌 **Multiple board support** - Leonardo, Pro Micro, R4 WiFi
- 🎛️ **Component library** - Buttons, toggles, encoders
- ⌨️ **Custom key mapping** - Assign any keyboard key
- 📥 **Instant code generation** - Download ready-to-upload .ino files
- 🎨 **Modern UI** - Clean, cyberpunk-inspired design

---

## 🚀 Quick Start

### 1. Choose Your Hardware

**Supported Arduino Boards:**
- Arduino Leonardo (recommended - native USB HID support)
- Arduino Pro Micro (recommended - native USB HID support)
- Arduino UNO R4 WiFi (⚠️ keyboard mode only)

**Supported Components:**
- Push buttons (momentary)
- 2-position toggle switches
- 3-position toggle switches (ON-OFF-ON)
- Rotary encoders (with optional click)

### 2. Use the Configurator

1. **Open the configurator** in Chrome or Edge browser
2. **Select your Arduino board** from the dropdown
3. **Configure each pin:**
   - Choose what component is connected (button, toggle, encoder, etc.)
   - Assign a keyboard key to each component
4. **Generate code** - Click "Generate Arduino Code"
5. **Download** - Click "Download .ino File"

### 3. Upload to Your Arduino

1. Open **Arduino IDE**
2. Open the downloaded `.ino` file
3. Select your board: **Tools → Board → [Your Board]**
4. Select the correct port: **Tools → Port → [Your COM Port]**
5. Click **Upload** (→ button)
6. Done! Your button box is ready!

---

## 🔧 Wiring Guide

### Basic Wiring Rules:

**Push Buttons & Toggles:**
- One pin → Arduino GPIO pin
- Other pin → GND (ground)

**2-Position Toggle (as 2 separate buttons):**
- Left pin → Arduino GPIO pin
- Center pin → GND
- Right pin → Different Arduino GPIO pin

**3-Position Toggle (ON-OFF-ON):**
- Top pin → Arduino GPIO pin
- Middle pin → GND
- Bottom pin → Different Arduino GPIO pin

**Rotary Encoder:**
- CLK (or A) → Arduino GPIO pin
- DT (or B) → Arduino GPIO pin
- GND → GND
- SW (click button) → Arduino GPIO pin (optional)

### Example Wiring Diagram:

```
Button:
  [Button Pin 1] ──→ Arduino Pin 2
  [Button Pin 2] ──→ GND

Toggle Switch (2-position):
  [Left Pin]   ──→ Arduino Pin 5
  [Center Pin] ──→ GND
  [Right Pin]  ──→ Arduino Pin 6

Rotary Encoder:
  [CLK Pin] ──→ Arduino Pin A4
  [DT Pin]  ──→ Arduino Pin A5
  [GND]     ──→ GND
  [SW Pin]  ──→ Arduino Pin 7 (optional)
```

**Important:** All components share a common GND connection.

---

## 🎮 Using in DCS World

Once your Arduino is programmed:

1. **Plug in your Arduino** - Windows will detect it as a keyboard
2. **Open DCS World**
3. **Go to Settings → Controls**
4. **Select your aircraft** (e.g., F-15C, F/A-18C)
5. **Bind controls:**
   - Click on the control you want to bind (e.g., "Landing Gear Down")
   - Press/flip the switch on your button box
   - DCS will detect the key and bind it
6. **Save and fly!** 🚁

---

## ⚠️ Troubleshooting

### "Code won't compile"

**Problem:** Arduino IDE shows compilation errors

**Solutions:**
- ✅ Make sure you have the **Keyboard library** installed (built-in for Leonardo/Pro Micro)
- ✅ For Leonardo/Pro Micro: No additional libraries needed
- ✅ For R4 WiFi: Code uses built-in Keyboard library
- ✅ Check that your board is correctly selected in **Tools → Board**

---

### "Can't upload to Arduino"

**Problem:** Upload fails or can't find COM port

**Solutions:**
- ✅ Check USB cable is connected (use a **data cable**, not charge-only)
- ✅ Select the correct board: **Tools → Board → [Your Arduino]**
- ✅ Select the correct port: **Tools → Port → COM[X]**
- ✅ Try a different USB port on your computer
- ✅ **For R4 WiFi:** If stuck, double-press reset button quickly, then upload immediately

---

### "Arduino R4 WiFi won't upload / shows 'Invalid serial port'"

**Problem:** R4 WiFi gets into a bad state after uploading joystick code

**Solutions:**
1. **Enter bootloader mode:**
   - Unplug Arduino
   - Hold reset button
   - Plug in USB while holding reset
   - Wait 2 seconds, release reset
   - LED should fade (bootloader mode)
2. **Upload immediately** while LED is fading
3. **If that fails:**
   - Try a different computer
   - Try a different USB cable
   - Use Keyboard mode code (not Joystick mode)

---

### "DCS doesn't detect my button presses"

**Problem:** Keys work in Notepad but not in DCS

**Solutions:**
- ✅ Make sure you're in the **Controls menu** when pressing buttons
- ✅ Try simpler keys (numbers, letters) instead of function keys
- ✅ Check if another program is intercepting the keys
- ✅ Restart DCS after plugging in Arduino

---

### "Button presses trigger multiple times"

**Problem:** One press registers as multiple presses

**Solutions:**
- ✅ Code already includes debouncing (50ms delay)
- ✅ If still happening, increase `delay(50)` to `delay(100)` in the code
- ✅ Check for loose wiring
- ✅ Use pull-up resistors if not using `INPUT_PULLUP`

---

### "Configurator won't open / shows blank page"

**Problem:** Web page doesn't load correctly

**Solutions:**
- ✅ Use **Chrome** or **Edge** browser (required for full functionality)
- ✅ Make sure JavaScript is enabled
- ✅ Clear browser cache and reload
- ✅ Check browser console for errors (F12 → Console tab)

---

### "Some pins don't work on R4 WiFi"

**Problem:** Pin 3 or other pins not responding

**Solutions:**
- ✅ **Pin 3 is known to be faulty on some R4 boards** - avoid it
- ✅ Use different pins from the dropdown
- ✅ Test pins individually with simple code first
- ✅ Some pins may be reserved for internal use

---

## 📝 Key Mapping Tips

**Best practices for key assignment:**

✅ **DO:**
- Use uncommon keys (F13-F24, brackets, equals, semicolon)
- Use number keys (1-9, 0)
- Use Page Up/Down for encoders
- Test keys in Notepad first to confirm they work

❌ **AVOID:**
- Common game keys (WASD, Space, Enter)
- Modifier keys alone (Ctrl, Alt, Shift)
- Keys used by Windows (Win key, Alt+Tab, etc.)
- Keys DCS uses for other functions

**Popular key choices:**
- Toggles: 1, 2, 3, 4, 5, 6, 7, 8, 9, 0
- Buttons: [, ], \, =, ;, ', ,, .
- Encoders: Page Up/Down, Home/End

---

## 🛠️ Hardware Tips

### Choosing Components:

**Buttons:**
- 6x6mm tactile buttons (cheap, easy to find)
- Arcade buttons (larger, satisfying click)
- Momentary switches (professional feel)

**Toggle Switches:**
- MTS-102 (2-position)
- MTS-103 (3-position ON-OFF-ON)
- Check pinout before buying!

**Rotary Encoders:**
- EC11 encoder (common, cheap)
- Make sure it has detents (clicks when rotated)
- Optional: with push button (SW pin)

**Wiring:**
- 22-24 AWG wire
- Different colors for organization
- Heat shrink tubing for clean connections
- Label everything!

---

## 🏗️ Build Tips

### 3D Printing Your Enclosure:

1. **Design in Fusion 360** (or Tinkercad for beginners)
2. **Key measurements:**
   - 6mm holes for 6x6mm tactile buttons
   - 6mm holes for MTS-102/103 toggle switches
   - 7mm holes for EC11 rotary encoders
   - Add **0.2-0.3mm tolerance** for 3D printed holes
3. **Print settings:**
   - 0.2mm layer height
   - 3-4 walls for strength
   - 20% infill minimum
4. **Test print first!** Print one button/switch hole to check fit

### Wiring Organization:

- Use a breadboard for prototyping first
- Test each component individually before final assembly
- Solder connections for reliability
- Use heat shrink or electrical tape on all connections
- Bundle wires with zip ties or braided sleeve
- Label each wire (masking tape + marker)

### Testing:

1. **Test each component individually first**
2. **Use Serial Monitor** to verify pin readings
3. **Test in Notepad** before testing in DCS
4. **Document your key mappings** for reference

---

## 🤝 Contributing

Found a bug? Have a feature request? Contributions are welcome!

1. Fork the repository
2. Create your feature branch
3. Submit a pull request

---

## 📜 License

This project is open source and available under the MIT License.

---

## 💡 Credits

Created by **oliverhasko991-collab**

Special thanks to the DCS and Arduino communities!

---

## 🔗 Useful Links

- [Arduino IDE Download](https://www.arduino.cc/en/software)
- [DCS World](https://www.digitalcombatsimulator.com/)
- [Arduino Keyboard Library Documentation](https://www.arduino.cc/reference/en/language/functions/usb/keyboard/)
- [Arduino Forum](https://forum.arduino.cc/)

---

**Happy flying! ✈️🎮**

If you found this helpful, give it a ⭐ on GitHub!
