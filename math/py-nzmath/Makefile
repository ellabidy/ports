# Created by: Wen Heping <wenheping@gmail.com>
# $FreeBSD$

PORTNAME=	nzmath
PORTVERSION=	1.2.0
CATEGORIES=	math python
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/NZMATH-${PORTVERSION}
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	NZMATH-${PORTVERSION}

MAINTAINER=	wen@FreeBSD.org
COMMENT=	Number theory oriented calculation system

USES=		python
USE_PYTHON=	distutils
PYDISTUTILS_PKGNAME=	NZMATH

OPTIONS_DEFINE=	DOCS

post-install:
	@${MKDIR} ${STAGEDIR}${DATADIR}
	${INSTALL_DATA} ${WRKSRC}/data/discriminant.csv ${STAGEDIR}${DATADIR}
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/manual/*.pdf ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
