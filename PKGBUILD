pkgname=megasync
pkgver=3.5.3
pkgrel=1
pkgdesc="Sync your files to your Mega account. Official app."
url='http://mega.nz'
arch=('x86_64')
license=('custom:MEGA')
depends=('qt5-base' 'c-ares' 'curl' 'crypto++' 'hicolor-icon-theme' 'libuv' 'libsodium')
makedepends=('qt5-tools')
source=("https://mega.nz/linux/MEGAsync/Debian_8.0/${pkgname}_${pkgver}.orig.tar.gz")
md5sums=('5c910eea1ca1c44aea81e5dc81338a09')

prepare() {
    cd "${pkgname}-${pkgver}/MEGASync/mega"
    ./clean.sh
    ./autogen.sh
    ./configure \
    --disable-silent-rules \
    --disable-curl-checks \
    --disable-megaapi \
    --with-cryptopp \
    --with-sodium \
    --with-zlib \
    --with-sqlite \
    --with-cares \
    --with-curl \
    --without-freeimage \
    --without-termcap \
    --disable-posix-threads \
    --disable-examples \
    --prefix=/usr
}

build() {
    cd "${pkgname}-${pkgver}"
    qmake-qt5 CONFIG+="release" MEGA.pro
    lrelease-qt5 MEGASync/MEGASync.pro
    make
}

package() {
    cd "${pkgname}-${pkgver}"
    make INSTALL_ROOT="${pkgdir}" install
    install -Dm644 debian.copyright "${pkgdir}"/usr/share/licenses/megasync/license
    
    cd "MEGASync"
    install -Dm755 megasync "${pkgdir}"/usr/bin/megasync
}
