# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: csslayer <wengxt AT gmail com>

pkgname=fcitx5
pkgver=5.1.10
_dictver=20121020
pkgrel=1
pkgdesc="Next generation of fcitx"
arch=('x86_64')
url="https://github.com/fcitx/fcitx5"
license=('LGPL-2.1-or-later AND Unicode-DFS-2016')
conflicts=('fcitx')
groups=('fcitx5-im')
depends=('cairo' 'enchant' 'iso-codes' 'libgl' 'libxkbcommon-x11' 'pango' 'systemd' 'wayland'
         'xcb-imdkit' 'xcb-util-wm' 'libxkbfile' 'gdk-pixbuf2')
makedepends=('git' 'extra-cmake-modules' 'ninja' 'wayland-protocols' 'fmt')
source=("git+https://github.com/fcitx/fcitx5.git#tag=$pkgver?signed"
        "https://download.fcitx-im.org/data/en_dict-$_dictver.tar.gz")
noextract=("en_dict-$_dictver.tar.gz")
sha512sums=('9c99cda8091ed9ab909ee1ac13633077002a738d4a9a369c2bd5159ce892253a3e8f4b0fddf4e204aff19a416877658b080e1f5f58b887eb2e536520ef52f39e'
            '8418bd02492bfd786c0fab93be4400ef027ec8e9fac02220cc1f653f5eb67f54573a6a84a15baba19bb34ab892745c87df16499d6304ea75009131e2ab3b97f2')
validpgpkeys=('2CC8A0609AD2A479C65B6D5C8E8B898CBF2412F9') # Weng Xuetian <wengxt@gmail.com>

prepare() {
  mv en_dict-$_dictver.tar.gz fcitx5/src/modules/spell/en_dict-$_dictver.tar.gz
  # grep to make sure the version is correct
  grep "SPELL_EN_DICT_VER $_dictver" fcitx5/src/modules/spell/CMakeLists.txt
}

build() {
  cd $pkgname

  cmake -GNinja -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib \
        -DCMAKE_INSTALL_SYSCONFDIR=/etc -DCMAKE_INSTALL_LIBEXECDIR=/usr/lib .
  ninja
}

check() {
  cd $pkgname
  ninja test
}

package() {
  cd $pkgname
  DESTDIR="$pkgdir" ninja install
  install -Dm644 LICENSES/Unicode-DFS-2016.txt -t "$pkgdir"/usr/share/licenses/$pkgname/
}
