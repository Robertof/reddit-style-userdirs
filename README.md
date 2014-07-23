reddit style userdirs
=====================
Introduction
-----

This patch allows Apache to process userdirs prefixed with `/u/`, just like reddit.

Two patches are available. One works with Arch Linux's PKGBUILD, the second one is the actual patch (which is applied to Apache's source tree).

The patch works with Apache 2.4.10 (should work with >= 2.4), and with the first revision of Arch Linux's Apache 2.4.10 PKGBUILD.

Instructions
------------
### Arch Linux

With Arch Linux, it's really easy to apply this patch. First, [update/install ABS](https://wiki.archlinux.org/index.php/ABS#Why_would_I_want_to_use_ABS.3F). Then, run the following commands:

```sh
# clone this repository in a directory, get in it
cp -R /var/abs/extra/apache/* . # copy apache buildfiles
patch -Np0 -i PKGBUILD.patch # patch our PKGBUILD
makepkg -c # compile Apache (may require a long time)
pacman -U apache-*.tar.xz # install Apache
systemctl restart httpd # restart Apache
```

### Every other Linux distribution

[Download Apache's source code](http://httpd.apache.org/download.cgi), extract it, get in the source directory and run:

```sh
patch -Np0 -i "/path/to/mod_userdir.patch"
```

If you downloaded the right version of Apache and you are in the correct directory, the patch is now applied and you can build Apache as explained in the [official documentation](http://httpd.apache.org/docs/2.4/install.html).

License
-------

Since this is a really small patch there's no need to put a license on it. So yeah, public domain!
