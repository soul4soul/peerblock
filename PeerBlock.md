# Background #

PeerBlock is a "fork" of the Peer Guardian 2 project.  That base PG2 code hadn't been updated in ~2 years, and the most recent version from back then was still just a beta for Windows Vista support.  With Windows 7 now in Release Candidate mode, it seemed like time to resurrect the project and try to get it working without requiring all the myriad hacks/workarounds necessary to get PG2 working, especially under 64-bit environments.


# What's Changed? #

First off, the base code (SVN [r1](https://code.google.com/p/peerblock/source/detail?r=1) here at Google Code) was the state of the PG2 source available at sourceforge.net.  [r2](https://code.google.com/p/peerblock/source/detail?r=2) was the merging-in of nightstalker\_x's PG2 RC1 Test3 changes from a forum post at the Phoenix Labs website.

Since then, I've updated most of the third-party libs to the latest-and-greatest versions; this included adding a small portion of the Boost libs to source-control to make it easier to ensure that everyone's building with the same version of Boost.  I'm also a big fan of trace-logging, so I wrote a small thread-safe logger (tracelog.h and .cpp) and have been sprinkling trace-log statements throughout the code.  I'm a bit anal-retentive when it comes to code commenting as well, so have been slowly updating code-comments: adding function "headers", dropping in the occasional comment to explain what's going on (as I understand it), etc.  Most occurrences of Peer Guardian related text has been changed to instead refer to PeerBlock, to minimize confusion over which version of the program you're running at any given time.


# Where are we Going? #

From here, I want to fix some of the base PG2 bugs.  The "hanging when updating lists" thing is just a bug, and should be relatively-easily fixable.  The fact that the tool requires Administrator privilege is a bit more interesting - I believe that the best way to remove this restriction is to migrate the app into a Service instead, and have the GUI merely act as an interface to that service; to the best of my knowledge, the only reason Admin priv is required is because it's loading a driver, and Services run under a different user account which should better allow that.

The bigger issue though is Driver Signing.  To get around this we really need to build a signed driver, and to do that we need a code-signing certificate.  The cheapest one I've found is $180 for one, and that will need to be paid yearly if we want to continue making changes to the driver.  So we're going to need some mad donations if we wanna get there from here...

Other than that, any other changes are likely to be a ways off.  Switch over to the PG3 base-code?  Merge the PG3-specific changes in with our PG2-based PeerBlock code?  Do something entirely different?  I dunno!  We'll see as that time comes.