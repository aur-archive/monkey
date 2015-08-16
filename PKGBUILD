#Maintainer: Christian Stankowic <info at stankowic hypen development dot net>
#Contributor: Gary Wright <wriggary at gmail dot com>
pkgname=monkey
pkgver=1.5.5
pkgrel=1
pkgdesc="A very small and fast open source web server for Linux"
arch=('i686' 'x86_64')
url="http://www.monkey-project.com/"
license=('Apache')
depends=('gcc-libs')
optdepends=('php' 'polarssl')
source=("http://www.monkey-project.com/releases/1.5/$pkgname-$pkgver.tar.gz"
    monkey)
install=monkey.install
md5sums=('bd2410f6612ec4a9076c3921145e4b75'
	 '1527d1fbddddcfd69ad328639dcd0eed')

build() {
  cd $srcdir/$pkgname-$pkgver
  ./configure --prefix=/usr --bindir=/usr/bin --sysconfdir=/etc/$pkgname --default-user=http --default-port=80 \
  --datadir=/srv/http --logdir=/var/log/$pkgname --plugdir=/usr/lib/$pkgname --enable-shared --systemddir=$pkgdir/lib/systemd/system --pidfile=/var/run/monkey.pid --enable-plugins=polarssl
  make 
}

package() {
  cd $srcdir/$pkgname-$pkgver

  make DESTDIR=$pkgdir install

  msg2 "Change default pid file location from /var/log to /var/run/monkey"
  sed -i -e "s/\/var\/log\/monkey\/monkey.pid/\/var\/run\/monkey.pid/" $pkgdir/etc/monkey/monkey.conf

  msg2 "Disabling user setting in monkey configuration file"
  sed -i -e "s/User http/#User http/g" $pkgdir/etc/monkey/monkey.conf

  install -Dm 755 "$srcdir/monkey" "$pkgdir/etc/rc.d/monkey"
}
