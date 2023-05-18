# Maintainer: Bardia Moshiri <fakeshell@bardia.tech>

pkgname=pulseaudio-module-keepalive
pkgver=14.2
pkgrel=1
pkgdesc="PulseAudio keepalive module"
arch=('x86_64' 'aarch64')
url="https://github.com/sailfishos/pulseaudio-module-keepalive"
license=('LGPLv2+')
depends=('pulseaudio-hybris')
makedepends=('meson' 'pulsecore-headers')
source=('pulseaudio-module-keepalive::git+https://github.com/sailfishos/pulseaudio-module-keepalive'
        'module-version.patch')
sha256sums=('SKIP'
            'bc304be0394b1a2b9c30beee493d7a4d50cf850db38c14821fdb80a8d2c5590f')

prepare() {
    cd pulseaudio-module-keepalive
    echo "14.2" > .tarball-version

    local src
    for src in "${source[@]}"; do
      src="${src%%::*}"
      src="${src##*/}"
      [[ $src = *.patch ]] || continue
      echo "Applying patch $src..."
      patch -Np1 < "../$src"
    done
}

build() {
  cd pulseaudio-module-keepalive
  meson --prefix=/usr build
  cd build
  ninja
}

package() {
  cd pulseaudio-module-keepalive/build
  mkdir -p ${pkgdir}/usr/lib/pulse-14.2/modules
  cp src/*.so ${pkgdir}/usr/lib/pulse-14.2/modules/
}
