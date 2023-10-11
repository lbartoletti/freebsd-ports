PORTNAME=	cgal
PORTVERSION=	5.6
CATEGORIES=	math
MASTER_SITES=	https://github.com/${PORTNAME:tu}/${PORTNAME}/releases/download/v${PORTVERSION}/
DISTNAME=	${PORTNAME:tu}-${PORTVERSION}

MAINTAINER=	wen@FreeBSD.org
COMMENT=	Computational geometry library
WWW=		https://www.cgal.org/

LICENSE=	GPLv3 LGPL3
LICENSE_COMB=	multi

BROKEN_sparc64=	does not build: fails to compile all_files.cpp

BUILD_DEPENDS=	${LOCALBASE}/lib/libntl.a:math/ntl
LIB_DEPENDS=	libboost_system.so:devel/boost-libs \
		libmpfr.so:math/mpfr \
		libgmp.so:math/gmp

#TODO math/mpfi, math/rs, graphics/qglviewer
#Not yet in ports
USES=		cmake eigen:3 shebangfix tar:xz

NO_ARCH=	yes

SHEBANG_FILES=	scripts/cgal_create_CMakeLists \
		scripts/cgal_create_cmake_script

.include <bsd.port.mk>
