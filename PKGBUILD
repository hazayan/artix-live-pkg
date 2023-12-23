# Maintainer: artoo <artoo@artixlinux.org>
# Contributor: nous <nous@artixlinux.org>
# Contributor: dudemanguy <dudemanguy@artixlinux.org>

pkgbase=artix-live
pkgname=('artix-live-base'
        'artix-live-openrc'
        'artix-live-runit'
        'artix-live-s6'
        'artix-live-dinit'
        'artix-grub-live')
pkgver=2023.12
pkgrel=4
pkgdesc='Artix live session'
arch=('any')
url="https://gitea.artixlinux.org/artix/artix-live"
license=('GPL')
makedepends=('git' 'bash' 'artools-base')
_commit=74f8284a74d473c9931007fd78d99da0e3587465 # 0.14
source=("git+$url.git#commit=$_commit")
sha256sums=('SKIP')
#
# pkgver() {
#     date +%Y.%m
# }

build() {
    make -C "${pkgbase}"
}

package_artix-live-base() {
    pkgdesc='Artix live base scripts'
    depends=('artools-base' 'bash')

    make -C "${pkgbase}" DESTDIR=${pkgdir} install_base install_xdg
}

package_artix-live-openrc() {
    pkgdesc='Artix live openrc init scripts'
    depends=('artix-live-base')

    make -C "${pkgbase}" DESTDIR=${pkgdir} install_rc

    install -d "${pkgdir}"/etc/runlevels/default
    ln -sf /etc/init.d/pacman-init "${pkgdir}"/etc/runlevels/default/pacman-init
    ln -sf /etc/init.d/artix-live "${pkgdir}"/etc/runlevels/default/artix-live
}

package_artix-live-runit() {
    pkgdesc='Artix live runit init scripts'
    depends=('artix-live-base')

    make -C "${pkgbase}" DESTDIR=${pkgdir} install_runit

    install -d "${pkgdir}"/etc/runit/runsvdir/default
    ln -sf /etc/runit/sv/pacman-init "${pkgdir}"/etc/runit/runsvdir/default/pacman-init
}

package_artix-live-s6() {
    pkgdesc='Artix live s6 init scripts'
    depends=('artix-live-base')

    make -C "${pkgbase}" DESTDIR=${pkgdir} install_s6
}

package_artix-live-dinit() {
    pkgdesc='Artix live dinit init scripts'
    depends=('artix-live-base')

    make -C "${pkgbase}" DESTDIR=${pkgdir} install_dinit
}

package_artix-grub-live() {
    pkgdesc='Artix grub live'

    make -C "${pkgbase}" PREFIX=/usr DESTDIR=${pkgdir} install_grub
}
