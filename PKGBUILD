pkgname=megasync
pkgver=2.1.1
pkgrel=1
pkgdesc="Sync your files to your Mega account. Official app"
arch=('x86_64')
url="http://mega.co.nz"
license=('custom:The Clarified Artistic License')
depends=('openssl' 'c-ares' 'libgcrypt' 'crypto++' 'qt' 'libpng' 'sqlite')
source=("https://mega.co.nz/linux/MEGAsync/Debian_8.0/amd64/${pkgname}_${pkgver}_amd64.deb")
md5sums=('cee950ece38f6e920b919309806aa6c1')

install="${pkgname}.install"
options=(!strip)

package() {
	cd "${srcdir}"
	pwd
	tar -xJf data.tar.xz -C ${pkgdir}
	rm -r ${pkgdir}/usr/share/doc
	mkdir -p ${pkgdir}/usr/lib
	ln -s /usr/lib/libcryptopp.so ${pkgdir}/usr/lib/libcrypto++.so.9
}
