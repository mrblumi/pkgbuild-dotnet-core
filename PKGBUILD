# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Max Liebkies <mail@maxliebkies.de>

pkgbase=dotnet-core
pkgname=('dotnet-host' 'dotnet-runtime')
pkgver=2.1.0
pkgrel=1
arch=('x86_64')
url='https://www.microsoft.com/net/core'
license=('MIT')
options=('staticlibs')
source=('https://download.microsoft.com/download/9/1/7/917308D9-6C92-4DA5-B4B1-B4A19451E2D2/dotnet-runtime-2.1.0-linux-x64.tar.gz')
sha256sums=('fee8973feb7f964a20be8ed7ff8e277d343b7a9ee032af2f4deb90913e58f638')

package_dotnet-host() {
  pkgdesc='A generic driver for the .NET Core Command Line Interface'

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/bin,usr/share/licenses/dotnet-host}
  cp -dr --no-preserve='ownership' dotnet host "${pkgdir}"/opt/dotnet/
  install -m 644 *.txt -t "${pkgdir}"/usr/share/licenses/dotnet-host/
  ln -s /opt/dotnet/dotnet "${pkgdir}"/usr/bin/
}

package_dotnet-runtime() {
  pkgdesc='The .NET Core runtime'
  depends=('dotnet-host' 'icu' 'krb5' 'lttng-ust' 'openssl-1.0' 'zlib'
           'libcurl.so')
  provides=('dotnet-runtime-2.1')
  conflicts=('dotnet-runtime-2.1')

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/share/licenses}
  cp -dr --no-preserve='ownership' shared "${pkgdir}"/opt/dotnet/
  ln -s dotnet-host "${pkgdir}"/usr/share/licenses/dotnet-runtime
}

# vim: ts=2 sw=2 et:
