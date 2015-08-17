# Contributor: Konstantin Shabanov <kes.eclipse@gmail.com>
# Contributor: Evka
# Maintainer: Jose Riha <jose 1711 gmail com>

pkgname=udpxy
pkgver=1.0.23.0
_pkgver=1.0.23-0
pkgrel=2
pkgdesc="small-footprint UNIX/Linux daemon to relay multicast UDP traffic to client's TCP (HTTP) connection."
arch=(i686 x86_64)
url="http://udpxy.sf.net"
license=('GPL3')
source=(http://sourceforge.net/projects/$pkgname/files/$pkgname/Chipmunk-1.0/$pkgname.${_pkgver}-prod.tar.gz
	$pkgname.conf
	$pkgname.rc
	$pkgname.service
	pidfile.patch
)
backup=('etc/conf.d/udpxy')

md5sums=('3dd99ba264078e873cbe1d98369ed423'
         '48993e68830724e3c78f8b4fb7690a15'
         '833fc814391c965b2eccda500c0fe637'
         '2154ba3871b708d90af11ceca081f7b9'
         '7a268f58ee964895377c95d16c9c633a')

build() {
  cd "$srcdir/$pkgname-${_pkgver}"
  patch -Np1 -i "${srcdir}/pidfile.patch"
  sed -i '/ln -s $(INSTALLROOT)\/bin\/$(EXEC) $(INSTALLROOT)\/bin\/$(UDPXREC/s%$(INSTALLROOT)%/usr%' Makefile
  make
}

package() {
  cd "$srcdir/$pkgname-${_pkgver}"
  make INSTALLROOT="$pkgdir/usr" install
  # Install rc script
  #install -D -m755 $srcdir/$pkgname.rc $pkgdir/etc/rc.d/$pkgname
  # Install conf.d file
  install -D -m644 $srcdir/$pkgname.conf $pkgdir/etc/conf.d/$pkgname
  # Install systemd unit
  install -D -m644 $srcdir/$pkgname.service $pkgdir/usr/lib/systemd/system/$pkgname.service
}
