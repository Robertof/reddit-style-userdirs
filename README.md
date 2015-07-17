reddit style userdirs
=====================
Introduction
-----

This patch allows Apache to process userdirs prefixed with `/u/`, just like reddit.

Two patches are available. One works with Arch Linux's PKGBUILD, the second one is the actual patch (which is applied to Apache's source tree).

The patch works with Apache 2.4.16 (should work with >= 2.4), and with apache 2.4.16-1 from the Arch Build System.

Instructions
------------
### Arch Linux

With Arch Linux, it's really easy to apply this patch. First, [update/install ABS](https://wiki.archlinux.org/index.php/ABS#Why_would_I_want_to_use_ABS.3F). Then, run the following commands:

```sh
# clone this repository in a directory, get in it
cp -R /var/abs/extra/apache/* . # copy apache buildfiles
patch -Np0 -i PKGBUILD.patch # patch the PKGBUILD
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

Configuring
-----------

There's no configuration. Think of the `/u/$USER` as an alias of `/~$USER`. Each specific option of userdirs will be applied to reddit-style URLs.

Troubleshooting
---------------

### The patch is not working! You liar!

Are you *really* sure you are applying the patch to the *exact* Apache version specified in this file? If you need the patch for an older version, please see the commit history.

If you are 100% sure, then open an issue, I'll look into it.

### I'm using Arch Linux, and makepkg complains about GPG signatures.

This is an issue since the latest versions of Apache's PKGBUILD. The source code of Apache is downloaded directly from its website, and thus it is signed by the Apache maintainer. ([check here the name and keys of the maintainers](http://httpd.apache.org/download.cgi#verify))

To fix it, you may either disable the signature checking of makepkg (using `makepkg --skippgpcheck`) or import the maintainer's key. Here's [how to do it](https://wiki.archlinux.org/index.php/Makepkg#Signature_checking).

License
-------

Public domain.
