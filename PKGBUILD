# Maintainer: Cosmo <cptncosmo@gmail.com>
pkgname=fluxer-bin
pkgver=0.0.8
pkgrel=1
pkgdesc="Fluxer Desktop Application"
arch=('x86_64' 'aarch64')
url="https://fluxer.app"
license=('AGPL-3.0')
depends=('gtk3' 'nss' 'alsa-lib')
options=('!strip')

source=("fluxer.desktop")
sha256sums=('c4f29013726c32cd70e9dfa830dc49895ea3824d302d8963cd6cd39d6cb54711')

source_x86_64=("fluxer-${pkgver}-x64.tar.gz::https://api.fluxer.app/dl/desktop/stable/linux/x64/latest/tar_gz")
sha256sums_x86_64=('acf6398fa6810720fed85b06c011b324e7db4fec6bf2fc7ad93c2446c3600f2d')

source_aarch64=("fluxer-${pkgver}-arm64.tar.gz::https://api.fluxer.app/dl/desktop/stable/linux/arm64/latest/tar_gz")
sha256sums_aarch64=('77b874a98caf48de5bc4ccf03119f45262fe26fd7be085b57d7b40b1505d0ec8')

package() {
    # Determine directory name based on architecture
    if [ "$CARCH" = "x86_64" ]; then
        _arch_dir="fluxer-stable-${pkgver}-x64"
    elif [ "$CARCH" = "aarch64" ]; then
        _arch_dir="fluxer-stable-${pkgver}-arm64"
    fi

    check_dir="${srcdir}/${_arch_dir}"
    
    # Fallback search if directory name is different
    if [ ! -d "$check_dir" ]; then
        cd "${srcdir}"
        # try to find directory matching pattern
        _arch_dir=$(ls -d fluxer-*-"${pkgver}"-* 2>/dev/null | head -n 1)
    fi

    if [ -z "$_arch_dir" ] || [ ! -d "${srcdir}/${_arch_dir}" ]; then
        echo "Error: Could not find extracted directory for architecture $CARCH"
        # Lists content of srcdir to help debugging
        ls -la "${srcdir}"
        return 1
    fi

    cd "${srcdir}/${_arch_dir}"

    install -d "${pkgdir}/opt/${pkgname}"
    cp -r . "${pkgdir}/opt/${pkgname}/"

    install -d "${pkgdir}/usr/bin"
    ln -s "/opt/${pkgname}/fluxer" "${pkgdir}/usr/bin/fluxer"

    install -Dm644 "${srcdir}/fluxer.desktop" "${pkgdir}/usr/share/applications/fluxer.desktop"
    
    if [ -f "resources/512x512.png" ]; then
        install -Dm644 "resources/512x512.png" "${pkgdir}/usr/share/icons/hicolor/512x512/apps/fluxer.png"
    fi
}
