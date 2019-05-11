
Install dependencies
```
export PATH="/usr/local/opt/gettext/bin:$PATH"
brew install gettext intltool glib libtool autoconf automake pkg-config
brew install imagemagick graphicsmagick pstoedit
git clone https://github.com/autotrace/autotrace.git
cd autotrace
autoreconf -ivf
intltoolize --force
aclocal
test -e /usr/local/lib/pkgconfig/libffi.pc || ln -s ../../Cellar/libffi/3.2.1/lib/pkgconfig/libffi.pc /usr/local/lib/pkgconfig/
```

Configure General
```
sh ./configure MAGICK_CFLAGS="$(pkg-config graphicsmagick --cflags)" MAGICK_LIBS="$(pkg-config graphicsmagick --libs)"
```

Configure withour ImageMagick 
(for solving buggy messages: Invalid chunk type)
```
./configure MAGICK_CFLAGS="$(pkg-config graphicsmagick --cflags)" MAGICK_LIBS="$(pkg-config graphicsmagick --libs)" --without-magick --without-pstoedit
```

Build and Install
```
make
make install
```