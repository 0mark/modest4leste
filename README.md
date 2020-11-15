# modest4leste

This is the documentation for the ongoing project to port the mail client [Modest](https://github.com/lexborisov/Modest) to maemo leste. Modest is based on Tinymail (no link available, the projects page is gone).

## Tinymail

Depends on Gnomevfs2. Needs to be ported to Gvfs. With some slight modifications (as described [here](https://github.com/maemo-leste/bugtracker/issues/207)), Tinymail compiles on Ascii (which still had gnomevfs2), but not on Beowulf anymore.

This method disables the optional HTML renderer. Possible renderer are Webkit, Mozembed and GtkHtml. Modest only can be build with WebKit or GtkHtml. I guess (but do not know) that Tinymail has to be build with the same renderer.

My [fork](https://github.com/0mark/tinymail), which already has the patches mentioned above.

**Notes**
* There is a new branch, *nognomevfs*, in which i disabled libtinymail-gnomevfs. Now it compiles. But i guess this libtinymail-gnomevfs is important for Modest. This libtinymail-gnomevfs is a single 500 line file. Thus, with a bit of luck, porting to gvfs might not be too hard.

## Modest

Modest depends on either WebKitGtk or GtkHtml as a HTML renderer. There is no option to disable rendering completely. WebKitGtk is not maintained for many years and was known to have security issues. GtkHtml is also not maintained for years. 

I think a decent quick solutiuon would be to simply use GtkHtml. Yes, its unmaintained. But i think it poses not much of a threat, considering its low complexity and high obscurity. Not more than using an equaly unmaintained mail lib anyway. To do so, Modest has to be adopt GtkHtml 4, as it depends on 3.8, which uses deprecated GDK methods. Hopefully that would not be too hard. A copy of GtkHtml with all files to build a deb is in this repo.

A better, and not to hard, solution would be to either remove the html view or replace GtkHtml by either Dillo or a simple Textbox and a filter (like Elinks).

Like Tinymail, Modest depends on GnomeVfs2. And has to be ported to Gvfs too.

Also depends on libmodest-dbus-client. I could find some [tarballs](http://maemo.muarf.org/apt-mirror/mirror/repository.maemo.org/pool/maemo5.0/free/libm/libmodest-dbus-client/) of it, but not much more. It has no real license but a file which states that it comes from Nokia and can be distributed if some requierements are met. I am pretty sure i can include it in this repo (and i did so), but i think it should be rewritten. Its not that complicated i guess.

My [fork](https://github.com/0mark/modest). Right now, nothing there.
