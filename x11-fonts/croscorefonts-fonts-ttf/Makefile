# Created by: Pedro Giffuni
# $FreeBSD$

PORTNAME=	croscorefonts
PORTVERSION=	1.31.0
CATEGORIES=	x11-fonts
MASTER_SITES=	http://gsdview.appspot.com/chromeos-localmirror/distfiles/ \
		LOCAL/sunpoet

MAINTAINER=	office@FreeBSD.org
COMMENT=	Fonts created from by Google for ChromeOS to replace MS TTF

LICENSE=	APACHE20

NO_ARCH=	yes
NO_BUILD=	yes
USES=		fonts tar:bzip2
USE_XORG=	x11

SUB_FILES=	pkg-message

FONTNAME=	ChromeOS

do-install:
	${MKDIR} ${STAGEDIR}${FONTSDIR}/
	${INSTALL_DATA} ${WRKSRC}/*.ttf ${STAGEDIR}${FONTSDIR}/

.include <bsd.port.mk>
