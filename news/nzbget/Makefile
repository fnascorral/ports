# Created by: Lewis Thompson <purple@lewiz.net>
# $FreeBSD$

PORTNAME=	nzbget
PORTVERSION=	17.1
DISTVERSIONPREFIX=	v
PORTREVISION=	2
CATEGORIES=	news

MAINTAINER=	toxic@doobie.com
COMMENT=	Binary newsreader supporting NZB files

LICENSE=	GPLv2

LIB_DEPENDS=	libxml2.so:textproc/libxml2

USES=		ncurses pkgconfig shebangfix compiler:c++14-lang
USE_RC_SUBR=	nzbget
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-libcurses-includes=${NCURSESINC} \
		--with-libcurses-libraries=${NCURSESLIB}
CONFIGURE_ENV=	LOCALBASE="${LOCALBASE}"
MAKE_JOBS_UNSAFE=	yes
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-lpthread
BINMODE=	0755

SHEBANG_FILES=	scripts/*.py
SUB_FILES=	pkg-message

USE_GITHUB=	yes

OPTIONS_DEFINE=	7Z PYTHON RAR DOCS
OPTIONS_SINGLE=	TLSLIB
OPTIONS_SINGLE_TLSLIB=	GNUTLS OPENSSL
OPTIONS_DEFAULT=	OPENSSL PAR PYTHON RAR 7Z
7Z_DESC=	Support extraction of 7z archives
PYTHON_DESC=	Support for python post-processing scripts
RAR_DESC=	Support extraction of rar archives

7Z_RUN_DEPENDS=		7z:archivers/p7zip

PYTHON_USES=		python:run

RAR_RUN_DEPENDS=	unrar:archivers/unrar

OPENSSL_CONFIGURE_ON=	--with-tlslib=OpenSSL \
			--with-openssl-includes=${OPENSSLINC} \
			--with-openssl-libraries=${OPENSSLLIB}
OPENSSL_USE=		OPENSSL=yes

GNUTLS_CONFIGURE_ON=	--with-tlslib=GnuTLS
GNUTLS_LIB_DEPENDS=	libgnutls.so:security/gnutls \
			libgcrypt.so:security/libgcrypt

.include <bsd.port.options.mk>

.if (${ARCH} == "i386")
CONFIGURE_ARGS+=	--disable-sigchld-handler
.endif

.if ${OSVERSION} < 1000500
USE_GCC=		yes
CONFIGURE_ENV+=		zlib_LIBS='-lz ' \
			zlib_CFLAGS=' '
.endif

post-install:
	${INSTALL_DATA} ${WRKSRC}/nzbget.conf \
		${STAGEDIR}${PREFIX}/etc/nzbget.conf.sample

.include <bsd.port.mk>
