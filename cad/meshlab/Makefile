PORTNAME=	meshlab
DISTVERSIONPREFIX=	MeshLab-
DISTVERSION=	2025.07
CATEGORIES=	cad

MAINTAINER=	lbartoletti@FreeBSD.org
COMMENT=	3D triangular meshes processing and editing tool
WWW=		https://www.meshlab.net/

LICENSE=	GPLv2

BUILD_DEPENDS=	${LOCALBASE}/include/CGAL/Cartesian.h:math/cgal \
		${LOCALBASE}/include/eigen3/Eigen/Core:math/eigen3
LIB_DEPENDS=	libopenctm.so:cad/openctm \
		libxerces-c.so:textproc/xerces-c3 \
		libqhull_r.so:math/qhull \
		libmuparser.so:math/muparser \
		lib3ds.so:graphics/lib3ds \
		libembree4.so:graphics/embree \
		libtbb.so:devel/onetbb

MASTER_SITES=	https://github.com/ispc/ispc/releases/download/v1.18.1/:ispc
DISTFILES=	ispc-v1.18.1-linux.tar.gz:ispc

USES=		cmake dos2unix gl  qmake:no_configure qt:5
DOS2UNIX_GLOB=	*.c *.cpp *.h
USE_CXXSTD=	c++14
USE_GITHUB=	yes
GH_ACCOUNT=	cnr-isti-vclab
GH_TUPLE=	cnr-isti-vclab:vcglib:4d010e8:vcglib/src/vcglib \
		alemuntoni:levmar:2.6.1:levmar/src/external/downloads/levmar-2.6.1 \
		libigl:libigl:v2.4.0:libigl/src/external/downloads/libigl-2.4.0 \
		cnr-isti-vclab:nexus:v2025.05:nexus/src/external/downloads/nexus-2025.05 \
		cnr-isti-vclab:corto:v2025.07:corto/src/external/downloads/corto-2025.07 \
		alemuntoni:StructureSynth:1.5.1:structsynth/src/external/downloads/StructureSynth-1.5.1 \
		syoyo:tinygltf:v2.6.3:tinygltf/src/external/downloads/tinygltf-2.6.3 \
		alemuntoni:u3d:1.5.1:u3d/src/external/downloads/u3d-1.5.1 \
		asmaloney:libE57Format:v3.1.1:libe57/src/external/downloads/libE57Format-3.1.1 \
		3MFConsortium:lib3mf:v2.4.1:lib3mf/src/external/downloads/lib3mf-2.4.1

PATCH_SITES=	https://github.com/cnr-isti-vclab/meshlab/commit/ \
		https://github.com/cnr-isti-vclab/vcglib/commit/
PATCHFILES+=	5be8ff76533b1335acc6295152f9ef947459f565.patch:-p1

USE_GL=		gl glu glew
USE_LDCONFIG=	yes
USE_QT=		buildtools:build core gui network \
		opengl xml widgets

CMAKE_ARGS=	-DMESHLAB_USE_DEFAULT_BUILD_AND_INSTALL_DIRS:BOOL=ON \
		-DMESHLAB_ALLOW_DOWNLOAD_SOURCE_LIB3MF:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_EIGEN:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_OPENCTM:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_GLEW:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_MUPARSER:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_NEWUOA:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_LIB3DS:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_QHULL:BOOL=OFF \
		-DMESHLAB_ALLOW_BUNDLED_XERCES:BOOL=OFF \
		-DCMAKE_INSTALL_PREFIX=${PREFIX} \
		-DMESHLAB_LIB_INSTALL_DIR=${PREFIX}/lib \
		-DMESHLAB_PLUGIN_INSTALL_DIR=${PREFIX}/lib/meshlab/plugins \
		-DMESHLAB_BIN_INSTALL_DIR=${PREFIX}/bin \
		-DMESHLAB_SHADER_INSTALL_DIR=${PREFIX}/share/meshlab/shaders

CMAKE_INSTALL_PREFIX=	${PREFIX}

MAKE_ENV=		DESTDIR=${STAGEDIR}

post-extract:
	@${MKDIR} ${WRKSRC}/src/external/downloads
	${EXTRACT_CMD} ${EXTRACT_BEFORE_ARGS} ${DISTDIR}/ispc-v1.18.1-linux.tar.gz \
		${EXTRACT_AFTER_ARGS} -C ${WRKSRC}/src/external/downloads
	# Set up corto inside nexus
	@${RM} -rf ${WRKSRC}/src/external/downloads/nexus-2025.05/src/corto
	@${MV} ${WRKSRC}/src/external/downloads/corto-2025.07 ${WRKSRC}/src/external/downloads/nexus-2025.05/src/corto

.include <bsd.port.mk>
