# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Noah Heller <softwareenginer@pm.me>
pkgname=advantagescope-git
pkgver=4.1.2
pkgrel=1
epoch=
pkgdesc="UNOFFICIAL build of advantage scope by FRC team 6328"
arch=(x86_64)
url="https://github.com/Mechanical-Advantage/AdvantageScope.git"
license=('MIT')
groups=()
depends=(nspr libxdamage dbus nss libxcb libxext glib2 libxrandr mesa libxfixes alsa-lib alsa-lib glibc gcc-libs libcups libxkbcommon cairo at-spi2-core pango expat libx11 gtk3 libdrm libxcomposite hicolor-icon-theme)
makedepends=(sudo jq curl git npm emsdk tar)
checkdepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=("git+$url")
noextract=()
sha256sums=('SKIP')
validpgpkeys=()

build() {
	cd AdvantageScope
	sudo /usr/lib/emsdk/emsdk install latest
	sudo /usr/lib/emsdk/emsdk activate latest
	source /usr/lib/emsdk/emsdk_env.sh
	npm install
	jq '. + { homepage: "https://github.com/Mechanical-Advantage/AdvantageScope" }' package.json > temp.json && mv temp.json package.json
	npm run build -- --linux --config.linux.target=pacman
	curl -OL https://raw.githubusercontent.com/Mechanical-Advantage/AdvantageScope/refs/heads/main/LICENSE
	cd dist
	tar xvf advantagescope-$pkgver.pacman
}


package() {
	cd AdvantageScope
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/$pkgname/LICENSE"
	cd dist
	cp -rf opt "$pkgdir"
  cp -rf usr "$pkgdir"
  mkdir -p "$pkgdir/usr/bin"
  ln -s "/opt/AdvantageScope/$pkgname" "$pkgdir/usr/bin/$pkgname"
}
