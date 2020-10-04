# Building QtPass on Postmarket OS

Oddly enough the inner workings of this application deserve an introduction before everything else:

* [pass](https://password-store.com) - an epic password manager that uses the unix philosophy to store your secret stuff.
* GPG - a swiss army knife for encrypting literally anything.
* git - the backend behind github (this website). It keeps track of changes you make in code or anything else. Used with pass to sync your changes across computers

With all thse tools together, QTPass can be forged to drive everything into a gui for the end-user to enjoy.

## Limitations

N/A so far, check [linuxOnMobile's](https://linmob.net/2020/07/27/pinephone-daily-driver-challenge-part2-flatpak-and-scaling-in-phosh.html) page on scale-to-fit so your phone is happier showing everything.

# HEY YOU!

These instructions will probbaly need docker, check out [this page](./dockerSetup.md) for more information.

## Build

Done with docker setup? Let's go!

Install this stuff inside your container:

`apk add qt5-qtbase-dev qtchooser make g++ qt5-qttools-dev`

Grab the repository, this also should take you to the official documentation:

`git clone https://github.com/IJHack/QtPass.git`

Jump into that directory and run:

`qmake && make`

Like qTox, qtPass is a single executable with no other files to move around, so the only step left for the phone user is to change permissions and run.