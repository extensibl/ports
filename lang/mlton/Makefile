COMMENT =    MLton compiler
V =          20130715
DISTNAME =   mlton-${V}
REVISION =   1
CATEGORIES = lang

MAINTAINER = Alexander Abushkevich <alex@extensibl.com>
HOMEPAGE =   http://mlton.org

DISTFILES =  on-${V}-release${EXTRACT_SUFX}:0
SUPFILES =   mlton-${V}-bootstrap-OpenBSD-${OSREV}-${MACHINE_ARCH}.tar.gz:1

.if defined(SUPFILES)
DISTFILES += ${SUPFILES}
.endif

MASTER_SITES0 = https://github.com/MLton/mlton/archive/
MASTER_SITES1 = https://extensibl.com/pub/mlton/

ONLY_FOR_ARCHS = amd64

# BSD/MIT
PERMIT_PACKAGE_CDROM =  Yes
PERMIT_PACKAGE_FTP =    Yes
PERMIT_DISTFILES_FTP =  Yes

WRKDIST =       ${WRKDIR}/mlton-on-$V-release

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

# Instructions on how to generate bootstrap files:
BOOTSTRAP_DIR=  ${WRKDIR}/bootstrap-new/bootstrap
bootstrap: fake
	cd ${WRKBUILD} && ${GMAKE} # First round of compilation
	# Recompile mlton with itself, keep intermediary files for further use as bootstrap. 
	# Extra recompilation cycle makes sense when MLton versions change.
	cd ${WRKBUILD}/mlton && ${GMAKE} clean 
	cd ${WRKBUILD}/mlton && rm -f mlton-compile
	cd ${WRKBUILD} && PATH=${PATH}:${WRKBUILD}/build/bin/ COMPILE_ARGS=" -keep g " ${MAKE}	
	
	# Archive bootstrap files
	mkdir -p ${BOOTSTRAP_DIR}
	cp ${WRKBUILD}/mlton/*.c ${BOOTSTRAP_DIR}
	cp ${WRKBUILD}/mlyacc/src/yacc.grm.* ${BOOTSTRAP_DIR}
	cp ${WRKBUILD}/bootstrap/Makefile ${BOOTSTRAP_DIR}
	cp ${WRKBUILD}/bootstrap/README ${BOOTSTRAP_DIR}
	cd ${WRKDIR} && tar zcf mlton-${V}-bootstrap-OpenBSD-${OSREV}-${MACHINE_ARCH}.tar.gz ${BOOTSTRAP_DIR}
	

.include <bsd.port.mk>

