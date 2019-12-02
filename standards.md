# Common
Unidata limits named commons to 7 characters

* Universe/Unidata do not have a swap statement.  Use MVDBTOOLKIT.SWAP

# MD Entries

Unidata

Unidata does not appear (need update) to allow directory dictionaries.  You need to create a unidata file
CREATE-FILE DIR MVDBTOOLKIT.BP

ED VOC MVDBTOOLKIT.BP
<PRE>
1>DIR
2>mvdbtoolkit\mvdbtoolkit.bp
3>D_MVDBTOOLKIT
</PRE>

For wobj we will just create a new entry

ED VOC MVDBTOOLKIT.WOBJ.BP
<PRE>
1>DIR
2>mvdbtoolkit\mvdbtoolkit.bp]mwobj.bp
3>D_MVDBTOOLKIT
</PRE>

# SENTENCE=()

Unidata syntax: @SENTENCE() vs SENTENCE()

