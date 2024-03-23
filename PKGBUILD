# Maintainer: Knut Ahlers <knut at ahlers dot me>
# Contributor: Alice Gaudon <alice at gaudon dot pro>
# Contributor: Benjamin Klettbach <b dot klettbach at gmail dot com >
# Contributor: Jonathan Steel <jsteel at archlinux.org>
# Contributor: ArcticVanguard <LideEmily at gmail dot com>
# Contributor: ledti <antergist at gmail dot com>

pkgname=obs-studio-browser
pkgver=30.1.1
pkgrel=1
pkgdesc="Free and open source software for video recording and live streaming. Built with the browser plugin."
arch=("i686" "x86_64")
url="https://github.com/obsproject/obs-studio"
license=("GPL2")
depends=(
  "curl"
  "ffmpeg"
  "gtk-update-icon-cache"
  "jack"
  "jansson"
  "libxcomposite"
  "libxinerama"
  "libxkbcommon-x11"
  "mbedtls"
  "pciutils"
  "pipewire"
  "qrcodegencpp-cmake"
  "qt5-x11extras"
  "qt6-svg"
  "rnnoise"
  "x264"
)
makedepends=(
  "asio"
  "cef-minimal-obs"
  "cmake"
  "git"
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
)
sha256sums=('4ee676256816b57a9240ef9ca0c11d92f53e94207acb0614e6835a1aac32cef9')

prepare() {
  cd $pkgname
  git submodule update --init --recursive
}

build() {
  cmake -B build -S $pkgname \
    -DBUILD_BROWSER=ON \
    -DCALM_DEPRECATION=ON \
    -DCEF_ROOT_DIR="/opt/cef" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DENABLE_AJA=OFF \
    -DENABLE_JACK=ON \
    -DENABLE_LIBFDK=ON \
    -DENABLE_NEW_MPEGTS_OUTPUT=OFF \
    -DENABLE_VST=ON \
    -DENABLE_WEBRTC=OFF \
    -DOBS_VERSION_OVERRIDE="$pkgver-$pkgrel" \
    -Wno-dev

  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}

# vim: ts=2:sw=2:expandtab
