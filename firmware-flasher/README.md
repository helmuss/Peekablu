# Flasher Firmware

This folder contains the manifest and firmware binaries for the **Flasher Firmware** option.

## Required Binary Files

To make this firmware flashable, you need to upload the following 4 binary files to this directory:

### 1. `bootloader.bin`
- **Location in Arduino IDE:** After compilation, find at:
  - **Windows:** `%TEMP%\arduino\sketches\<sketch_name>\bootloader.bin`
  - **macOS/Linux:** `/tmp/arduino/sketches/<sketch_name>/bootloader.bin`
- **Offset:** 0x1000 (4096 bytes)

### 2. `partitions.bin`
- **Location in Arduino IDE:** After compilation, find at:
  - **Windows:** `%TEMP%\arduino\sketches\<sketch_name>\partitions.bin`
  - **macOS/Linux:** `/tmp/arduino/sketches/<sketch_name>/partitions.bin`
- **Offset:** 0x8000 (32768 bytes)

### 3. `boot_app0.bin`
- **Location in Arduino IDE:** This file is usually located in your Arduino15 packages folder:
  - **Windows:** `%LOCALAPPDATA%\Arduino15\packages\esp32\hardware\esp32\<version>\tools\partitions\boot_app0.bin`
  - **macOS:** `~/Library/Arduino15/packages/esp32/hardware/esp32/<version>/tools/partitions/boot_app0.bin`
  - **Linux:** `~/.arduino15/packages/esp32/hardware/esp32/<version>/tools/partitions/boot_app0.bin`
- **Offset:** 0xE000 (57344 bytes)

### 4. `app.bin`
- **Location in Arduino IDE:** After compilation, find at:
  - **Windows:** `%TEMP%\arduino\sketches\<sketch_name>\<sketch_name>.ino.bin`
  - **macOS/Linux:** `/tmp/arduino/sketches/<sketch_name>/<sketch_name>.ino.bin`
- **Note:** Rename this file to `app.bin` when placing it in this folder
- **Offset:** 0x10000 (65536 bytes)

## How to Export from Arduino IDE

1. **Compile your sketch:**
   - Open your Arduino sketch
   - Select **Tools → Board → esp32 → Arduino Nano ESP32**
   - Select **Sketch → Verify/Compile**

2. **Export compiled binary:**
   - After successful compilation, go to **Sketch → Export Compiled Binary**
   - This generates the firmware files in the temporary build directory

3. **Locate the files:**
   - Use the paths mentioned above based on your operating system
   - Look for the temporary sketch directory created by Arduino IDE
   - The sketch name folder contains your compiled binaries

4. **Copy files to this folder:**
   - Copy all 4 binary files to this `firmware-flasher/` directory
   - Ensure filenames match exactly: `bootloader.bin`, `partitions.bin`, `boot_app0.bin`, `app.bin`

5. **Commit and push:**
   - Add the files to git and push to update the repository
   - GitHub Pages will automatically serve the updated firmware

## Verification

After uploading, this folder should contain:
- ✅ `manifest.json` (already present)
- ✅ `README.md` (this file)
- ✅ `bootloader.bin` (upload this)
- ✅ `partitions.bin` (upload this)
- ✅ `boot_app0.bin` (upload this)
- ✅ `app.bin` (upload this)

Once all files are present, users can flash this firmware through the web interface!
