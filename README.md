# Privacy Dots
  
Script that displays the status of your microphone, camera, location and screen sharing with colored dots along with which apps are using them.

![Status dots displayed in Waybar showing microphone, camera, location and screen sharing indicators in green, orange, blue and purple](./assets/privacy-dots.png)

## Features

- **Microphone Status:** Shows a green dot when any microphone is in use.
- **Camera Status:** Shows an orange dot when any camera is active.
- **Location Status:** Shows a blue dot when location services are in use.
- **Screen Sharing Status:** Shows a purple dot when screen sharing is active.
- **Easy to Customize:** Add new statuses or change colors easily. The functionality is handled by a simple Bash script, and styling is managed with CSS.

## Defaults

The backend script polls status information every 3 seconds by default. It provides formatted text, tooltips, and styling classes, which you can use with any bar to display.

## Dependencies

1. `pipewire`
2. `v4l2loopback-dkms`
3. `jq`
4. `dbus`

## Installation

### Arch Linux

Install from AUR with your helper of choice (example uses `yay`):

```shell
yay -S privacy-dots
```

### Manual

```shell
cd /path/to/script/

curl -O https://github.com/alvaniss/privacy-dots/privacy_dots.sh

chmod +x privacy_dots.sh
```

## Adding to Waybar

1. Add this module to your Waybar config:

```jsonc
{
    "custom/privacy-dots": {
        "exec": "/path/to/script/privacy_dots.sh", // or if installed from AUR: "exec": "privacy-dots",
        "return-type": "json",
        "interval": 3,
        "format": "{text}",
        "tooltip": true,
        "escape": false,
        "markup": "pango"
    }
}
```

You can add this module to any section (`modules-left`, `modules-center`, or `modules-right`) according to your preference. For example, to add it to the center:

```jsonc
"modules-center": ["clock", "custom/privacy-dots"]
```

2. Add this module style to `~/.config/waybar/style.css` (optional):

```css
#custom-privacy-dots {
  padding: 0 10px;
  font-size: 12px;
  letter-spacing: 3px;
}
```

## Notes

- This fork improves on the original script by adding a working location usage tracker and rewriting the camera tracker, which can now be triggered even by a virtual webcam.

- Since I use Waybar, guide for it is the only one that's present here. If you implement this script to work with another status bar, please submit a PR with the installation guide!

- I don’t have a laptop with a hardware-implemented webcam or location detection feature, so I can not guarantee that it will work fully with them. I’ve tried my best to use alternatives that go through the same processes, but it might still behave differently on your hardware.

- All indicators tested and proved to be working with `OBS`, `gpu-screen-recorder`, `Discord` and `Telegram`. Screen Sharing indicator does not work when sharing tabs in the web version of Discord in the same browser.

## TODO

- [ ] Add more installation guides for different bars
- [x] Add which apps use those features to the tooltip
- [x] Add an indicator if screen is being recorded/shared

## License

This project is open source. See the LICENSE file for details
