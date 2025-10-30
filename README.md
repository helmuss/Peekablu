# 🎯 Peekablu

**Peekablu** is a web-based ESP32 firmware flasher that allows users to easily flash their Arduino Nano ESP32 (ESP32-S3) boards with custom firmware directly from their browser - no Arduino IDE or additional software required!

## 🌟 Features

- **Dual Firmware Options:** Choose between Poster Firmware or Flasher Firmware
- **Browser-Based Flashing:** No software installation needed
- **Modern UI:** Clean, intuitive interface with visual feedback
- **One-Click Installation:** Select firmware and flash with a single button
- **ESP32-S3 Optimized:** Specifically configured for Arduino Nano ESP32

## 🚀 Live Demo

**Flasher URL:** `https://helmuss.github.io/Peekablu/`

Visit the URL above in Chrome, Edge, or Opera to start flashing!

## 🖥️ Browser Requirements

This flasher uses ESP Web Tools which requires:
- ✅ Google Chrome
- ✅ Microsoft Edge
- ✅ Opera
- ❌ Firefox (not supported)
- ❌ Safari (not supported)

## 📖 How to Use

### For End Users (Flashing Firmware):

1. **Open the flasher** in Chrome, Edge, or Opera browser
2. **Connect your Arduino Nano ESP32** to your computer via USB
3. **Select your desired firmware:**
   - 📊 **Poster Firmware** - For display and poster functionality
   - ⚡ **Flasher Firmware** - For advanced flashing capabilities
4. **Click "Install Firmware"** button
5. **Select your device** from the popup dialog
6. **Wait for the flash** to complete
7. **Done!** Your device is now running the selected firmware

### For Developers (Uploading Firmware):

If you want to update the firmware binaries that users can flash:

#### Step 1: Compile Your Arduino Sketch

1. Open your sketch in Arduino IDE
2. Select **Tools → Board → esp32 → Arduino Nano ESP32**
3. Compile: **Sketch → Verify/Compile**
4. Export: **Sketch → Export Compiled Binary**

#### Step 2: Locate the Binary Files

After compilation, find these files in the temporary build directory:

**On macOS/Linux:**
```bash
/tmp/arduino/sketches/<your_sketch_name>/
```

**On Windows:**
```
%TEMP%\arduino\sketches\<your_sketch_name>\
```

You need these 4 files:
- `bootloader.bin`
- `partitions.bin`
- `<your_sketch_name>.ino.bin` (rename to `app.bin`)
- `boot_app0.bin` (from Arduino15 packages folder)

**Finding boot_app0.bin:**
- **macOS:** `~/Library/Arduino15/packages/esp32/hardware/esp32/<version>/tools/partitions/boot_app0.bin`
- **Linux:** `~/.arduino15/packages/esp32/hardware/esp32/<version>/tools/partitions/boot_app0.bin`
- **Windows:** `%LOCALAPPDATA%\Arduino15\packages\esp32\hardware\esp32\<version>\tools\partitions\boot_app0.bin`

#### Step 3: Upload to GitHub

1. **Choose the firmware folder:**
   - For Poster variant: `firmware-poster/`
   - For Flasher variant: `firmware-flasher/`

2. **Copy the 4 binary files** to the chosen folder

3. **Commit and push:**
   ```bash
   git add firmware-poster/*.bin  # or firmware-flasher/*.bin
   git commit -m "Update firmware binaries"
   git push
   ```

4. **Wait ~1 minute** for GitHub Pages to rebuild

5. **Done!** Users can now flash your updated firmware

## 📁 Project Structure

```
Peekablu/
├── index.html                  # Main flasher web interface
├── README.md                   # This file
├── firmware-poster/           # Poster firmware files
│   ├── manifest.json          # ESP Web Tools manifest
│   ├── README.md              # Instructions for this firmware
│   ├── bootloader.bin         # (Upload your file here)
│   ├── partitions.bin         # (Upload your file here)
│   ├── boot_app0.bin          # (Upload your file here)
│   └── app.bin                # (Upload your file here)
└── firmware-flasher/          # Flasher firmware files
    ├── manifest.json          # ESP Web Tools manifest
    ├── README.md              # Instructions for this firmware
    ├── bootloader.bin         # (Upload your file here)
    ├── partitions.bin         # (Upload your file here)
    ├── boot_app0.bin          # (Upload your file here)
    └── app.bin                # (Upload your file here)
```

## 🔧 Memory Offsets (ESP32-S3)

Each manifest.json is configured with the following memory offsets for Arduino Nano ESP32:

| File | Offset (Hex) | Offset (Decimal) |
|------|-------------|------------------|
| `bootloader.bin` | 0x0 | 0 |
| `partitions.bin` | 0x8000 | 32768 |
| `boot_app0.bin` | 0xE000 | 57344 |
| `app.bin` | 0x10000 | 65536 |

## 🛠️ Technical Details

- **ESP Web Tools Version:** 11
- **Target Chip:** ESP32-S3 (Arduino Nano ESP32)
- **Flash Mode:** Full erase on new install
- **Communication Protocol:** Web Serial API

## 📝 Updating Firmware

To update the firmware that users can flash:

1. Modify your Arduino sketch
2. Export compiled binaries
3. Copy the 4 .bin files to the appropriate `firmware-*/` folder
4. Push to GitHub
5. GitHub Pages automatically updates

## 🔒 Security Note

This flasher completely erases the device before installing new firmware. Make sure users understand they will lose any existing data on their ESP32.

## 🤝 Contributing

To add new firmware options:

1. Create a new `firmware-<name>/` folder
2. Add `manifest.json` and required .bin files
3. Update `index.html` to include the new option
4. Commit and push changes

## 📚 Resources

- [ESP Web Tools Documentation](https://esphome.github.io/esp-web-tools/)
- [Arduino Nano ESP32 Guide](https://docs.arduino.cc/hardware/nano-esp32/)
- [ESP32-S3 Technical Reference](https://www.espressif.com/sites/default/files/documentation/esp32-s3_technical_reference_manual_en.pdf)

## 📄 License

This project structure is open source. Add your own license as needed.

## 💬 Support

For issues or questions:
1. Check the README files in each firmware folder
2. Verify you're using Chrome, Edge, or Opera
3. Ensure your Arduino Nano ESP32 is properly connected
4. Try a different USB cable if connection fails

---

**Built with ❤️ using ESP Web Tools**
