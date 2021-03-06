# Created by: Nicola Vitale <nivit@FreeBSD.org>
# $FreeBSD$

PORTNAME=	Jinja2
PORTVERSION=	2.9.5
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
PKGNAMESUFFIX?=

MAINTAINER=	nivit@FreeBSD.org
COMMENT?=	Fast and easy to use stand-alone template engine

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}MarkupSafe>=0.23:textproc/py-MarkupSafe
TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}MarkupSafe>=0.23:textproc/py-MarkupSafe

NO_ARCH=	yes
USES?=		python
.if empty(PKGNAMESUFFIX)
USE_PYTHON=	autoplist distutils
.endif

EXAMPLESDIR=	${PREFIX}/share/examples/${PKGNAMEPREFIX}${PORTNAME}

OPTIONS_DEFINE?=	BABEL EXAMPLES
OPTIONS_DEFAULT?=	BABEL
BABEL_DESC=		Enable Babel extension

BABEL_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}Babel>=1.3:devel/py-babel

.include <bsd.port.pre.mk>

.if ${PKGNAMESUFFIX} == "-doc"
BUILD_DEPENDS+=	${PKGNAMEPREFIX}sphinx>=1.1.3:textproc/py-sphinx
DOCSDIR=	${PREFIX}/share/doc/${PKGNAMEPREFIX}${PORTNAME}
PORTDOCS=	*
PORT_OPTIONS:=	${PORT_OPTIONS:NEXAMPLES}

do-build:
	(cd ${WRKSRC}/docs && ${MAKE} html)

do-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC}/docs/_build/html && ${COPYTREE_SHARE} . ${STAGEDIR}${DOCSDIR} \
		"! -name .buildinfo")
.endif

.if ${PORT_OPTIONS:MEXAMPLES}
PORTEXAMPLES=	*
post-build:
	${PYTHON_CMD} -m compileall ${WRKSRC}/examples ; \
	${PYTHON_CMD} -O -m compileall ${WRKSRC}/examples

post-install:
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	(cd ${WRKSRC}/examples && ${COPYTREE_SHARE} . ${STAGEDIR}${EXAMPLESDIR})
.endif

check regression-test test: build
.if empty(PKGNAMESUFFIX)
	@cd ${WRKSRC} && ${PYTHON_CMD} ${PYSETUP} test
.else
	@${DO_NADA}
.endif

.include <bsd.port.post.mk>
