pkgname=vanta
pkgver=2.15.0
pkgrel=1
pkgdesc="Vanta Device Monitor"
arch=('x86_64')
url="https://www.vanta.com/"
depends=('systemd')
license=('custom:vanta')
source=("https://agent-downloads.vanta.com/targets/versions/${pkgver}/vanta-amd64.deb"
        'vanta.service.patch')
sha256sums=('02ba826388dee61aaf3e97f4bec61896620bc616754e7d107c0efcc79abd43a0'
            '43b2806cf7a94dc196a4809dfaa9551c11c1e37bad4b5490d548b426b337b46e')

prepare() {
    mkdir -p data
    tar -C data -xzf data.tar.gz
    cd data
    patch -p1 -i ../vanta.service.patch
}

package() {
    install -Dm644 data/usr/lib/systemd/system/vanta.service "$pkgdir"/usr/lib/systemd/system/vanta.service
    install -Dm644 data/usr/share/doc/vanta/changelog.gz "$pkgdir"/usr/share/doc/vanta/changelog.gz
    install -Dm644 data/var/vanta/cert.pem "$pkgdir"/var/vanta/cert.pem
    install -Dm755 data/var/vanta/launcher "$pkgdir"/var/vanta/launcher
    install -Dm755 data/var/vanta/metalauncher "$pkgdir"/var/vanta/metalauncher
    install -Dm755 data/var/vanta/osqueryd "$pkgdir"/var/vanta/osqueryd
    install -Dm755 data/var/vanta/osquery-vanta.ext "$pkgdir"/var/vanta/osquery-vanta.ext
    install -Dm755 data/var/vanta/vanta-cli "$pkgdir"/var/vanta/vanta-cli
    mkdir -pm755 "$pkgdir"/usr/bin
    ln -s --relative "$pkgdir"/var/vanta/vanta-cli "$pkgdir"/usr/bin/vanta-cli
}
