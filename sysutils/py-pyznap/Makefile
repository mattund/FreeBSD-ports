# $FreeBSD$

PORTNAME=		pyznap
DISTVERSIONPREFIX=	v
DISTVERSION=		1.1.0
CATEGORIES=		sysutils python
PKGNAMEPREFIX=		${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	driesm.michiels@gmail.com
COMMENT=	ZFS snapshot tool written in Python

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}configparser>3.5.0:devel/py-configparser@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}paramiko>=2.4.2:security/py-paramiko@${PY_FLAVOR} \
		mbuffer:misc/mbuffer \
		pv:sysutils/pv

USES=		python:3.5+
USE_PYTHON=	autoplist concurrent distutils

USE_GITHUB=	yes
GH_ACCOUNT=	yboetz

NO_ARCH=	yes
SUB_FILES=	pkg-message
SUB_LIST=	BINDIR=${PREFIX}/bin ETCDIR=${PREFIX}/etc

post-patch:
	${REINPLACE_CMD} -e 's|/etc/pyznap/|${PREFIX}/etc/pyznap/|g' ${WRKSRC}/${PORTNAME}/main.py

.include <bsd.port.mk>
