COMMENT =    MLton compiler
V =          44d05975f6d1f933ad9bffb3f0b1c06ca97eddbe
DISTNAME =   mlton-${V}
REVISION =   13
CATEGORIES = lang

MAINTAINER = Alexander Abushkevich <alex@extensibl.com>
HOMEPAGE =   http://mlton.org

DISTFILES =  ${V}${EXTRACT_SUFX}:0
SUPFILES =   mlton-bootstrap-OpenBSD-5.9-amd64.tar.gz:1

.if defined(SUPFILES)
DISTFILES += ${SUPFILES}
.endif

MASTER_SITES0 = https://github.com/extensibl/mlton/archive/
MASTER_SITES1 = https://extensibl.com/pub/mlton/

ONLY_FOR_ARCHS = amd64

# BSD/MIT
PERMIT_PACKAGE_CDROM =  Yes
PERMIT_PACKAGE_FTP =    Yes
PERMIT_DISTFILES_FTP =  Yes

USE_GMAKE =     Yes
MODULES +=      gnu
WANTLIB +=      c m gmp
BUILD_DEPENDS = shells/bash archivers/gtar
LIB_DEPENDS =   devel/gmp
MAKE_ENV =      PATH=${PATH}:${WRKBUILD}/build/bin/:${WRKBUILD}/mllex/

do-build:
	cd ${WRKBUILD} && WITH_GMP=/usr/local ${GMAKE} dirs runtime

.if ! exists( ${WRKBUILD}/bootstrap )
	cd ${WRKBUILD} && cp -r ../bootstrap .
.endif

	cd ${WRKBUILD} && ${MAKE} -C bootstrap compile_bootstrap
	cd ${WRKBUILD} && cp bootstrap/mlton-compile build/lib/
	cd ${WRKBUILD} && cp bootstrap/yacc.grm.* mlyacc/src/

	cd ${WRKBUILD} && ${GMAKE} basis-no-check script mlbpathmap constants libraries
	cd ${WRKBUILD} && PATH=${PATH}:${WRKBUILD}/mllex/ ${GMAKE} tools
	cd ${WRKBUILD} && ${GMAKE} install

.include <bsd.port.mk>

