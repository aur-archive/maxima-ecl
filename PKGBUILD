# $Id: PKGBUILD 150832 2012-02-23 12:01:17Z juergen $
# Maintainer: Ronald van Haren <ronald.archlinux.org>
# Contributor: Damir Perisa <damir@archlinux.org>
# Modified to compile against ecl by: maribu

pkgname=maxima-ecl
provides=('maxima')
_pkgname=maxima
pkgver=5.35.1
pkgrel=1
pkgdesc="Maxima compiled against ecl - works not only on x86 but also on arm"
arch=('armv5te' 'armv6h' 'armv7h' 'i686' 'x86_64')
license=('GPL')
url="http://maxima.sourceforge.net"
depends=('ecl' 'texinfo' 'sh')
makedepends=('python2')
optdepends=('gnuplot: plotting capabilities' 'rlwrap: readline support via /usr/bin/rmaxima' 'tk: graphical xmaxima interface')
options=('!zipman') # don't zip info pages or they won't work inside maxima
install=maxima.install
source=("http://downloads.sourceforge.net/sourceforge/${_pkgname}/${_pkgname}-${pkgver}.tar.gz"
        "${_pkgname}.desktop")
md5sums=('4bb0b999645ec2b20b7e301d36f83a4c'
         '24aa81126fbb8b726854e5a80d4c2415')

build() {
  cd ${srcdir}/${_pkgname}-${pkgver}

  # set correct python executable to create docs
  sed -i "s|${PYTHONBIN:-python}|python2|" doc/info/extract_categories.sh

  ./configure --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info \
	--libexecdir=/usr/lib --enable-ecl --with-default-lisp=ecl
  make
}

package() {
  cd ${srcdir}/${_pkgname}-${pkgver}
  make DESTDIR=${pkgdir} install

  # install some freedesktop.org compatibility
  install -Dm644 ${srcdir}/${_pkgname}.desktop \
  	${pkgdir}/usr/share/applications/${_pkgname}.desktop

  # make sure, we have a nice icon for the desktop file at the right place ;)
  install -d ${pkgdir}/usr/share/pixmaps/
  ln -s /usr/share/maxima/${pkgver}/xmaxima/maxima-new.png \
	${pkgdir}/usr/share/pixmaps/${_pkgname}.png
}
