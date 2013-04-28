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

* Or maybe it's OS/X is doing this, I don't know.
