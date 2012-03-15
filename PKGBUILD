# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
pkgver=1.0
_pkgver=1.0
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
arch=('i686' 'x86_64')
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'intltool>=0.40' 'lcms2' 'lensfun>=0.2.3' 'libglade' 'dbus-glib'
	 'curl' 'libgnome-keyring' 'libgphoto2' 'libusb-compat' 'openexr' 'sqlite3')
makedepends=('intltool>=0.40' 'cmake' 'librsvg')
#	     'gnome-doc-utils' 'libxslt' 'fop')
optdepends=('librsvg')
install=darktable.install
options=(!libtool)
source=(http://downloads.sourceforge.net/project/darktable/darktable/${_pkgver}/darktable-$pkgver.tar.gz)
md5sums=('b72375782519b7a4a6b8efcad1bfcf6b')

build() {
  cd $srcdir/$pkgname-$pkgver
#  mv doc/usermanual/CMakeLists.tx doc/usermanual/CMakeLists.txt
  mkdir -p build
  cd build
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
  cd $srcdir/$pkgname-$pkgver/build
  make DESTDIR=$pkgdir install
  mv "${pkgdir}/usr/share/doc/darktable" "${pkgdir}/usr/share/doc/${pkgname}-${pkgver}"
#  mkdir -p "${pkgdir}/usr/share/gconf/schemas/"
#  mv "${pkgdir}/etc/gconf/schemas/darktable.schemas" "${pkgdir}/usr/share/gconf/schemas/"
}
