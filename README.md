Note, that…
-----------
This is a fork of the original APW widget by mokasin (now unmaintained), ported to work with 4.0.

It contains some fixes from the actionless fork and some of my own.

It has a lot of bugs....

Awesome Pulseaudio Widget
=========================

Awesome Pulseaudio Widget (APW) is a little widget for
[Awesome WM](http://awesome.naquadah.org/), using the awful progressbar widget,
to display default's sink volume and control Pulseaudio.

It's compatible with Awesome 4.0.  Well, kind of.  At least, moreso than the original.


Get it
------

```sh
cd $XDG_CONFIG_HOME/awesome/
git clone https://github.com/mokasin/apw.git
```

Use it
------

For some reason, you need to put APW inside a container or it'll eat a big chunk out of your wibar and cover other widgets.
This needs to be fixed.  Until then, place it inside a container, like so:

```lua
-- Load the widget.
local APW = require("apw/widget")

-- Put it in a container
local apw_container = wibox.container.background(APW)
apw_container.forced_width = 40

-- Example: Add to wibox. Here to the right. Do it the way you like it.
right_layout:add(apw_container)

-- Configure the hotkeys.
awful.key({ }, "XF86AudioRaiseVolume",  APW.Up),
awful.key({ }, "XF86AudioLowerVolume",  APW.Down),
awful.key({ }, "XF86AudioMute",         APW.ToggleMute),

```

Customize it
------------

### Theme

*Important:* `beautiful.init` must be called before you `require` apw for
theming to work.

Just add these variables to your Beautiful theme.lua file and set them
to whatever colors or gradients you wish:

```lua
--{{{ APW
theme.apw_fg_color = {type = 'linear', from = {0, 0}, to={40,0},
    stops={{0, "#CC8888"}, {.4, "#88CC88"}, {.8, "#8888CC"}}}
theme.apw_bg_color = "#333333"
theme.apw_mute_fg_color = "#CC9393"
theme.apw_mute_bg_color = "#663333"
--}}}

```

### Directly edit widget.lua

You also can customize some properties by editing the configuration variables
directly in `widget.lua` (i.e. add a margin).
It is advisable to customize the source file in an own branch. This makes it
easy to update to a new version of APW via rebasing.

Mixer
----

Right-clicking the widget launches a mixer.  By default this is `pavucontrol`,
but you can set a different command by calling SetMixer() on your APW object:

```lua
local APW = require("apw/widget")
APW:SetMixer("mixer_command -whatever")
```

### Tip
You could update the widget periodically if you'd like. In case, the volume is
changed from somewhere else.

```lua
APWTimer = timer({ timeout = 0.5 }) -- set update interval in s
APWTimer:connect_signal("timeout", APW.Update)
APWTimer:start()
```

Contributing
------------
Just fork it and file a pull request. I'll look into it.
