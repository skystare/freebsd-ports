# Created by: Pedro F. Giffuni <giffunip@tutopia.com>
# $FreeBSD$

PORTNAME=	silo
PORTVERSION=	4.10.2
DISTVERSIONSUFFIX=	-bsd
PORTREVISION=	8
CATEGORIES=	science
MASTER_SITES=	http://wci.llnl.gov/content/assets/docs/simulation/computer-codes/${PORTNAME}/silo-${PORTVERSION}/

MAINTAINER=	dbaio@FreeBSD.org
COMMENT=	Mesh and field I/O library and scientific database

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/COPYRIGHT

USES=		gmake libtool readline
USE_LDCONFIG=	yes

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--enable-shared --disable-static
INSTALL_TARGET=	install-strip

OPTIONS_DEFINE=			FORTRAN HDF5 PYTHON QT4
OPTIONS_DEFAULT=		HDF5
OPTIONS_SUB=			yes

FORTRAN_CONFIGURE_ENABLE=	fortran
FORTRAN_USES=			fortran

HDF5_LIB_DEPENDS=		libhdf5.so:science/hdf5
HDF5_CONFIGURE_ON=		--with-hdf5=${LOCALBASE}/include,${LOCALBASE}/lib
HDF5_PLIST_SUB=			SUFX_HDF5="h5"
HDF5_PLIST_SUB_OFF=		SUFX_HDF5=""

PYTHON_CONFIGURE_ENABLE=	pythonmodule
PYTHON_USES=			python:2.7

QT4_USES=			qmake:no_env qt:4
QT4_USE=			XORG=ice,sm,x11,xext,xi,xmu,xt \
				QT=corelib,gui,linguisttools_build,moc_build,uic_build
QT4_CONFIGURE_ON=		--with-Qt-dir=${PREFIX} \
				--with-Qt-lib="QtGui -lQtCore"
QT4_CONFIGURE_ENABLE=		silex
QT4_DESKTOP_ENTRIES=		"Silex" "Silex browser for Silo files" \
				"" "silex" "" true

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MQT4}
DEPRECATED=		Qt4 has been EOL since december 2015
EXPIRATION_DATE=	2019-03-15
.endif

post-patch:
	@${REINPLACE_CMD} -e \
		's|\(_Qt_dir/include\)"|\1/qt4"| ; \
		 s|\(_Qt_dir/lib\)"|\1/qt4"| ; \
		 s|\(/uic\)"|\1-qt4"| ; \
		 s|\(/moc\)"|\1-qt4"| ; \
		 s|\(/lrelease\)"|\1-qt4"| ; \
		 s|\(/lupdate\)"|\1-qt4"|' ${WRKSRC}/configure
	@${REINPLACE_CMD} -e \
		'/-avoid-version/s|^|#| ; \
		 /^install-data-am/s|:.*|:|' ${WRKSRC}/src/Makefile.in
	@${REINPLACE_CMD} -e \
		'/-ldl/s|^|#|' ${WRKSRC}/tests/Makefile.in
	@${REINPLACE_CMD} -e \
		's|@libdir@|@pythondir@|' ${WRKSRC}/tools/python/Makefile.in
	@${REINPLACE_CMD} -e \
		's|\(INBUILD\));|\1, me);|' ${WRKSRC}/src/hdf5_drv/silo_hdf5.c

.if defined(MAINTAINER_MODE)
regression-test: build
	@cd ${WRKSRC}/tests && ${SETENV} ${MAKE_ENV} ${MAKE_CMD} check
.endif

.include <bsd.port.mk>
