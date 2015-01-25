# build-asuswrt-merlin

Helper scripts to build RMerl/asuswrt-merlin without much extra typing.

## Summary

Last tested on `master` as of 2015-01-25. The script takes care of the steps mentioned above for Ubuntu 13.10 and newer. In addition it does fixups to the source tree which ensure that it can run without superuser rights as long as the user makes has all the packages installed. It will also check for the packages being installed and bail out with a meaningful error message if not.

It can be run in two modes: with or without `sudo` involved. With `sudo` it will use the symbolic link method inside `/opt`, whereas without it will modify the files in the source tree to adjust hardcoded paths.

If you are running inside a [`tmux`](http://tmux.sourceforge.net/) pane, this will also pipe the output into a log file.

## Syntax

* Unprivileged: `./ubuntu-build-image <router-model> [path-to-asuswrt-merlin]`
* With `sudo`: `USE_SUDO=1 ./ubuntu-build-image <router-model> [path-to-asuswrt-merlin]`

You can leave out the `path-to-asuswrt-merlin` argument and the script will check the folder it resides in for a marker file (`README-merlin.txt`) to see whether this is the expected source tree.

Any non-empty value for `USE_SUDO` can be used and you can of course also export it up front, instead of prepending it to the command line.

## Contribute

Please contribute by reporting issues and sending pull requests.

Oh and feel free to fork or embed this into your repository.

## License

This work is released into the public domain. See LICENSE. If public domain is not an acknowledged legal concept in your country, treat as CC0.

If neither of these suite your needs, please ask by opening a ticket.
