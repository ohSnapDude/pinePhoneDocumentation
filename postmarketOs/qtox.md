# Building Qtox on postmarket OS

Qtox is an awesome chat application that allows users to talk to eachother without the need for servers (Peer to Peer).
The application itself is not bundled inside the alpine linux repositories, so it will have to be built yourself for the time being.

## Limitations

* On the pinephone, webcams are detected, but not usable. I take it it's because the camera itself have a slightly different architechture than actual webacams. This is a problem also seen in cheese photo booth.
* You will need to use `scale-to-fit` to properly show the application in both landscape and portrait. Without it, the screen resolution combines portrait and landscape's biggest points. linuxOnMobile did a good segment on [one his articles describing this](https://linmob.net/2020/07/27/pinephone-daily-driver-challenge-part2-flatpak-and-scaling-in-phosh.html), as it applies to many applications besides Qt ones.

Besides these two, virtually everything else works. In my experimentation, a random side effect is that the sounds compiled in the your new app for some reason are sped up and are higher pitched. Hearing the ringtone this way though reveals where it comes from :)

# wait wait wait wait wait

Before moving on, everything here should be done through Docker. If you haven't set up docker yet, check [this page](./dockerSetup.md) out to make something quick & dirty.


## Ok now lets start:

Read the above? Ok time to start.

I traversed through the list of items on my container, and it looks like your going to need all this below, just run apk to install it all:

```bash
sudo apk add automake check cmake ffmpeg-dev g++ git libexif-dev libqrencode-dev libsodium-dev openal-soft-dev openssl-dev opus-dev qt5-qtsvg-dev toxcore-dev qt5-qttools-dev sqlcipher-dev make
```

This is a similar list of items found on the official [build instructions](https://github.com/qTox/qTox/blob/master/INSTALL.md#compile-qtox) for qtox, with some differences:

* we're using a pre-built version of toxcore instead of compiling it like in the original instructions
* the package names are obviously different because we're in alpine and not in another distro.
* some packages are here, others are not. This is everything that allowed it to finally compile.

For this step, go to your mounted volume inside the docker container. We want to reach this outside the environment when finished.

Next, clone the qtox repo:

`https://github.com/qTox/qTox.git`

Go inside the new folder and run this:

`cmake .`

Then this if you didn't run into errors (This part takes a while):

`make -j$(nproc)`

After that your done! Like the official docs say, you can use `./qtox` to launch the app (outside the container of course). This specific file can be moved anywhere you like in the filesystem of your pinephone.