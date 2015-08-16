# Joshua Netterfield <drmrshdw@gmail.com>
# Based on the PKGBUILD for pensil-svn

pkgname="hathor-svn"
pkgver=65
pkgrel=3
pkgdesc="A better music player built on last.fm and Rdio"
url="http://hathor.nettek.ca"
license=("GPL2")
arch=("i686" "x86_64")
depends=("qt" "qoauth" "liblastfm" "flashplugin" "phonon" "taglib")
makedepends=("subversion")
source=()
md5sums=()

_svntrunk="http://hathor.googlecode.com/svn/trunk/"
_svnmod="hathor-svn-2"

build() {
	msg "Connecting to SVN server..."
	if [ -d ${_svnmod}/.svn ]; then
		(cd "${_svnmod}" && svn cleanup && svn update -r ${pkgver})
	else
		svn co ${_svntrunk} ${_svnmod} -r ${pkgver} --config-dir ./
	fi

	cd ${_svnmod}
	qmake
	make clean
	make -j2

	# install headers
	install -d ${pkgdir}/usr/include/libhathor
	install libhathor/*.h ${pkgdir}/usr/include/libhathor

	install -d ${pkgdir}/usr/lib
	install -d ${pkgdir}/usr/bin
	install -D -m755 "hathor/hathor" "${pkgdir}/usr/bin/hathor"
	install -D -m755 "libhathor/libhathor.so.1.0.0" "${pkgdir}/usr/lib/libhathor.so.1.0.0"
	ln -s "${pkgdir}/usr/lib/libhathor.so.1.0.0" "${pkgdir}/usr/lib/libhathor.so.1.0"
	ln -s "${pkgdir}/usr/lib/libhathor.so.1.0.0" "${pkgdir}/usr/lib/libhathor.so.1"
	ln -s "${pkgdir}/usr/lib/libhathor.so.1.0.0" "${pkgdir}/usr/lib/libhathor.so"

	install -d ${pkgdir}/usr/share/hathor-20120128/plugins
	install -m755 hathor/plugins/*.so "${pkgdir}/usr/share/hathor-20120128/plugins/"
}

# vim: set noet ff=unix:
