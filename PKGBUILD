# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: csslayer <wengxt AT gmail com>

pkgname=fcitx5
pkgver=0.0.0.20181128
_commit=984f3f2c1fdcecb7de4dfb39b876c2821e366a59
_endictver=20121020
pkgrel=1
pkgdesc="Next generation of fcitx"
arch=('i686' 'x86_64')
url="https://github.com/fcitx/fcitx5"
license=('GPL')
depends=('cairo' 'enchant' 'iso-codes' 'libgl' 'libxkbcommon-x11' 'pango' 'systemd' 'wayland'
         'wayland-protocols' 'xcb-imdkit' 'xcb-util-wm' 'libxkbfile' 'fmt' 'gdk-pixbuf2')
makedepends=('extra-cmake-modules')
source=("https://gitlab.com/fcitx/fcitx5/-/archive/$_commit/fcitx5-$_commit.tar.bz2"
        https://download.fcitx-im.org/data/en_dict-$_endictver.tar.gz)
sha512sums=('21e6848a252bd2dce1029c1e5b6f796cc3a47eaa835c08931a723b3bb770dd8b04eee3f30e46e5890ef46a5a591c29aa9751e6ba10decd4e10790c12b3ff07c3'
            '8418bd02492bfd786c0fab93be4400ef027ec8e9fac02220cc1f653f5eb67f54573a6a84a15baba19bb34ab892745c87df16499d6304ea75009131e2ab3b97f2')

prepare() {
  cd $pkgname-$_commit/src/modules/spell/dict
  ln -s "$srcdir"/en_dict-$_endictver.tar.gz ./
}

build(){
  cd $pkgname-$_commit
 
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_LIBDIR=/usr/lib .
  make
}

package() {
  cd $pkgname-$_commit
  make DESTDIR="$pkgdir" install
}
