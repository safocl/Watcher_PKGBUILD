_pkgname='Watcher'
pkgname="${_pkgname}-git"
pkgver=r132.8a1992b
pkgrel=2
arch=('x86_64')
url='https://github.com/safocl/Watcher'
license=('GPL3')
depends=('sdl2_mixer' 'gtkmm-4.0' 'nlohmann-json')
makedepends=('git' 'cmake')
source=("${_pkgname}::git+https://github.com/safocl/Watcher.git")
md5sums=('SKIP')

pkgver(){
    cd "$srcdir/${_pkgname}"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cmake -B build -S ${_pkgname} -G Ninja --install-prefix=/usr -DCMAKE_BUILD_TYPE=Release
    cmake --build build -j$(cat /proc/cpuinfo|grep processor|wc -l)
}

package(){
    DESTDIR="$pkgdir" cmake --install build
    rm -rf $pkgdir/usr/{lib,include}
}
