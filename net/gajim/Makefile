# $OpenBSD: Makefile,v 1.65 2014/01/02 11:35:18 jasper Exp $


COMMENT=	jabber client written in pygtk
DISTNAME=	gajim-0.16.1
EXTRACT_SUFX =	.tar.bz2
CATEGORIES=	net x11

MASTER_SITES=	${HOMEPAGE}/downloads/0.16/

HOMEPAGE=	http://www.gajim.org/

MAINTAINER=	Pierre-Emmanuel Andre <pea@openbsd.org>

# GPLv3 only
PERMIT_PACKAGE_CDROM=	Yes

CONFIGURE_STYLE=gnu
CONFIGURE_ENV=	CFLAGS="-I${LOCALBASE}/include" \
		LDFLAGS="-L${LOCALBASE}/lib"
CONFIGURE_ARGS=	${CONFIGURE_SHARED}

USE_GMAKE=	Yes
LIBTOOL_FLAGS=	--tag=disable-static

MODULES=	lang/python \
		textproc/intltool

COMMON_DEPENDS= databases/py-sqlite2 \
		net/py-dns \
		x11/dbus-python \
		x11/py-gtk2  \
		security/py-openssl \
		security/py-crypto \
		net/avahi,-python,no_mono,no_qt3,no_qt4 \
		net/py-nbxmpp \
		textproc/gtkspell \
		devel/py-notify

BUILD_DEPENDS=	${COMMON_DEPENDS}

RUN_DEPENDS=	${COMMON_DEPENDS} \
		devel/desktop-file-utils \
		devel/py-asn1 \
		x11/gtk+3,-guic

.include <bsd.port.mk>
