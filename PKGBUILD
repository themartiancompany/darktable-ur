# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
pkgver=2.0.0
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'intltool>=0.40' 'lcms2' 'lensfun>=0.2.3' 'libglade' 'dbus-glib'
	 'curl' 'libsecret' 'libgphoto2' 'openexr' 'sqlite' 'libxslt'
	 'libsoup' 'gtk3' 'pugixml' 'gtk-engines' 'json-glib' 'flickcurl' 'lua52' 'colord')
makedepends=('intltool>=0.40' 'cmake' 'librsvg')
optdepends=('librsvg')
install=darktable.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/darktable-org/darktable/archive/release-$pkgver.tar.gz")
md5sums=('1a95dd4d7dce7c9d76988d0cca003a5f')

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
