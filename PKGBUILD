# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
pkgver=0.7
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
arch=(i686 x86_64)
url=http://darktable.sf.net/
license=('GPL3')
depends=('exiv2>=0.18' 'gconf>=2.26' 'intltool>=0.40' 'lcms' 'lensfun>=0.2.3' 'libglade'
	 'curl' 'libgnome-keyring' 'libgphoto2')
makedepends=('intltool>=0.40')
optdepends=('openexr' 'librsvg')
install=darktable.install
options=(!libtool)
source=(http://downloads.sourceforge.net/project/darktable/darktable/$pkgver/darktable-$pkgver.tar.gz)
md5sums=('8220427138bb66772310f3961adc2ebe')

build() {
  # Linking fails with --as-needed linker option
  unset LDFLAGS
  cd $srcdir/$pkgname-$pkgver
  autoreconf
  ./configure --prefix=/usr --disable-schemas-install --with-gconf-schema-file-dir=/usr/share/gconf/schemas
  make
  make DESTDIR=$pkgdir install
  mkdir -p $pkgdir/usr/share/doc/$pkgname-$pkgver
  install -m644 AUTHORS LICENSE NEWS README TODO TRANSLATORS $pkgdir/usr/share/doc/$pkgname-$pkgver
}
