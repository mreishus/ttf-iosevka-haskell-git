# Maintainer: Matthew Reishus <m.reishus@fastmail.com>
# Contributor: Andy Kluger <AndyKluger@gmail.com>
# Contributor: Markus Weimar <mail@markusweimar.de>
pkgname=ttf-iosevka-haskell-git
pkgver=r1614.09e50636
pkgrel=1
pkgdesc='A slender monospace sans-serif and slab-serif typeface. Built with Haskell ligatures.'
arch=('any')
url='https://be5invis.github.io/Iosevka/'
license=('custom:OFL')
makedepends=('git' 'nodejs' 'npm' 'ttfautohint' 'otfcc')
depends=('fontconfig' 'xorg-font-utils')
conflicts=()
provides=()
source=(
  "git+https://github.com/be5invis/Iosevka"
  "private-build-plans.toml"
)
md5sums=(
  'SKIP'
  '96bdf98121277a2c84aa536dbc1790ea'
)

pkgver() {
  cd Iosevka
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  buildplans="$HOME/.config/iosevka/private-build-plans.toml"
  [[ -f "$buildplans" ]] && cp "$buildplans" ../ || echo "$buildplans not found, using pkgbuild creator's"
  cp ../private-build-plans.toml Iosevka/
}

build() {
  cd Iosevka
  npm install
  npm run build -- contents::iosevka-termlig-haskell
}

package() {
  install -d "${pkgdir}/usr/share/fonts/TTF"
  install -m644 Iosevka/dist/*/ttf/*.ttf "${pkgdir}/usr/share/fonts/TTF/"
  install -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 Iosevka/LICENSE.md "${pkgdir}/usr/share/licenses/${pkgname}/"
}
