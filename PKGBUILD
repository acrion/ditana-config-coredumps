# Maintainer: Stefan Zipproth <s.zipproth@ditana.org>
# Author: Stefan Zipproth <s.zipproth@ditana.org>

pkgname=ditana-config-coredumps
pkgver=1.01
pkgrel=1
pkgdesc="Deactivate coredumps (temporary activation is possible)."
arch=(any)
url="https://github.com/acrion/ditana-config-coredumps"
license=('AGPL-3.0-or-later')
conflicts=()
depends=(systemd)
makedepends=()
source=(
    '50-ditana.conf'
    '50-ditana-limits.conf'
)
sha256sums=(
    'SKIP'
    'SKIP'
)

package() {
    install -Dm644 "$srcdir/50-ditana.conf"        "$pkgdir/etc/security/limits.d/50-ditana.conf"
    install -Dm644 "$srcdir/50-ditana-limits.conf" "$pkgdir/etc/systemd/system.conf.d/50-ditana-limits.conf"
}
