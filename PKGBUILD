#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Build Failure. Package cannot find source directory
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

_downloadid='b17880a8bd654989a1641b0179c2db2f'
_referid='a621f90811c846f4bcd7016ec896311f'
_siteurl="https://www.blackmagicdesign.com/api/register/us/download/${_downloadid}"
_useragent="User-Agent: Mozilla/5.0 (X11; Linux ${CARCH}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36"
_reqjson="{ \
    \"platform\": \"Linux\", \
    \"country\": \"us\", \
    \"firstname\": \"Arch\", \
    \"lastname\": \"Linux\", \
    \"email\": \"someone@archlinux.org\", \
    \"phone\": \"202-555-0194\", \
    \"state\": \"New York\", \
    \"city\": \"AUR\", \
    \"hasAgreedToTerms\": true, \
    \"product\": \"Desktop Video ${pkgver} SDK\" \
}"

_srcurl="$(curl \
            -s \
            -H "$_useragent" \
            -H 'Content-Type: application/json;charset=UTF-8' \
            -H "Referer: https://www.blackmagicdesign.com/support/download/${_referid}/Linux" \
            --data-ascii "$_reqjson" \
            --compressed \
            "$_siteurl")"

DLAGENTS=("https::/usr/bin/curl \
              -gqb '' -C - --retry 3 --retry-delay 3 \
              -H Upgrade-Insecure-Requests:\ 1 \
              -H ${_useragent// /\\ } \
              -o %o \
              --compressed \
              %u")

pkgname=decklink-sdk
pkgver=12.2.2
pkgrel=2
epoch=1
pkgdesc='Blackmagic DeckLink SDK'
arch=('any')
url='https://www.blackmagicdesign.com/support/family/capture-and-playback'
license=('custom')
makedepends=('poppler')
provides=('blackmagic-decklink-sdk')
conflicts=('blackmagic-decklink-sdk')
replaces=('blackmagic-decklink-sdk')
source=("Blackmagic_DeckLink_SDK_${pkgver}.zip"::"$_srcurl")
sha256sums=('542ed9bdb888c06458379f939becc9dc6efc6787ef6b1d31e8c41f02df68541f')

prepare() {
    pdftotext -layout "Blackmagic DeckLink SDK ${pkgver}/End User License Agreement.pdf"
}

package() {
    install -D -m644 "Blackmagic DeckLink SDK ${pkgver}/End User License Agreement.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    cp -dr --no-preserve='ownership' "Blackmagic DeckLink SDK ${pkgver}/Linux/include" "${pkgdir}/usr"
}
