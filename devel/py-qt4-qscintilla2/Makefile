# Created by: Danny Pansters <danny@ricin.com>
# $FreeBSD$

PORTNAME=	qscintilla2
PORTVERSION=	${QSCI2_VERSION}
PORTREVISION=	1
PORTEPOCH=	1
CATEGORIES=	devel python
MASTER_SITES=	${MASTER_SITES_QSCI2}
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}qt4-
DISTNAME=	${QSCI2_DISTNAME}

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Python bindings for QScintilla2 (PyQt4), QSci module

DEPRECATED=		Qt4 has been EOL since december 2015
EXPIRATION_DATE=	2019-03-15

LIB_DEPENDS=	libqscintilla2_qt4.so:devel/qscintilla2

DISTINFO_FILE=	${.CURDIR:H}/qscintilla2/distinfo
DESTDIRNAME=	INSTALL_ROOT

HAS_CONFIGURE=	yes

USES=		python pyqt:4 qmake:no_env qt:4
USE_PYQT=	sip core gui
USE_PYTHON=	concurrent flavors py3kplist
USE_QT=		corelib gui moc_build qmake_build

OPTIONS_DEFINE=		DEBUG
DEBUG_CONFIGURE_ON=	--debug --trace

PYQT_APIDIR=	${PREFIX}/share/qt4/qsci
CONFIGURE_ARGS=	--pyqt PyQt4 -d ${PYTHONPREFIX_SITELIBDIR}/PyQt4 -v ${PYQT_SIPDIR} \
		--apidir ${PYQT_APIDIR} --qmake ${QMAKE} --pyqt-sipdir ${PYQT_SIPDIR} \
		--sip ${SIP}
WRKSRC=		${WRKDIR}/${DISTNAME}/Python
ALL_TARGET=	#empty

do-configure:
	cd ${WRKSRC} && ${SETENV} ${CONFIGURE_ENV}\
		${PYTHON_CMD} configure.py ${CONFIGURE_ARGS}

.include <bsd.port.mk>
