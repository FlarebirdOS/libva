pkgname=libva
pkgver=2.22.0
pkgrel=2
pkgdesc="Video Acceleration (VA) API for Linux"
arch=('x86_64')
url="https://01.org/linuxmedia/vaapi"
license=('MIT')
depends=(
    'libdrm'
    'libx11'
    'libxext'
    'libxfixes'
    'mesa'
    'wayland'
)
makedepends=(
    'libglvnd'
    'meson'
)
backup=(etc/libva.conf)
source=(https://github.com/intel/libva/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha256sums=(467c418c2640a178c6baad5be2e00d569842123763b80507721ab87eb7af8735)

build() {
    cd ${pkgname}-${pkgver}

    local meson_args=(
    )

    CFLAGS+=" -DENABLE_VA_MESSAGING" # Option missing

    ${meson_options} "${meson_args[@]}"

    ${meson_build}
}

package() {
    cd ${pkgname}-${pkgver}

    ${meson_install} ${pkgdir}

    install -Dm 644 /dev/stdin ${pkgdir}/etc/libva.conf <<END
LIBVA_MESSAGING_LEVEL=1
END
}
