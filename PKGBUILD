# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
epoch=1
pkgver=2.0.7
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
epoch=1
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'lcms2' 'lensfun>=0.2.3' 'desktop-file-utils'
	 'curl' 'libsecret' 'libgphoto2' 'openexr' 'sqlite' 'libxslt'
	 'libsoup' 'gtk3' 'pugixml' 'json-glib' 'flickcurl' 'lua52'
	 'colord' 'colord-gtk' 'graphicsmagick')
makedepends=('intltool>=0.40' 'cmake' 'librsvg' 'osm-gps-map' 'libcups')
optdepends=('librsvg' 'osm-gps-map' 'libcups')
source=("https://github.com/darktable-org/darktable/releases/download/release-$pkgver/darktable-$pkgver.tar.xz")
sha256sums=('a9226157404538183549079e3b8707c910fedbb669bd018106bdf584b88a1dab')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  mkdir -p build
  cd build
  CXXFLAGS+=" -fpermissive"
  cmake \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_INSTALL_LIBDIR=/usr/lib \
      -DCMAKE_BUILD_TYPE=Release \
      -DBINARY_PACKAGE_BUILD=1 \
      -DBUILD_USERMANUAL=False \
      -DUSE_LIBSECRET=On \
      -DUSE_LUA=On \
      -DUSE_GNOME_KEYRING=Off \
      -DUSE_COLORD=On \
      -DPROJECT_VERSION=$pkgver \
      ..
  make

  cd ../tools/basecurve
  cmake .
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver/build"
  make DESTDIR="$pkgdir" install
  ln -s darktable/libdarktable.so "$pkgdir/usr/lib/libdarktable.so"
  install -Dm0755 ../tools/basecurve/dt-curve-tool "$pkgdir"/usr/bin/dt-curve-tool
  install -Dm0755 ../tools/basecurve/dt-curve-tool-helper "$pkgdir"/usr/bin/dt-curve-tool-helper
}
