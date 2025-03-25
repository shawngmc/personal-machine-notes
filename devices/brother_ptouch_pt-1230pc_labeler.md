# Brother P-Touch Labeler PT-1230PC

Based on instructions from [here](https://github.com/HenrikBengtsson/brother-ptouch-label-printer-on-linux?tab=readme-ov-file)

## Installation

```
# Install libusb and compat
sudo dnf install -y libusb-compat-0.1 libusb-compat-0.1-devel libusb1 libusb1-devel
# Install other pre-reqs
sudo dnf install -y cmake gd-devel gettext

# Clone it
cd /tmp
git clone https://git.familie-radermacher.ch/linux/ptouch-print.git

# Build it/Lights-on test
cd ptouch-print
./build.sh
build/ptouch-print --version

# Install system-wide, including UDEV rules to access
sudo make -C build/ install

# Cleanup
cd /tmp
rm -rf ptouch-print
```

## Examples
```
# HDMI Switch Label
sudo ptouch-print --font "Noto Sans Mono" --fontsize 20 --text "Output: Samsung   Dell" "Input:  Gaming    Flex      Work      Mac" --writepng hdmi.png
img2sixel hdmi.png
sudo ptouch-print --image hdmi.png

# USB Switch Labels
sudo ptouch-print --font "Noto Sans Mono" --fontsize 20 --text "KB        Mouse     Keypad     Flex" --writepng usbdev.png
img2sixel usbdev.png
sudo ptouch-print --image usbdev.png
sudo ptouch-print --font "Noto Sans Mono" --fontsize 15 --text "1: Gaming" "2: Flex" "3: Work" "4: Mac --writepng usbhost.png
img2sixel usbhost.png
sudo ptouch-print --image usbhost.png
```

## Notes
- Must be in E-Mode, not EL/P-Lite (Switch on back to E, not EL)
- ```libusb_open error :LIBUSB_ERROR_ACCESS``` means a UDev Permission error - either use Sudo or reboot?
- ```sudo dnf install -y libsixel-utils``` to view the PNGs on the cli easily with ```img2sixel```