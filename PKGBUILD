# Maintainer: Eli Schwartz <eschwartz@archlinux.org>

_pkgname=httpcore
pkgname=python-httpcore
pkgver=0.14.3
pkgrel=1
pkgdesc="A minimal HTTP client"
arch=('any')
url="https://github.com/encode/${_pkgname}"
license=('BSD')
depends=('python-anyio' 'python-h11' 'python-sniffio')
optdepends=('python-h2: for HTTP/2 support')
makedepends=('python-setuptools' 'python-h2')
checkdepends=('hypercorn' 'python-curio' 'python-pproxy' 'python-pytest-asyncio' 'python-pytest-trio' 'python-trustme' 'uvicorn')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/${pkgver}.tar.gz")
sha512sums=('05e92109839c2e2f7ec81fea9507fb15a12d1bf6ae92048170953b1cb0139237b81c892feff1bc3840e06887e8916cadcc4124725874344524e45e3640a00379')
b2sums=('140c55af60f54ff13db958cecef50af2b8857837c00c2e5b1ec48d8866bc08146f608864a3dcaed0014505ba0ea10b8d457a763ecf434a0d40a2e11debdd4003')

prepare() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    # do not run coverage in unittests!
    sed -i '/^addopts/d' setup.cfg
}

build() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    python setup.py build
}

check() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    # raise open files limits, many tests will fail otherwise
    ulimit -S -n 4096

    python -m pytest
}

package() {
    cd "${srcdir}"/${_pkgname}-${pkgver}

    python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
    install -Dm644 LICENSE.md "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE.md
}
