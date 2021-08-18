# Maintainer: nArno <aquedesin@gmail.com>
pkgname=xf86-video-fbturbo
pkgver=0.4.0
pkgrel=1
pkgdesc="video driver optimized for the devices powered by the Allwinner SoC"
url="https://github.com/ssvb/xf86-video-fbturbo"
arch="all"
license="custom"
subpackages="$pkgname-doc"
makedepends="xorg-server-dev libxi-dev fontsproto randrproto videoproto renderproto autoconf automake util-macros libtool"

source="$pkgname-$pkgver.tar.gz::https://github.com/ssvb/xf86-video-fbturbo/archive/refs/tags/$pkgver.tar.gz"

prepare() {
	default_prepare
	cd src
	for p in $(find "$startdir" -name '*.patch'); do patch < $p; done
}

build() {
	export CFLAGS="$CFLAGS -Wno-implicit-function-declaration -Wno-int-conversion -Wno-discarded-qualifiers"
	export LDFLAGS="$LDFLAGS -Wl,-z,lazy"
	autoreconf -vi
	./configure \
		--build=$CBUILD \
		--host=$CHOST \
		--prefix=/usr
	make
}

package() {
	make DESTDIR="$pkgdir" install
	install -Dm644 COPYING "$pkgdir"/usr/share/licenses/$pkgname/COPYING
}
sha512sums="
9675f7df7811cc4607baefeb6cfef93df618a2995675f5e1b316b4f703da758b04f909d887a6c9d0d7f274a215036864ea712fcf76d50f5084321ea3dbd3e23c  xf86-video-fbturbo-0.4.0.tar.gz
"
