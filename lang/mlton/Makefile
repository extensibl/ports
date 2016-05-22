COMMENT=    MLton compiler
DISTNAME=   mlton-snapshot
REVISION=   9
CATEGORIES= lang

MAINTAINER=     Alexander Abushkevich <alex@extensibl.com>

HOMEPAGE=       http://mlton.org

GH_ACCOUNT=     extensibl
GH_PROJECT=     mlton
GH_COMMIT=      a3c9b441f693124016114fff59341db2a710eb4a
COMMIT=      a3c9b441f693124016114fff59341db2a710eb4a


DISTFILES =   ${COMMIT}.tar.gz:0
SUPFILES =    mlton-bootstrap-OpenBSD-5.9-amd64.tar.gz:1
.if defined(SUPFILES)
DISTFILES   += ${SUPFILES}
.endif
MASTER_SITES0 = https://github.com/extensibl/mlton/archive/
MASTER_SITES1 = https://extensibl.com/pub/mlton/

ONLY_FOR_ARCHS = amd64

# BSD
PERMIT_PACKAGE_CDROM=   Yes
PERMIT_PACKAGE_FTP=     Yes
PERMIT_DISTFILES_FTP=   Yes

USE_GMAKE=              Yes
WANTLIB +=              c m gmp
BUILD_DEPENDS =         shells/bash archivers/gtar devel/gmp
MAKE_ENV =  PATH=${PATH}:${WRKBUILD}/build/bin/:${WRKBUILD}/mllex/


pre-build:
        echo ${WRKSRC}
        echo ${WRKDIR}
        cd ${WRKBUILD} && ${GMAKE} dirs runtime
        @if [ ! -d ${WRKBUILD}/bootstrap ]; then \
                cd ${WRKBUILD} && cp -r ../bootstrap . \
        fi
        cd ${WRKBUILD} && ${MAKE} -C bootstrap
        cd ${WRKBUILD} && cp bootstrap/mlton-compile build/lib/
        cd ${WRKBUILD} && cp bootstrap/yacc.grm.* mlyacc/src/

do-build:
        cd ${WRKBUILD} && ${GMAKE} basis-no-check script mlbpathmap constants libraries
        cd ${WRKBUILD} && PATH=${PATH}:${WRKBUILD}/mllex/ ${GMAKE} tools
        cd ${WRKBUILD} && ${GMAKE} install

.include <bsd.port.mk>
