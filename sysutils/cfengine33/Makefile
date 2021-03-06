# Created by: jrhett@netconsonance.com
# $FreeBSD$

PORTNAME=	cfengine
PORTVERSION=	3.3.8
PORTREVISION=	14
CATEGORIES=	sysutils
MASTER_SITES=	https://s3.amazonaws.com/cfengine.package-repos/tarballs/
PKGNAMESUFFIX=	33

MAINTAINER=	cy@FreeBSD.org
#		gjb@FreeBSD.org is also committer for this port
#		skreuzer@FreeBSD.org is also committer for this port
COMMENT=	Systems administration tool for networks
CPE_VENDOR=	gnu

DEPRECATED=		OpenSSL 1.1.X is not supported.
EXPIRATION_DATE=	2021-09-30

FETCH_BEFORE_ARGS=	-o ${DISTDIR}/${DISTFILES}

CONFLICTS=	cfengine-2* cfengine-3.[124-9]* cfengine-devel-* \
		cfengine3[0124-9]-* cfengine31[0-9]-*

USE_RC_SUBR=	cf-execd cf-serverd

USES=		cpe gmake libtool ssl
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CFLAGS+=	-I${OPENSSLINC}
LDFLAGS+=	-L${OPENSSLLIB}
# EXAMPLESDIR=	${PREFIX}/share/examples/cfengine3
DOCSDIR=	${PREFIX}/share/doc/cfengine
CONFIGURE_ARGS=	--docdir=${DOCSDIR} \
		--htmldir=${DOCSDIR}/html \
		--with-pcre=${LOCALBASE} \
		--enable-fhs
CFLAGS+=	-Wno-error=implicit-function-declaration

LIB_DEPENDS+=	libpcre.so:devel/pcre

OPTIONS_DEFINE=	PGSQL MYSQL LIBVIRT
OPTIONS_SINGLE=	DB
OPTIONS_SINGLE_DB=	TOKYOCABINET QDBM
TOKYOCABINET_DESC=	Enable TokyoCabinet database backend
QDBM_DESC=	Enable QDBM database backend
PGSQL_DESC=	Enable PostgreSQL integration
MYSQL_DESC=	Enable MySQL integration
LIBVIRT_DESC=	Enable libvirt integration
OPTIONS_DEFAULT=TOKYOCABINET

post-patch:
	@${REINPLACE_CMD} -e '/^htmldir/s!=.*!= @htmldir@!' \
		${WRKSRC}/docs/Makefile.in

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
