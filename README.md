# build-asuswrt-merlin

Helper scripts to build [RMerl/asuswrt-merlin](https://github.com/RMerl/asuswrt-merlin) without much extra typing.

* Backlink to [Compile firmware from source using Ubuntu](https://github.com/RMerl/asuswrt-merlin/wiki/Compile-Firmware-from-source-using-Ubuntu).

## Summary

Last tested on `master` from RMerl/asuswrt-merlin as of 2015-01-25. The script takes care of the steps mentioned above for Ubuntu 13.10 and newer. In addition it does fixups to the source tree which ensure that it can run without superuser rights as long as the user makes sure all the packages are installed. It will also check for the packages being installed and bail out with a meaningful error message if not.

It can be run in two modes: with or without `sudo` involved. With `sudo` it will use the symbolic link method inside `/opt`, whereas without it will modify the files in the source tree to adjust hardcoded paths.

If you are running inside a [`tmux`](http://tmux.sourceforge.net/) pane, this will also pipe the output into a log file.

## Syntax

* Unprivileged: `./ubuntu-build-image <router-model> [path-to-asuswrt-merlin]`
* With `sudo`: `USE_SUDO=1 ./ubuntu-build-image <router-model> [path-to-asuswrt-merlin]`

You can leave out the `path-to-asuswrt-merlin` argument and the script will check the folder it resides in for a marker file (`README-merlin.txt`) to see whether this is the expected source tree.

Any non-empty value for `USE_SUDO` can be used and you can of course also export it up front, instead of prepending it to the command line.

### Special syntax for prerequisites

In order to have the script install all the prerequisites using `apt-get`, use the following method:

* `./ubuntu-build-image --prereq` (or `-P`)

Please note that this requires you to be a sudoer. Usually that means you need to be a member of the group `sudo` on `.deb`-based distros or `wheel` on `.rpm`-based distros.

## Usage on Ubuntu

### Preparation

* Verify you have `git` installed, otherwise do `sudo apt-get --no-install-recommends install git git-man`.
* Change into a folder inside of which you'd like the repository to reside (e.g. `~`).
* Clone the RMerl/asuswrt-merlin source:
  * via SSH: `git clone git@github.com:RMerl/asuswrt-merlin.git`
  * via HTTPS: `git clone https://github.com/RMerl/asuswrt-merlin.git`
* Clone this repository or download the raw `ubuntu-build-image` script:
  * via SSH: `git@github.com:assarbad/build-asuswrt-merlin.git`
  * via HTTPS: `https://github.com/assarbad/build-asuswrt-merlin.git`
  * Download `wget https://raw.githubusercontent.com/assarbad/build-asuswrt-merlin/master/ubuntu-build-image && chmod +x ubuntu-build-image`
* Copy `ubuntu-build-image` into the clone of RMerl/asuswrt-merlin (e.g. `~/asuswrt-merlin`).
* Change into the RMerl/asuswrt-merlin directory (e.g. `~/asuswrt-merlin`) and invoke `./ubuntu-build-image --prereq` there.
  * This will prompt you to execute a `sudo` command to install all prerequisites. This command does not check before whether some packages are missing, though. Remember that this requires you to be a sudoer!

### Building an image

Well, the syntax has been explained above. Running the script is as easy as invoking (from our previous example):

    ~/asuswrt-merlin/ubuntu-build-image RT-N66U

The name of the router is case-insensitive. Also, it handles the models with their U, R, and W prefixes.

At this point you'll probably want to take a break and come back later. This will take quite a while.

### Starting over

* Change into the clone directory
* You'll want to issue a `git reset --hard` inside the cloned repository to undo all the changes `ubuntu-build-image` does
* And then start over after the preparation steps above

## Contribute

Please contribute by reporting issues and sending pull requests.

Oh and feel free to fork or embed this into your repository.

## License

This work is released into the public domain. See LICENSE. If _public domain_ is not a recognized legal concept in your jurisdiction, treat as [CC0](https://creativecommons.org/publicdomain/zero/1.0/); which should have the proper wording for many jurisdictions. The disclaimer from `LICENSE` (second to last paragraph) still applies.

If neither of these suite your needs, please ask by opening a ticket.
