# Maintainer: Knut Ahlers <knut at ahlers dot me>
# Contributor: Alice Gaudon <alice at gaudon dot pro>
# Contributor: Benjamin Klettbach <b dot klettbach at gmail dot com >
# Contributor: Jonathan Steel <jsteel at archlinux.org>
# Contributor: ArcticVanguard <LideEmily at gmail dot com>
# Contributor: ledti <antergist at gmail dot com>

pkgname=obs-studio-browser
pkgver=29.1.0
pkgrel=0
pkgdesc="Free and open source software for video recording and live streaming. Built with the browser plugin."
arch=("i686" "x86_64")
url="https://github.com/obsproject/obs-studio"
license=("GPL2")
depends=(
  "curl"
  "ffmpeg"
  "gtk-update-icon-cache"
  "jansson"
  "libajantv2"
  "libxcomposite"
  "libxinerama"
  "libxkbcommon-x11"
  "mbedtls"
  "pciutils"
  "pipewire"
  "qt5-x11extras"
  "rnnoise"
  "x264"
)
makedepends=(
  "asio"
  "cef-minimal-obs"
  "cmake"
  "git"
  "jack"
  "libfdk-aac"
  "libxcomposite"
  "luajit"
  "nlohmann-json"
  "python"
  "sndio"
  "swig"
  "vlc"
  "websocketpp"
)
optdepends=(
  "vlc: VLC Media Source"
  "swig: Scripting"
  "luajit: Lua scripting"
  "python: Python scripting"
  "v4l2loopback-dkms: Virtual camera output"
)
provides=("obs-studio=$pkgver")
conflicts=("obs-studio")
source=(
  "$pkgname::git+https://github.com/obsproject/obs-studio.git#tag=$pkgver"
  0001-Enforce_-Wmaybe-uninitialized_never_turn_into_error.patch
)
sha256sums=('SKIP'
            '9227a5f3439d19c2c75e369bc6701dc83c4ac54cc371b7f74e55c9e275512f6c')

prepare() {
  cd $pkgname
  git submodule update --init --recursive
  patch -Np1 <"$srcdir/0001-Enforce_-Wmaybe-uninitialized_never_turn_into_error.patch"
}

build() {
  cd $pkgname

  mkdir -p build
  cd build

  cmake \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DBUILD_BROWSER=ON \
    -DCEF_ROOT_DIR="/opt/cef" \
    -DOBS_VERSION_OVERRIDE=$pkgver \
    -DENABLE_NEW_MPEGTS_OUTPUT=OFF \
    ..

  make
}

package() {
  cd $pkgname/build

  make install DESTDIR="$pkgdir"
}

# vim: ts=2:sw=2:expandtab
