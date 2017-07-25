# Pomodoro Bash

A pomodoro timer for people with UNIX command-line powers.

It includes:
* an ASCII dinosaur!
* an ASCII puppy!
* optional support for:
  * pop-up notifications
  * audio notifications (like the roar of a T-Rex and the bark of a puppy)
  * status icon in the notification area with the number of minutes left
  * changing your chat status (e.g., HipChat or Slack)

# Running

On the command line:
```
$ pomodoro-bash
```

Or search for "pomodoro" in Unity/GNOME launcher.

# Installation

## Via PPA

```
sudo add-apt-repository ppa:gabrielx/pomodoro-bash
sudo apt-get update
sudo apt-get install pomodoro-bash
```

## Manually

1. If running Windows, then install Cygwin. https://www.cygwin.com/
1. Clone or download this git repo. https://github.com/gabrielmdeal/pomodoro-bash/archive/master.zip
1. cd into the downloaded repo directory
1. Run `./build/bin/install $PWD`  Optionally pass the target directory as a second argument (e.g., ` ./build/bin/install $PWD /usr/local`).

# Installing optional features

## Ubuntu

To enable pop-up notifications, install this:
* `sudo apt install libnotify-bin`

To enable audio notifications, install *one* of these:
* `sudo apt install pulseaudio-utils`
* `sudo apt install sndfile-programs`
* or `mpg123` or `madplay`

To enable the status icon in the notification area, install this:
* https://github.com/fossfreedom/indicator-sysmonitor

To enable auto minimizing and activating of the pomo window (-m option), install this:
* `sudo apt install xdotool wmctrl`

## Windows with Cygwin

To enable pop-up notifications, install one of these:
* http://vaskovsky.net/notify-send/
* http://www.paralint.com/projects/notifu/index.html

To enable audio notifications, install one of these:
* http://www.videolan.org/vlc/
* madplay (available from https://www.cygwin.com/)

To enable the status icon in the notification area, install this:
* I haven't figured out an easy way to support this.

To enable auto minimizing and activating of the pomo window (-m option), install this:
* https://github.com/gabrielmdeal/window-control

The command for a Start Menu shortcut:
* C:\cygwin\bin\mintty -C /usr/share/pomodoro-bash/config/pomodoro-bash.minttyrc -e /usr/bin/bash -il pomodoro-bash

## MacOS

Haven't tested recently on MacOS.  Audio notifications should work if `afplay` is installed.  Pop-up notifications should work if a current version of AppleScript is installed.  The status icon shouldn't work.
