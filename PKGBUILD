pkgname=megasync
pkgver=3.6.7.0
pkgrel=1
_sdkver=3.4.0
pkgdesc="Easy automated syncing between your computers and your MEGA cloud drive"
url='http://mega.nz/#sync'
arch=('x86_64')
license=('custom:MEGA LIMITED CODE REVIEW LICENCE')
depends=('glibc>=2.27' 'gcc-libs' 'qt5-base>=5.11' 'qt5-tools>=5.11' 'icu>=61.1' 'sqlite' 'openssl' 'zlib' 'qt5-svg>=5.11' 'bzip2' 'xz' 'c-ares' 'curl' 'crypto++' 'hicolor-icon-theme' 'libuv' 'libsodium' 'mediainfolib')
makedepends=('unzip' 'wget' 'ca-certificates' 'qt5-tools' 'bzip2' 'xz')
source=("https://github.com/meganz/MEGAsync/archive/v${pkgver}_Linux.tar.gz"
        "https://github.com/meganz/sdk/archive/v${_sdkver}.tar.gz")
sha256sums=('2c11747db5aab4149a1fd01371ffa914970491ea70b71d7bcbec3475c0e6507f'
            '0a13576ac3efb741dd67c43698a99ff1ff721cc806f28908cc0bdba808d4988b')

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
    
    mkdir -p ${pkgdir}/etc/sysctl.d/
    echo "fs.inotify.max_user_watches = 524288" > ${pkgdir}/etc/sysctl.d/100-megasync-inotify-limit.conf    
}
