# localtld

**localtld** allows software that rely on NSSwitch to resolve domains for local applications (like myapp.dev).


## Installation

Execute the following commands:

    $ git clone https://github.com/jweslley/localtld.git
    $ cd localtld
    $ make
    $ sudo make install

then edit `/etc/nsswitch.conf` file

    $ sudo vi /etc/nsswitch.conf

appending `localtld` to the end of the line containing `hosts:`. You'll get something like:

    hosts: files localtld dns

> Note: This line may vary depending on your distro, but remember: just append `localtld` or place `localtld` before `dns` (later is recommended to avoid slowness caused by DNS resolution).

Finally, restart your browser after editing `/etc/nsswitch.conf`.


## Test usage

Command line software like `host` and `dig` won't resolve the address, but `getent` will. Thus:

    $ getent hosts myapp.dev
    ::1             myapp.dev

    $ getent hosts acme.dev
    ::1             acme.dev


## Custom TLDs

By default, `localtld` will resolve all domains ending in `.dev` to localhost. Change this by exporting an environment variable named `LOCALTLD`. Example:

    export LOCALTLD=app


Also, you can resolve multiple domains to localhost by setting `LOCALTLD` a comma-separated list of top-level domains.

    export LOCALTLD=dev,app,local


## Credits

Code is from [prax](https://github.com/ysbaddaden/prax) by ysbaddaden and collaborators.
