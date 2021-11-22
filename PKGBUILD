# Maintainer: Hu Butui <hot123tea123@gmail.com>

_realname=mp11
pkgbase=mingw-w64-${_realname}
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=1.77.0
pkgrel=1
pkgdesc="C++11 metaprogramming library (contains only cmake file)"
arch=('any')
mingw_arch=('mingw32' 'mingw64' 'ucrt64' 'clang64' 'clang32')
url="https://github.com/boostorg/mp11"
license=('custom')
depends=(
  "${MINGW_PACKAGE_PREFIX}-gcc-libs"
)
makedepends=("${MINGW_PACKAGE_PREFIX}-cmake")
source=("${_realname}-${pkgver}.tar.gz::https://github.com/boostorg/mp11/archive/refs/tags/boost-${pkgver}.tar.gz")
sha256sums=('19944405b0a788dccaceb18dcb7c22dbdea15f962fd2096407d8a8132f0e5447')

build() {
  echo "==> Build shared version"
  MSYS2_ARG_CONV_EXCL="-DCMAKE_INSTALL_PREFIX=" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    -B "${srcdir}/build-shared-${MINGW_CHOST}" \
    -DBUILD_SHARED_LIBS=ON \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=${MINGW_PREFIX} \
    -DBUILD_TESTING=OFF \
    -G'MSYS Makefiles' \
    -S ${_realname}-boost-${pkgver}
  ${MINGW_PREFIX}/bin/cmake.exe --build "${srcdir}/build-shared-${MINGW_CHOST}"
}

package() {
  DESTDIR="${pkgdir}" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    --build "${srcdir}/build-shared-${MINGW_CHOST}" \
    --target install
  rm -rfv "${pkgdir}/${MINGW_PREFIX}/include"
}
