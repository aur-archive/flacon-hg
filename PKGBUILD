# Contributor: Gustavo Alvarez <sl1pkn07@gmail.com>

pkgname=flacon-hg
pkgver=0.8.0.105.8b29558
pkgrel=1
pkgdesc="Extracts individual tracks from one big audio file containing the entire album of music and saves them as separate audio files. (Mercurial Version)"
arch=('any')
url="http://code.google.com/p/flacon/"
license=('GPL')
depends=('python2' 'python2-pyqt' 'python2-chardet' 'flac' 'shntool' 'hicolor-icon-theme')
optdepends=('vorbis-tools: For OGG support'
            'mac: For APE support'
            'wavpack: For WavPack support'
            'ttaenc: For TrueAudio support'
            'lame: For MP3 support'
            'mp3gain: For MP3 Replay Gain support'
            'vorbisgain: For OGG Replay Gain support')
conflicts=('flacon')
provides=('flacon')
install=flacon.install
source=('flacon::hg+https://code.google.com/p/flacon/')
md5sums=('SKIP')
_hgrepo=flacon

pkgver() {
  cd "${_hgrepo}"
  echo $(cat flacon.py | grep FLACON_VERSION | cut -d "'" -f2).$(hg identify -n).$(hg identify -i | cut -c-7)
}

prepare() {
  rm -rf "${srcdir}/python"
  mkdir "${srcdir}/python"
  ln -s /usr/bin/python2 "${srcdir}/python/python"
  export PATH="${srcdir}/python":$PATH
  cd "${_hgrepo}"
  rm -fr distr
  sed 's|python$|&2|' -i $(find . -type f)
  sed 's|python|python2|' -i Makefile
}

build() {
  cd "${_hgrepo}"
  make
}

check() {
  cd "${_hgrepo}"
  python2 tests/flacon_tests.py
}

package() {
  cd "${_hgrepo}"
  make DESTDIR="${pkgdir}" install
}
