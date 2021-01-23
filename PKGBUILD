# Maintainer: Rin Cat <me@rin.cat>
# Contributor: Ryan Farley <ryan.farley@gmx.com>

pkgname=rtl88x2bu-dkms-git
_pkgbase=rtl88x2bu
pkgver=5.8.7.1.r111.afc917d
_pkgver=5.8.7.1
pkgrel=1
pkgdesc="Kernel module for Realtek rtl88x2bu WiFi chipset"
arch=('i686' 'x86_64' 'armv7l')
url="https://github.com/RinCat/RTL88x2BU-Linux-Driver"
license=('GPL2')
depends=('dkms' 'bc')
makedepends=('git')
source=("git+https://github.com/RinCat/RTL88x2BU-Linux-Driver.git"
	"set-arm-arch.patch")
sha256sums=('SKIP'
            '7445475f6f021806d873deafa8a95c2822df46296674a744de7a24871c8aa0c5')

pkgver() {
    cd "${srcdir}/RTL88x2BU-Linux-Driver"
    printf '%s.r%s.%s' "${_pkgver}" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    echo $CARCH
    cd "${srcdir}/RTL88x2BU-Linux-Driver"
    if [ "$CARCH" = "armv7h" ]; then
    	patch --forward --strip=1 --input="${srcdir}/set-arm-arch.patch"
    fi
}

package() {
    cd "${srcdir}/RTL88x2BU-Linux-Driver"
    mkdir -p "${pkgdir}/usr/src/${_pkgbase}-${pkgver}"
    cp -pr * "${pkgdir}/usr/src/${_pkgbase}-${pkgver}"
    install -Dm644 dkms.conf "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/dkms.conf"
    sed -e "s/@PKGVER@/${pkgver}/" -i "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/dkms.conf"
}
