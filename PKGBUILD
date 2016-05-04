# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

# Don't bump to 2.1 plz, it's a development branch. (- bpiotrowski)

pkgname=darktable
pkgver=2.0.4
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
epoch=1
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'lcms2' 'lensfun>=0.2.3' 'desktop-file-utils'
	 'curl' 'libsecret' 'libgphoto2' 'openexr' 'sqlite' 'libxslt'
	 'libsoup' 'gtk3' 'pugixml' 'osm-gps-map' 'json-glib' 'flickcurl' 'lua52'
	 'colord' 'colord-gtk' 'graphicsmagick')
makedepends=('intltool>=0.40' 'cmake' 'librsvg')
optdepends=('librsvg')
source=("$pkgname-$pkgver.tar.gz::https://github.com/darktable-org/darktable/archive/release-$pkgver.tar.gz")
md5sums=('130a0bd61cabd21f2df67dadc62be792')

build() {
  cd "$srcdir/$pkgname-release-$pkgver"
  mkdir -p build
  cd build
  CXXFLAGS+=" -fpermissive"
  cmake \
      -DCMAKE_INSTALL_PREFIX=/usr \
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
  cd "$srcdir/$pkgname-release-$pkgver/build"
  make DESTDIR="$pkgdir" install
  install -Dm0755 ../tools/basecurve/dt-curve-tool $pkgdir/usr/bin/dt-curve-tool
  install -Dm0755 ../tools/basecurve/dt-curve-tool-helper $pkgdir/usr/bin/dt-curve-tool-helper
}
