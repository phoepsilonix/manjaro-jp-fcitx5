# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: csslayer <wengxt AT gmail com>

pkgname=fcitx5
pkgver=0.0.0.20200728
_commit=327912d9c855f906d823f7c70c188b7faf2c268e
_endictver=20121020
pkgrel=1
pkgdesc="Next generation of fcitx"
arch=('x86_64')
url="https://github.com/fcitx/fcitx5"
license=('GPL')
conflicts=('fcitx')
groups=('fcitx5-im')
depends=('cairo' 'enchant' 'iso-codes' 'libgl' 'libxkbcommon-x11' 'pango' 'systemd' 'wayland'
         'wayland-protocols' 'xcb-imdkit' 'xcb-util-wm' 'libxkbfile' 'fmt' 'gdk-pixbuf2'
         'cldr-emoji-annotation')
makedepends=('extra-cmake-modules')
source=("https://github.com/fcitx/fcitx5/archive/$_commit/fcitx5-$_commit.tar.gz"
        https://download.fcitx-im.org/data/en_dict-$_endictver.tar.gz)
sha512sums=('1aa5c2d3545fe2a28e9a92c7a53af28d7c17262df4e58ebcc963dae35e77cacc451887cf8ea6b78a591ad41e11ac03ef308d9373c5bb86f928cc2a4e562598d2'
            '8418bd02492bfd786c0fab93be4400ef027ec8e9fac02220cc1f653f5eb67f54573a6a84a15baba19bb34ab892745c87df16499d6304ea75009131e2ab3b97f2')

prepare() {
  cd $pkgname-$_commit/src/modules/spell/dict
  ln -s "$srcdir"/en_dict-$_endictver.tar.gz ./
}

build() {
  cd $pkgname-$_commit

  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib .
  make
}

check() {
  cd $pkgname-$_commit
  make test
}

package() {
  cd $pkgname-$_commit
  make DESTDIR="$pkgdir" install
}
