## $Id$
# Maintainer: TheKit <nekit1000 at gmail.com>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

pkgname=nemo-qml-plugin-devicelock-git
pkgver=0.2.23.r0.gdd20dae
pkgrel=1
pkgdesc="Device lock plugin for Nemo Mobile"
arch=('x86_64' 'aarch64')
url="https://git.sailfishos.org/mer-core/nemo-qml-plugin-devicelock"
license=('GPL')
depends=('qt5-base' 'nemo-keepalive' 'nemo-qml-plugin-dbus')
makedepends=('git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=('git+https://git.sailfishos.org/mer-core/nemo-qml-plugin-devicelock.git')
md5sums=('SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd "$srcdir/${pkgname%-git}"
    sed -i "s|libsystemd-daemon|libsystemd|g" ./src/nemo-devicelock/host/host.pro
    sed -i "s|libsystemd-daemon|libsystemd|g" ./src/daemon/daemon.pro
}

build() {
	cd "$srcdir/${pkgname%-git}"
	qmake
	make
}

package() {
	cd "$srcdir/${pkgname%-git}"
	make INSTALL_ROOT="$pkgdir/" install
	cd "$pkgdir"
	cp -r lib usr/
	rm -rf lib
}
