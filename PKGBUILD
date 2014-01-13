# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
pkgver=1.4
_pkgver=1.4
pkgrel=2
pkgdesc="Utility to organize and develop raw images"
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'intltool>=0.40' 'lcms2' 'lensfun>=0.2.3' 'libglade' 'dbus-glib'
	 'curl' 'libgnome-keyring' 'libgphoto2' 'openexr' 'sqlite' 'libxslt'
	 'libsoup' 'gtk-engines' 'json-glib' 'flickcurl')
makedepends=('intltool>=0.40' 'cmake' 'librsvg')
optdepends=('librsvg')
install=darktable.install
source=(http://downloads.sourceforge.net/project/darktable/darktable/${_pkgver}/darktable-$pkgver.tar.xz
	https://github.com/darktable-org/darktable/commit/74dbfa3b24bcc216ec91e12551b6b434e4a43a22.diff)
md5sums=('896416931ded4579f528cd11edad470c'
         'f959e371f8648eeef8ad6dd6e1403d29')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  patch -p1 <$srcdir/74dbfa3b24bcc216ec91e12551b6b434e4a43a22.diff
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  mkdir -p build
  cd build
  CXXFLAGS+=" -fpermissive"
  cmake \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_BUILD_TYPE=Release \
      -DDONT_INSTALL_GCONF_SCHEMAS=True \
      -DBINARY_PACKAGE_BUILD=1 \
      -DUSE_GCONF_BACKEND=Off \
      -DBUILD_USERMANUAL=False \
      ..
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver/build"
  make DESTDIR="$pkgdir" install
  mv "${pkgdir}/usr/share/doc/darktable" "${pkgdir}/usr/share/doc/${pkgname}-${pkgver}"
}
