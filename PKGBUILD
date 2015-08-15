# Maintainer: Tomas Kral <tomas.kral@gmail.com>
pkgname=curveprotect
pkgver=20111121
pkgrel=5
pkgdesc="Curveprotect is a complex collection of tools for protecting wide range of internet services with CurveCP + DNSCurve."
arch=("any")
url="http://curveprotect.org"
license=("custom:PublicDomain")
depends=("daemontools" "ucspi-tcp" "python2")
makedepends=()
options=()
install=curveprotect.install
source=("http://curveprotect.org/testing/$pkgname-$pkgver.tar.bz2" "python2.patch")
md5sums=("181a82bb80825eb1ab096b2cfa23e996" "91956d95440abbfeb470cc207c7d0860")


build() {
  #patch for python2
  cd "$srcdir/$pkgname-$pkgver/www"
  patch -p1 -i ${startdir}/python2.patch

  #build
  cd "$srcdir/$pkgname-$pkgver"
  ./do

}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  install -D -m644 LICENCE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  # make use of debian package source
  for dir in `cat debian/curveprotect.dirs`; do
    mkdir -p "${pkgdir}/${dir}"
  done

  cat debian/curveprotect.install debian/curveprotect-bin.install |
  (
    while read line
    do
      _src=`echo "$line" | cut -d " " -f 1`
      _dst=`echo "$line" | cut -d " " -f 2`
      mkdir -p ${pkgdir}/${_dst}
      cp -r ${_src} ${pkgdir}/${_dst}
    done
  )

}

