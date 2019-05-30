# Maintainer: Rickie Kerndt <kerndtr@kerndt.com>
# Maintainer: Donald Webster (fryfrog@gmail.com)

pkgname=unifi-video
pkgver=3.10.3
pkgrel=1
pkgdesc="Centralized management system for Ubiquiti UniFi Surveillance Cameras"
arch=('x86_64')
url="https://www.ubnt.com/"
license=('custom')
depends=('mongodb' 'java-runtime>=8' 'java-runtime<9' 'java-jsvc' 'lsb-release')
conflicts=('unifi-video-beta')
install=unifi-video.install
source=("${pkgname}-${pkgver}.deb::https://dl.ubnt.com/firmwares/ufv/v${pkgver}/${pkgname}.Ubuntu18.04_amd64.v${pkgver}.deb"
        'unifi-video.service'
        'unifi-video.sysusers'
        'unifi-video.tmpfiles'
        'unifi-video.patch')

sha256sums=('36b1520c64672fe9843d5352ba86408f138895041203b56234cd8290e102f911'
            '9df948b046347c25e7c83e4837284ef63d9f8d3f28daa20a6c36e203e3ebfdb3'
            '90fb2f826a70d3b7815cd6a2253c2af6754c17504be28ef92ee223bd02093730'
            'c31918e3ef0eb55f44639af0ae5db029654230b84d5ae0c55c18fbb2c80dfc70'
            'f639b93bbee689d7864533628eac4fe3fa1dd9227c8db63ae2f484473ce3e2d3')

            
package() {
    tar xf "${srcdir}/data.tar.gz" -C "${pkgdir}"/
    rm -r "${pkgdir}/etc" # removes init.d and sudoers files don't want to overwrite
    mv "${pkgdir}/usr/sbin" "${pkgdir}/usr/bin"
    chmod +x ${pkgdir}/usr/bin/unifi-video ${pkgdir}/usr/lib/unifi-video/bin/ubnt.* ${pkgdir}/usr/lib/unifi-video/bin/evo*

    cd "${pkgdir}/usr/bin"
    patch -N < "${srcdir}/unifi-video.patch"

    install -D -m 644 "${srcdir}/unifi-video.service" "${pkgdir}/usr/lib/systemd/system/unifi-video.service"
    install -D -m 644 "${srcdir}/unifi-video.sysusers" "${pkgdir}/usr/lib/sysusers.d/unifi-video.conf"
    install -D -m 644 "${srcdir}/unifi-video.tmpfiles" "${pkgdir}/usr/lib/tmpfiles.d/unifi-video.conf"
}
