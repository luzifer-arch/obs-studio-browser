# Maintainer: Knut Ahlers <knut at ahlers dot me>
# Contributor: Alice Gaudon <alice at gaudon dot pro>
# Contributor: Benjamin Klettbach <b dot klettbach at gmail dot com >
# Contributor: Jonathan Steel <jsteel at archlinux.org>
# Contributor: ArcticVanguard <LideEmily at gmail dot com>
# Contributor: ledti <antergist at gmail dot com>

pkgname=obs-studio-browser
pkgver=30.1.2
pkgrel=2
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
  "libdatachannel"
  "libxcomposite"
  "libxdamage"
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
  0001-obs-ffmpeg-Fix-incompatible-pointer-types-with-FFmpe.patch
)
sha256sums=('0390743a85c3294abdb73ddf7d5d60354b5283f77cc9680026b2641600ae5384'
            'f4356ddabd4b54662f685ec88432e2830cdeb1904665d14c64d2daa3ea7d254e')

prepare() {
  cd $pkgname
  git submodule update --init --recursive
  patch -Np1 <"$srcdir"/0001-obs-ffmpeg-Fix-incompatible-pointer-types-with-FFmpe.patch
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
    -DENABLE_WEBRTC=ON \
    -DOBS_VERSION_OVERRIDE="$pkgver-$pkgrel" \
    -Wno-dev

  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}

# vim: ts=2:sw=2:expandtab
