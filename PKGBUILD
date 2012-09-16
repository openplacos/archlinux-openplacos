# No licence for this

# Maintainer: flagos <flagospub@gmail.com>
pkgname=OpenplacOS-unstable-git
pkgver=20120916
pkgrel=1
pkgdesc="Software for automoted systems like home automation, aquariophily and indoor gardens"
arch=('any')
url="http://openplacos.tuxfamily.org/"
license=('GPL')
groups=()
depends=('ruby' 'dbus' 'sqlite')
makedepends=('git')
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=openplacos.install
source=()
noextract=()
md5sums=() #generate with 'makepkg -g'

_gitroot=git://github.com/openplacos/openplacos.git
_gitname=openplacos

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname" --branch unstable
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build" --branch unstable
  cd "$srcdir/$_gitname-build"

}

package() {
  cd "$srcdir/$_gitname-build"
  touch Makefile.defs
  make DESTDIR="$pkgdir/" INITDIR="/etc/rc.d/" INSTALLDIR="/usr/lib/ruby/openplacos" UDEVDIR="/etc/udev/rules.d" DBUSCONFDIR="/etc/dbus-1/system.d" DEFAULTCONFDIR="/etc/" BINDIR="/usr/bin/"  install
  mv $pkgdir/etc/openplacos $pkgdir/etc/openplacos.conf
}

# vim:set ts=2 sw=2 et:
