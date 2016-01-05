# Introduction #

This page details the third-party code which PeerBlock uses.  Included should be version and license information, location from which new code drops can be downloaded, tips & tricks on merging their code with ours, what we're actually using them for, etc.


# Libraries #

## Boost ##

Thus far I've copied-in all the headers we're using, just to make it easier to build everything.  We're not currently linking against anything that requires a compiled lib, and unless there's a compelling reason otherwise I think I'd like to leave it that way.


## lib7z ##

This source tree _looks_ like it came from the 7-zip LZMA SDK, but with files renamed/moved from their original directories.  No idea which version the original PG2 code was from.

The current version won't link with the PG2/PeerBlock code, as we're trying to use some routines that must've been renamed/removed at some point in the past.  LOTS of compilation errors, not sure it's worth tracking down at this point.


## libcurl ##

Upstream sources located at the [curl website](http://curl.haxx.se/libcurl).  Looks like ...\libcurl\include is a copy of curl\include, and ...\libcurl\src is copied in from curl\lib.

Based on the curlver.h (and verified by checking out all the revision-stamps on each of the files), it looks like base PG2 code was running v7.16.2.  However, they made some modifications to this code, which will need to be re-added whenever we update libcurl.  Look at SVN [r25](https://code.google.com/p/peerblock/source/detail?r=25) for the diffs; I reset the libcurl lib code back to 7.16.2 for [r24](https://code.google.com/p/peerblock/source/detail?r=24), then added back in the PG-specific changes for [r25](https://code.google.com/p/peerblock/source/detail?r=25).  [r26](https://code.google.com/p/peerblock/source/detail?r=26) updated libcurl to v7.19.5, and includes the forward-ported PG-specific mods.

I also had to patch around some strange internal bug with libcurl, a rare one that's not easily reproducible and so has never been addressed by the libcurl devs in the past.  See [r67](https://code.google.com/p/peerblock/source/detail?r=67) and [r68](https://code.google.com/p/peerblock/source/detail?r=68) commits for the diffs.  Doesn't fix the root-cause of the problem, just lets us not choke and die if we hit it.


## libp2p ##

This library appears to have been written by the same guys who wrote PeerGuardian; here's their [wiki-page](http://wiki.phoenixlabs.org/wiki/Libp2p) on it.  I guess the version checked-in to source-control is always the latest-and-greatest.  Looks like this is the API to handle their block-list format.


## miniunzip ##

Based on the unzip.h file, this library looks like it's at v1.01e from the [minizip site](http://www.winimage.com/zLibDll/minizip.html).  Looks like the code is now  part of [Zlib](http://www.zlib.net).  Appears to support .gz files only?

Need to check whether we still use this code anymore, or whether that functionality was (or could be) migrated over to lib7z instead...


## sqlite3-plus ##

This looks like it's a wrapper around sq3lite, written by one of the original developers of PeerGuardian ("PhrostByte" / Cory Nelson).  The [most recent package](http://sourceforge.net/project/showfiles.php?group_id=112954) available as of 6/10/09 was released 6/16/05, however the sourceforge source had been most recently modified (added?) sometime around 5/20/09.  Quite a lot of changes in the new (SourceForge SVN [r206](https://code.google.com/p/peerblock/source/detail?r=206)) version.


## sqlite ##

According to sqlite3.h, the baseline PG2 code was using v3.3.17.  I since updated it to 3.6.14.2.  Download the recommended "amalgamation" package from [their website](http://sqlite.org/download.html).


## tinyxml ##

Base PG2 code was at v2.5.3 (released 5/6/07), and this is still the most recent package available on sourceforge as of 6/2/09.  Sources were modified later in the year though, and should possibly be the ones to upgrade to at this point - worth checking out sometime.