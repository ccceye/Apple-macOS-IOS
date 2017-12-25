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

These two commands let you copy and paste text from the command line. Of course, you could also just use your mouse—but the real power of `pbcopy` and `pbpaste` comes from the fact that they’re UNIX commands, and that means they benefit from piping, redirection, and the ability to be in scripts in conjunction with other commands. Typing:

`$ ls ~ | pbcopy`

…will copy a list of files in your home directory to the OS X clipboard. You can easily capture the contents of a file:

`$ pbcopy < blogpost.txt`

..or do something crazier. This hacked-up script will grab the link of the latest Google doodle and copy it to your clipboard.
```
$ curl http://www.google.com/doodles#oodles/archive | grep -A5 'latest-doodle on' | grep 'img src' | sed s/.*'<img src="\/\/'/''/ | sed s/'" alt=".*'/''/ | pbcopy
```
Using `pbcopy` with pipes is a great way to capture the output of a command without having to scroll up and carefully select it. This makes it easy to share diagnostic information. `pbcopy` and `pbpaste` can also be used to automate or speed up certain kinds of tasks. For instance, if you want to save email subject lines to a task list, you could copy the subjects from Mail.app and run:

`$ pbpaste >> tasklist.txt`


## 3. mdfind

Many a Linux power user has tried to use locate to search for files on a Mac and then quickly discovered that it didn’t work. There’s always the venerable UNIX find command, but OS X comes with its own killer search tool: Spotlight. So why not tap into its power from the command line?

That’s exactly what `mdfind` does. Anything `Spotlight` can find, `mdfind` can find too. That includes the ability to search inside files and metadata.

`mdfind` comes with a few conveniences that make it stand out from its big blue brother. For instance, the `-onlyin` flag can restrict the search to a single directory:

`$ mdfind -onlyin ~/Documents essay`

The mdfind database should stay up to date in the background, but you can also troubleshoot it (as well as Spotlight) using `mdutil`. If Spotlight isn’t working the way it should, `mdutil -E` will erase the index and rebuild it from scratch. You can also turn off indexing entirely with `mdutil -i off`.


