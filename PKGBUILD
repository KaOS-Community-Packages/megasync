pkgname=megasync
pkgver=2.9.1
pkgrel=1
pkgdesc="Sync your files to your Mega account. Official app."
url='http://mega.nz'
arch=('x86_64')
license=('custom:MEGA')
depends=('qt5-base' 'c-ares' 'curl' 'crypto++' 'hicolor-icon-theme' 'libuv')
makedepends=('git' 'qt5-tools')
source=("git+https://github.com/meganz/MEGAsync.git#tag=v${pkgver//./_}_0_Linux")
md5sums=('SKIP')

prepare() {
	cd MEGAsync
	sed 's|git@github.com:meganz/sdk.git|https://github.com/meganz/sdk.git|g' -i .gitmodules
	git submodule update --init --recursive

	cd src/MEGASync/mega
	./autogen.sh
	./configure --disable-examples \
	            --disable-posix-threads \
	            --without-freeimage \
	            --without-sodium
}

build() {
	cd MEGAsync/src
	/usr/lib/qt5/bin/qmake CONFIG+=release MEGA.pro
	/usr/lib/qt5/bin/lrelease MEGASync/MEGASync.pro
	make
}

package() {
	cd MEGAsync
	install -Dm644 LICENCE.md "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

	cd src/MEGASync
	install -Dm755 megasync "${pkgdir}/usr/bin/megasync"

	cd platform/linux/data
	install -Dm644 megasync.desktop "${pkgdir}/usr/share/applications/megasync.desktop"
	cp -r icons "${pkgdir}/usr/share"
}
