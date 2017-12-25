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

## 4. screencapture

`screencapture` lets you take many different kinds of screenshots. It’s similar to `Grab.app` and the keyboard shortcuts `cmd + shift + 3` and `cmd + shift + 4`, except it’s far more flexible. Here are just a few different ways you can use screencapture:

Capture the contents of the screen, including the cursor, and attach the resulting image (named ‘image.png’) to a new Mail message:

`$ screencapture -C -M image.png`

Select a window using your mouse, then capture its contents without the window’s drop shadow and copy the image to the clipboard:

`$ screencapture -c -W`

Capture the screen after a delay of 10 seconds and then open the new image in `Preview`:

`$ screencapture -T 10 -P image.png`

Select a portion of the screen with your mouse, capture its contents, and save the image as a `pdf`:

`$ screencapture -s -t pdf image.pdf`

To see more options, type `screencapture --help`

## 5. launchctl

`launchctl` lets you interact with the OS X init script system, `launchd`. With launch daemons and launch agents, you can control the services that start up when you boot your computer. You can even set up scripts to run periodically or at timed intervals in the background, similar to cron jobs on Linux.

For example, if you’d like to have the Apache web server start automatically when you turn on your Mac, simply type:

`$ sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist`

Running `launchctl list` will show you what launch scripts are currently loaded. `sudo launchctl unload [path/to/script]` will stop and unload running scripts, and adding the `-w` flag will remove those scripts permanently from your boot sequence. I like to run this one on all the auto-update “helpers” created by Adobe apps and Microsoft Office.

Launchd scripts are stored in the folllowing locations:

```
~/Library/LaunchAgents    
/Library/LaunchAgents          
/Library/LaunchDaemons
/System/Library/LaunchAgents
/System/Library/LaunchDaemons
```

To see what goes into a launch agent or daemon, there’s a great blog post by Paul Annesley that walks you through the file format. And if you’d like to learn how to write your own `launchd` scripts, Apple provides some helpful documentation on their Developer site. There’s also the fantastic Lingon app if you’d prefer to avoid the command line entirely.



## 6. say

This is a fun one: `say` converts text to speech, using the same `TTS engine` OS X uses for `VoiceOver`. Without any options, say will simply speak whatever text you give it out loud.:

`$ say "Never trust a computer you can't lift."`

You can also use say to speak the contents of a text file with the `-f` flag, and you can store the resulting audio clip with the `-o` flag:

`$ say -f mynovel.txt -o myaudiobook.aiff`

The `say` command can be useful in place of console logging or alert sounds in scripts. For instance, you can set up an Automator or Hazel script to do batch file processing and then announce the task’s completion with `say`.

But the most enjoyable use for `say` is rather more sinister: if you have `ssh` access to a friend or coworker’s Mac, you can silently log into their machine and haunt them through the command line. Give ‘em a Siri-ous surprise.

You can set the voice (and language!) used by `say` by changing the default setting in the **Dictation & Speech** panel in System Preferences.


## 7. diskutil

`diskutil` is a command line interface to the **Disk Utility** app that comes with OS X. It can do everything its graphical cousin can, but it also has some extra capabilities—such as filling a disk with zeroes or random data. Simply type `diskutil list` to see the path names of disks and removable media attached to your machine, and then point the command at the volume you want to operate on. **Be careful: `diskutil` can permanently destroy data if it’s used incorrectly**.

