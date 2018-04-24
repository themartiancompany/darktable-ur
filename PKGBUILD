# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable
epoch=2
pkgver=2.4.3
pkgrel=1
pkgdesc="Utility to organize and develop raw images"
arch=('x86_64')
url="https://darktable.org"
license=('GPL3')
depends=('pugixml' 'libjpeg-turbo' 'colord-gtk' 'libgphoto2' 'openexr' 'lensfun' 'iso-codes'
         'exiv2' 'flickcurl' 'openjpeg2' 'graphicsmagick' 'lua' 'osm-gps-map' 'libsecret')
makedepends=('cmake' 'intltool' 'desktop-file-utils' 'llvm' 'clang' 'python-jsonschema' 'libwebp')
source=("https://github.com/darktable-org/darktable/releases/download/release-${pkgver}/darktable-${pkgver/rc/.rc}.tar.xz"{,.asc})
sha256sums=('1dc5fc7bd142f4c74a5dd4706ac1dad772dfc7cd5538f033e60e3a08cfed03d3'
            'SKIP')
validpgpkeys=('C4CBC150699956E2A3268EF5BB5CC8295B1779C9')

prepare() {
    mkdir -p build
}

build() {
    cd build
    cmake ../${pkgname}-${pkgver/rc/~rc} \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=/usr/lib \
        -DCMAKE_BUILD_TYPE=Release \
        -DBINARY_PACKAGE_BUILD=1 \
        -DBUILD_USERMANUAL=False \
        -DUSE_LIBSECRET=On \
        -DUSE_LUA=On \
        -DUSE_COLORD=On \
        -DPROJECT_VERSION=${pkgver}
    make
}

package() {
    cd build
    make DESTDIR="${pkgdir}" install
    ln -s darktable/libdarktable.so "${pkgdir}"/usr/lib/libdarktable.so
}
