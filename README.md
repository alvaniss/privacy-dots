# Privacy Dots
  
Displays the status of your microphone, camera, and location with beautiful colored dots.

![Status dots displayed in Waybar showing microphone, camera, and location indicators in green, orange, and blue](./assets/privacy-dots.png)

## Capabilities

- **Mic Status:** Shows a green dot when any microphone is in use.
- **Cam Status:** Shows an orange dot when any camera is active.
- **Loc Status:** Shows a blue dot when location services are in use.
- **Easy to Customize:** Add new statuses or change colors easily. The functionality is handled by a simple Bash script, and styling is managed with CSS.

## Defaults

The backend script polls status information every 3 seconds by default. It provides formatted text, tooltips, and styling classes, which you can use with any bar to display.

## Notes

This fork improves the original script by adding an actually working location usage tracker and rewriting the camera tracker, which can now be triggered even by a virtual webcam. And as I use Waybar, guide for it is the only one that's present.

Also I want to note that I don't have a laptop on which I can test this script and I'm forced to rely on using my phone as camera to test the camera tracker and `/usr/lib/geoclue-2.0/demos/agent` as a geolocation trigger. I can not guarantee that it fully works with the actual hardware modules. 

## Dependencies

1. `pipewire`
2. `v4l2loopback-dkms`
3. `jq`
4. `dbus`

## Installation for Waybar

1. Download the script and place it into your scripts folder: [privacy_dots.sh](https://github.com/alvaniss/privacy-dots/blob/main/privacy_dots.sh)

2. Add this module to your waybar config:

```jsonc
{
    "custom/privacydots": {
        "exec": "/path/to/script/privacydots.sh",
        "return-type": "json",
        "interval": 3,
        "format": "{text}",
        "tooltip": true,
        "escape": false,
        "markup": "pango"
    }
}
```

3. Add this module style to `~/.config/waybar/style.css` (optional):

```css
#custom-privacydots {
  padding: 0 10px;
  font-size: 12px;
  letter-spacing: 3px;
}
```

## TODO

(PRs are more than welcome btw)

- [ ] Add which apps use those features to the tooltip
- [ ] Add more installation guides for different bars
