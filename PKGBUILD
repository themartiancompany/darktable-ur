# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
pkgver=0.9.3
_pkgver=0.9
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'gconf>=2.26' 'intltool>=0.40' 'lcms2' 'lensfun>=0.2.3' 'libglade'
	 'curl' 'libgnome-keyring' 'libgphoto2' 'libusb-compat' 'openexr' 'sqlite3')
makedepends=('intltool>=0.40' 'cmake' 'sqlite3')
optdepends=( 'librsvg')
install=darktable.install
options=(!libtool)
source=(http://downloads.sourceforge.net/project/darktable/darktable/${_pkgver}/darktable-$pkgver.tar.gz)
md5sums=('49253a3a2990a4bf8e0b0a19295f19bd')

build() {
  cd $srcdir/$pkgname-$pkgver
  mkdir -p build
  cd build
  cmake \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_BUILD_TYPE=Release \
      -DBUILD_USERMANUAL=False \
      -DDONT_INSTALL_GCONF_SCHEMAS=True \
      -DBINARY_PACKAGE_BUILD=1 \
      ..
  make
}

package() {
  cd $srcdir/$pkgname-$pkgver/build
  make DESTDIR=$pkgdir install
  mv "${pkgdir}/usr/share/doc/darktable" "${pkgdir}/usr/share/doc/${pkgname}-${pkgver}"
  mkdir -p "${pkgdir}/usr/share/gconf/schemas/"
  mv "${pkgdir}/etc/gconf/schemas/darktable.schemas" "${pkgdir}/usr/share/gconf/schemas/"
}
