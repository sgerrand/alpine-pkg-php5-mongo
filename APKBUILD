# Contributor: Sasha Gerrand <alpine-pkgs@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkgs@sgerrand.com>
pkgname=php5-mongo
_pkgrealname=mongo
_pkgsrcname=mongo-php-driver-legacy
pkgver=1.6.14
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

md5sums="d76bd379135d2d9269c43be0406d050b  php5-mongo-1.6.14.tar.gz"
sha256sums="4c64c53f334760f18861935bfa4b695c51c662e64dbedfef94e908974bf06aca  php5-mongo-1.6.14.tar.gz"
sha512sums="3ffb0f181141467894f0315ec1536bb14fbda9861e45ef93802366bc907972b48727f5bef9fb8a8d121743b43036782a225e0a034a5d97c471b3188dbe57e01b  php5-mongo-1.6.14.tar.gz"
