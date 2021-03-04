# Maintainer: Chocobo1 <chocobo1 AT archlinux DOT net>

pkgname=libupnp-git
pkgver=1.14.1.r0.g52906b2
pkgrel=1
pkgdesc="Portable open source UPnP development kit"
arch=('i686' 'x86_64')
url="https://pupnp.sourceforge.io/"
license=('BSD')
depends=('glibc')
makedepends=('git')
provides=('libupnp' 'libixml.so=11-64' 'libupnp.so=17-64')
conflicts=('libupnp')
options=('staticlibs')
source=("git+https://github.com/pupnp/pupnp.git#tag=release-1.14.1")
sha256sums=('SKIP')


pkgver() {
  cd "pupnp"

  git describe --long --tags | sed 's/^release-//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "pupnp"
  git cherry-pick -n 066c4ed35518b9cfc4c156649d032e24029ac0ec

  ./bootstrap
  ./configure \
    --prefix="/usr" \
    --enable-reuseaddr
  make
}

check() {
  cd "pupnp"

  make check
}

package() {
  cd "pupnp"

  make DESTDIR="$pkgdir" install
  install -Dm644 "COPYING" -t "$pkgdir/usr/share/licenses/libupnp"
}
