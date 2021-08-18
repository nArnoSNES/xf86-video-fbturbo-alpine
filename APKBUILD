# Maintainer: nArno <aquedesin@gmail.com>
pkgname=xf86-video-fbturbo
pkgver=0.4.0
pkgrel=4
pkgdesc="video driver optimized for the devices powered by the Allwinner SoC"
url="https://github.com/ssvb/xf86-video-fbturbo"
arch="all"
license="custom"
subpackages="$pkgname-doc"
depends=
makedepends="xorg-server-dev libxi-dev fontsproto randrproto videoproto renderproto autoconf automake util-macros libtool"

source="$pkgname-$pkgver.tar.gz::https://github.com/ssvb/$pkgname/archive/refs/tags/$pkgver.tar.gz"

_builddir="$srcdir"/$pkgname-$pkgver
prepare() {
	cd "$_builddir"/src
	for p in $(find "$startdir" -name '*.patch'); do patch < $p; done
}

build() {
	cd "$_builddir"
	export LDFLAGS="$LDFLAGS -Wl,-z,lazy"
	autoreconf -vi || return 1
	./configure \
		--build=$CBUILD \
		--host=$CHOST \
		--prefix=/usr \
		|| return 1
	make || return 1
}

package() {
	cd "$_builddir"
	make DESTDIR="$pkgdir" install || return 1
	install -Dm644 COPYING "$pkgdir"/usr/share/licenses/$pkgname/COPYING
}
sha512sums="
9675f7df7811cc4607baefeb6cfef93df618a2995675f5e1b316b4f703da758b04f909d887a6c9d0d7f274a215036864ea712fcf76d50f5084321ea3dbd3e23c  xf86-video-fbturbo-0.4.0.tar.gz
"
