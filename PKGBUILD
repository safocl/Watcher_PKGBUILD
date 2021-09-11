_pkgname='Watcher'
pkgname="${_pkgname}-git"
pkgver=r103.3761618
pkgrel=1
arch=('x86_64')
url='https://github.com/safocl/Watcher'
license=('GPL3')
depends=('sdl2_mixer' 'gtkmm-4.0')
makedepends=('git' 'cmake')
source=("${_pkgname}::git+https://github.com/safocl/Watcher.git")
md5sums=('SKIP')

pkgver(){
    cd "$srcdir/${_pkgname}"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare(){
    cd "$srcdir/${_pkgname}"
    git submodule update --init
}

build() {
    cd "$srcdir/${_pkgname}"

    rm -rf build && mkdir build
    cd build

    cmake --install-prefix=/usr -DCMAKE_BUILD_TYPE=Release ..
    cmake --build . -j$(cat /proc/cpuinfo|grep processor|wc -l)
}

package(){
    cd "$srcdir/${_pkgname}/build"
    make DESTDIR="$pkgdir/" install

    rm -rf $pkgdir/usr/{lib,include}
}
