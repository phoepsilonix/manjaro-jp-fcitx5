# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: csslayer <wengxt AT gmail com>

pkgname=fcitx5
pkgver=0.0.0.20200820
_commit=f9d206a9559e3b589aaac1ba822b56495a470f45
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
sha512sums=('b3fd148e696a8ae6efaaf15f46f106225e34418f448b406f2a3a38938bf53279533259e476df7baa0f4304882caa5876664b691a17a41d9f5b2c26fc7a2ecce7'
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
