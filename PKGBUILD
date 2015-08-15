# Maintainer: Andy Bryson <agbryson@gmail.com>
pkgname=goldencheetah-git
pkgver=20130317
pkgrel=1
pkgdesc="Cycling Performance Software"
url="http://goldencheetah.org/"
arch=('x86_64' 'i686')
license=('GPL2')
depends=('libftd2xx' 'qt4' 'git' 'qtwebkit' 'clucene' 'flex' 'bison' 'libical' 'liboauth' 'vlc')
install=""
source=(gcconfig.patch README) 
md5sums=('c4e5216bbd3b08376d2198608fb527f4'
         '43809cb0214ee4e5688c2fcdd13cb086')

_gitroot="git://github.com/GoldenCheetah/GoldenCheetah.git"
_gitname="master"
 
build() {
    cd "$srcdir"
 
    msg "Connecting to GIT server...."
    if [[ -d $_gitname ]]; then
        cd "$_gitname"
        git checkout "$_gitname"
        git pull origin "$_gitname"
        msg "The local files are updated."
    else
        git clone --depth 1 "$_gitroot" "$_gitname"
        cd "$_gitname"
        git checkout "$_gitname"
    fi
    msg "GIT checkout done or server timeout"
 
    # TODO: How should I deal with this?
    #sudo cp /usr/lib/CLucene/clucene-config.h /usr/include/CLucene
    patch -i ../../gcconfig.patch -o src/gcconfig.pri src/gcconfig.pri.in
    cp qwt/qwtconfig.pri.in qwt/qwtconfig.pri
 
    qmake-qt4 -recursive .
    make
}
 
package() {
    install -Dm755 "$_gitname/src/GoldenCheetah" "$pkgdir/usr/bin/GoldenCheetah"
}
