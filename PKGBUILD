# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Max Liebkies <mail@maxliebkies.de>

pkgbase=dotnet-core
pkgname=('dotnet-host' 'dotnet-runtime')
pkgver=2.0.7
pkgrel=1
arch=('x86_64')
url='https://www.microsoft.com/net/core'
license=('MIT')
depends=('gcc-libs' 'glibc')
options=('staticlibs')
source=('https://download.microsoft.com/download/A/9/F/A9F8872C-48B2-41DB-8AAD-D5908D988592/dotnet-runtime-2.0.7-linux-x64.tar.gz')
sha256sums=('680ea40a1fafb7a6f93897df70077b64f0081b7d9b0f1358f5897ffd949d6b71')

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

# vim: ts=2 sw=2 et:
