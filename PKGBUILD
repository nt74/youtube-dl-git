# Maintainer: Nikos Toutountzoglou <nikos.toutou@gmail.com>

pkgname=youtube-dl-git
_reponame=youtube-dl
pkgver=2021.12.17.r200.g6fece0a96
pkgrel=1
pkgdesc="A command-line program to download videos from YouTube.com and a few more sites"
arch=('any')
url="https://ytdl-org.github.io/youtube-dl/"
license=('custom')
depends=('python')
makedepends=(
  'python-setuptools'
  'python-pypandoc'
  )
optdepends=(
  'ffmpeg: for video post-processing'
  'rtmpdump: for rtmp streams support'
  'atomicparsley: for embedding thumbnails into m4a files'
  'python-pycryptodome: for hlsnative downloader'
  )
provides=("youtube-dl-git=${pkgver}")
conflicts=(
  'youtube-dl-git'
  'youtube-dl'
  )
source=('git+https://github.com/ytdl-org/youtube-dl.git')
sha256sums=('SKIP')

pkgver() {
  git -C "$srcdir/$_reponame" describe --tags --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd ${_reponame}
  sed -i 's|etc/bash_completion.d|share/bash-completion/completions|' setup.py
  sed -i 's|etc/fish/completions|share/fish/vendor_completions.d|' setup.py
}

build() {
  cd ${_reponame}
  make all
}

package() {
  cd ${_reponame}
  python setup.py install --root="${pkgdir}/" --optimize=1
  mv "${pkgdir}/usr/share/bash-completion/completions/${_reponame}.bash-completion" \
    "${pkgdir}/usr/share/bash-completion/completions/${pkgname}"
  install -Dvm644 ${_reponame}.plugin.zsh "${pkgdir}/usr/share/zsh/site-functions/_${_reponame}"
  install -Dvm644 -t "${pkgdir}/usr/share/licenses/${_reponame}" LICENSE
}
