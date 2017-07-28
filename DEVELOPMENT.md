# Building the Debian package

https://www.debian.org/doc/manuals/maint-guide/update.en.html

```
APP=pomodoro-bash
SOURCE_VERSION=NN.NN.NN
DIR=${APP}/${APP}-$SOURCE_VERSION

sudo apt-get install build-essential debhelper
mkdir -p $DIR
git clone git@github.com:gabrielmdeal/pomodoro-bash.git $DIR

cd $APP
tar zcvf ${APP}_$SOURCE_VERSION.orig.tar.gz ${APP}-$SOURCE_VERSION --exclude-vcs --exclude=debian --exclude='*~' --exclude=".*#"

cd ${APP}-$SOURCE_VERSION

package_version="0gabrielxppa1"
dch -v "$SOURCE_VERSION-$package_version"
dch -r --no-force-save-on-release
git commit -m "Debian change log entry for v$SOURCE_VERSION" debian/changelog && git push
git tag -a "v$SOURCE_VERSION" -m "New version v$SOURCE_VERSION" && git push origin --tags

debuild clean && debuild -us -uc && lintian -EvIL +pedantic && sudo apt-get remove -y pomodoro-bash && sudo dpkg -i ../pomodoro-bash_$SOURCE_VERSION-${package_version}_all.deb && /usr/bin/pomodoro-bash
rm ../pomodoro-bash_${SOURCE_VERSION}-${package_version}* && debuild clean && debuild -S && lintian -EvIL +pedantic --no-tag-display-limit

# Use 'dput -f' if the first try fails.
dput ppa:gabrielx/${APP} ../${APP}_${SOURCE_VERSION}-${package_version}_source.changes
debuild clean

```

Finally, copy the packge to other distributions: https://launchpad.net/~gabrielx/+archive/ubuntu/pomodoro-bash/+copy-packages

# QA

* `for n in dash bash posh ; do POSIXLY_CORRECT=1 dash bin/pomodoro-bash -p -w 5 -b 5; done`
* https://github.com/koalaman/shellcheck
* `checkbashisms --force --posix bin/pomodoro-bash`
* `desktop-file-validate src/share/doc/applications/*.desktop`
* `lintian -EvIL +pedantic`

# Converting to ico

`convert -density 384 -background transparent circle-question.svg -define icon:auto-resize -colors 256 circle-question.ico`

# Debugging

Under bash and *in a file*:
```
dump_stack() {
  local frame=0
  while caller $frame; do
      frame=$((frame + 1));
  done
}
```

# To do

* Get it working under Windows Subsystem for Linux: https://msdn.microsoft.com/commandline/wsl/about
  * The timeout set via `stty` has no effect on `dd`, so `dd` blocks until it gets keyboard input.
  * Even if I fix this, the pop-up notifications won't work since it is essentially running in a VM.  Audio probably won't work either.
* Use https://github.com/matryer/bitbar to display status in the MacOS status menu.
* Windows taskbar notification
  * Shell_NotifyIcon(): https://www.codeproject.com/kb/shell/stealthdialog.aspx
  * http://www.mingw.org/
* https://github.com/julienXX/terminal-notifier
  * `terminal-notifier -message xx -title xx -subtitle xx`
* `sudo apt-get install python-notify2`
  * `if python -m notify2`
  * `  POMO_NOTIFICATION_COMMAND='python -c \"import notify2; notify2.init('psh'); m = notify2.Notification('pomodoro-bash', '%s'); m.show();\""`

