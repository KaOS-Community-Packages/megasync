pkgname=megasync
pkgver=4.0.2.0
pkgrel=1
_sdkver=3.4.8
pkgdesc="Easy automated syncing between your computers and your MEGA cloud drive"
url='http://mega.nz/#sync'
arch=('x86_64')
license=('custom:MEGA LIMITED CODE REVIEW LICENCE')
depends=('glibc>=2.27' 'gcc-libs' 'qt5-base>=5.11' 'qt5-tools>=5.11' 'icu>=61.1' 'sqlite' 'openssl>=1.1.1' 'zlib' 'qt5-svg>=5.11' 'bzip2' 'xz' 'c-ares' 'curl' 'crypto++' 'hicolor-icon-theme' 'libuv' 'libsodium' 'mediainfolib')
makedepends=('unzip' 'wget' 'ca-certificates' 'qt5-tools' 'bzip2' 'xz')
source=("https://github.com/meganz/MEGAsync/archive/v${pkgver}_Linux.tar.gz"
        "https://github.com/meganz/sdk/archive/v${_sdkver}.tar.gz")
sha256sums=('5153aa382f8fd2a518af90c98c4933e5d5df6810d1b2143a7ff1ae667458ae17'
            '26f89d7f253e821dd8c46a46a382e3664bc8398b4750c8703be0888c1c3b10a3')
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
