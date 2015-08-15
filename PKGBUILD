# Contributor: Patrice Peterson <runiq at archlinux dot us>
pkgname=dwm-sprinkles-svn-experimental
pkgver=86
pkgrel=1
pkgdesc="Dwm with sprinkles patches—experimental branch"
arch=('i686' 'x86_64')
url="http://0mark.unserver.de/dwm-sprinkles/"
license=('GPL')
depends=('libxinerama')
makedepends=('subversion')
provides=(dwm-sprinkles)
conflicts=(dwm-sprinkles dwm-sprinkles-svn)

_svntrunk="https://svn.0mark.unserver.de/dwm/branches/experimental"
_svnmod=dwm-sprinkles

build() {
  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 || return 1
  make PREFIX=/usr DESTDIR=$pkgdir install || return 1

  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE && \
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
}

