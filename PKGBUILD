pkgname=ccache
pkgver=3.7.8
pkgrel=1
pkgdesc='Compiler cache that speeds up recompilation by caching previous compilations'
url='https://ccache.dev/'
arch=('x86_64')
license=('GPL3')
depends=('zlib')
source=(https://github.com/ccache/ccache/releases/download/v${pkgver}/ccache-${pkgver}.tar.xz)
sha512sums=('dc8cc9cd5f6f054421f0ecb50f66e0af85222c347d59fecd4555dfe1d8d6cbdca304818de8bc8a39fc1a1225567c141ce104ac315369bf6c307e9da67e14b51c')

build() {
  cd ${pkgname}-${pkgver}
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc
  make
}

check() {
  cd ${pkgname}-${pkgver}
  make check
}

package() {
  cd ${pkgname}-${pkgver}

  install -Dm 755 ccache -t "${pkgdir}/usr/bin"
  install -Dm 644 doc/ccache.1 -t "${pkgdir}/usr/share/man/man1"
  install -Dm 644 doc/{AUTHORS,MANUAL,NEWS}.adoc README.md -t "${pkgdir}/usr/share/doc/${pkgname}"

  install -d "${pkgdir}/usr/lib/ccache/bin"
  local _prog
  for _prog in gcc g++ c++; do
    ln -s /usr/bin/ccache "${pkgdir}/usr/lib/ccache/bin/$_prog"
    ln -s /usr/bin/ccache "${pkgdir}/usr/lib/ccache/bin/${CHOST}-$_prog"
  done
  for _prog in cc clang clang++; do
    ln -s /usr/bin/ccache "${pkgdir}/usr/lib/ccache/bin/$_prog"
  done
}
