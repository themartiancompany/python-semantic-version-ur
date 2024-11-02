# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Simon Sapin <simon dot sapin at exyr dot org>
# Contributor: Kyle Keen <keenerd@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=semantic-version
_Pkg=semanticversion
_pkgname="python-${_Pkg}"
pkgname="${_py}-${_pkg}"
pkgver=2.10.0
pkgrel=3
pkgdesc="A library implementing the 'SemVer' scheme."
_http="https://github.com"
_ns="rbarrois"
url="${_http}/${_ns}/python-${_Pkg}"
license=(
  'BSD'
)
arch=(
  'any'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-setuptools"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-django"
)
source=(
  "${url}/archive/${pkgver}/${_pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  'e060dd60db62663c6ebf21fdca33b2390d9bbad15fbdfa504221ab646426f09168caf00e79cee7ed4ef442c23fd587c9e421aa744990101ea626b58f4e320242'
)

build() {
  cd \
    "${_pkgname}-${pkgver}"
  "${_py}" \
    setup.py \
      build
}

check() {
  cd \
    "${_pkgname}-${pkgver}"
  "${_py}" \
    setup.py \
      egg_info
  pytest
}

package() {
  cd \
    "${_pkgname}-${pkgver}"
  "${_py}" \
    setup.py \
      install \
        --root="${pkgdir}" \
	--optimize=1
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
