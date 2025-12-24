# Package Sources Reference

## How blendOS resolves packages in system.yaml

When you list packages in `system.yaml`, blendOS/pacman searches for them in this order:

1. **Your custom repos** (defined in `package-repos:`)
2. **blendOS repos** (breakfast, etc.)
3. **Arch official repos** (core, extra, multilib)

## What comes from where:

### From YOUR aura repo (`https://aura-repo.cortexnest.icu/$arch`)

Only packages YOU built and added:

- ✅ `aura-cli` - Your CLI tool
- ✅ `aura-shell` - Your QuickShell desktop shell
- ✅ `aura-meta` - Meta package (depends on above + more)
- ✅ Any AUR packages you build (quickshell-git, dart-sass, app2unit, etc.)

### From Arch official repos (core, extra)

Everything else:

- ✅ `hyprland`, `waybar`, `mako`, `wofi` - Official Arch packages
- ✅ `firefox`, `docker`, `rust`, `python` - Official Arch packages
- ✅ `fish`, `ghostty`, `btop` - Official Arch packages
- ✅ All other packages in the list

### From blendOS repos (breakfast)

blendOS-specific packages (automatically configured):

- ✅ `blend-git`
- ✅ `blend-settings-git`
- ✅ `akshara-git`
- ✅ etc.

## What aura-meta pulls automatically:

When you install `aura-meta`, it automatically pulls these as dependencies:

```
aura-cli                      (from YOUR repo)
aura-shell                    (from YOUR repo)
hyprland                      (from Arch)
xdg-desktop-portal-hyprland   (from Arch)
xdg-desktop-portal-gtk        (from Arch)
hyprpicker                    (from Arch)
wl-clipboard                  (from Arch)
cliphist                      (from Arch)
inotify-tools                 (from Arch)
app2unit                      (from YOUR repo if you built it)
wireplumber                   (from Arch)
trash-cli                     (from Arch)
foot                          (from Arch)
fish                          (from Arch)
eza                           (from Arch)
fastfetch                     (from Arch)
starship                      (from Arch)
btop                          (from Arch)
jq                            (from Arch)
adw-gtk-theme                 (from Arch)
papirus-icon-theme            (from Arch)
qt5ct-kde                     (from Arch)
qt6ct-kde                     (from Arch)
ttf-jetbrains-mono-nerd       (from Arch)
```

## So in auraos.yaml, you only need:

1. **aura-meta** - Pulls all the above
2. **Additional packages** you want that aren't in aura-meta

## Example package install flow:

User runs: `sudo akshara update` (with auraos.yaml configured)

1. blendOS reads `/system.yaml`
2. Sees `package-repos:` → Adds your aura repo to pacman
3. Starts installing packages:
   - `aura-meta` → Looks in repos → Found in `https://aura-repo.cortexnest.icu/x86_64/`
   - `aura-meta` depends on `aura-cli` → Found in aura repo
   - `aura-meta` depends on `hyprland` → Found in Arch extra repo
   - `firefox` → Found in Arch extra repo
   - `docker` → Found in Arch extra repo
4. Done!

## Building your aura repo:

To add packages to your aura repo:

```bash
# Build AUR packages
cd /path/to/aur-package
makepkg -sf

# Add to your repo
cp *.pkg.tar.zst /path/to/aura-repo/x86_64/
cd /path/to/aura-repo/x86_64/
repo-add aura.db.tar.gz *.pkg.tar.zst

# Upload to server
rsync -av /path/to/aura-repo/ server:/var/www/aura-repo/
```

## Summary:

**Your aura repo = Only for packages YOU build (aura-cli, aura-shell, aura-meta, AUR packages)**

**Everything else = Comes from Arch official repos (already configured)**

The `package-repos:` section just ADDS your repo, it doesn't replace the others!
