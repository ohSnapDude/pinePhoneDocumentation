# Installing applications manually (and how to add an app icon)

This set of instructions applies to pretty much any version of linux with `bash` or `ash`.

After building an application from scratch, it's natrual to need a desktop icon to launch your precious new gem. Since all desktop files do is launch an executable, you can also use these instructions to build our own shortcuts that don't even directly link to applications themselves, such as a shell script that launches three firefox tabs at once.

## Start!

...sortof. You need an application to link first. This will depend on what you're installing. This document will just focus on a single binary file being placed in a local folder

If you need examples to go off of, I'll be pulling some examples from a couple of previous builds - [qtPass](../postmarketOs/qtpass.md) and [qTox](../postmarketOs/qtox.md).

If jumped from one of those or another page from this repo talking about building something, you will probably need to set the permissions of the app to yourself so you can move it around. You can do this by running:

`sudo chown user ./path/to/Executable`

for qtPass, you can find the executable after it's compiled in the root folder -> main

*From here on out, login to the user that will see these desktop shortcuts to run the rest of the instructions. In my case with postmarketOs, that user is `user`* If you are on an ssh session, this is easily done by running

`sudo su yourUsernameHere`

Many linux distributions have support for using ~/.local/ as a place to install local executables. On alpine linux you will need to do some extra items before starting:

1. create the directory: `~/.local/bin`
1. run this: `echo "export PATH=$PATH:~/.local/bin" >> ~user/.profile`
    * if you're running bash instead change `~/.profile` to `~/.bashrc`

After this, just copy the executable into `.local/bin`:

`cp /path/to/yourExcutable ~/.local/bin`

From here if you restarted your terminal and logged into the target user, the application should be launchable by command!

## The `.desktop` file

Here's the fun part! Many applications may already have this file, like qTox that has this right in it's root folder, a.k.a: `io.github.qtox.qTox.desktop`. qtPass also has one: `qtpass.desktop`. Other applications may have it but not neccessarily in the root folder, so you can go on a hunt for it *or make one yourself* (see below)

For the .desktop file, it would just be copied over to `~/.local/share/applications`. After this all you have to do is edit the file to point to your new executable and give it an icon.

Below is a sample configuration:

```
[Desktop Entry]
Type=Application
Name=My awesome app name
Version=1.0
GenericName=whatIsThisAppInANutshell
Comment=How would you describe this app in one short sentence?
Exec=/path/to/my/app
Icon=/path/to/my/catIcon.png
Terminal=false
Categories=sampleCategory;Stuff
Keywords=words;the;gui;will;use;in;search;boxes
```

If you are making an app from scratch, you can use the template above to start from somewhere. You don't need to include everything for it to work. A way more in-depth article regarding this is from the [guys at gnome](https://developer.gnome.org/integration-guide/stable/desktop-files.html.en)

If you're importing an existing desktop file from some source code that you compiled, you will need to change two things specifcally:

* the executable path (`Exec`)
* the icon path (`Icon`)

For the executable, that's easy! It's the path to the binary you placed in `.local/bin` or anywhere else you might've placed it. You should know where this is so I'll leave you to it.

The icon is a little different. I can tell you where the icons are for qtPass and qTox, but anything else you will need to find in the source code or you can make it yourself (fun!)

Each path starts at the root folder of the repo:

* qtPass: `artwork/icon.svg` or any of the others. Lover of vector so I chose this
* qTox: `img/icons/qtox.svg`

I wouldn't suggest directly linking these though, instead copy the image you want into your home directory into a folder you remember. I personally created a new directory: `~/.local/share/custIcons`

After this just replace the path for the icon and `phosh` will automatically update the home screen.

## Troubleshooting

* If your application is inside `/home/user/.local/bin` or was added to a directory that `$PATH` looks at, you don't need to hard link the app. for example my config just has `qtox` instead of `/home/user/.local/bin/qtox`. Otherwise, you need to hard-link the path just like the example on the end of the previous sentence.
* For both images and excutables, the tilde `~` or any directory shortcuts is not supported, therefore like the previous point mentioned, these need to be hard-linked.
* Remember to give yourself proper ownership and permissions for the desktop file to be editable. (see top of this page for example usage of `chown`)