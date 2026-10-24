# Maintainer: dingdang66686
pkgname=waydroid
pkgver=1.6.3
pkgrel=4
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
_commit=8bc9aa6e01bd7c430b7562abddf474b329854cb4
source=("$pkgname-$pkgver.tar.gz::https://github.com/dingdang66686/waydroid-rootless/archive/$_commit.tar.gz")
sha256sums=('5b77ae4ca30559d4215f77af11ab7f520d48e66ed9be6d032ebb552a576bb78f')

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
