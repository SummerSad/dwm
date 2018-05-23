# Maintainer: SummerSad <hauvipapro@gmail.com>

pkgname=dwm
pkgver=6.1
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
_patches=(
	"theme.patch"
	"termgap.patch"
	"binding.patch"
)
source=("http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz"
	"dwm.desktop"
	"${_patches[@]}")
sha256sums=('c2f6c56167f0acdbe3dc37cca9c1a19260c040f2d4800e3529a21ad7cce275fe'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            'e5a8807c408692c4d1abfc59cd5b3a2ddb2bcd06ccaa5593cb94ec60687f3bef'
            'c00522ca00ca6c21c3e9c049717d75bc0e30ff63ef0742a00d90797699ff187d'
            'b35ae938c22d186605d2f1de6a345b01f5aaa3fedef5b9de9efe91f48ec38aba')

prepare() {
	cd $srcdir/$pkgname-$pkgver
	# patch
	for file in "${_patches[@]}"; do
		if [[ "$file" == *.diff || "$file" == *.patch ]]; then
			echo "Applying patch $(basename $file)..."
			patch -Np1 <"$srcdir/$(basename ${file})"
		fi
	done
}

build() {
	cd $srcdir/$pkgname-$pkgver
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
	cd $srcdir/$pkgname-$pkgver
	make PREFIX=/usr DESTDIR=$pkgdir install
	install -Dm644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
	install -Dm644 README $pkgdir/usr/share/doc/$pkgname/README
	install -Dm644 $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
