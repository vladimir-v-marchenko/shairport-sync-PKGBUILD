# Maintainer: Elia Cereda <eliacereda+arch at gmail dot com>

pkgname=shairport-sync-git
pkgver=2.4.1.r0.g808fbc8
pkgrel=1
pkgdesc='Emulates an AirPort Express for the purpose of streaming music from iTunes and compatible iPods and iPhones'
url='https://github.com/mikebrady/shairport-sync'
arch=(i686 x86_64 armv6h armv7h)
license=('custom')
backup=(etc/conf.d/shairport-sync)
install='shairport-sync.install'
depends=(alsa-lib libdaemon openssl avahi popt libsoxr libconfig)
makedepends=(git)
source=("git+https://github.com/mikebrady/shairport-sync.git"
	shairport-sync.install
	shairport-sync.service
	shairport-sync.conf
	remove-init.d.patch)
sha1sums=('SKIP'
          'd51485f3857529b70a29b38814ea60e7dde54ca8'
          'fe62feeef1c947ed6ed3500b7b922dcaf9e8987c'
          '6c4979abddb4b1c0242a941279d41617ab8d183c'
          '1f405744b5d2435f82cc13c77179a4e9de15e97a')

pkgver() {
  cd shairport-sync
  
  git describe --long --tags | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
  cd shairport-sync
  
  git apply "$srcdir/remove-init.d.patch"
}

build() {
  cd shairport-sync

  autoreconf -i -f
  ./configure --with-alsa --with-avahi --with-ssl=openssl --with-soxr --prefix="$pkgdir/usr"
  make
}

package() {
  install -D -m644 shairport-sync.service "$pkgdir/usr/lib/systemd/system/shairport-sync.service"
  install -D -m644 shairport-sync.conf "$pkgdir/etc/conf.d/shairport-sync"

  cd shairport-sync

  install -D -m664 LICENSES "$pkgdir/usr/share/licenses/$pkgname/LICENSE"  

  make install
}
