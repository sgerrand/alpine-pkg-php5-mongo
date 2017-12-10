# Contributor: Sasha Gerrand <alpine-pkgs@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkgs@sgerrand.com>
pkgname=php5-mongo
_pkgrealname=mongo
_pkgsrcname=mongo-php-driver-legacy
pkgver=1.6.16
pkgrel=0
pkgdesc="MongoDB driver for PHP 5"
url="https://github.com/mongodb/$_pkgsrcname"
arch="all"
license="Apache-2"
depends="php5-cli"
depends_dev=""
makedepends="$depends_dev autoconf cyrus-sasl-dev openssl-dev php5-dev"
install=""
subpackages="$pkgname-dev $pkgname-doc"
source="$pkgname-$pkgver.tar.gz::https://github.com/mongodb/$_pkgsrcname/archive/$pkgver.tar.gz"

builddir="$srcdir/$_pkgsrcname-$pkgver"
build() {
	cd "$builddir"
	phpize || return 1
	./configure --build=$CBUILD \
		--host=$CHOST \
		--prefix=/usr \
		--sysconfdir=/etc/php5 \
		--localstatedir=/var \
		--disable-static \
		--enable-shared \
		--mandir=/usr/share/man \
		--enable-mongo \
		--with-mongo-sasl \
	|| return 1
	make || return 1
}

package() {
	cd "$builddir"
	make INSTALL_ROOT="$pkgdir/" install || return 1
	install -d "$pkgdir"/etc/php5/conf.d || return 1
	echo "extension=$_pkgrealname.so" > "$pkgdir"/etc/php5/conf.d/$_pkgrealname.ini
}

dev() {
	mkdir -p "$subpkgdir"
	default_dev
	cd "$builddir"
}

doc() {
	mkdir -p "$subpkgdir"
	default_doc
	cd "$builddir"
	for _doc in CONTRIBUTING.md LICENSE.md README.md; do
		install -Dm644 $_doc "$subpkgdir"/usr/share/doc/$pkgname/$_doc || return 1
	done
}

sha512sums="f5713dd2494315e4f13d7138d18b8041fe273132f09cf87372d2bb8ebea2a72783dd1bab17d9ad48f2491d2868206062791a381a3e6425dfa9e7963fb755041f  php5-mongo-1.6.16.tar.gz"
