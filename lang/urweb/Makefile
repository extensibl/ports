# $OpenBSD: Makefile,v 1.7 2013/03/11 10:50:31 espie Exp $

COMMENT=	Ur/Web compiler
EXTRACT_SUFX=   .tgz
DISTNAME=	urweb-20150520
REVISION=	10
CATEGORIES=	lang

MAINTAINER=     Alexander Abushkevich <alex@abushkevi.ch>

HOMEPAGE=	http://impredicative.com/ur/
MASTER_SITES=	http://impredicative.com/ur/

#WRKDIST =	${WRKDIR}/${DISTNAME}

# BSD
PERMIT_PACKAGE_CDROM=	Yes
PERMIT_PACKAGE_FTP=     Yes
PERMIT_DISTFILES_FTP=   Yes

WANTLIB= crypto m pthread ssl

USE_GMAKE=		Yes
NO_CHECKSUM=            No

RUN_DEPENDS=		
BUILD_DEPENDS=		lang/mlton

CONFIGURE_STYLE=        simple


.include <bsd.port.mk>
