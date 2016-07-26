pkgname=megasync
pkgver=2.9.8
pkgrel=1
pkgdesc="Sync your files to your Mega account. Official app."
url='http://mega.nz'
arch=('x86_64')
license=('custom:MEGA')
depends=('qt5-base' 'c-ares' 'curl' 'crypto++' 'hicolor-icon-theme' 'libuv' 'libsodium')
makedepends=('qt5-tools')
source=("https://mega.nz/linux/MEGAsync/Debian_8.0/${pkgname}_${pkgver}.orig.tar.gz")
md5sums=('2f69968f02096bec83b8967c8102e342')

prepare() {
	export QT_SELECT=5
	cd "${pkgname}-${pkgver}"/MEGASync/mega
	./autogen.sh
	./configure --disable-examples \
	            --disable-posix-threads \
	            --without-freeimage \
	            --without-sodium
}

build() {
	cd "${pkgname}-${pkgver}"
	/usr/lib/qt5/bin/qmake CONFIG+=release MEGA.pro
	/usr/lib/qt5/bin/lrelease MEGASync/MEGASync.pro
	make
}

package() {
	cd "${pkgname}-${pkgver}"
    	make INSTALL_ROOT="${pkgdir}" install
    	install -Dm644 debian.copyright "$pkgdir"/usr/share/licenses/megasync/license
    
    	cd "MEGASync"
	install -Dm755 megasync "$pkgdir"/usr/bin/megasync
}
