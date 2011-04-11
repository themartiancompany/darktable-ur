# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
pkgver=0.8
pkgrel=4
pkgdesc="Utility to organize and develop raw images"
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'gconf>=2.26' 'intltool>=0.40' 'lcms2' 'lensfun>=0.2.3' 'libglade'
	 'curl' 'libgnome-keyring' 'libgphoto2' 'libusb-compat' 'openexr')
makedepends=('intltool>=0.40')
optdepends=( 'librsvg')
install=darktable.install
options=(!libtool)
source=(http://downloads.sourceforge.net/project/darktable/darktable/0.8/darktable-$pkgver.tar.gz)
md5sums=('1724601b0d7012a414f5398e5029cb45')

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
  make DESTDIR=$pkgdir install

  mv "${pkgdir}/usr/share/doc/darktable" "${pkgdir}/usr/share/doc/${pkgname}-${pkgver}"
  mkdir -p "${pkgdir}/usr/share/gconf/schemas/"
  mv "${pkgdir}/etc/gconf/schemas/darktable.schemas" "${pkgdir}/usr/share/gconf/schemas/"
}
