# No licence for this

# Maintainer: flagos <flagospub@gmail.com>
pkgname=OpenplacOS-unstable-git
pkgver=20130309
pkgrel=1
pkgdesc="Software for automoted systems like home automation, aquariophily and indoor gardens"
arch=('any')
url="http://openplacos.tuxfamily.org/"
license=('GPL')
groups=()
depends=('ruby' 'dbus' 'sqlite' 'git')
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
_gitbranch=testing

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname" --branch "$_gitbranch"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build" --branch "$_gitbranch"
  cd "$srcdir/$_gitname-build"

}

package() {
  cd "$srcdir/$_gitname-build"
  touch Makefile.defs
  make DESTDIR="$pkgdir/" INITDIR="/etc/rc.d/" INSTALLDIR="/usr/lib/ruby/openplacos" UDEVDIR="/etc/udev/rules.d" DBUSCONFDIR="/etc/dbus-1/system.d" DEFAULTCONFDIR="/etc/" BINDIR="/usr/bin/"  install
  mv $pkgdir/etc/openplacos $pkgdir/etc/openplacos.conf
}

# vim:set ts=2 sw=2 et:
