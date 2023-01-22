# Maintainer: giornogoldenwind <114269150+giornogoldenwind at users.noreply.github.com>
# Maintainer (AUR): Fabio 'Lolix' Loli <fabio.loli@disroot.org> -> https://github.com/FabioLolix
# Contributor (AUR): erk <v at erk dot io>
pkgname=vnote
pkgver=3.16.0
pkgrel=1
pkgdesc="A Vim-inspired note-taking application, especially for Markdown."
arch=(amd64)
url="https://vnotex.github.io/vnote/en_us/"
license=(LGPL3)
depends=(qtbase5-dev qtwebengine5-dev libqt5svg5-dev libqt5x11extras5-dev)
makedepends=(git qt5-qmake)
source=("git+https://github.com/vnotex/vnote.git#tag=v${pkgver}"
        "vnotex-vtextedit::git+https://github.com/vnotex/vtextedit"
        "vnotex-QHotkey::git+https://github.com/vnotex/QHotkey.git"
        "vnotex-syntax-highlighting::git+https://github.com/vnotex/syntax-highlighting"
        "vnotex-hunspell::git+https://github.com/vnotex/hunspell"
        "vnotex-sonnet::git+https://github.com/vnotex/sonnet")
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP')

prepare() {
  cd "${pkgname}"

  install -d build

  git submodule init
  git config 'submodule.libs/vtextedit.url' "${srcdir}/vnotex-vtextedit"
  git config 'submodule.libs/QHotkey.url' "${srcdir}/vnotex-QHotkey"
  git -c protocol.file.allow=always submodule update --remote  # prevent commit hash mismatch

  cd "libs/vtextedit"
  git submodule init
  git config 'submodule.src/libs/syntax-highlighting.url' "${srcdir}/vnotex-syntax-highlighting"
  git config 'submodule.src/libs/hunspell.url' "${srcdir}/vnotex-hunspell"
  git config 'submodule.src/libs/sonnet.url' "${srcdir}/vnotex-sonnet"
  git -c protocol.file.allow=always submodule update --remote  # prevent commit hash mismatch
}

build() {
  cd "${pkgname}/build"
  qmake ../vnote.pro
  make
}

package() {
  cd "${pkgname}/build"
  make INSTALL_ROOT="$pkgdir" install
}

# vim: set sw=4 expandtab:


