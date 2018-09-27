# Contributor: Yoyo Fernández, https://github.com/yoyo308
# Contributor: Pablo Cesar Agudelo Castro, https://github.com/pcagudelo
# Contributor: Gabriel, https://github.com/Gabrielgtx
# Contributor: Francisco Josué Morazán Arriola, https://github.com/fjmorazan
# Contributor: abucodonosor, https://github.com/abucodonosor
# Contributor: Benjamin VAUDOUR, https://github.com/bvaudour
# Contributor: md2z34, https://github.com/md2z34
# Contributor: Gunther Strube, https://github.com/bits4fun

pkgname=megasync
pkgver=3.6.6.0
pkgrel=1
_sdkver=3.3.9
pkgdesc="Sync your files to your Mega account. Official app."
url='https://github.com/meganz/megasync'
arch=('x86_64')
license=('custom:MEGA LIMITED CODE REVIEW LICENCE')
depends=('qt5-base' 'qt5-svg' 'c-ares' 'curl' 'crypto++' 'hicolor-icon-theme' 'libuv' 'libsodium' 'mediainfolib')
makedepends=('qt5-tools' 'swig' 'doxygen')
source=("https://github.com/meganz/MEGAsync/archive/v${pkgver}_Linux.tar.gz"
        "https://github.com/meganz/sdk/archive/v${_sdkver}.tar.gz")
sha256sums=('377a0b77b2506ebe0052d6366c3b5b74c3012cb4938e4df5e4b003677073f5fa'
            '522b63bf2f2d1eeff0644ef106fff94fcd4f6a844e01539cc6cfb30d16463dba')

prepare() {
    rm -rf MEGAsync-${pkgver}_Linux/src/MEGASync/mega
    mv sdk-${_sdkver} MEGAsync-${pkgver}_Linux/src/MEGASync/mega

    cd "MEGAsync-${pkgver}_Linux/src/MEGASync/mega"
    ./autogen.sh
    ./configure \
        --prefix=/usr \
        --disable-examples \
        --disable-java \
        --disable-php \
        --disable-python \
        --enable-chat \
        --enable-gcc-hardening \
        --with-cares \
        --with-cryptopp \
        --with-curl \
        --with-sodium \
        --with-sqlite \
        --with-zlib \
        --without-freeimage \
        --without-termcap \
    --without-ffmpeg
}

build() {
    cd "${srcdir}/MEGAsync-${pkgver}_Linux/src"
    qmake-qt5 CONFIG+="release" MEGA.pro
    lrelease-qt5 MEGASync/MEGASync.pro
    make
}

package() {
    cd "MEGAsync-${pkgver}_Linux"
    install -Dm 644 LICENCE.md "${pkgdir}/usr/share/licenses/megasync/LICENCE.md"
    install -Dm 644 installer/terms.txt "${pkgdir}/usr/share/licenses/megasync/terms.txt"

    cd src/MEGASync
    install -Dm 755 megasync "${pkgdir}/usr/bin/megasync"

    cd platform/linux/data
    install -Dm 644 megasync.desktop "${pkgdir}/usr/share/applications/megasync.desktop"

    cd icons/hicolor
    for size in 16x16 32x32 48x48 128x128 256x256
    do
        install -Dm 644 "${size}/apps/mega.png" "${pkgdir}/usr/share/icons/hicolor/${size}/apps/mega.png"
    done
}
