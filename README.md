cbfix
=====

This is a simple script intended to fix a problem that sometimes occurs
in cbr and cbz files.  The problem is that filenames which represent two-page
pages in the comic are sometimes labeled as, eg, "Comic Name v3 02-0405.jpg"
(for an image representing pages 04 and 05 in issue 2). Some CBR/CBZ readers,
including the one I use, sort the filenames numerically rather than
alphabetically*, so all of the two-page images wind up at the end.

All this script does is to open all cbr/cbz files underneath a given
directory, check for filenames in the format "0405.jpg", and rename them
to, for instance, "Comic Name v3 02-04-05.jpg".

(*) Or maybe it's OS/X doing this, I don't know.

Dependencies
------------
This project uses [rarfile](https://github.com/markokr/rarfile/) to
parse CBR files. It needs a `rar` executable somewhere on the PATH
in order to re-create CBR files (but it should eventually be able to
convert from CBR to CBZ files). If you need a rar executable, try the
[official version from rarlabs](http://www.rarlab.com/download.htm).

You'll need to `pip install rarfile` to get the CBR stuff working.

Portability
-----------
I've only tested this on OS/X. No reason it shouldn't work on Linux,
or even Windows, but some tweaking might be necessary.

Also you'll need Python 2.7.

TODO
----
Here's a list of stuff that's still unfinished:

* Check for rarfile module / rar executable, disable CBR if it isn't present
* Test CBZ file extraction and compression
* Conversion from CBR to CBZ and vice-versa (probably requires mild refactoring)
* Split out rar file `register_archive_format()` bit and put it up on PyPI
* Nuke out Thumbs.db, .DS_Store and other irritants
* It wouldn't be hard to plug in metadata generation here either

Bugs
----

I have a few archives similar to this:

    $ rar lb Comeek-comic-name.cbr
    Comeek 38 - Foo bar baz
    Comeek3800.jpg
    Comeek3801.jpg
    Comeek3802.jpg
    Comeek3803.jpg
    Comeek3804.jpg
    Comeek3805.jpg
    Comeek3806.jpg
    Comeek3807.jpg
    Comeek3808.jpg
    Comeek3809.jpg
    Comeek3810.jpg
    Comeek3811.jpg
    Comeek3812.jpg
    Comeek3813.jpg
    Comeek3814.jpg
    Comeek3815.jpg
    Comeek3816.jpg
    Comeek3817.jpg
    Comeek3818.jpg
    Comeek3819.jpg
    Comeek3820-21.jpg
    Comeek3822.jpg
    Comeek3823.jpg
    Comeek3824.jpg
    Thumbs.db

The script currently renames them thusly, actually breaking them:

    Adding    ./Comeek 38 - Foo bar baz/Comeek38-00.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-01.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-02.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-03.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-04.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-05.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-06.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-07.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-08.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-09.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-10.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-11.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-12.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-13.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-14.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-15.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-16.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-17.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-18.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-19.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-22.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-23.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek38-24.jpg   OK
    Adding    ./Comeek 38 - Foo bar baz/Comeek3820-21.jpg OK
    Adding    ./Comeek 38 - Foo bar baz/Thumbs.db         OK
    Adding    ./Comeek 38 - Foo bar baz                   OK

That should be fixed.
