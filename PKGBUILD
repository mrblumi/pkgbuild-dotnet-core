# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Max Liebkies <mail@maxliebkies.de>

pkgbase=dotnet-core
pkgname=('dotnet-host' 'dotnet-runtime' 'aspnet-runtime' 'dotnet-sdk')
pkgver=2.1.2+302
pkgrel=1
arch=('x86_64')
url='https://www.microsoft.com/net/core'
license=('MIT')
makedepends=(
  'clang' 'cmake' 'curl' 'git' 'icu' 'krb5' 'libunwind' 'lldb' 'llvm'
  'lttng-ust' 'openssl-1.0' 'zlib'
)
options=('staticlibs')
_commit='1dd84aaa2e44f1694ce0e681f96b6cd4e79f48ff'
source=(
  "dotnet-source-build::git+https://github.com/dotnet/source-build.git#tag=v${pkgver/[0-9]\+}"
  'dotnet-application-insights::git+https://github.com/Microsoft/ApplicationInsights-dotnet.git'
  'dotnet-cli::git+https://github.com/dotnet/cli.git'
  'dotnet-cli-migrate::git+https://github.com/dotnet/cli-migrate.git'
  'dotnet-clicommandlineparser::git+https://github.com/dotnet/clicommandlineparser.git'
  'dotnet-common::git+https://github.com/aspnet/common.git'
  'dotnet-core-setup::git+https://github.com/dotnet/core-setup.git'
  'dotnet-coreclr::git+https://github.com/dotnet/coreclr.git'
  'dotnet-corefx::git+https://github.com/dotnet/corefx.git'
  'dotnet-fsharp::git+https://github.com/Microsoft/VisualFSharp.git'
  'dotnet-msbuild::git+https://github.com/Microsoft/msbuild.git'
  'dotnet-newtonsoft-json::git+https://github.com/JamesNK/Newtonsoft.Json.git'
  'dotnet-nuget-client::git+https://github.com/NuGet/NuGet.Client.git'
  'dotnet-roslyn::git+https://github.com/dotnet/roslyn.git'
  'dotnet-roslyn-tools::git+https://github.com/dotnet/roslyn-tools.git'
  'dotnet-sdk::git+https://github.com/dotnet/sdk.git'
  'dotnet-standard::git+https://github.com/dotnet/standard.git'
  'dotnet-templating::git+https://github.com/dotnet/templating.git'
  'dotnet-vstest::git+https://github.com/Microsoft/vstest.git'
  'dotnet-websdk::git+https://github.com/aspnet/websdk.git'
  'dotnet-xliff-tasks::git+https://github.com/dotnet/xliff-tasks.git'
  'https://download.microsoft.com/download/1/f/7/1f7755c5-934d-4638-b89f-1f4ffa5afe89/aspnetcore-runtime-2.1.2-linux-x64.tar.gz'
  'dotnet-coreclr-rid.patch'
)
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            '08459d8bfb3c177ee93ae1271d4a81d50f12f8ab6232c86c81142a79e1bb237f'
            '2c4fc48151e5319d57c8761091709070a17da91eddc2de8a26bc32c60679bfee')

prepare() {
  cd dotnet-source-build

  for submodule in src/{application-insights,cli,cli-migrate,clicommandlineparser,common,core-setup,coreclr,corefx,fsharp,msbuild,newtonsoft-json,nuget-client,roslyn,roslyn-tools,sdk,standard,templating,vstest,websdk,xliff-tasks}; do
    git submodule init ${submodule}
    git config submodule.${submodule}.url ../dotnet-${submodule#src/}
    git submodule update
  done

  cd src/coreclr

  patch -Np1 -i "${srcdir}"/dotnet-coreclr-rid.patch
}

build() {
  cd dotnet-source-build

  export PKG_CONFIG_PATH='/usr/lib/openssl-1.0/pkgconfig'
  export SOURCE_BUILD_SKIP_SUBMODULE_CHECK=1

  ./build.sh
}

package_dotnet-host() {
  pkgdesc='A generic driver for the .NET Core Command Line Interface'

  cd dotnet-source-build/bin/x64/Release

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/bin,usr/share/licenses/dotnet-host}
  tar -C "${pkgdir}"/opt/dotnet -xf dotnet-sdk-${pkgver/[0-9]\+}-linux-x64.tar.gz ./dotnet ./host
  tar -C "${pkgdir}"/usr/share/licenses/dotnet-host -xf dotnet-sdk-${pkgver/[0-9]\+}-linux-x64.tar.gz ./LICENSE.txt ./ThirdPartyNotices.txt
  chown root:root -R "${pkgdir}"/opt/dotnet
  ln -s /opt/dotnet/dotnet "${pkgdir}"/usr/bin/
}

package_dotnet-runtime() {
  pkgdesc='The .NET Core runtime'
  depends=('dotnet-host' 'icu' 'krb5' 'libunwind' 'openssl-1.0' 'zlib'
           'libcurl.so')
  optdepends=('lttng-ust: CoreCLR tracing')
  provides=('dotnet-runtime-2.1')
  conflicts=('dotnet-runtime-2.1')

  cd dotnet-source-build/bin/x64/Release

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/share/licenses}
  tar -C "${pkgdir}"/opt/dotnet -xf dotnet-sdk-${pkgver/[0-9]\+}-linux-x64.tar.gz ./shared
  chown root:root -R "${pkgdir}"/opt/dotnet
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

package_dotnet-sdk() {
  pkgdesc='The .NET Core SDK'
  depends=('dotnet-runtime')
  provides=('dotnet-sdk-2.1')
  conflicts=('dotnet-sdk-2.1')

  cd dotnet-source-build/bin/x64/Release

  install -dm 755 "${pkgdir}"/{opt/dotnet,usr/share/licenses}
  tar -C "${pkgdir}"/opt/dotnet -xf dotnet-sdk-${pkgver/[0-9]\+}-linux-x64.tar.gz ./sdk
  chown root:root -R "${pkgdir}"/opt/dotnet
  ln -s dotnet-host "${pkgdir}"/usr/share/licenses/dotnet-sdk
}

# vim: ts=2 sw=2 et:
