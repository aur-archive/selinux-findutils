# $Id: PKGBUILD 100218 2010-11-21 23:38:22Z stephane $
# Maintainer: Nicky726 <Nicky726@gmail.com>

pkgname=selinux-findutils
_origname=findutils
pkgver=4.4.2
pkgrel=5
pkgdesc="GNU utilities to locate files with Gentoo SELinux patch"
arch=('i686' 'x86_64')
license=('GPL3')
groups=('selinux' 'selinux-system-utilities')
depends=('glibc' 'sh' 'selinux-usr-libselinux')
conflicts=("${_origname}")
provides=("${_origname}=${pkgver}-${pkgrel}")
url="http://www.gnu.org/software/findutils"
source=(ftp://ftp.gnu.org/pub/gnu/findutils/${_origname}-${pkgver}.tar.gz{,.sig}
        http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/sys-apps/${_origname}/files/${_origname}-${pkgver}-selinux.diff)
install=findutils.install
sha1sums=('e8dd88fa2cc58abffd0bfc1eddab9020231bb024'
          '77d9585d9feea0814752a31bf109fe287f528243'
          '96318be5586d324a13805da81907406a95c6514c')

build() {
  cd "${srcdir}/${_origname}-${pkgver}"

  # Apply SELinux patch
  patch -Np1 -i "${srcdir}/${_origname}-${pkgver}-selinux.diff"

  # Don't build or install locate because we use mlocate,
  # which is a secure version of locate.
  sed -i '/^SUBDIRS/s/locate//' Makefile.in

  ./configure --prefix=/usr
  make
}

check() {
  cd "${srcdir}/${_origname}-${pkgver}"
  make check
}

package() {
  cd "${srcdir}/${_origname}-${pkgver}"
  make DESTDIR=$pkgdir install
}
