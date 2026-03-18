# Waybar config (top + dock)

Waybar configuration for Hyprland with a top “system” bar and a bottom dock‑like bar (auto‑hide).
## Screenshot

![Screenshot](assets/screen.jpg)

## Arborescence

```bash
~/.config/waybar
├── config                # barre du haut (non inclus ici)
├── style.css             # style barre du haut
├── config-bottom.jsonc   # dock du bas
├── style-bottom.css      # style dock du bas
└── power_menu.xml        # menu power (wofi / wlogout, etc.)
```

## Barre du bas : dock
config-bottom.jsonc defines a dock‑style Waybar, centered at the bottom, with keybind‑hide.
### Principales options :

```text
{
  "name": "dockbar",
  "id": "dockbar",
  "layer": "bottom",
  "position": "bottom",
  "mod": "dock",
  "exclusive": true,
  "gtk-layer-shell": true,
  "height": 40,
  "margin-bottom": 10,
  "margin-left": 500,
  "margin-right": 500,
  "start_hidden": true,
  "on-sigusr1": "toggle",
  "on-sigusr2": "toggle",

  "modules-left": [
    "custom/space",
    "custom/launcher",
    "custom/separator"
  ],
  "modules-center": [
    "custom/deezer",
    "custom/firefox",
    "custom/perplexity",
    "custom/files",
    "custom/kitty"
  ],
  "modules-right": [
    "power-profiles-daemon",
    "battery",
    "custom/space"
  ]
}
```

### Main modules :
- custom/launcher: application menu (wofi).
- custom/deezer: launches deezer-desktop.
- custom/firefox: launches Firefox.
- custom/perplexity: launches Perplexity (your custom launcher).
- custom/files: launches Thunar.
- custom/kitty: launches Kitty.
- battery: battery status (icon + percentage).
- power-profiles-daemon: current power profile.

### Module config snippets : 

```text
"custom/launcher": {
  "format": "",
  "on-click": "wofi --width=400 --height=500 --xoffset=500 --yoffset=430 --show drun",
  "tooltip": false
},

"custom/deezer": {
  "format": "",
  "on-click": "deezer-desktop",
  "tooltip": false
},

"battery": {
  "bat": "BAT1",
  "interval": 60,
  "states": {
    "warning": 30,
    "critical": 15
  },
  "format": "{icon} {capacity}%",
  "format-icons": ["", "", "", "", ""]
}
```

## Top bar style :
style.css handles the main (top) bar, with modules grouped on the left / center / right and a Catppuccin‑like theme.

### Features :

- Font : JetBrainsMono Nerd Font, 12pt.
- .modules-left, .modules-center, .modules-right groups with semi‑transparent background and rounded borders.
- Workspaces as compact pills with active, hover and urgent states.
- Specific colors for network, bluetooth, audio, backlight, battery, PPD, clock, power, music.

### Workspaces examples:

```css
#workspaces button {
  font-size: 2pt;
  border-radius: 5px;
  color: #bac2de;
  background: rgba(93, 93, 93, 0.8);
  padding: 0px 6px;
  margin-top: 6px;
  margin-bottom: 6px;
}

#workspaces button.active {
  color: #1e1e2e;
  font-weight: 600;
  background: #cdd6f4;
  padding: 0px 10px;
  margin-top: 2px;
  margin-bottom: 2px;
}
```

### Hover modules de droite :

```css
#network:hover,
#bluetooth:hover,
#wireplumber:hover,
#backlight:hover,
#battery:hover,
#power-profiles-daemon:hover,
#custom-power:hover,
#tray:hover,
#custom-music:hover {
  background: rgba(93, 93, 93, 0.8);
  border-radius: 5px;
  border-bottom: 1px solid #bb9af7;
  margin-bottom: 4px;
}
```

### Dock style (bottom bar)
- style-bottom.css applies a dock look with rounded corners and icons that grow on hover.

### Features:
- Rounded background (border-radius: 16px;) with a light translucent fill.
- Center icons (deezer, firefox, perplexity, files, kitty) at 18px that scale up to 42px on hover.
- Battery + power‑profiles aligned on the right, with underline‑style hover.​

### Snippets :

```css
window#waybar {
  background: rgba(200, 200, 200, 0.1);
  border-radius: 16px;
  color: #c0caf5;
}

#custom-deezer,
#custom-firefox,
#custom-files,
#custom-perplexity,
#custom-kitty {
  border-radius: 12px;
  padding-left: 20px;
  padding-right: 20px;
  margin-top: 19px;
  margin-bottom: 19px;
  font-size: 18px;
}

#custom-deezer:hover,
#custom-firefox:hover,
#custom-files:hover,
#custom-kitty:hover,
#custom-perplexity:hover {
  font-size: 42px;
  margin-top: 1px;
  margin-bottom: 1px;
}
```

###Dependencies

#### Main required packages:
- waybar
- wofi (launcher)
- thunar (file manager, or adjust the command)
- kitty
- firefox
- deezer-desktop
- power-profiles-daemon
- fonts: JetBrainsMono Nerd Font, and Nerd Fonts for icons (, , etc.)
- wlogout
- NetworkManagerGtk
- Hyprpicker
- Blueman-manager

### Hyprland integration
Waybar is started from the Hyprland config (example):

```text
exec-once = waybar -c ~/.config/waybar/config -s ~/.config/waybar/style.css
exec-once = waybar -c ~/.config/waybar/config-bottom.jsonc -s ~/.config/waybar/style-bottom.css
```
### Keybind 
- <leader>space : bottom waybar
