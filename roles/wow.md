# World of Warcraft

# Using Faugus instead of Lutris
By default, Lutris (0.5.19 in Fedora 41) uses wine-ge for WoW. It can't seem to use ge-proton properly - battle.net will launch, but WoW cant detect the graphics card - it's not bridging DX12 -> Vulkan properly via VKD3D.

Instead, use Faugus Launcher. It uses the new UMU-Launcher for GE-Proton, and works much better.
```
sudo dnf -y copr enable faugus/faugus-launcher
sudo dnf -y install faugus-launcher
# Optional tools
sudo dnf -y install mangohud
sudo dnf -y install gamemode
```

Consider using Bottles, but can I use GE-Proton with it? Yes!
https://docs.usebottles.com/components/runners

## Not working
- TSM Desktop App

## Cut and Paste Scratchpad
```
# Install other tools?
sudo dnf install wl-clipboard xclip 

# Install Rust Toolchain
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
# Re-source env
. "$HOME/.cargo/env"
# Install Clipboard-sync
cargo install clipboard-sync
# Copy the systemd unit
wget -P "$HOME/.config/systemd/user/" https://raw.githubusercontent.com/dnut/clipboard-sync/master/clipboard-sync.service

```

## CurseForge
Use the AppImage!
```
curl -o curseforge-latest-linux.zip https://curseforge.overwolf.com/downloads/curseforge-latest-linux.zip
unzip curseforge-latest-linux.zip
ail-cli CurseForge*.AppImage
rm -rf curseforge-latest-linux.zip
```

# TradeSkillMaster
```
curl -o tsm-setup.exe https://app-cdn.tradeskillmaster.xyz/legacyDesktopApp/setup.exe
# Add Installer as App in Faugus Launcher to get it in the right namespace
# Setup still won't show up - it launches, but never appears

```