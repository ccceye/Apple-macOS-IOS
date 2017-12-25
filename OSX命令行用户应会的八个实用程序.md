# Eight Terminal Utilities Every OS X Command Line User Should Know

The OS X Terminal opens up a world of powerful UNIX utilities and scripts. If you’re migrating from Linux, you’ll find many familiar commands work the way you expect. But power users often aren’t aware that OS X comes with a number of its own text-based utilities not found on any other operating system. Learning about these Mac-only programs can make you more productive on the command line and help you bridge the gap between UNIX and your Mac.

## 1. open

`open` opens files, directories and applications. Exciting, right? But it really does come in handy as a command-line double-click. For instance, typing:

`$ open /Applications/Safari.app/`

…will launch Safari as if you had double-clicked its icon in the Finder.

If you point `open` at a file instead, it will try to load the file with its associated GUI application. `open screenshot.png` on an image will open that image in Preview. You can set the `-a` flag to choose the app yourself, or `-e` to open the file for editing in TextEdit.

Running `open` on a directory will take you straight to that directory in a Finder window. This is especially useful for bringing up the current directory by typing `open .`

Remember that the integration between Finder and Terminal goes both ways – if you drag a file from Finder into a Terminal window, its full path gets pasted into the command line.

## 2. pbcopy and pbpaste

