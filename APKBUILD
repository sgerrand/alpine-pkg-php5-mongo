# Contributor: Sasha Gerrand <alpine-pkgs@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkgs@sgerrand.com>
pkgname=php5-mongo
_pkgrealname=mongo
_pkgsrcname=mongo-php-driver-legacy
pkgver=1.6.15
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

sha512sums="afd92669c410d58c99e3e6d9ad776552b6161efbcfff69768029eab2bba158be9cd96d69acb7464d502051bbc28192dee20e4624f5d42ea7f6b2e613f1b46bf9  php5-mongo-1.6.15.tar.gz"
