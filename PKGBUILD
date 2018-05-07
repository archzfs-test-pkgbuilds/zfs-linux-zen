# Maintainer: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
# ! WARNING !
#
# The archzfs packages are kernel modules, so these PKGBUILDS will only work with the kernel package they target. In this
# case, the archzfs-linux-zen packages will only work with the default linux-zen package! To have a single PKGBUILD target many
# kernels would make for a cluttered PKGBUILD!
#
# If you have a custom kernel, you will need to change things in the PKGBUILDS. If you would like to have AUR or archzfs repo
# packages for your favorite kernel package built using the archzfs build tools, submit a request in the Issue tracker on the
# archzfs github page.
#
pkgbase="zfs-linux-zen"
pkgname=("zfs-linux-zen" "zfs-linux-zen-headers")

pkgver=0.7.8.4.16.7.1
pkgrel=1
makedepends=("linux-zen-headers=4.16.7-1" "spl-linux-zen-headers")
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("https://github.com/zfsonlinux/zfs/releases/download/zfs-0.7.8/zfs-0.7.8.tar.gz")
sha256sums=("70ba0edd72914d4bfc9a9426cf26725e955a9509acbddb6902efb9eebb35f150")
license=("CDDL")
depends=("kmod" "spl-linux-zen" "zfs-utils-common=0.7.8" "linux-zen=4.16.7-1")

build() {
    cd "${srcdir}/zfs-0.7.8"
    ./autogen.sh
    ./configure --prefix=/usr --sysconfdir=/etc --sbindir=/usr/bin --libdir=/usr/lib \
                --datadir=/usr/share --includedir=/usr/include --with-udevdir=/lib/udev \
                --libexecdir=/usr/lib/zfs-0.7.8 --with-config=kernel \
                --with-linux=/usr/lib/modules/4.16.7-1-zen/build \
                --with-linux-obj=/usr/lib/modules/4.16.7-1-zen/build
    make
}

package_zfs-linux-zen() {
    pkgdesc="Kernel modules for the Zettabyte File System."
    install=zfs.install
    provides=("zfs")
    groups=("archzfs-linux-zen")
    conflicts=('zfs-linux-zen-git')
    replaces=("zfs-git")
    cd "${srcdir}/zfs-0.7.8"
    make DESTDIR="${pkgdir}" install
    cp -r "${pkgdir}"/{lib,usr}
    rm -r "${pkgdir}"/lib
    # Remove src dir
    rm -r "${pkgdir}"/usr/src
}

package_zfs-linux-zen-headers() {
    pkgdesc="Kernel headers for the Zettabyte File System."
    conflicts=('zfs-archiso-linux-headers' 'zfs-archiso-linux-git-headers' 'zfs-linux-hardened-headers' 'zfs-linux-hardened-git-headers' 'zfs-linux-lts-headers' 'zfs-linux-lts-git-headers' 'zfs-linux-headers' 'zfs-linux-git-headers' 'zfs-linux-vfio-headers' 'zfs-linux-vfio-git-headers'  'zfs-linux-zen-git-headers' )
    cd "${srcdir}/zfs-0.7.8"
    make DESTDIR="${pkgdir}" install
    rm -r "${pkgdir}/lib"
    # Remove reference to ${srcdir}
    sed -i "s+${srcdir}++" ${pkgdir}/usr/src/zfs-*/4.16.7-1-zen/Module.symvers
}
