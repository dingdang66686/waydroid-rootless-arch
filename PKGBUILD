# Maintainer: dingdang66686
pkgname=waydroid
pkgver=1.6.3
pkgrel=3
pkgdesc="Rootless podman backend for Waydroid"
arch=('x86_64')
url="https://github.com/dingdang66686/waydroid-rootless"
license=('GPL-3.0-only')
depends=('python' 'python-gbinder>=1.3.0' 'python-gobject' 'python-dbus' 'gtk3' 'pulse-native-provider' 'podman' 'crun' 'passt')
optdepends=('waydroid-image: local Android images' 'python-pyclip: clipboard manager support')
provides=('waydroid-rootless')
conflicts=('waydroid-rootless')
replaces=('waydroid-rootless')
install="$pkgname.install"
_commit=a27084d8c244079ffa64d6fdf1b75ff6b43af744
source=("$pkgname-$pkgver.tar.gz::https://github.com/dingdang66686/waydroid-rootless/archive/$_commit.tar.gz")
sha256sums=('7da1d75410820b9bf1283fdd63ccc8ffc08592afb9739ec7199933775bc1a776')

package() {
  local src="$srcdir/waydroid-rootless-$_commit"

  ( cd "$src" && make install DESTDIR="$pkgdir" USE_SYSTEMD=0 USE_NFTABLES=0 )

  rm -f "$pkgdir/usr/bin/waydroid"
  install -Dm755 "$startdir/waydroid" "$pkgdir/usr/bin/waydroid"
  install -Dm644 "$startdir/waydroid.service" \
    "$pkgdir/usr/lib/systemd/user/waydroid.service"

  install -Dm644 "$src/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 "$src/README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 "$src/ROOTLESS.md" "$pkgdir/usr/share/doc/$pkgname/ROOTLESS.md"

  find "$pkgdir/usr/lib/waydroid" -name '__pycache__' -type d -prune -exec rm -rf {} +
}
