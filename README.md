# Pomodoro Bash

A pomodoro timer for people with UNIX command-line powers.

It includes:
* an ASCII dinosaur!
* an ASCII puppy!
* optional support for:
  * pop-up notifications
  * audio notifications (like the roar of a T-Rex and the bark of a puppy)
  * status icon in the notification area
  * changing your chat status (e.g., HipChat or Slack)

# Installation

## Via PPA

```
sudo add-apt-repository ppa:gabrielx/pomodoro-bash
sudo apt-get update
sudo apt-get install pomodoro-bash
```

## Manually

1. Clone or download this git repo
1. cd into the downloaded repo directory
1. Run `./build/bin/install .`.  Optionally pass the target directory as a second argument (e.g., `/usr/local`).


# Installing optional features

## Ubuntu and friends

To enable pop-up notifications, install this:
* `sudo apt install libnotify-bin`

To enable audio notifications, install one of these:
* `sudo apt install pulseaudio-utils`
* `sudo apt install sndfile-programs`
* or `mpg123` or `madplay`

To enable the status icon in the notification area, install this:
* https://github.com/fossfreedom/indicator-sysmonitor

## Windows with Cygwin

Install Cygwin: https://www.cygwin.com/

To enable pop-up notifications, install one of these:
* http://vaskovsky.net/notify-send/
* http://www.paralint.com/projects/notifu/index.html

To enable audio notifications, install one of these:
* http://www.videolan.org/vlc/
* madplay (available from https://www.cygwin.com/)

To enable the status icon in the notification area, install this:
* I don't know how.

To make a pretty shortcut in the Start Menu:
1. Create a shortcut with a target like one of these:
 * C:\cygwin\bin\mintty.exe -i C:\Users\Gabriel\config\local\share\pomodoro-bash\images\tomato13.ico --title "Pomodoro Bash" -o Scrollbar=None -o ScrollbackLines=0  -e C:\Users\Gabriel\bin\cygwin-bootstrap pomodoro-bash

## MacOS

Haven't tested recently on MacOS.  Audio notifications should work if `afplay` is installed.  Pop-up notifications should work if a current version of AppleScript is installed.  The status icon shouldn't work.
