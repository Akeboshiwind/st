# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgname=st
pkgver=0.8.1
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
url="http://st.suckless.org"
_patches=("https://st.suckless.org/patches/clipboard/st-clipboard-0.8.1.diff"
          "https://st.suckless.org/patches/hidecursor/st-hidecursor-0.8.1.diff"
          "https://st.suckless.org/patches/scrollback/st-scrollback-0.8.diff"
          "https://st.suckless.org/patches/scrollback/st-scrollback-mouse-0.8.diff"
          "https://st.suckless.org/patches/scrollback/st-scrollback-mouse-altscreen-0.8.diff"
          "https://st.suckless.org/patches/spoiler/st-spoiler-20180309-c5ba9c0.diff"
          "https://st.suckless.org/patches/vertcenter/st-vertcenter-20180320-6ac8c8a.diff")
source=("http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz"
        "config.h"
        "${_patches[@]}")
sha256sums=('c4fb0fe2b8d2d3bd5e72763e80a8ae05b7d44dbac8f8e3bb18ef0161c7266926'
            'a9d436ae145cd557f48237ffc577e9f96d5a09a8036a31b12ede6838e9db0f84'
            'f22e0165aacb2bc86d000728c81f68022abcc601dbfd09e516e1ba772225d7e6'
            'bf3fe4e855f67fc9ae69b7328399ce06567f6aae3c9fb7fc8e7ec26c89e41dfd'
            '8279d347c70bc9b36f450ba15e1fd9ff62eedf49ce9258c35d7f1cfe38cca226'
            '3fb38940cc3bad3f9cd1e2a0796ebd0e48950a07860ecf8523a5afd0cd1b5a44'
            'e9f73c4de379d54ae107d0f4dd7b068a6628326c1bd7e11bfcd33d9079290347'
            'd947586a2059adbbcbd7c35733450530038aa5cf97c1e3e586728606ba6f8f4b'
            '04e6a4696293f668260b2f54a7240e379dbfabbc209de07bd5d4d57e9f513360')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/tic /d' Makefile

  # Apply patches
  for patch in "${_patches[@]}"; do
    echo "Applying patch $(basename $patch)..."
    patch -Np1 -i "$srcdir/$(basename $patch)"
  done

  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
