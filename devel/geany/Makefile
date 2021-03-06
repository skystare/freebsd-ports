# Created by: Remington Lang <MrL0Lz@gmail.com>
# $FreeBSD$

PORTNAME=	geany
PORTVERSION=	1.33
PORTREVISION=	1
CATEGORIES=	devel editors
MASTER_SITES=	http://download.geany.org/ SF

MAINTAINER=	madpilot@FreeBSD.org
COMMENT=	Fast and lightweight GTK+ IDE

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2

USES=		compiler:c++11-lang desktop-file-utils gettext-tools gmake libtool \
		localbase pathfix pkgconfig tar:bzip2
GNU_CONFIGURE=	yes
INSTALLS_ICONS=	yes
USE_GNOME=	cairo gtk20 intltool
USE_LDCONFIG=	yes
INSTALL_TARGET=	install-strip

OPTIONS_DEFINE=	VTE NLS DOCS
OPTIONS_DEFAULT=	VTE
OPTIONS_SUB=	yes

NLS_USES=	gettext-runtime
NLS_CONFIGURE_ENABLE=	nls

VTE_DESC=	Embedded virtual terminal
VTE_CONFIGURE_ENABLE=	vte
VTE_USE=	GNOME=vte

post-patch-DOCS-off:
	@${REINPLACE_CMD} -e '/^SUBDIRS/ s|doc||' ${WRKSRC}/Makefile.in

post-patch-NLS-off:
	@${REINPLACE_CMD} -e '/^SUBDIRS/ s|po||' ${WRKSRC}/Makefile.in

.include <bsd.port.mk>
