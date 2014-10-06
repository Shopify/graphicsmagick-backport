# Graphicsmagick 1.3.18 backport for Ubuntu 12.04 LTS

A backport of [GraphicsMagick](http://www.graphicsmagick.org/) version 1.3.18 for Ubuntu 12.04. GraphicsMagick 1.3.18 includes support for the `-auto-orient` flag.

Contains the original source of 1.3.18, with small modifications to `configure.ac` and `Makefile.am` per this [askUbuntu answer](http://askubuntu.com/a/527747/329826).

## Compiling

See [GraphicsMagick's README](http://www.graphicsmagick.org/README.html) for dependency requirements.

```
autoreconf -f -i
./configure
make
```

To install, use `sudo make install`.

## License

GraphicsMagick is licensed under the MIT License. See [http://www.graphicsmagick.org/Copyright.html].

## Precompiled Binary

Version information of the included precompiled binary, configured to run on CircleCI Ubuntu images: (`gm -version`):

```
GraphicsMagick 1.3.18 2013-03-10 Q8 http://www.GraphicsMagick.org/
Copyright (C) 2002-2013 GraphicsMagick Group.
Additional copyrights and licenses apply to this software.
See http://www.GraphicsMagick.org/www/Copyright.html for details.

Feature Support:
  Thread Safe              yes
  Large Files (> 32 bit)   yes
  Large Memory (> 32 bit)  yes
  BZIP                     yes
  DPS                      no
  FlashPix                 no
  FreeType                 yes
  Ghostscript (Library)    no
  JBIG                     no
  JPEG-2000                yes
  JPEG                     yes
  Little CMS               yes
  Loadable Modules         no
  OpenMP                   yes (200805)
  PNG                      yes
  TIFF                     yes
  TRIO                     no
  UMEM                     no
  WMF                      yes
  X11                      yes
  XML                      yes
  ZLIB                     yes

Host type: x86_64-unknown-linux-gnu

Configured using the command:
  ./configure

Final Build Parameters:
  CC       = gcc -std=gnu99
  CFLAGS   = -fopenmp -g -O2 -Wall -pthread
  CPPFLAGS = -I/usr/include/freetype2 -I/usr/include/libxml2
  CXX      = g++
  CXXFLAGS = -pthread
  LDFLAGS  = -L/usr/lib -L/usr/lib
  LIBS     = -llcms -ltiff -lfreetype -ljasper -ljpeg -lpng12 -lwmflite -lX11 -llzma -lbz2 -lxml2 -lz -lm -lgomp -lpthread
```
