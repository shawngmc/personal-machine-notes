# ASUS TUF Gaming FX507 Laptop

## Specs
[Vendor Page](https://www.asus.com/us/laptops/for-gaming/tuf-gaming/asus-tuf-gaming-f15-2023/techspec/)

## Linux
### Fedora 41
#### Status
- CPU: Good
- GPU: NVidia, Type-C not working
- Battery: Good
- Touchpad: Good
- Keyboard: OK - RGB Control not working
- SSD: Good
- RAM: Good
- Ethernet: Good
- WiFi: Good
- Bluetooth:


#### NVidia
See [this Reddit thread](https://www.reddit.com/r/Fedora/comments/18bj1kt/fedora_nvidia_secure_boot/)

Beyond that:
- Can only seem to get one external monitor working
  - Only one dedicated port - HDMI
  - Tried two USB-C DP Alt Mode Adapters
    - WeMe WM6309A - No device recognition whatsoever
    - DOCKCASE Explorer Edition Visual Smart USB C Hub (6-in-1)
      - Seems to recognize other parts OK
      - Unlike another laptop w/o DP Alt Mode, it doesn't report a problem with DP Alt Mode - just doesn't seem to see it
      - Tried ```sudo modprobe typec_displayport```; no luck


#### Keyboard
OpenRGB cannot control it - use asusctl. See install procedure below.
Then use CLI ```asusctl aura static -c ffffff``` or the ROG Control Center app.


#### Apps
- ASUS-Linux Tools
- Chrome
- Discord
- Htop
- Input Remapper
- Lutris
  - Battle.net
- NVidia Drivers
- Steam
- Tabby
- Tor Browser Launcher
- Ungoogled Chromium
- VS Code
- Wine


##### ASUS-Linux
[See the Fedora guide](https://asus-linux.org/guides/fedora-guide/)
```
# Enable Asusd
systemctl start asusd
# Enable Supergfxd
systemctl start supergfxd
```