# matrix-consume

An automatic matrix image uploader.

`matrix-consume` uploads randomly selected images from a local folder to a specified Matrix room.
After an image is uploaded, it is moved to trash.
The script can wait for new images to be moved to the folder,
thus acting as a daemon.

By default, there's a 3 seconds timeout between uploads, but it can be changed.

## How to use

0) Install [requirements](requirements.txt) with `pacman`.
1) Download the [script](matrix-consume).
2) Create a [config file](config.example).
3) Run matrix-consume.

## Running

> To display a help screen, run `matrix-consume -h`.

To consume a folder and exit, run:

```
matrix-consume --config ~/.config/my-config
```

`matrix-consume` leaves a *lock* file in the folder
to ensure there's only one instance of the script working in it.
Don't delete it manually.

## Autostart

You can add matrix-consume to autostart (e.g., to `~/.xprofile`).
In the example below, the script waits for new files to be moved to the folder
and uploads them to the Matrix room.
After each uploaded image the scripts sleeps for `10` seconds.

```
{ matrix-consume --config ~/.config/my-config --timeout 10 --watch 2>&1 | logger; } &
```
