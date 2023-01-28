# Merged with official ABS solid PKGBUILD by João, 2021/02/21 (all respective contributors apply herein)
# Maintainer: João Figueiredo <jf.mundox@gmail.com>
# Contributor: zan <zan@420blaze.it>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=solid-git
pkgver=5.80.0_r643.gc0e435e
pkgrel=1
pkgdesc='Hardware integration and detection'
arch=($CARCH)
url='https://community.kde.org/Frameworks'
license=(LGPL)
depends=(qt5-base media-player-info upower udisks2)
makedepends=(git extra-cmake-modules-git qt5-tools qt5-doc doxygen qt5-declarative)
conflicts=(${pkgname%-git})
provides=(${pkgname%-git})
optdepends=('qt5-declarative: QML bindings')
groups=(kf5-git)
source=("git+https://github.com/KDE/${pkgname%-git}.git")
sha256sums=('SKIP')

pkgver() {
    cd ${pkgname%-git}
      _ver="$(grep -m1 'set(KF5\?_VERSION' CMakeLists.txt | cut -d '"' -f2 | tr - .)"
        echo "${_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

build() {
    cmake -B build -S ${pkgname%-git} \
        -DBUILD_TESTING=OFF \
            -DBUILD_QCH=ON \
                -DWITH_NEW_POWER_ASYNC_API=ON \
                    -DWITH_NEW_POWER_ASYNC_FREEDESKTOP=ON \
                        -DWITH_NEW_SOLID_JOB=ON # https://bugs.archlinux.org/task/64093
                          cmake --build build
}

package() {
    DESTDIR="$pkgdir" cmake --install build
}
source=("git+https://github.com/KDE/${pkgname%-git}#branch=kf5")
