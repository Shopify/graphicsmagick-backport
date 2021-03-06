2013-03-09  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - version.sh, www/index.rst: Prepare for 1.3.18 release.

2013-03-04  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c (DisplayImageCommand): display is supposed to
    respond to +/-usePixmap, but was not.  It was responding to
    +/-use\_pixmap.  Now it responds to both.

2013-03-03  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - doc/GraphicsMagick.imdoc: Relocated some <im> .. </im> tags, to
    include several paragraphs that were omitted from the
    GraphicsMagick man page (Environment, Configuration Files, and
    Copyright).

  - doc/imdoc2man: the </pre> tag was being deleted instead of
    replaced with nothing, which caused the first line of the
    subsequent material to be joined to the last line of the <pre>
    block.

2013-03-02  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (ReadOnePNGImage): Avoid a libpng16 warning about
    storing unknown chunks.

2013-02-25  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (WriteOnePNGImage): Call png\_set\_bKGD(), etc.,
    after png\_set\_IHDR() because they depend on members of info\_ptr
    which are set by png\_set\_IHDR().

2013-02-20  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/resource.c (InitializeMagickResources): Enable the
    dynamic adjustment of OpenMP threads if there is more than one
    thread available.

2013-02-18  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - configure.ac and configure: Check for libpng17 and libpng16.

2013-02-13  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - www/programming.rst: Add mention of Clement Farabet's Lua
    scripting language wrapper for GraphicsMagick.

2013-02-10  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/pixel\_cache.c (GetCacheNexus): Re-write function so it
    has a single point of return.
    (AcquireCacheNexus): Reduce the number of return points.
    (SetCacheNexus): Re-write function so it has a single point of
    return.

2013-02-02  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - NEWS.txt: Update with latest news.

  - magick/export.c (ExportAlphaQuantumType): Fix export of alpha
    for RGBA image and depth 8.  Due to typo, was exporting 16-bits
    rather than 8, causing output corruption or crashes.  Resolves
    issue reported in SourceForge GraphicsMagick forum under title
    "CMYK per-channel byte order TIFF crashes gm".

2013-02-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/studio.h (MagickIsBlank): Add macro to substitute for ISO
    C99 isblank() which is not globally available.  Update 'gm batch'
    code which had substituted isspace() for isblank() to use it.

2013-01-31  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c (BatchCommand): Flush stdout at key points in
    order to ensure that user sees text when it is produced.

2013-01-30  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/random.c (InitializeMagickRandomGenerator): Use
    MagickTsdKeyCreate2() in order to avoid a small memory leak.

  - magick/tsd.c (MagickTsdKeyCreate2): New private function to
    support allocating a thread-specific data key with a specified
    destructor function.  For single-threaded build, MagickTsdKey\_t is
    now type void\* and there is provision to support the destructor
    function.

2013-01-29  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/command.c (BatchCommand): New 'gm batch' command to
    accept one or more GraphicsMagick commands from a specified text
    file, standard input, or CLI.  Feature is implemented by Kenneth
    Xu.  Submitted via SourceForge Patch #3602331 "Add interactive or
    batch mode support to 1.3.17".

2013-01-27  Glenn Randers-Pehrson  <glennrp@simple.dallas.tx.us>

  - coders/png.c (WriteOnePNGImage): Added PNG48 and PNG64 support.
    Added PNG00 support (png encoder that inherits its color-type and
    bit-depth from the input, if the input was a PNG datastream).

2013-01-26  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - coders/png.c (WriteOnePNGImage): PNG8 support was using
    image->colors to decide if the input image is PseudoClass.  This
    is totally bogus.  Use image->storage\_class to determine if image
    is PseudoClass and quantize image colors if it is not.

  - magick/delegate.c (InvokePostscriptDelegate): Only invoke
    MagickSpawnVP() if Ghostscript filename argument is non-empty.
    This argument may be empty if Ghostscript is not found on a
    Windows system.  Report a "Failed to find Ghostscript" error if
    the Ghostscript command name is empty. Resolves SourceForge issue
    #3601816 "Win64 build crashes trying to convert PDF to any other
    format".

  - magick/utility.c (MagickSpawnVP): Verify that file argument is
    non-NULL and not empty.

2013-01-15  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - VisualMagick/tiff/LIBRARY.txt: Fix pre-processor definitions for
    libtiff so that they use multiple statements rather than one long
    statement.  Resolves SourceForge issue 3601001 "libtiff won't
    compile with ICL".

2013-01-06  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/memory.h (MagickAllocateAlignedArray): New macro to wrap
    use of MagickMallocAlignedArray().

  - magick/memory.c (MagickMallocAlignedArray): New private function
    to support safe allocation of an array in memory with a specified
    alignment.  Allocation may only be freed using MagickFreeAligned()
    and the allocation may not be reallocated.

2013-01-05  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - magick/{animate.c,display.c,utility.c}: Only invoke chdir() if
    path is not an empty string.  Previously sometimes chdir() was
    passed an empty string (because chdir() was not needed) and this
    was ok because we ignored the error status.  Now that we check the
    chdir() error status, some X11 GUI functions (e.g. save file to
    current directory) encounter annoying issues.

  - magick/shear.c (IntegralRotateImage): Limit integral rotate to
    two threads.

  - coders/pnm.c (ReadPNMImage): Limit PNM reader to two threads.

2013-01-01  Bob Friesenhahn  <bfriesen@simple.dallas.tx.us>

  - configure.ac (MAGICK\_FEATURES): MinGW static build does not
    build modules so MODULES feature should not be listed as
    supported.  Resolves MinGW test failures.

  - coders/dpx.c (OrientationTypeToDPXOrientation): Return U16 type
    as stored in DPX format.

  - coders/cineon.c: Add support for reading/writing 'orientation'
    setting.

  - coders/mpc.c: Add support for reading/writing 'orientation'
    setting.

  - coders/miff.c: Add support for reading/writing 'orientation'
    setting.

  - Rotate ChangeLog for 2012 and update web page copyright years.

