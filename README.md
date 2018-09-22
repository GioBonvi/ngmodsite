# Ngmodsite

This is a quick Python script written to rapidly enable and disable virtual host
configurations in Nginx the same way `a2ensite` and `a2dissite` work for Apache
web server.

## Installation

You can simply download and copy the script in a folder which is in your
`$PATH`, no further steps are required (although you will need to have Python 3
installed to run it):

```shell
git clone https://github.com/GioBonvi/ngmodsite.git
sudo cp ./ngmodsite/ngmodsite /usr/local/bin/ngmodsite
```

## Usage

```console
$ ngmodsite
usage: ngmodsite [-h] (-l | -e | -d) [hostname]

A program to enable and disable virtual hosts configurations in Nginx.

positional arguments:
  hostname       The hostname on which to operate. If not set every hostname
                 is listed.

optional arguments:
  -h, --help     show this help message and exit
  -l, --list     List enabled and disabled configurations
  -e, --enable   Enable a configuration
  -d, --disable  Disable a configuration
```

## Limitations

This is just a quick script written for personal use, so you might find it has
some limitations: feel free to adapt it to your needs.

- It assumes that the virtual host configuration files reside in the
  `sites-available` folder inside the `/etc/nginx` folder and that active
  configurations are symlinked from there into the `sites-enabled` folder. The
  paths of these folders can, however be configured by editing the `NGINX_PATH`,
  `SITES_AVAIL_PATH` and `SITES_EN_PATH` variables.
- It assumes each configuration file in those folders only contains one virtual
  host and follows the following naming convention (based on the hostname):
  - inside `sites-available`:
    - hostname: `domain.com` - path: `domain.com.conf`
    - hostname: `sub.domain.com` - path: `domain.com/sub.conf`
    - hostname: `a.b.domain.com` - path: `domain.com/b/a.conf`
  - inside `sites-enabled`:
    - hostname: `domain.com` - path: `domain.com.conf`
    - hostname: `sub.domain.com` - path: `sub.domain.com.conf`
    - hostname: `a.b.domain.com` - path: `a.b.domain.com.conf`
- It does not try to detect if you have the right permissions to operate in the
  nginx folder: it simply fails when you try creating or deleting a symlink
  and asks to try again using `sudo`.
- It requires the `argparse` python library which is included with Python >= 2.7
  and >= 3.2 or can be installed via `pip install argparse`.

## License

`ngmodsite` is published under the [MIT license][License link].

## Credits

The name of the script comes from [this answer][ServerFault answer] by Ghassen
Telmoudi to [this ServerFault question][ServerFault question] which I found
while googling for a nginx equivalent to `a2ensite`.  
I used his script for a while, then decided to change it adapting it to my
personal requirements and while the script was completely rewritten (in fact I
even switched from Bash to Python) the name stayed the same.

[License link]: https://github.com/GioBonvi/ngmodsite.git
[ServerFault question]: https://serverfault.com/questions/424452/nginx-enable-site-command
[ServerFault answer]: https://serverfault.com/a/562210