# waybar-media

A module to display currently playing media in your [Waybar](https://github.com/Alexays/Waybar).

Supports fetching data from the following media players:

* **Firefox, Google Chrome, Chromium** and other browsers  
  via [KDE Plasma Integration](https://community.kde.org/Plasma/Browser_Integration). You must follow their instructions for installing a browser extension and a native host. KDE Plasma itself is not required.
* **MPV**
* Potentially, any other player that supports [MPRIS](https://www.freedesktop.org/wiki/Specifications/mpris-spec/). Feel free to open an issue.

In the toolbar, the current title and artist are shown separated by a dash, like so: `Mountains - Hans Zimmer`.
Long titles/artists will be _ellipsized_ to 80 characters.

The tooltip displays more metadata, including the album and player name.


## Dependencies

* [pydbus](https://github.com/LEW21/pydbus) and its dependencies
* [psutil](https://psutil.readthedocs.io/en/latest/)

If you use Arch Linux, you may use the following packages: `python-pydbus python-psutil`


## Installation and configuration

Put `waybar-media.py` somewhere in your path, e.g. `~/.local/bin/`

Add to your Waybar configuration as a [custom module](https://github.com/Alexays/Waybar/wiki/Module:-Custom), like so:

```json
{
    "modules-center": ["custom/waybar-media"],
    "custom/waybar-media": {
        "return-type": "json",
        "exec": "waybar-media.py status",
        "on-click": "waybar-media.py playpause",
        "on-scroll-up": "waybar-media.py previous",
        "on-scroll-down": "waybar-media.py next",
        "escape": true
    }
}
```

As shown above, `waybar-media.py` always takes one argument. These are the available options:

* `status`: Print the status in [Waybar's JSON format](https://github.com/Alexays/Waybar/wiki/Module:-Custom#module-custom-config-return-type).
* `playpause`: Toggle the state of the current player.
* `previous`: Go to the previous song.
* `next`: Go to the next song.


## Styling

You may use the following classes to style the module:

* `playing`
* `paused`
* `stopped`

Here's an example:

```css
#custom-waybar-media.paused {
    color: grey;
}
```
