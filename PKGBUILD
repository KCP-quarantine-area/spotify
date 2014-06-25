pkgname=spotify
pkgver=0.9.10.17
_anotherpkgver=.g4129e1c.78
pkgrel=1
pkgdesc="A proprietary peer-to-peer music streaming service"
arch=('x86_64')
_carch=('_amd64')
license=('custom:"Copyright (c) 2006-2013 Spotify Ltd"')
install=spotify.install
url="http://www.spotify.com"
changelog='spotify.changelog'
options=('!strip')

md5sums+=('379cd63fb9f138928b30e3586a20ef29'
'8d7059f889257fca61edb926bf419111'
'ef25ddc5b6bf8fe1a0d64cbd79e1f7b4')

depends=("alsa-lib>=1.0.14" "glibc>=2.6" "libxss" "qtwebkit" "gconf" "nspr>=4.0"
         "nspr<5.0" "nss" "dbus" "systemd" "libgcrypt15" "gtk2")
optdepends=('desktop-file-utils: Adds URI support to compatible desktop environments'
            'ffmpeg-compat: Adds support for playback of local files')
source=("http://repository.spotify.com/pool/non-free/s/${pkgname}/${pkgname}-client_${pkgver}${_anotherpkgver}-${pkgrel}${_carch}.deb"
'spotify'
'spotify.protocol')

package() {
  cd "${srcdir}"

  ar x "${pkgname}-client_${pkgver}${_anotherpkgver}-${pkgrel}${_carch}.deb" > /dev/null
  tar -xzf data.tar.gz -C "${pkgdir}"

  install -d "${pkgdir}/usr/share/"
  mv "${pkgdir}/opt/spotify" "${pkgdir}/usr/share/"
  rm -r "${pkgdir}/opt"

  install -d "${pkgdir}/usr/share/spotify/libs/"

  # Bin Script
  install -Dm755 "${srcdir}/spotify" "${pkgdir}/usr/bin/spotify"

  # libplc4.so
  ln -s /usr/lib/libplc4.so "${pkgdir}/usr/share/spotify/libs/libplc4.so.0d"

  # libnspr4.so
  ln -s /usr/lib/libnspr4.so "${pkgdir}/usr/share/spotify/libs/libnspr4.so.0d"

  # libnss3.so
  ln -s /usr/lib/libnss3.so "${pkgdir}/usr/share/spotify/libs/libnss3.so.1d"

  # libnssutil3.so
  ln -s /usr/lib/libnssutil3.so "${pkgdir}/usr/share/spotify/libs/libnssutil3.so.1d"

  # libsmime3.so
  ln -s /usr/lib/libsmime3.so "${pkgdir}/usr/share/spotify/libs/libsmime3.so.1d"

  # libudev.so
  ln -s /usr/lib/libudev.so "${pkgdir}/usr/share/spotify/libs/libudev.so.0"

  # openssl
  ln -s /usr/lib/libssl.so "${pkgdir}/usr/share/spotify/libs/libssl.so.0.9.8"
  ln -s /usr/lib/libcrypto.so "${pkgdir}/usr/share/spotify/libs/libcrypto.so.0.9.8"

  # Copy license
  install -Dm644 "${pkgdir}/usr/share/doc/${pkgname}-client/copyright" "${pkgdir}/usr/share/licenses/${pkgname}/copyright"

  # Copy protocol file if KDE is installed
  if [ -f /usr/bin/startkde ]; then
    echo "Installing with KDE support"
    install -Dm644 "${srcdir}/spotify.protocol" "${pkgdir}/usr/share/kde4/services/spotify.protocol"
  fi
}
