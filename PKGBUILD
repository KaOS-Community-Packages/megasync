pkgname=megasync
pkgver=2.3.1
pkgrel=1
pkgdesc="Sync your files to your Mega account. Official app"
arch=('x86_64')
url="http://mega.nz"
license=('custom:The Clarified Artistic License')
depends=('openssl' 'c-ares' 'libgcrypt' 'crypto++' 'qt' 'libpng' 'sqlite')
source=("https://mega.nz/linux/MEGAsync/Debian_8.0/amd64/${pkgname}_${pkgver}_amd64.deb")
md5sums=('959153db992a3a2353d7853f941db5d7')

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
