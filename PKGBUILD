# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: csslayer <wengxt AT gmail com>

pkgname=fcitx5
pkgver=5.1.12
_dictver=20121020
_commit=c829acf10790135668e7a984f13f958542d9288c
pkgrel=9
pkgdesc="Next generation of fcitx"
arch=('x86_64')
url="https://github.com/fcitx/fcitx5"
license=('LGPL-2.1-or-later AND Unicode-DFS-2016')
conflicts=('fcitx')
groups=('fcitx5-im')
depends=('cairo' 'enchant' 'iso-codes' 'libgl' 'libxkbcommon-x11' 'pango' 'systemd' 'wayland'
         'xcb-imdkit' 'xcb-util-wm' 'libxkbfile' 'gdk-pixbuf2' 'json-c')
makedepends=('git' 'extra-cmake-modules' 'ninja' 'wayland-protocols' 'fmt')
source=("git+https://github.com/fcitx/fcitx5.git#commit=$_commit"
        "https://download.fcitx-im.org/data/en_dict-$_dictver.tar.gz"
        kde.patch)
noextract=("en_dict-$_dictver.tar.gz")
sha512sums=('c431c8829cd4983391701b2ab5522798c36951ff807ff8154601a7af0bffbdc95fab75b7d9d2e1d9a62a7e528b635944c798ae6f8f07428be2f4d1239bcc605a'
            '8418bd02492bfd786c0fab93be4400ef027ec8e9fac02220cc1f653f5eb67f54573a6a84a15baba19bb34ab892745c87df16499d6304ea75009131e2ab3b97f2'
            '86ba7f617773e39340f50d0eea3c07c85ecba0e12fdc26b810b3493df376965e4e9c6b359820623eba83ebc131d98941a89477a9c7d86790240c2e4fbb051527')
validpgpkeys=('2CC8A0609AD2A479C65B6D5C8E8B898CBF2412F9') # Weng Xuetian <wengxt@gmail.com>
install=fcitx5.install

prepare() {
  mv en_dict-$_dictver.tar.gz fcitx5/src/modules/spell/en_dict-$_dictver.tar.gz
  # grep to make sure the version is correct
  grep "SPELL_EN_DICT_VER $_dictver" fcitx5/src/modules/spell/CMakeLists.txt
  cd $pkgname
  patch -p1 -i ${srcdir}/kde.patch
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
