# Created by: Wen Heping <wenheping@gmail.com>
# $FreeBSD$

PORTNAME=	SOAP-WSDL
PORTVERSION=	3.003
CATEGORIES=	devel perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Perl module for SOAP with WSDL support

LICENSE=	ART10 GPLv1+
LICENSE_COMB=	dual

BUILD_DEPENDS=	${RUN_DEPENDS}
RUN_DEPENDS=	p5-Class-Load>=0.20:devel/p5-Class-Load \
		p5-Class-Std-Fast>=0.0.5:devel/p5-Class-Std-Fast \
		p5-Template-Toolkit>=2.18:www/p5-Template-Toolkit \
		p5-Term-ReadKey>=0:devel/p5-Term-ReadKey \
		p5-TimeDate>=0:devel/p5-TimeDate \
		p5-URI>=0:net/p5-URI \
		p5-XML-Parser>=0:textproc/p5-XML-Parser \
		p5-libwww>=0:www/p5-libwww

USES=		perl5
USE_PERL5=	configure

.include <bsd.port.mk>
