# $FreeBSD$

PORTNAME=	simgear
PORTVERSION=	2018.2.2
PORTREVISION=	1
CATEGORIES=	devel games
MASTER_SITES=	SF/flightgear/release-${PORTVERSION:R}

MAINTAINER=	martymac@FreeBSD.org
COMMENT=	Toolkit for 3D games and simulations

LICENSE=	GPLv2

BUILD_DEPENDS=	${LOCALBASE}/lib/libplibsl.a:x11-toolkits/plib
RUN_DEPENDS=	${LOCALBASE}/lib/libplibsl.a:x11-toolkits/plib
LIB_DEPENDS=	libboost_thread.so:devel/boost-libs \
		libosg.so:graphics/osg

USES=		alias cmake compiler:c++11-lib cpe gl jpeg openal:al,alut \
		tar:bzip2
USE_XORG=	ice sm x11 xext xi xmu xt
USE_GL=		gl glu glut

LDFLAGS_mips=	-losgDB
LDFLAGS_mips64=	-losgDB
LDFLAGS_powerpc64=	-losgDB
LDFLAGS_powerpc=	-losgDB
LDFLAGS_powerpcspe=	-losgDB
LDFLAGS_sparc64=	-losgDB

.include <bsd.port.mk>
