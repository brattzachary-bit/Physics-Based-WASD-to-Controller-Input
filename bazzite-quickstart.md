# PhysInput Quickstart for Bazzite

## Step 1: Install Dependencies

Bazzite is immutable, so use pip with `--user`:

```bash
pip install evdev PyQt6 --user
```

## Step 2: Add Yourself to Input Group

```bash
sudo usermod -aG input $USER
```

## Step 3: Log Out and Back In

**This is required.** The group change won't work until you do.

Or reboot if you want to be sure:
```bash
systemctl reboot
```

## Step 4: Download & Extract PhysInput

```bash
cd ~/Downloads
unzip physinput-linux-v1.1.0.zip
cd physinput-linux
```

## Step 5: Install PhysInput

```bash
pip install -e . --user
```

## Step 6: Run It

```bash
physinput
```

---

## All Commands (Copy/Paste Block)

```bash
# Run these in order
pip install evdev PyQt6 --user
sudo usermod -aG input $USER

# NOW LOG OUT AND BACK IN, then continue:

cd ~/Downloads
unzip physinput-linux-v1.1.0.zip
cd physinput-linux
pip install -e . --user
physinput
```

---

## Verify It's Working

```bash
# Check permissions and dependencies
physinput --check
```

Should show:
```
✓ Dependencies OK
✓ User is in 'input' group
```

---

## Troubleshooting

### "Command not found: physinput"

Add pip user bin to your PATH:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
physinput
```

### "Permission denied" on input devices

You didn't log out after adding to input group:

```bash
# Check if you're in the group
groups | grep input

# Quick workaround without logging out
newgrp input
physinput
```

### PyQt6 display issues

```bash
# Try forcing X11 if on Wayland
QT_QPA_PLATFORM=xcb physinput
```

### evdev build fails

Install build dependencies:

```bash
sudo rpm-ostree install python3-devel gcc
systemctl reboot
pip install evdev --user
```

---

## Create Desktop Shortcut (Optional)

```bash
cat > ~/.local/share/applications/physinput.desktop << 'EOF'
[Desktop Entry]
Type=Application
Name=PhysInput
Comment=Physics-based analog input for gaming
Exec=physinput
Icon=input-gaming
Terminal=false
Categories=Game;Utility;
EOF
```

Now it appears in your app menu.

---

## Uninstall

```bash
pip uninstall physinput
rm -rf ~/.config/physinput
rm ~/.local/share/applications/physinput.desktop
```
