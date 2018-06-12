# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Max Liebkies <mail@maxliebkies.de>
# Contributor: Florian Maunier <fmaunier@gmail.com>

pkgbase=dotnet-core
pkgname=('dotnet-host' 'dotnet-runtime' 'aspnet-runtime')
pkgver=2.1.0
pkgrel=3
arch=('x86_64')
url='https://www.microsoft.com/net/core'
license=('MIT')
options=('staticlibs')
source=('https://download.microsoft.com/download/9/1/7/917308D9-6C92-4DA5-B4B1-B4A19451E2D2/aspnetcore-runtime-2.1.0-linux-x64.tar.gz')
sha256sums=('1f75c6d98cf729f74dfbeb5a36207567912e0e61e9bac0bf0f72046fa7a81d4b')

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

  install -dm 755 "${pkgdir}"/{opt/dotnet/shared,usr/share/licenses}
  cp -dr --no-preserve='ownership' shared/Microsoft.NETCore.App "${pkgdir}"/opt/dotnet/shared/
  ln -s dotnet-host "${pkgdir}"/usr/share/licenses/dotnet-runtime
}

package_aspnet-runtime() {
  pkgdesc='The ASP.NET Core runtime'
  depends=('dotnet-runtime')
  provides=('aspnet-runtime-2.1')
  conflicts=('aspnet-runtime-2.1')

  install -dm 755 "${pkgdir}"/{opt/dotnet/shared,usr/share/licenses}
  cp -dr --no-preserve='ownership' shared/Microsoft.AspNetCore.{All,App} "${pkgdir}"/opt/dotnet/shared/
  ln -s dotnet-host "${pkgdir}"/usr/share/licenses/aspnet-runtime
}

# vim: ts=2 sw=2 et:
