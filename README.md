## README: RGB Hub Pro | Galax Controller Edition

This project is a lightweight, browser-based utility designed to control **Galax ARGB Hubs** (and compatible controllers using the `1a2c:1507` chipset) directly via the WebHID API. No bulky software installation is required—just a compatible browser.

---

### 🚀 Key Features

* **Zero Installation:** Runs entirely in the browser (Chrome, Edge, or Opera).
* **Custom Color Selection:** Full RGB spectrum control using an integrated color wheel.
* **Dynamic Lighting Modes:** Support for both custom color animations (Breathe, Blink, Laser) and hardware-preset patterns (Rainbow, Aurora, Meteor).
* **Cross-Platform Support:** Works on Windows and Linux (with minor permission adjustments).

---

### 🛠 Hardware Compatibility

This controller is specifically tuned for devices with the following hardware IDs:

* **Vendor ID:** `0x1a2c`
* **Product ID:** `0x1507`

Commonly found in **Galax ARGB Control Boxes** and certain built-in GPU/Case controllers that interface via internal USB headers.

---

### 📖 How to Use

1. **Open the Hub:** Launch the HTML file in a Chromium-based browser (Chrome, Edge).
2. **Connect:** Click **🔌 Connect Hub**. A browser popup will appear; select your device and click "Connect".
3. **Configure:** * Choose a **Lighting Mode** from the dropdown.
* If the mode supports custom colors, the **Color Wheel** will become active.


4. **Apply:** Click **Apply Settings** to send the command packet to your controller.

---

### 🐧 Linux Setup (udev Rules)

On Linux, browsers typically do not have permission to access HID raw devices by default. To fix this, you must create a udev rule:

1. Create a new rule file:
```bash
sudo nano /etc/udev/rules.d/99-rgb-hub.rules

```


2. Paste the following line into the file:
```bash
KERNEL=="hidraw*", ATTRS{idVendor}=="1a2c", ATTRS{idProduct}=="1507", MODE="0666"

```


3. Reload rules and replug your device:
```bash
sudo udevadm control --reload-rules && sudo udevadm trigger

```



---

### 🛠 Technical Details

The controller communicates using 64-byte HID report packets.

* **Report ID:** `0x00`
* **Header:** `0x80, 0x0b, 0x02, 0x0f`
* **Byte 4:** Mode ID
* **Byte 6:** Parameter/Speed ID
* **Bytes 8-10:** Red, Green, and Blue values (0-255)

---

### ⚠️ Disclaimer

*This project is an independent tool and is not affiliated with or endorsed by GALAX. Use it at your own risk. Incorrectly formatted packets are generally ignored by the hardware but always ensure your controller matches the IDs above.*

This video explains the fundamental connections of RGB hubs and controllers, which is helpful if you are setting up the Galax hardware for the first time.
