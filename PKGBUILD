# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Max Liebkies <mail@maxliebkies.de>

pkgbase=dotnet-core
pkgname=('dotnet-host' 'dotnet-runtime')
pkgver=2.0.0
pkgrel=1
arch=('x86_64')
url='https://www.microsoft.com/net/core'
license=('MIT')
depends=('gcc-libs' 'glibc')
options=('staticlibs')
source=("https://download.microsoft.com/download/5/F/0/5F0362BD-7D0A-4A9D-9BF9-022C6B15B04D/dotnet-runtime-${pkgver}-linux-x64.tar.gz")
sha256sums=('69ecad24bce4f2132e0db616b49e2c35487d13e3c379dabc3ec860662467b714')

package_dotnet-host() {
  pkgdesc='A generic driver for the .NET Core Command Line Interface'

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/bin,usr/share/licenses/dotnet-host}

  cp -dr --no-preserve='ownership' dotnet host "${pkgdir}"/opt/dotnet/
  install -m 644 *.txt -t "${pkgdir}"/usr/share/licenses/dotnet-host/
  ln -s /opt/dotnet/dotnet "${pkgdir}"/usr/bin/
}

package_dotnet-runtime() {
  pkgdesc='The .NET Core runtime'
  depends+=('dotnet-host' 'krb5' 'libunwind'  'lldb' 'lttng-ust' 'openssl-1.0' 'zlib'
            'libcurl.so' 'libuuid.so')
  provides=('dotnet-runtime-2.0')
  conflicts=('dotnet-runtime-2.0')

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/share/licenses}

  cp -dr --no-preserve='ownership' shared "${pkgdir}"/opt/dotnet/
  ln -s dotnet-host "${pkgdir}"/usr/share/licenses/dotnet-runtime
}

# vim:set ts=2 sw=2 et:
