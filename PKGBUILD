# $Id: PKGBUILD 168556 2012-10-13 11:43:27Z andyrtr $
# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Alexander Baldeck <Alexander@archlinux.org

pkgname=xf86-input-evdev-fedora
_pkgname=xf86-input-evdev
pkgver=2.7.3
pkgrel=3
pkgdesc="X.org evdev input driver, with patch from Fedora to fix qemu scroll wheel"
arch=(i686 x86_64)
url="http://xorg.freedesktop.org/"
license=('custom')
depends=('glibc' 'systemd-tools' 'mtdev')
makedepends=('xorg-server-devel' 'X-ABI-XINPUT_VERSION=19' 'resourceproto' 'scrnsaverproto')
conflicts=('xorg-server<1.14.0' 'X-ABI-XINPUT_VERSION<19' 'X-ABI-XINPUT_VERSION>=20' 'xf86-input-evdev')
provides=("xf86-input-evdev=$pkgver")
options=('!libtool' '!makeflags')
groups=('xorg-drivers' 'xorg')
source=(${url}/releases/individual/driver/${_pkgname}-${pkgver}.tar.bz2
        0001-Allow-relative-scroll-valuators-on-absolute-devices.patch)
sha256sums=('eb389413602c3d28c44bbfab0477c98582f0e2f5be5f41986e58e93a033fa504'
            '8094267c8671f7b1ac4c5d3b1f008f779b5a632e9ccd3b04cf5cdf51bdf75749')

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  patch -Np1 -i ../0001-Allow-relative-scroll-valuators-on-absolute-devices.patch

  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/"
}
