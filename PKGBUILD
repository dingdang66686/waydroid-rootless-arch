# Maintainer: dingdang66686
pkgname=waydroid-rootless
pkgver=1.6.3
pkgrel=1
pkgdesc="Rootless podman backend for Waydroid"
arch=('x86_64')
url="https://github.com/dingdang66686/waydroid-rootless"
license=('GPL-3.0-only')
depends=('waydroid' 'podman' 'crun' 'passt')
install="$pkgname.install"
_commit=2b2efe5dc0a0ea40ba033f4635a985d4d8a24189
source=("$pkgname-$pkgver.tar.gz::https://github.com/dingdang66686/waydroid-rootless/archive/$_commit.tar.gz")
sha256sums=('67a67999db8129f73d0afe2cbe0cb06b028fc8c8c93f4bc538daa8fc6331a7bc')

package() {
  local src="$srcdir/waydroid-rootless-$_commit"
  install -d "$pkgdir/usr/lib/$pkgname"
  install -Dm644 "$src/waydroid.py" "$pkgdir/usr/lib/$pkgname/waydroid.py"
  cp -a "$src/tools" "$pkgdir/usr/lib/$pkgname/"
  find "$pkgdir/usr/lib/$pkgname" -name '__pycache__' -type d -prune -exec rm -rf {} +

  install -Dm755 "$startdir/waydroid-rootless" "$pkgdir/usr/bin/waydroid-rootless"
  install -Dm644 "$startdir/waydroid-rootless.service" \
    "$pkgdir/usr/lib/systemd/user/waydroid-rootless.service"

  install -d "$pkgdir/usr/local/bin"
  ln -s /usr/bin/waydroid-rootless "$pkgdir/usr/local/bin/waydroid"

  install -Dm644 "$src/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 "$src/README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 "$src/ROOTLESS.md" "$pkgdir/usr/share/doc/$pkgname/ROOTLESS.md"
}
