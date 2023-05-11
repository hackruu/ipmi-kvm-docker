## ipmi-kvm-docker

(forked from solarkennedy/ipmi-kvm-docker)

Ever wanted to access and IPMI KVM console, only to find that you don't
have network access or the right version of java or a compatible
browser or credentials?

This container runs:

* Xvfb - X11 in a virtual framebuffer
* x11vnc - A VNC server that scrapes the above X11 server
* [noNVC](https://kanaka.github.io/noVNC/) - A HTML5 canvas vnc viewer
* Fluxbox - a small window manager
* Firefox - For browsing IPMI consoles
* Java-plugin - Because... you need java to access most IPMI KVM Consoles.

## Build It
    # change to cloned directory
    bash build_arm64.sh # for arm arch(apple m1 etc)
    # OR
    bash build_amd64.sh # for amd64 arch

## Run It
    # run built docker image
    bash run.sh
    # Now on your laptop
    xdg-open http://admin:8080
    # On a mac
    open http://admin:8080
    # Or just open in a browser

In your web browser you should see the firefox, ready to connect to
and IPMI KVM:

### Custom resolution

By default, the VNC session will run with a resolution of 1024x768 (with 24-bit color depth).
Custom resolutions can be specified with the docker environment variable RES, and must include color depth.

    $ docker run -p 8080:8080 -e RES=1600x900x24 ipmi-kvm-docker

### Mount volume

In case you need to mount floppy/iso images to the machine you can mount a volume to the container.

    $ docker run -p 8080:8080 -v /your/local/folder:/root/images ipmi-kvm-docker
