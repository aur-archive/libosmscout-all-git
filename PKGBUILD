# Maintainer: Antoine GIRARD <antoine.girard@sapk.fr>

pkgname=libosmscout-all-git
pkgver=0.1.a25dbcd
_pkgver=0.1
pkgrel=1
pkgdesc='Library for OpenStreetMap offline rendering and routing'
arch=(i686 x86_64)
url='https://sourceforge.net/p/libosmscout/'
license=(LGPL)
depends=("libxml2" "freeglut" "protobuf" "cairo" "pango")
#libtiger
optdepends=()
makedepends=(git)
source=(git://git.code.sf.net/p/libosmscout/code)
sha1sums=('SKIP')

_libs=('libosmscout' 'libosmscout-import' 'libosmscout-map' 'libosmscout-map-svg' 'libosmscout-map-cairo' 'libosmscout-map-opengl' 'Import');
# 'libosmscout-map-agg' 'libosmscout-map-qt'

pkgver() {
	cd code
	echo "$_pkgver.$(git log --pretty=format:"%h" | head -n1)"
}

build() {
	cd code
	export PKG_CONFIG_PATH="";

	for x in "${_libs[@]}"; do
	  if [ -d $x ]; then
	    echo Building $x...;
	    (cd $x && ./autogen.sh && ./configure --prefix=/usr/ && make);
	    export PKG_CONFIG_PATH="$PKG_CONFIG_PATH:$(pwd)/$x/";
	  fi
	done

}

package() {
	cd code

	for x in "${_libs[@]}"; do
	  if [ -d $x ]; then
	  	(cd $x && make DESTDIR="$pkgdir" install && cd ..)
	  fi
	done
	
	cp -R stylesheets  "$pkgdir/usr/share/libosmscout-stylesheets"
	mv "$pkgdir/usr/bin/Import" "$pkgdir/usr/bin/libosmscout-import"
}

