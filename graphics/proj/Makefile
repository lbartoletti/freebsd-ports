PORTNAME=	proj
PORTVERSION=	9.1.1
PORTEPOCH=	1
CATEGORIES=	graphics geography
#MASTER_SITES=	https://download.osgeo.org/proj/

MAINTAINER=	lbartoletti@FreeBSD.org
COMMENT=	Cartographic Projections library
WWW=		https://github.com/OSGeo/PROJ

LICENSE=	MIT
#LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libcurl.so:ftp/curl \
		libtiff.so:graphics/tiff
#RUN_DEPENDS=	proj-data>=0:graphics/proj-data

USES=		compiler:c++11-lang cmake cpe libtool pathfix pkgconfig sqlite
USE_LDCONFIG=	yes
USE_GITHUB=	yes
GH_ACCOUNT=	osgeo
GH_TAGNAME=	aa18b0b

CMAKE_OFF=	BUILD_TESTING

CPE_VENDOR=	proj_project

WRKSRC=		${WRKDIR}/PROJ-${GH_TAGNAME}

.include <bsd.port.mk>
