#Mantainer: M0Rf30
pkgname=printerd
pkgver=20120524
pkgrel=1
pkgdesc="A daemon to manage local and remote printers on Linux."
arch=('i686' 'x86_64')
url="http://gitorious.org/printerd"
license=('GPL2')
depends=('gnome-common' 'gobject-introspection')
makedepends=('git' 'intltool' 'gtk-doc')

_gitroot="git://gitorious.org/printerd/printerd.git"
_gitname="printerd"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone -l "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  ./autogen.sh
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var
  make
} 

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR=$pkgdir install
}
