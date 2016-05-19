# $OpenBSD: Makefile,v 1.7 2013/03/11 10:50:31 espie Exp $

COMMENT=	MLton compiler
V=              20130715
DISTNAME=	mlton-${V}
REVISION=       5
CATEGORIES=	lang

MAINTAINER=     Alexander Abushkevich <alex@abushkevi.ch>

HOMEPAGE=	http://mlton.org

GH_ACCOUNT=     AlexanderAA
GH_PROJECT=     mlton
GH_COMMIT=      24baaa47d8889e12d28bb08d366d048121d216a9

WRKDIST =	${WRKDIR}/mlton-${GH_COMMIT}

# BSD
PERMIT_PACKAGE_CDROM=	Yes
PERMIT_PACKAGE_FTP=     Yes
PERMIT_DISTFILES_FTP=   Yes

USE_GMAKE=		Yes
NO_CHECKSUM=            No

BUILD_DEPENDS=	lang/mlton/bootstrap>=${V}


.include <bsd.port.mk>
