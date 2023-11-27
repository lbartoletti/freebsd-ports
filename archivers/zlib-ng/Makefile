PORTNAME=	zlib-ng
DISTVERSION=	2.1.4
CATEGORIES=	archivers

MAINTAINER=	lbartoletti@FreeBSD.org
COMMENT=	Fork of the zlib data compression library
WWW=		https://github.com/zlib-ng/zlib-ng

LICENSE=	ZLIB

USES=		cmake:testing
USE_LDCONFIG=	yes
USE_GITHUB=	yes

TEST_DEPENDS=	googletest>0:devel/googletest

CMAKE_OFF=		WITH_GTEST
CMAKE_TESTING_ON=	ZLIB_ENABLE_TESTS \
			WITH_GTEST

.include <bsd.port.mk>
