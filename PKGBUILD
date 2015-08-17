# Maintainer: Christian Bühler <christian@cbuehler.de>
pkgname=qt3d
pkgver=754.bdb98ba
pkgrel=1
pkgdesc="Support for scripting Qt Quick applications in 3D using OpenGL"
arch=('x86_64')
url="https://qt.gitorious.org/qt/qt3d"
license=('LGPL')
depends=('mesa' 'qt5-declarative')
makedepends=('git' 'qt5-tools')
source=(git://gitorious.org/qt/$pkgname.git)
md5sums=('SKIP')

pkgver() {
    cd $pkgname
    echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

build() {
	cd "$srcdir/$pkgname"
	qmake-qt5
	make
	make docs
}

package() {
	cd "$srcdir/$pkgname"
	make INSTALL_ROOT="${pkgdir}" install
	make INSTALL_ROOT="${pkgdir}" install_docs

    # Fix wrong path in prl files
    find "${pkgdir}/usr/lib" -type f -name '*.prl' \
        -exec sed -i -e '/^QMAKE_PRL_BUILD_DIR/d;s/\(QMAKE_PRL_LIBS =\).*/\1/' {} \;
}
