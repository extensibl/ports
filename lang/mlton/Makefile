# $OpenBSD: Makefile,v 1.7 2013/03/11 10:50:31 espie Exp $

COMMENT=	MLton compiler
DISTNAME=	mlton-20130715
REVISION=       5
CATEGORIES=	lang

MAINTAINER=     Alexander Abushkevich <alex@abushkevi.ch>

HOMEPAGE=	http://mlton.org

GH_ACCOUNT=     AlexanderAA
GH_PROJECT=     mlton
#GH_COMMIT=      3bca4208edb4070ba46b5727a2b14ad753a99773
GH_COMMIT=      92fba119d48d62b115ac0d441dcbe84285a6a061

WRKDIST =	${WRKDIR}/mlton-${GH_COMMIT}

# BSD
PERMIT_PACKAGE_CDROM=	Yes
PERMIT_PACKAGE_FTP=     Yes
PERMIT_DISTFILES_FTP=   Yes

USE_GMAKE=		Yes
NO_CHECKSUM=            No


post-extract:
	tar xzf /home/a/Projects/mlton-s/mlton.cs.amd64.tar.gz
	gcc -fPIC -static -c -Ibuild/lib/include -Ibuild/lib/targets/unknown/include -I/usr/local/include -O1 -w mlton/mlton.*.[cs]
	gcc -s -Xlinker -zmuldefs -static -o build/lib/mlton-compile -Lbuild/lib/targets/unknown -L/usr/local/lib mlton.*.o -lmlton -lgmp -lgdtoa -lm

.include <bsd.port.mk>
