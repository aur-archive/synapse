# Maintainer: Alessio Sergi <asergi at archlinux dot us>

pkgname=synapse
pkgver=0.2.10
pkgrel=1
pkgdesc="A semantic file launcher"
arch=('i686' 'x86_64')
url="https://launchpad.net/synapse-project"
license=('GPL3')
depends=('desktop-file-utils' 'gtkhotkey' 'hicolor-icon-theme' \
         'json-glib' 'libgee' 'libnotify' 'libunique')
makedepends=('intltool' 'vala')
optdepends=('banshee: banshee plugin'
            'bc: calculator plugin'
            'devhelp: documentation plugin'
            'gnome-screensaver: screensaver plugin'
            'gnome-utils: dictionary plugin'
            'openssh: ssh plugin'
            'pastebinit: pastebin plugin'
            'rhythmbox: rhythmbox plugin'
            'xnoise: xnoise plugin'
            'zeitgeist-datahub: zeitgeist plugin')
install=$pkgname.install
source=("https://launchpad.net/$pkgname-project/0.2/$pkgver/+download/$pkgname-$pkgver.tar.gz"
        "fix-check-desktop.patch")
sha1sums=('6e8a800bdbdded4e167734c8e49d95a9e44998ff'
          'b64fa4efc4efd01f77f84d19a7a63c10186d0211')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  # no zeitgeist dep
  sed -i '/--pkg zeitgeist-1.0 \\/d' src/ui/Makefile.am
  sed -i 's/zeitgeist-1.0 --pkg //' src/ui/Makefile.in
  
  # XDG_CURRENT_DESKTOP fix
  patch -Np1 -i "$srcdir"/fix-check-desktop.patch

  # DSO fix
  export LDFLAGS="$LDFLAGS -ldl -lm"

  ./configure --prefix=/usr --disable-zeitgeist
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
