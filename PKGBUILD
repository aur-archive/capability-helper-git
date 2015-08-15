#pkgname=capability-helper
#pkgver=0.1

pkgname=capability-helper-git
pkgver=20120408
pkgrel=1
provides=('capability-helper=0.1')
conflicts=('capability-helper')
_gitroot='git://github.com/Blub/capability-helper.git'
_gitname='capability-helper'

pkgdesc="Helper configuration and scripts for non-setuid package variant install-scripts"
arch=('i686' 'x86_64')
license=('WTFPL')
url="https://github.com/Blub/capability-helper"
makedepends=('make')
depends=('libcap' 'sh' 'grep' 'sed')
# source=()

build() {
	cd "$srcdir"
	msg "Connecting to GIT server..."

	if [[ -d "$_gitname" ]]; then
		cd "$_gitname" && git pull origin
		msg "The local files are updated."
	else
		git clone "$_gitroot" "$_gitname"
	fi

	msg "GIT checkout done or server timeout"
	msg "Starting build..."

	rm -rf "$srcdir/$_gitname-build"
	git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
	cd "$srcdir/$_gitname-build"

	make
}

# TODO:
#check() {
#}

package() {
	cd "$srcdir/$_gitname-build"
	make DESTDIR="$pkgdir" install
}
