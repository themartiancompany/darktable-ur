# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
pkgver=1.6.5
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'intltool>=0.40' 'lcms2' 'lensfun>=0.2.3' 'libglade' 'dbus-glib'
	 'curl' 'libsecret' 'libgphoto2' 'openexr' 'sqlite' 'libxslt'
	 'libsoup' 'gtk-engines' 'json-glib' 'flickcurl' 'lua' 'colord')
makedepends=('intltool>=0.40' 'cmake' 'librsvg')
optdepends=('librsvg')
install=darktable.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/darktable-org/darktable/archive/release-$pkgver.tar.gz")
md5sums=('2d688e388313faab11c81dbb582fcbc8')

prepare() {
  cd "$srcdir/$pkgname-release-$pkgver/cmake"
  sed "s|@PROJECT_VERSION@|$pkgver|" version.cmake.cmake >version.cmake
}

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
  make -C ../tools/basecurve
}

package() {
  cd "$srcdir/$pkgname-release-$pkgver/build"
  make DESTDIR="$pkgdir" install
  install -Dm0755 ../tools/basecurve/dt-curve-tool $pkgdir/usr/bin/dt-curve-tool
  install -Dm0755 ../tools/basecurve/dt-curve-tool-helper $pkgdir/usr/bin/dt-curve-tool-helper
  mv "${pkgdir}/usr/share/doc/darktable" "${pkgdir}/usr/share/doc/${pkgname}-${pkgver}"
}
