# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Simon Sapin <simon dot sapin at exyr dot org>
# Contributor: Kyle Keen <keenerd@gmail.com>

pkgbase=python-semantic-version
pkgname=(python-semantic-version python2-semantic-version)
pkgver=2.6.0
pkgrel=2
pkgdesc="A library implementing the 'SemVer' scheme."
url="https://github.com/rbarrois/semantic-version"
license=('BSD')
arch=('any')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('python-pytest' 'python2-pytest') # 'python-django' 'python2-django') Test hangs
source=("$pkgbase-$pkgver.tar.gz::https://github.com/rbarrois/python-semanticversion/archive/v$pkgver.tar.gz")
sha512sums=('18db9279c2728565b13362c54bedbf569f0878cbe6bb58e631d87ffe7cff7d9131a30a2592cbf511091c03e854851159bbb298fe7469f53e8a2d92cf26ab4d0b')

prepare() {
  cp -a python-semanticversion-$pkgver{,-py2}
}

build() {
  cd "$srcdir"/python-semanticversion-$pkgver
  python setup.py build

  cd "$srcdir"/python-semanticversion-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/python-semanticversion-$pkgver
  rm tests/test_django.py
  py.test

  cd "$srcdir"/python-semanticversion-$pkgver-py2
  rm tests/test_django.py
  py.test2
}

package_python-semantic-version() {
  depends=('python')

  cd python-semanticversion-$pkgver
  python3 setup.py install --root="$pkgdir" --optimize=1
  install -D -m644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-semantic-version() {
  depends=('python2')

  cd python-semanticversion-$pkgver-py2
  python2 setup.py install --root="$pkgdir" --optimize=1
  install -D -m644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
