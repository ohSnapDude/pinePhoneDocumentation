# Adventures with pinephone

Greetings! This is a git repository documenting the adventures being had with the pinephone.

Documentation will be sorted out by OS most likely. It's a work in progress as more stuff is being placed on the phone. Certain things are general enough that they won't be organized by this method and will probably be dumped into the "general" folder.

This repository might also apply to other linux phones as well, in fact probably all of it would work, just keep in mind I'm using a pinephone with the specs listed below.

## My phone specs

The pinephone is a postmarketOS community edition, containing 3GB memory, Allwinner64 CPU, 32GB storage with some micro SD cards coming in the mail late (thanks amazon >:) ).

*Update -* Amazon failed to deliver the packages in the first place so I bought the sd cards from the nearest office depot.

## Status of becoming a daily driver

Right now I do not have everything needed for my daily use yet. When that time comes the pinehone will replace this iPhone 6S. Current tasks are as follows:

* ~password manager~ - [compiled qtPass](./postmarketOs/qtpass.md)
* Music
    * m3u reader - I plan on making this myself
    * ~internet radio~ - firefox
* ~Video~ - firefox as well. I tried using kodi for this, and even went as far as setting up youtube playback. On the pinephone, performance was subpar compared to watching youtube over firefox so here I am :P One day though... the precious vlc will work on my phone somehow.
* ~tox~ [Compiled qTox](./postmarketOs/qtox.md)
* ~contacts~ - doing more studying on this. ~Might create a script that converts vcf to the sqlite3 database gnome-contacts is using.~ I heard from linuxOnMobile you can port contacts from the `evolution` email client; so I'll give that a try.
	* Done! I used evolution on my main pc to transfer contacts over from VCF format.
* ~weather~ - weather.gov & gnome-weather
* ~mail client~ - geary.
* ~totp~ (one time passcodes) - ~I already have a script that can be modified to use `zenity`~ There's something better out there [that qtPass & pass are compatible with](https://github.com/tadfisher/pass-otp): `pass-otp` (just install that package on apk) convert your keys to [This format](https://github.com/google/google-authenticator/wiki/Key-Uri-Format), then in qtPass, go to preferences -> settings -> "Use pass-otp extension". Then set your programs to the "Use pass" radio button. On the pinephone I also have auto-copy on so I don't need to use the terminal keyboard and simulate CTRL-C
* ~map~ - pure maps; Thanks mastodon for the suggestion! Installed this via flatpak.
* ~calendar~ - using gnome-calendar

Wow! That got completed quickly. All that's left is to get a new sim for the pinephone. I'm really enjoying the pinephone overall so far.

One of the things I want to do next is dig into QT and learn how to make native linux apps that are mobile-first. It feels like theres a ton of potential out there, so at least taking a small dip wouldn't hurt.

## Resources

I use allot of documentation, here is a growing list of places I'm reading

* [Postmarket OS Wiki](https://wiki.postmarketos.org/wiki/Main_Page)
* [LinuxOnMobile](https://linmob.net)
* [Fosstodon](https://fosstodon.org)
* [Docker Documentation](https://docs.docker.com/)

I myself am not a direct source and I probably don't have every answer (just getting into this myself!), so these resources can help you along your path as well :)
