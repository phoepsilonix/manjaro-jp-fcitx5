# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: csslayer <wengxt AT gmail com>

pkgname=fcitx5
pkgver=0.0.0.20200318
_commit=2ce721fa3c33dcaf67020225af1e7cca08c1e02c
_endictver=20121020
pkgrel=2
pkgdesc="Next generation of fcitx"
arch=('x86_64')
url="https://github.com/fcitx/fcitx5"
license=('GPL')
depends=('cairo' 'enchant' 'iso-codes' 'libgl' 'libxkbcommon-x11' 'pango' 'systemd' 'wayland'
         'wayland-protocols' 'xcb-imdkit' 'xcb-util-wm' 'libxkbfile' 'fmt' 'gdk-pixbuf2'
         'cldr-emoji-annotation')
makedepends=('extra-cmake-modules')
source=("https://github.com/fcitx/fcitx5/archive/$_commit/fcitx5-$_commit.tar.gz"
        https://download.fcitx-im.org/data/en_dict-$_endictver.tar.gz)
sha512sums=('2ae18f2321181a82f3ff1f02f82cef5467c577029bcc9d67c1995764bea41707d55be86c19719b0017a4c2f03fda9d1779869cb79132fee342981235cdfe43ce'
            '8418bd02492bfd786c0fab93be4400ef027ec8e9fac02220cc1f653f5eb67f54573a6a84a15baba19bb34ab892745c87df16499d6304ea75009131e2ab3b97f2')

prepare() {
  cd $pkgname-$_commit/src/modules/spell/dict
  ln -s "$srcdir"/en_dict-$_endictver.tar.gz ./
}

build(){
  cd $pkgname-$_commit

  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib .
  make
}

package() {
  cd $pkgname-$_commit
  make DESTDIR="$pkgdir" install
}
