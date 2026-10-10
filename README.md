# 🏹 The Archer Dotfiles

A highly customized, blazingly fast Arch Linux setup using **bspwm**, heavily modified for a seamless, daily-driver experience.

## 🏆 Credits

This rice is proudly built upon the incredible foundational dotfiles by [gh0stzk](https://github.com/gh0stzk/dotfiles). The core aesthetic and theme engine belong to them, while this repository adds custom quality-of-life fixes, structural path optimizations, and improved window-management workflows.

---

## 📸 Overview

* **OS:** Arch Linux
* **Window Manager:** bspwm
* **Hotkey Daemon:** sxhkd
* **Terminal:** zsh + kitty/alacritty
* **App Launcher / Window Switcher:** Rofi
* **Wallpaper Engine:** feh (with dynamic caching)

---

## 🛠️ Step 1: Base Arch Linux Installation

If you are starting from scratch, boot into the Arch Linux live USB. When presented with the terminal, we recommend using the guided installer:

```bash
archinstall

```

**Recommended `archinstall` Settings:**

* **Profile:** Desktop -> bspwm
* **Audio:** Pipewire
* **Bootloader:** GRUB or systemd-boot
* **Network:** NetworkManager

Once the installation finishes and you reboot into your fresh Arch system, ensure your system is fully updated:

```bash
sudo pacman -Syu

```

---

## 📦 Step 2: Install Required Dependencies

Before applying these dotfiles, you must install the underlying software, tools, and crucial Nerd Fonts so the interface icons render correctly. Run the following command:

```bash
sudo pacman -S bspwm sxhkd rofi feh zsh stow xorg-xsetroot xclip xdotool polkit-gnome imagemagick jq ttf-jetbrains-mono-nerd ttf-nerd-fonts-symbols

```

*(Note: Ensure you have an AUR helper like `yay` or `paru` installed if you plan to use animated compositors like `picom-ftlabs-git` later on).*

---

## 🚀 Step 3: Installation & Deployment (Using GNU Stow)

This repository uses `stow` to cleanly manage configurations via symlinks. You do not need to use the original gh0stzk installer script or copy files manually.

**1. Clone this repository into your home folder:**

```bash
git clone https://github.com/Braveen811/the_archer_dotfiles.git ~/dotfiles
cd ~/dotfiles

```

**2. Backup any existing configurations (highly recommended):**

```bash
mv ~/.config/bspwm ~/.config/bspwm.bak
mv ~/.config/sxhkd ~/.config/sxhkd.bak
mv ~/.zshrc ~/.zshrc.bak

```

**3. Deploy the dotfiles using Stow:**

```bash
stow .

```

Stow will automatically create the correct shortcuts in your `~/.config` and `~/Pictures` directories pointing to this repository.

**4. Reload your Window Manager:**
Press `Super + Escape` (or `Super + Alt + r`) to reload bspwm and apply the themes!

---

## 🔧 Custom Tweaks & Fixes in this Build

This repository includes several specific workflow enhancements over the base configuration:

### 1. Centralized Wallpaper Management

Instead of scattering wallpapers across individual theme folders, this setup uses a single master directory synced via Stow.

* **Location:** `~/Pictures/MyWalls/Wallpapers/`
* **Fix:** The `WallSelect` Rofi script and `02-wallpaper.sh` backend have been rewritten using universal `$HOME` variables to pull dynamically from this master folder, generate thumbnails, and cache them instantly for any user.
* **Shortcut:** `Super + Alt + w`

### 2. Instant `Alt+Tab` Window Switching

The default Rofi node switcher requires you to press `Enter` to confirm a window selection. This config modifies Rofi flags to behave natively:

* Hold `Alt`, tap `Tab` to cycle.
* Release `Alt` to instantly switch to the selected window.

### 3. Smart Desktop Context Menu (jgmenu)

Right-clicking the empty desktop natively queries `bspc` to check for active windows before launching the menu. This ensures `jgmenu` only opens when clicking the actual wallpaper, bypassing X11/feh "root window" detection bugs.

### 4. Smart Window Closing

* `Super + x`: Politely asks an application to close (prompts to save work).
* `Super + Shift + x`: Instantly force-kills a frozen node/application.
