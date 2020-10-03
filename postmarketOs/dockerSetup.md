# Docker setup

See "setting up docker" below if you know what docker is, the next couple of sections just describe docker at a power user level.

In some cases, docker might be needed to compile new code. I'd actually recommend it most of the time because with docker
you can cilo the packages you need away from postmarketOs itself. After your done with your build environment, you can even delete it for extra space later.

## Grab docker or else -_-

For context, below is what happens when you *don't* use it:

```
pine64-pinephone:~$ sudo apk add qt5-qttools-dev
[sudo] password for XXX: 
fetch http://postmarketos1.brixit.nl/postmarketos/v20.05/aarch64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.12/main/aarch64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.12/community/aarch64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/edge/testing/aarch64/APKINDEX.tar.gz
ERROR: unsatisfiable constraints:
  mesa-git-gbm-0_git20200323-r0:
    breaks: mesa-dev-20.0.7-r0[mesa-gbm=20.0.7-r0]
    satisfies: mesa-git-dri-gallium-0_git20200323-r0[mesa-git-gbm] cogl-1.22.8-r0[so:libgbm.so.1] mutter-3.36.6-r0[so:libgbm.so.1]
               qt5-qtbase-x11-5.14.2-r1[so:libgbm.so.1] mesa-git-egl-0_git20200323-r0[so:libgbm.so.1]
               xorg-server-xwayland-1.20.9-r1[so:libgbm.so.1] wlroots-0.10.1-r0[so:libgbm.so.1]
  mesa-git-glapi-0_git20200323-r0:
    breaks: mesa-dev-20.0.7-r0[mesa-glapi=20.0.7-r0]
    satisfies: mesa-git-dri-gallium-0_git20200323-r0[mesa-git-glapi] mesa-git-dri-gallium-0_git20200323-r0[so:libglapi.so.0]
               mesa-git-gl-0_git20200323-r0[so:libglapi.so.0] mesa-git-gles-0_git20200323-r0[so:libglapi.so.0]
               mesa-git-egl-0_git20200323-r0[so:libglapi.so.0] mesa-git-osmesa-0_git20200323-r0[so:libglapi.so.0]
  mesa-git-egl-0_git20200323-r0:
    breaks: mesa-dev-20.0.7-r0[mesa-egl=20.0.7-r0]
    satisfies: mesa-git-dri-gallium-0_git20200323-r0[mesa-git-egl] gst-plugins-base-1.16.2-r3[so:libEGL.so.1]
               qt5-qtwayland-5.14.2-r0[so:libEGL.so.1] qt5-qtmultimedia-5.14.2-r0[so:libEGL.so.1] cogl-1.22.8-r0[so:libEGL.so.1]
               gnome-session-3.36.0-r3[so:libEGL.so.1] mutter-3.36.6-r0[so:libEGL.so.1] qt5-qtbase-x11-5.14.2-r1[so:libEGL.so.1]
               webkit2gtk-2.28.4-r0[so:libEGL.so.1] libwpebackend-fdo-1.6.0-r1[so:libEGL.so.1] wlroots-0.10.1-r0[so:libEGL.so.1]
  mesa-git-gl-0_git20200323-r0:
    breaks: mesa-dev-20.0.7-r0[mesa-gl=20.0.7-r0]
    satisfies: mesa-git-dri-gallium-0_git20200323-r0[mesa-git-gl] charging-sdl-0.1-r1[mesa-gl] osk-sdl-0.57-r1[mesa-gl]
               gst-plugins-base-1.16.2-r3[so:libGL.so.1] gnome-session-3.36.0-r3[so:libGL.so.1] mutter-3.36.6-r0[so:libGL.so.1]
               xorg-server-xwayland-1.20.9-r1[so:libGL.so.1] webkit2gtk-2.28.4-r0[so:libGL.so.1]
  mesa-git-gles-0_git20200323-r0:
    breaks: mesa-dev-20.0.7-r0[mesa-gles=20.0.7-r0]
    satisfies: mesa-git-dri-gallium-0_git20200323-r0[mesa-git-gles] phoc-0.4.2-r0[so:libGLESv2.so.2] py3-qt5-5.14.2-r0[so:libGLESv2.so.2]
               gnome-shell-3.36.6-r0[so:libGLESv2.so.2] qt5-qtwayland-5.14.2-r0[so:libGLESv2.so.2]
               qt5-qtmultimedia-5.14.2-r0[so:libGLESv2.so.2] gnome-session-3.36.0-r3[so:libGLESv2.so.2]
               mutter-3.36.6-r0[so:libGLESv2.so.2] qt5-qtbase-x11-5.14.2-r1[so:libGLESv2.so.2] wlroots-0.10.1-r0[so:libGLESv2.so.2]
  mesa-git-osmesa-0_git20200323-r0:
    breaks: mesa-dev-20.0.7-r0[mesa-osmesa=20.0.7-r0]
  mesa-git-xatracker-0_git20200323-r0:
    breaks: mesa-dev-20.0.7-r0[mesa-xatracker=20.0.7-r0]
```

That whole cryptic mess basically means there are things your pinephone needs to live on in order to do basic functionality for some of your favorite applications. Therefore postmarket os is smart and prevents you from that specifc item it so we don't break anything. How in the blazes do we fix that?

## Meet docker

To fix the above issue you need a place separate from postmarketOs. This can be on the same device without the mess of partitioning, virtual machines, or assiging drivers. In a nutshell, docker containers help you setup mini spaces you can create, duplicate and throw away with no fuss. They act like a regular operating systems that cannot see the one running it. They also have super powers like sharing folders with postmarketOS so you can take your code to the actual phone when your finished compiling it.

## setting up docker

First install it via apk:

`sudo apk add docker`

Docker needs to run it's service before running it, so run this command whenever you need docker and you restarted your pinephone:

`rc-service docker start`

For our usage, alpine linux is probably the best choice. This is actually what postmarketOs is based on. The whole OS is only 5MB compared to many other big options! Run this command to grab alpine:

`sudo docker pull alpine`

This is not the container, rather it's an "image", a template to make your container. Containers can become images too, but that's beyond the scope of this walkthrough.

Before making the container, make a directory that will hold your builds, in this example it will be folder named "dockerBuilds"

`mkdir dockerBuilds`

We'll make the folder here because docker can share folders with you and other containers.

Let's create your first container. You will need to edit the command to make it work, so read about each parameter below to understand what's going on.

* `run` - We're creating a new container and running it at the same time
* `-it` - "Interactive terminal" for short, once we make the container, we log in immediately into the cli
* `--name` - The item after this (in my example below "build") is the name of the container. Make it something you can remember easily.
* `-v` - short for "volume", this helps you link a folder in your phone to one in the docker container. in the example below, I have it linked to the `dockerBuilds` folder made above. The colon `:` after that is where this folder will be linked in the container. In the example it's mounted to `/mnt`. You can use `-v` to link as many real-world folders as you like to places in your container
* `alpine` - our image we downloaded earlier!

All of that put together we'd get something similar to:

`sudo docker run -it --name build -v /home/yourUserNameHere/dockerBuilds:/mnt alpine`

Only yours should be different.

If done correctly, you should be inside the container! If you want to get out, use `ctrl-D` or the `exit` command.

## opening the container in the future

Now that it's setup, the process of opening it again and accessing it is a bit different.

Once again, remember to run this whenever your phone has restarted to use docker:
`rc-service docker start`

Start your container:

`sudo docker start build`

Then jump into the container's terminal:

`sudo docker attach build`

## One last thing:

In your docker container, you will need allot of packages that aren't in the regular package lists to compile new code in this guide. You can achive this by entering the follwing in the contianer:

`echo http://dl-cdn.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories`

This should hopefully have everything you need!