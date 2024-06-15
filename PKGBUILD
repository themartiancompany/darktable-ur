# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Bruno Pagani <archange@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika <hanatos at gmail dot com>

_colord="true"
_libsecret='true'
_os="$( \
  uname \
    -o)"
[[ "${_os}" == "Android" ]] && \
  _colord='false' \
  _libsecret='true'
_pkg=darktable
pkgname="${_pkg}"
epoch=2
pkgver=4.6.1
pkgrel=3
pkgdesc="Utility to organize and develop raw images"
arch=(
  x86_64
  arm
  aaarch64
  i686
  armv7h
  mips
  powerpc
)
url="https://${_pkg}.org"
license=(
  GPL3
)
depends=(
  pugixml
  libjpeg-turbo
  libgphoto2
  openexr
  lensfun
  iso-codes zlib
  exiv2
  flickcurl
  openjpeg2
  graphicsmagick
  lua
  osm-gps-map
  openmp
  gmic
  libavif
  jasper
  libjxl
)
[[ "${_colord}" == "true" ]] && \
  depends+=(
    colord-gtk
  )
[[ "${_libsecret}" == "true" ]] && \
  depends+=(
    libsecret
  )
optdepends=(
  'dcraw: base curve script'
  'perl-image-exiftool: base curve script'
  'imagemagick: base curve and noise profile scripts'
  'ghostscript: noise profile script'
  'portmidi: game and midi controller input devices'
  'gnuplot: noise profile script'
)
makedepends=(
  cmake
  intltool
  desktop-file-utils
  llvm
  clang
  portmidi
  python-jsonschema
  libwebp
)
_http="https://github.com"
_ns="${_pkg}-org"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${_url}/releases/download/release-${pkgver}/${_pkg}-${pkgver}.tar.xz"{,.asc})
sha256sums=(
  '16edc0a070293e2d3cda4ea10e49bda9bde932e23f9e62e2fa2e7ac74acf7afd'
  'SKIP'
)
validpgpkeys=(
  # darktable releases <release@darktable.org>
  C4CBC150699956E2A3268EF5BB5CC8295B1779C9
  # Pascal Obry <pascal@obry.net>
  F10F9686652B0E949FCD94C318DCA123F949BD3B
) 

build() {
  local \
    _cmake_opts=() \
    _colord_flag
  if [[ "${_colord}" == "true" ]]; then
    _colord_flag='ON'
  elif [[ "${_colord}" == "false" ]]; then
    _colord_flag='OFF'
  fi
  if [[ "${_libsecret}" == "true" ]]; then
    _libsecret_flag='ON'
  elif [[ "${_libsecret}" == "false" ]]; then
    _libsecret_flag='OFF'
  fi
  _cmake_opts=(
    -DCMAKE_INSTALL_PREFIX=/usr
    -DCMAKE_INSTALL_LIBEXECDIR=/usr/lib
    -DCMAKE_BUILD_TYPE=Release
    -DBINARY_PACKAGE_BUILD=1
    -DBUILD_USERMANUAL=False
    -DUSE_LIBSECRET="${_libsecret_flag}"
    -DUSE_LUA=ON
    -DUSE_COLORD="${_colord_flag}"
    -DBUILD_CURVE_TOOLS=ON
    -DBUILD_NOISE_TOOLS=ON
    -DRAWSPEED_ENABLE_LTO=ON
    -DPROJECT_VERSION=${pkgver}
  )
  cmake \
    -B build \
    -S ${pkgname}-${pkgver} \
    "${_cmake_opts[@]}"
  make \
    -C \
      build
}

package() {
  make \
    -C \
      build \
    DESTDIR="${pkgdir}" \
    PREFIX="/usr" \
    install
  ln \
    -s \
    "${_pkg}/lib${_pkg}.so" \
    "${pkgdir}/usr/lib/lib${_pkg}.so"
}

