# AuraOS Track for blendOS

Beautiful Aesthetics Meets Powerful Dev Tools - as a blendOS track!

## What is this?

This is a blendOS track that transforms a fresh blendOS installation into AuraOS, featuring:

- 🎨 **Hyprland Desktop** - Beautiful tiling Wayland compositor
- 🚀 **Aura-Dots** - Pre-configured dotfiles with custom Hyprland setup
- 🛠️ **Dev Tools** - Docker, Git tools, language runtimes, modern CLI utilities
- 🎭 **Aura Shell & CLI** - Custom shell and CLI utilities

## Installation Methods

### Method 1: During Installation (Recommended)

1. Boot the official blendOS ISO
2. When jade-gui installer asks for track, enter:
   ```
   https://aura-repo.cortexnest.icu/tracks/auraos.yaml
   ```

### Method 2: After Installation

1. Install blendOS normally with any track (or blendos-base)
2. After first boot, edit `/system.yaml`:
   ```bash
   sudo nano /system.yaml
   ```
3. Change the track settings:
   ```yaml
   repo: 'https://aura-repo.cortexnest.icu/tracks'
   impl: 'https://github.com/blend-os/tracks/raw/main'
   track: 'auraos'
   ```
4. Apply the changes:
   ```bash
   sudo akshara update
   ```
5. Reboot

### Method 3: Custom Track Repo

Fork this repo and customize `auraos.yaml` to your liking, then:

1. Upload to GitHub/GitLab
2. Use your repo URL during installation

## What Gets Installed?

### Desktop Environment
- Hyprland with custom Aura configuration
- SDDM login manager
- Waybar, Mako, Wofi
- All necessary Wayland protocols

### Development Tools
- Docker + Docker Compose
- Git tools (LazyGit, GitHub CLI)
- Language runtimes (Rust, Ruby, Python, Lua)
- Modern CLI tools (bat, eza, ripgrep, fd, zoxide, btop)

### Aura Components
- **aura-cli** - Aura CLI utilities
- **aura-shell** - QuickShell-based desktop shell
- **Aura-Dots** - Complete desktop configuration

### AUR Packages

Some packages need to be installed from AUR after first boot:
- walker (app launcher)
- xdg-terminal-exec
- hyprland-preview-share-picker
- And more...

Run this after installation:
```bash
install-aura-aur-packages
```

## Essential Keybindings

- `SUPER + RETURN` - Open terminal
- `SUPER + SPACE` - Application launcher
- `SUPER + Q` - Close window
- `SUPER + 1-9` - Switch workspaces
- `SUPER + F` - Toggle fullscreen

## Customization

### Adding More Packages

Edit `/system.yaml` and add packages under `packages:`, then run:
```bash
sudo akshara update
```

### Modifying Aura Configuration

Your Aura-Dots configs are in `~/.local/share/aura-dots/`

Edit configs in `~/.config/hypr/` and other locations as needed.

## Differences from Traditional AuraOS ISO

| Aspect | ISO Approach | Track Approach |
|--------|-------------|----------------|
| Updates | Reinstall or custom update | `sudo akshara update` |
| Customization | Rebuild ISO | Edit `/system.yaml` |
| Immutability | No | Yes (blendOS atomic) |
| Storage | ~3GB ISO | Minimal install |
| Installation | Custom installer | Official blendOS installer |

## Benefits of Track Approach

✅ **Atomic Updates** - Rollback if something breaks
✅ **Declarative Config** - Your entire system in one file
✅ **Easy Customization** - Edit YAML, not rebuild ISO
✅ **Official blendOS Support** - Uses official installer and tools
✅ **Smaller Download** - No need for large custom ISO

## Troubleshooting

### Track not found during installation

Make sure the URL is correct and your internet connection works.

### Packages fail to install

Check that the aura repository is accessible:
```bash
curl -I https://aura-repo.cortexnest.icu/x86_64/aura.db
```

### Aura-Dots not installed

Run manually:
```bash
cd ~/.local/share/aura-dots
fish install.fish --noconfirm
```

## Repository Structure

```
auraos-track/
├── auraos.yaml          # Main track file
├── README.md            # This file
└── assets/              # Branding assets (optional)
```

## Links

- **Aura-Dots**: https://github.com/CjLogic/Aura-Dots
- **blendOS**: https://blendos.co
- **blendOS Tracks**: https://github.com/blend-os/tracks

## License

Same as blendOS and Aura-Dots components.

---

Built with ❤️ using blendOS tracks and Aura aesthetics.
