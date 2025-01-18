# Maintainer: Knut Ahlers <knut at ahlers dot me>
# Contributor: Alice Gaudon <alice at gaudon dot pro>
# Contributor: Benjamin Klettbach <b dot klettbach at gmail dot com >
# Contributor: Jonathan Steel <jsteel at archlinux.org>
# Contributor: ArcticVanguard <LideEmily at gmail dot com>
# Contributor: ledti <antergist at gmail dot com>

pkgname=obs-studio-browser
pkgver=31.0.1
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
  "uthash"
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
  "nv-codec-headers.tar.gz::https://github.com/FFmpeg/nv-codec-headers/releases/download/n12.1.14.0/nv-codec-headers-12.1.14.0.tar.gz"
)
# XXX nv-codec-headers are kept back at version n12.1.14.0 due to OBS not supporting any newer version
sha256sums=('6a06481b64bf499e2000d5fe2da42a81818f4b2affb4a5bb46a62cfefd49ce92'
            '62b30ab37e4e9be0d0c5b37b8fee4b094e38e570984d56e1135a6b6c2c164c9f')

prepare() {
  cd $pkgname
  git submodule update --init --recursive
}

build() {
  # Mitigate `error: ‘sample_fmts’ is deprecated` in v31.x
  export CFLAGS+=" -Wno-error=deprecated-declarations"

  cmake -B build -S $pkgname \
    -DFFnvcodec_INCLUDE_DIR="nv-codec-headers-12.1.14.0/include/" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DENABLE_BROWSER=ON \
    -DENABLE_VST=ON \
    -DENABLE_VLC=OFF \
    -DENABLE_NEW_MPEGTS_OUTPUT=OFF \
    -DENABLE_AJA=OFF \
    -DENABLE_JACK=ON \
    -DENABLE_LIBFDK=ON \
    -DENABLE_WEBRTC=ON \
    -DOBS_VERSION_OVERRIDE="$pkgver-$pkgrel" \
    -DCALM_DEPRECATION=ON \
    -DCEF_ROOT_DIR="/opt/cef" \
    -Wno-dev

  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}

# vim: ts=2:sw=2:expandtab
