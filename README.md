<h1 align="center">waybar-media</h1>

<p align="center">
A module to display currently playing media in your <a href="https://github.com/Alexays/Waybar">Waybar</a>.
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/7fd2caa3-d566-40eb-b8a1-1f87a24ac795" height="150">
</p>

> [!NOTE] 
> You're probably better off using [Waybar's native MPRIS module](https://github.com/Alexays/Waybar/wiki/Module:-MPRIS) rather than this custom one!  
> It does the same thing, and is way more customizable and robust.


---

Shows data from:

* **Firefox, Google Chrome, Chromium** and other browsers
* **MPV**
* Potentially, any other player with [MPRIS](https://www.freedesktop.org/wiki/Specifications/mpris-spec/) support. Feel free to open an issue or a pull request!

The current title and artist are shown in the toolbar. Long titles/artists are _ellipsized_ to 80 characters.

The tooltip displays more metadata, including the album and player name.


## Installation

For Arch Linux, **use the AUR package**: [waybar-media-git](https://aur.archlinux.org/packages/waybar-media-git)

You'll probably also want to install this, to get data from browsers: `pacman -S plasma-browser-integration`

<br/>

If you can't use the AUR package, follow these steps:

- Install the Python packages listed in `requirements.txt` (they should be available as a package from your distribution)
- Put `waybar-media.py` somewhere in your $PATH
- For browser integration, follow instructions from [KDE Plasma Integration](https://community.kde.org/Plasma/Browser_Integration) to install the native host and the browser extension(s). Note: KDE Plasma itself is not required.


## Configuration

Add to your Waybar configuration as a [custom module](https://github.com/Alexays/Waybar/wiki/Module:-Custom), like so:

```json
"custom/waybar-media": {
    "return-type": "json",
    "exec": "waybar-media.py status",
    "on-click": "waybar-media.py playpause",
    "on-scroll-up": "waybar-media.py previous",
    "on-scroll-down": "waybar-media.py next",
    "escape": true
}
```

`waybar-media.py` always takes one argument. These are the available options:

* `status`: Print the status in [Waybar's JSON format](https://github.com/Alexays/Waybar/wiki/Module:-Custom#module-custom-config-return-type).
* `playpause`: Toggle the state of the current player.
* `previous`: Go to the previous song.
* `next`: Go to the next song.

### Styling

You may use the following classes to style the module:

* `playing`
* `paused`
* `stopped`

Here's an example to be placed in the `styles.css` file alongside the Waybar configuration. See [Waybar's Styling docs](https://github.com/Alexays/Waybar/wiki/Styling) for more ideas.

```css
#custom-waybar-media.paused {
    color: grey;
}
```

## Troubleshooting

#### Waybar logs show `[error] waybar-media stopped unexpectedly, is it endless?`

The script is erroring out. Run `waybar-media.py status` directly in your terminal to see which errors show up.

#### Running the script shows `ModuleNotFoundError: No module named 'pydbus'`

The dependencies have not been installed. Check the installation instructions.
