# Created by: jrhett@netconsonance.com
# $FreeBSD$

PORTNAME=	cfengine
PORTVERSION=	3.5.3
PORTREVISION=	15
CATEGORIES=	sysutils
MASTER_SITES=	https://s3.amazonaws.com/cfengine.package-repos/tarballs/

MAINTAINER=	cy@FreeBSD.org
#		gjb@FreeBSD.org is also committer for this port
#		skreuzer@FreeBSD.org is also committer for this port
COMMENT=	Systems administration tool for networks

DEPRECATED=		OpenSSL 1.1.X is not supported.
EXPIRATION_DATE=	2021-09-30

LICENSE=	GPLv3

CPE_VENDOR=	gnu

LIB_DEPENDS=	libpcre.so:devel/pcre

CONFLICTS=	cfengine-2* cfengine3[0-46-9]-* cfengine31[0-9]-*
.if !defined(MASTERDIR)
PKGNAMESUFFIX=	35
CONFLICTS+=	cfengine-3.*
.endif

FETCH_BEFORE_ARGS=	-o ${DISTDIR}/${DISTFILES}

USE_RC_SUBR=	cf-execd cf-serverd cf-monitord

USES=		cpe gmake libtool ssl
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CFLAGS+=	-Wno-return-type
CFLAGS+=	-I${OPENSSLINC}
LDFLAGS+=	-L${OPENSSLLIB}
# EXAMPLESDIR=	${PREFIX}/share/examples/cfengine3
DOCSDIR=	${PREFIX}/share/doc/cfengine
CONFIGURE_ARGS=	--docdir=${DOCSDIR} \
		--htmldir=${DOCSDIR}/html \
		--libexecdir=${PREFIX}/libexec \
		--libdir=${PREFIX}/libexec \
		--mandir=${PREFIX}/man \
		--with-workdir=/var/cfengine \
		--with-pcre=${LOCALBASE} \
		--enable-fhs
INSTALL_TARGET=	install-strip

OPTIONS_DEFINE=	PGSQL MYSQL LIBVIRT
OPTIONS_SINGLE=	DB
OPTIONS_SINGLE_DB=	TOKYOCABINET QDBM
TOKYOCABINET_DESC=	Enable TokyoCabinet database backend
QDBM_DESC=	Enable QDBM database backend
OPTIONS_DEFAULT=TOKYOCABINET

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MTOKYOCABINET}
CONFIGURE_ARGS+=	--with-tokyocabinet=${LOCALBASE}
LIB_DEPENDS+=	libtokyocabinet.so:databases/tokyocabinet
.endif

.if ${PORT_OPTIONS:MQDBM}
CONFIGURE_ARGS+=	--with-qdbm=${LOCALBASE}
LIB_DEPENDS+=	libqdbm.so:databases/qdbm
.endif

.if ${PORT_OPTIONS:MPGSQL}
USES+=			pgsql
CONFIGURE_ARGS+=	--with-postgresql=${LOCALBASE}
.endif

.if ${PORT_OPTIONS:MMYSQL}
USES+=			mysql
BROKEN=			configure: error: MySQL client library exports symbols (EVP_CIPHER_CTX_init) clashing with OpenSSL.
CONFIGURE_ARGS+=	--with-mysql=${LOCALBASE}
LIB_DEPENDS+=		libmysqlclient.so:${_MYSQL_CLIENT}
LDFLAGS+=		-L${LOCALBASE}/lib/mysql
.endif

.if ${PORT_OPTIONS:MLIBVIRT}
CONFIGURE_ARGS+=	--with-libvirt=${LOCALBASE}
LIB_DEPENDS+=		libvirt.so:devel/libvirt
.endif

.include <bsd.port.pre.mk>

.if ${OPSYS} == "FreeBSD" && ${OSVERSION} >= 1200085
.if ${SSL_DEFAULT} != "openssl"
BROKEN_FreeBSD_12=	fails to build with openssl111, install security/openssl
BROKEN_FreeBSD_13=	fails to build with openssl111, install security/openssl
.endif
.endif

.include <bsd.port.post.mk>
