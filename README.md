thunner
=======

A curses Google Play Music client

'thunner' - thunder (Doric Scots)

Requirements
------------

* Python 2
* [Simon Weber's Unofficial Google Music API][weber]
* [mpv](http://mpv.io/)
* Some songs on Google Play Music
* One or more internets
* A colour terminal

Usage
-----

Chmod `thunner` and add to your path. Make sure you have a `~/.thunnerrc` file; see below for configuration.

Keys
----

* Arrow keys : menu navigation
* enter : play (plays whatever is under the cursor, be that a song/album/artist or higher level menu item, but also queues the rest of the items in the current menu playing down the list and looping round to the top)
* ] : play (plays only the item under the cursor, be that a song/album/artist or higher level menu item.
* . : next
* , : previous
* spacebar : pause
* q : quit

Configuration
-------------

Configuration of thunner is via `~/.thunnerrc`. An example file is as follows:

        email <your e-mail address here>
        pass <your password here>
        deviceid 1234567890123456
        color myhighlight black yellow
        color mynormal white black
        assign myhighlight current-item
        assign mynormal text

`email` is required.
`pass` is not required, although if it is omitted, you will be prompted for your password on each startup. Spaces are allowed in `pass`.
Any number of `color` and `assign` lines are allowed.

An "app password" can be used to avoid storing your Google password in plaintext, this is strongly recommended. These can be obtained [here](https://security.google.com/settings/security/apppasswords). App passwords are also the only way to use thunner if you have 2-factor auth set up.

`deviceid` is a mobile device ID. This 16-digit hexadecimal string can be found by dialing `*#*#8255#*#*` or downloading [this DeviceID app](https://play.google.com/store/apps/details?id=com.evozi.deviceid) from the Google Play Store. If `deviceid` is omitted, the ID of one of your already-registered mobile devices will be selected.

`color` takes three arguements: a name (which the user chooses), a foreground colour and a background colour. Foreground and background colours can be of the following values:

* `default`
* `black`
* `red`
* `green`
* `yellow`
* `blue`
* `magenta`
* `cyan`
* `white`

`default` picks up the foreground/background colours of the terminal. I believe `black` to `white` are colours 0-7 as per your X resources (e.g. `*color0: #575757`).

`assign` takes two arguements a named colour pair (as defined via `color`) and a destination. The following destinations are defined:

* `thunner` - the colour of "thunner" (top left)
* `header-text` - colour of text in the header (location in menu tree)
* `header-sep` - colour of separators between header text
* `header-border` - colour of border below header
* `footer-border` - colour of border above footer
* `footer-sep` - colour of separators between footer text
* `status` - colour of status (playing/paused/stopped)
* `current-artist` - colour of currently playing artist in footer
* `current-song` - colour of currently playing song in footer
* `current-item` - colour of highlighted row in menu
* `text` - other rows in menu

Where the above are not defined in `~/.thunnerrc` they default to `default` which in turn is defined as:

      color default default default

For consitency's sake I've spelt "colour" as "color" in the code.

thunner also checks for `~/.thunnerlogo` on start-up and will show the contents of said file whilst connecting.

To Do
-----

* Add a random mode
* Add the ability to define new playlists
* Fix compilations under "Artists"
* Check compatibility with other OSes
* Add more customisations
* Add RGB definition to configuration file for terminals that support `init_color`
* Hide lag from API calls
* Add search mode

Known Issues
------------

* Compilations aren't currently handled well; Going to "Albums" will show n copies of an compilation album where n is the number of different artists on the album.
* API calls can be slow causing lag between input and playback. Avoid switching songs too quickly (with 'next', 'previous', etc.)

[weber]: https://github.com/simon-weber/Unofficial-Google-Music-API "Simon Weber's Unofficial Google Music API"
