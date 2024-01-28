# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_npmname=nopt
pkgname=nodejs-$_npmname
pkgver=7.2.0
pkgrel=1
pkgdesc="Node/npm Option Parsing library"
arch=('any')
url="https://github.com/npm/nopt"
license=('custom:ISC')
depends=('nodejs')
makedepends=('npm')
source=("https://registry.npmjs.org/$_npmname/-/$_npmname-$pkgver.tgz")
noextract=($_npmname-$pkgver.tgz)
sha256sums=('bb53479b5329f2a66322c48f910ed6532c71bfe6f081b2b48fd2d62bfbe883a8')
options=("!strip")

package() {
  local \
    _build
  _build="${srcdir}/_build"
  mkdir \
    -p \
    "${_build}"
  npm \
    install \
        -g \
        --prefix \
	  "${_build}/usr" \
	  "${srcdir}/${_npmname}-${pkgver}.tgz"
  # Non-deterministic race in npm gives
  # 777 permissions to random directories.
  # See https://github.com/npm/npm/issues/9359
  # for details.
  chmod \
    -R u=rwX,go=rX \
    "${_build}/"*

  # npm installs package.json owned by build user
  # https://bugs.archlinux.org/task/63396
  chown \
    -R \
      0:0 \
    "${_build}/"* || \
    true
  mv \
    "${_build}/"* \
    "${pkgdir}"
  install \
    -d \
      "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "../../../lib/node_modules/${_npmname}/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set sw=2 sts=-1 et:
