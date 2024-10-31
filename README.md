clipnotify is a simple program that, using the
[XFIXES](https://cgit.freedesktop.org/xorg/proto/fixesproto/plain/fixesproto.txt)
extension to X11, waits until a new selection is available and then exits.

It was primarily designed for [clipmenu](https://github.com/cdown/clipmenu), to
avoid polling for new selections.

Here's how it's intended to be used:

    while read; do
        [an event happened, do something with the selection]
    done < <(clipnotify -l)

Or:

    while clipnotify; do
        [an event happened, do something with the selection]
    done

clipnotify doesn't try to print anything about the contents of the selection,
it just exits when it changes. This is intentional -- X11's selection API is
verging on the insane, and there are plenty of others who have already lost
their sanity to bring us xclip/xsel/etc. Use one of those tools to complement
clipnotify.

You can choose a particular selection with `-s`, and loop instead of exiting
with `-l`. See `clipmenu -h` for more information.

# Building instructions

Building clipnotify from source has a dependency on a file called `X11/extensions/Xfixes.h`.
If you are on a Linux OS which uses `apt`, you can find which package contains this file using:

```sh
sudo apt-get install apt-file
sudo apt-file update
apt-file search X11/extensions/Xfixes.h
```
which (at the time of writing) will return:
> libxfixes-dev

so to successfully compile clipnotify by running `make` you will need to do this first:
```sh
sudo apt-get install libxfixes-dev
```
