pkgname=megasync
pkgver=2.0.0
pkgrel=1
pkgdesc="Sync your files to your Mega account. Official app"
arch=('x86_64')
url="http://mega.co.nz"
license=('custom:The Clarified Artistic License')
depends=('openssl' 'c-ares' 'libgcrypt' 'crypto++' 'qt' 'libpng' 'sqlite')
source=("https://mega.co.nz/linux/MEGAsync/Debian_7.0/amd64/${pkgname}_${pkgver}_amd64.deb")
md5sums=('a96197054f4c4a9fbc74185704a34c94')

install="${pkgname}.install"
options=(!strip)

package() {
	cd "${srcdir}"
	pwd
	tar -xzf data.tar.gz -C ${pkgdir}
	rm -r ${pkgdir}/usr/share/doc
	mkdir -p ${pkgdir}/usr/lib
	ln -s /usr/lib/libcryptopp.so ${pkgdir}/usr/lib/libcrypto++.so.9
}
