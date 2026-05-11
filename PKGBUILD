# Maintainer: BadBoy <luckmelove2@gmail.com>

pkgname='gui-for-singbox'
_pkgname='GUI.for.SingBox'
pkgver='1.24.0'
pkgrel='1'
pkgdesc='GUI for SingBox'
arch=('x86_64')
url="https://github.com/GUI-for-Cores/${_pkgname}"
license=('GPL3')
depends=(
    'glibc'
    'webkit2gtk-4.1'
)
provides=("${pkgname}")
conflicts=("${pkgname}")
install="${pkgname}.install"
source=(
    "${url}/releases/download/v${pkgver}/${_pkgname}-linux-amd64.zip"
    "${pkgname}.desktop"
    "https://raw.githubusercontent.com/GUI-for-Cores/${_pkgname}/main/build/appicon.png"
    "${pkgname}.install"
)
sha256sums=('SKIP'
            '7c4b032bc966c20889bb87a328afa34d4ae191d2171c084ba99f959aa6429c8b'
            '08257d0d21c76a56e48e38105460927293a452ddc6b0b62db401bf5b5b9b7adf'
            'f20042b6b20131c6b8ae40b5ed321b9707f6755d5fe06c7474922d753c476c24')

package() {
    msg "Packaging ${pkgname}"
    install -dm755 "${pkgdir}/opt/${pkgname}"
    bsdtar -xf "${_pkgname}-linux-amd64.zip" -C "${pkgdir}/opt/${pkgname}"
    chmod 755 "${pkgdir}/opt/${pkgname}/${_pkgname}"
    install -Dm644 "appicon.png" "${pkgdir}/opt/${pkgname}/icon/${pkgname}.png"
    install -Dm644 "${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
}
