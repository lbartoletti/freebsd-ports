PORTNAME=	psql
DISTVERSION=	${QT6_VERSION}
CATEGORIES=	databases
PKGNAMEPREFIX=	qt6-

PATCH_SITES=	https://github.com/qt/qtbase/commit/
PATCHFILES=	3f45905953d57e0174059d7d9d6bc75c3c1c406c.patch:-p1

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Qt base (core, gui, widgets, network,...)
WWW=		https://www.qt.io/

BUILD_DEPENDS=	xml:textproc/xmlstarlet \
		${LOCALBASE}/include/vulkan/vulkan.h:graphics/vulkan-headers \
		${LOCALBASE}/include/linux/input.h:devel/evdev-proto
LIB_DEPENDS=	\
		libicui18n.so:devel/icu \
		libdouble-conversion.so:devel/double-conversion \
		libpcre2-16.so:devel/pcre2 \
		libzstd.so:archivers/zstd \
		libpng16.so:graphics/png \
		libfreetype.so:print/freetype2 \
		libbrotlidec.so:archivers/brotli \
		libxcb-icccm.so:x11/xcb-util-wm\
		libxcb-image.so:x11/xcb-util-image \
		libxcb-keysyms.so:x11/xcb-util-keysyms \
		libxkbcommon-x11.so:x11/libxkbcommon \
		libudev.so:devel/libudev-devd \
		libmtdev.so:devel/libmtdev \
		libinput.so:x11/libinput \
		libcups.so:print/cups

USES=		cmake compiler:c++17-lang gettext-runtime gl gnome jpeg perl5 pgsql pkgconfig python \
		qt-dist:6,base shebangfix xorg
USE_QT=		base
USE_GNOME=	glib20 gtk30 pango cairo gdkpixbuf2
USE_GL=		egl gl opengl
USE_XORG=	xcb x11 sm ice
CMAKE_ON=	QT_AVOID_CMAKE_ARCHIVING_API \
		QT_FIND_ALL_PACKAGES_ALWAYS \
		FEATURE_sql_psql
CMAKE_OFF=	QT_FEATURE_eglfs \
		QT_FEATURE_gssapi
SHEBANG_FILES=	${WRKSRC}/mkspecs/features/uikit/device_destinations.sh \
		${WRKSRC}/mkspecs/features/uikit/devices.py \
		${WRKSRC}/mkspecs/features/data/mac/objc_namespace.sh \
		${WRKSRC}/util/android/android_emulator_launcher.sh \
		${WRKSRC}/util/testrunner/qt-testrunner.py
USE_LDCONFIG=	${PREFIX}/${QT_LIBDIR_REL}

# zstd from base fails to compress files during the build (error 11: unsupported argument)
BINARY_ALIAS=	zstd=${LOCALBASE}/bin/zstd

.include <bsd.port.pre.mk>

.if ${ARCH} == "armv6" || ${ARCH} == "armv7"
BUILD_DEPENDS+=	as:devel/binutils
CMAKE_ARGS+=	-DCMAKE_ASM_FLAGS=-no-integrated-as
.endif

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/lib/cmake/Qt6
	${MKDIR} ${STAGEDIR}${PREFIX}/lib/cmake/Qt6Sql
	${MKDIR} ${STAGEDIR}/${QT_PLUGINDIR}/sqldrivers
	${INSTALL_DATA} ${WRKDIR}/.build/lib/qt6/cmake/Qt6/FindPostgreSQL.cmake ${STAGEDIR}${PREFIX}/lib/cmake/Qt6/FindPostgreSQL.cmake
	${INSTALL_DATA} ${WRKDIR}/.build/lib/qt6/cmake/Qt6Sql/Qt6QPSQLDriverPluginConfig.cmake ${STAGEDIR}${PREFIX}/lib/cmake/Qt6Sql/Qt6QPSQLDriverPluginConfig.cmake
	${INSTALL_DATA} ${WRKDIR}/.build/lib/qt6/cmake/Qt6Sql/Qt6QPSQLDriverPluginConfigVersion.cmake ${STAGEDIR}${PREFIX}/lib/cmake/Qt6Sql/Qt6QPSQLDriverPluginConfigVersion.cmake
	${INSTALL_DATA} ${WRKDIR}/.build/lib/qt6/cmake/Qt6Sql/Qt6QPSQLDriverPluginConfigVersionImpl.cmake ${STAGEDIR}${PREFIX}/lib/cmake/Qt6Sql/Qt6QPSQLDriverPluginConfigVersionImpl.cmake
	${INSTALL_DATA} ${WRKDIR}/.build/lib/cmake/Qt6Sql/Qt6QPSQLDriverPluginAdditionalTargetInfo.cmake ${STAGEDIR}${PREFIX}/lib/cmake/Qt6Sql/Qt6QPSQLDriverPluginAdditionalTargetInfo.cmake
	${INSTALL_DATA} ${WRKDIR}/.build/lib/cmake/Qt6Sql/Qt6QPSQLDriverPluginTargets.cmake ${STAGEDIR}${PREFIX}/lib/cmake/Qt6Sql/Qt6QPSQLDriverPluginTargets.cmake
	${INSTALL_DATA} ${WRKDIR}/.build/lib/qt6/plugins/sqldrivers/libqsqlpsql.so ${STAGEDIR}/${QT_PLUGINDIR}/sqldrivers/libqsqlpsql.so

.include <bsd.port.post.mk>
