COMMENT =    MLton compiler
V =          20130715
DISTNAME =   mlton-${V}
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

WRKDIST =       ${WRKDIR}/mlton-on-$V-release

USE_GMAKE =     Yes
MODULES +=      gnu
WANTLIB +=      c m gmp
BUILD_DEPENDS = shells/bash archivers/gtar
RUN_DEPENDS   = shells/bash
LIB_DEPENDS =   devel/gmp
MAKE_ENV =      PATH=${PATH}:${WRKBUILD}/build/bin/:${WRKBUILD}/mllex/

post-extract:
	mv ${WRKDIR}/bootstrap ${WRKBUILD}/ 

do-build:
	# Prerequisites, directory layout
	cd ${WRKBUILD} && WITH_GMP=/usr/local ${GMAKE} dirs runtime
	# Compile, link MLton compiler executable from bootstrap C sources,
	# because we do not have any SML compiler available yet.
	# Also copy bootstrap files for mlyacc. 
	cd ${WRKBUILD} && ${MAKE} -C bootstrap compile_bootstrap
	cd ${WRKBUILD} && mv bootstrap/mlton-compile build/lib/
	cd ${WRKBUILD} && mv bootstrap/yacc.grm.* mlyacc/src/
	# Now build the rest with the bootstrapped MLton compiler
	cd ${WRKBUILD} && ${GMAKE} basis-no-check script mlbpathmap constants libraries
	cd ${WRKBUILD} && PATH=${PATH}:${WRKBUILD}/mllex/ ${GMAKE} tools

# bootstrap target generates MLton (and mlyacc) bootstrap files
BOOTSTRAP_DIR=  ${WRKDIR}/bootstrap-new/bootstrap
bootstrap: fake
	cd ${WRKBUILD} && ${GMAKE} # First round of compilation
	# Recompile mlton with itself, keep intermediary files for further use as bootstrap. 
	# Extra recompilation cycle makes sense when MLton versions change.
	cd ${WRKBUILD}/mlton && ${GMAKE} clean 
	cd ${WRKBUILD}/mlton && rm -f mlton-compile
	cd ${WRKBUILD} && PATH=${PATH}:${WRKBUILD}/build/bin/ COMPILE_ARGS=" -keep g " ${GMAKE}	
	
	# Archive bootstrap files
	mkdir -p ${BOOTSTRAP_DIR}
	mv ${WRKBUILD}/mlton/*.c ${BOOTSTRAP_DIR}
	mv ${WRKBUILD}/mlton/*.s ${BOOTSTRAP_DIR}
	mv ${WRKBUILD}/mlyacc/src/yacc.grm.* ${BOOTSTRAP_DIR}
	mv ${WRKBUILD}/bootstrap/Makefile ${BOOTSTRAP_DIR}
	mv ${WRKBUILD}/bootstrap/README ${BOOTSTRAP_DIR}
	cd ${WRKDIR}/bootstrap-new/ && tar zcf mlton-${V}-bootstrap-OpenBSD-${OSREV}-${MACHINE_ARCH}.tar.gz bootstrap

.include <bsd.port.mk>

