COMMENT =    Ur/Web compiler and library
V =          20160515
DISTNAME =   urweb-${V}
CATEGORIES = lang

MAINTAINER = Alexander Abushkevich <alex@extensibl.com>
HOMEPAGE =   http://www.impredicative.com/ur/

EXTRACT_SUFX = .tgz
DISTFILES =    urweb-${V}${EXTRACT_SUFX}

MASTER_SITES = http://www.impredicative.com/ur/

# BSD/MIT
PERMIT_PACKAGE_CDROM =  Yes

CONFIGURE_STYLE= gnu
USE_GMAKE =      Yes
WANTLIB +=       c m 
BUILD_DEPENDS =  lang/mlton
LIB_DEPENDS =    devel/gmp

SO_VERSION =    0.0
SHARED_LIBS +=  urweb                    ${SO_VERSION}
SHARED_LIBS +=  urweb_cgi                ${SO_VERSION}
SHARED_LIBS +=  urweb_fastcgi            ${SO_VERSION}
SHARED_LIBS +=  urweb_http               ${SO_VERSION}
SHARED_LIBS +=  urweb_static             ${SO_VERSION}


.include <bsd.port.mk>

