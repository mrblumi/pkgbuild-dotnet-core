# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Max Liebkies <mail@maxliebkies.de>

pkgbase=dotnet-core
pkgname=('dotnet-host' 'dotnet-runtime')
pkgver=2.0.4
pkgrel=1
arch=('x86_64')
url='https://www.microsoft.com/net/core'
license=('MIT')
depends=('gcc-libs' 'glibc')
options=('staticlibs')
source=("https://download.microsoft.com/download/2/B/2/2B2854E7-7EAE-4FE9-85D2-19ACCD716F18/dotnet-runtime-${pkgver}-linux-x64.tar.gz")
sha256sums=('9c0080bd82ea26a5721fa063885c5675071af9741693e90efeb8eea8c70ac6bc')

package_dotnet-host() {
  pkgdesc='A generic driver for the .NET Core Command Line Interface'

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/bin,usr/share/licenses/dotnet-host}

  cp -dr --no-preserve='ownership' dotnet host "${pkgdir}"/opt/dotnet/
  install -m 644 *.txt -t "${pkgdir}"/usr/share/licenses/dotnet-host/
  ln -s /opt/dotnet/dotnet "${pkgdir}"/usr/bin/
}

package_dotnet-runtime() {
  pkgdesc='The .NET Core runtime'
  depends+=('dotnet-host' 'icu' 'krb5' 'libunwind'  'lldb' 'lttng-ust' 'openssl-1.0' 'zlib'
            'libcurl.so' 'libuuid.so')
  provides=('dotnet-runtime-2.0')
  conflicts=('dotnet-runtime-2.0')

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/share/licenses}

  cp -dr --no-preserve='ownership' shared "${pkgdir}"/opt/dotnet/
  ln -s dotnet-host "${pkgdir}"/usr/share/licenses/dotnet-runtime
}

# vim:set ts=2 sw=2 et:
