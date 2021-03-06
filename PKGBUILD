# Maintainer: lykaner <lykaner@posteo.net>
# Contributor: lykaner <lykaner@posteo.net>

pkgname=keepassc-dev
pkgver=20140126
pkgrel=1
pkgdesc="KeePassC is a curses-based password manager compatible to KeePass v.1.x and KeePassX"
arch=(any)
url="http://www.nongnu.org/keepassc"
license=('GPL')
groups=
depends=('python-kppy>=1.4.0' 'python>=3.3')
optdepends=('xsel: copy usernames and password to clipboard')
makedepends=('git')
provides=('keepassc')
conflicts=('keepassc')

_gitroot='git://github.com/raymontag/keepassc.git'
_gitname='keepassc'

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin development
    msg "The local files are updated."
  else
    git clone -b development "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  msg "Running setup.py build"
  python setup.py build
}

package() {
  cd "$srcdir/$_gitname-build"
  python setup.py install --root="$pkgdir/" --optimize=1
}

# vim:set ts=2 sw=2 et:
