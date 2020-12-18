# Maintainer: Alice Gaudon <alice at gaudon dot pro>
# Contributor: Benjamin Klettbach <b dot klettbach at gmail dot com >
# Contributor: Jonathan Steel <jsteel at archlinux.org>
# Contributor: ArcticVanguard <LideEmily at gmail dot com>
# Contributor: ledti <antergist at gmail dot com>

pkgname=obs-studio-browser
pkgver=26.1.0
pkgrel=1
pkgdesc="Free and open source software for video recording and live streaming. Built with the browser plugin."
arch=("i686" "x86_64")
url="https://github.com/obsproject/obs-studio"
license=("GPL2")
depends=(
	"curl"
	"ffmpeg"
	"gtk-update-icon-cache"
	"jansson"
	"libxinerama"
	"libxkbcommon-x11"
	"qt5-x11extras"
)
makedepends=(
	"cef-minimal"
	"cmake"
	"git"
	"jack"
	"libfdk-aac"
	"libxcomposite"
	"luajit"
	"python"
	"swig"
	"vlc"
	"x264"
)
optdepends=(
	"libfdk-aac: FDK AAC codec support"
	"libxcomposite: XComposite capture support"
	"jack: JACK Support"
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
	"git+https://github.com/obsproject/obs-browser.git"
)
sha256sums=('SKIP' 'SKIP')

prepare() {
	cd $pkgname
	git config submodule.plugins/obs-browser.url $srcdir/obs-browser
	git submodule update
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
		-DOBS_VERSION_OVERRIDE=$pkgver ..

	make
}

package() {
	cd $pkgname/build

	make install DESTDIR="$pkgdir"
}

# vim: ts=2:sw=2:expandtab
