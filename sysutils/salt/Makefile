# $OpenBSD: Makefile,v 1.5 2013/12/27 10:19:30 landry Exp $

COMMENT =	remote execution and configuration management system

MODPY_EGG_VERSION =	2014.1.3
DISTNAME =	salt-${MODPY_EGG_VERSION}

CATEGORIES =	sysutils net devel

HOMEPAGE =	http://saltstack.org/

# Apache 2.0
PERMIT_PACKAGE_CDROM =	Yes

MASTER_SITES =	${MASTER_SITE_PYPI:=s/salt/}

MODULES =	lang/python
RUN_DEPENDS =	net/py-zmq \
		net/py-msgpack \
		net/py-libcloud \
		www/py-jinja2 \
		security/py-M2Crypto \
		security/py-crypto \
		textproc/py-yaml

TEST_DEPENDS =	devel/py-pip \
		sysutils/salt-testing

LOCALSTATEDIR =	${BASELOCALSTATEDIR}/salt
SYSCONFDIR =	${BASESYSCONFDIR}/salt
SUBST_VARS	+=	LOCALSTATEDIR SYSCONFDIR

# master-roots-dir is a non-functional remainder of a non-implemented function
MODPY_DISTUTILS_INSTALLARGS +=	--salt-config-dir=${SYSCONFDIR} \
								--salt-srv-root-dir=${LOCALSTATEDIR} \
								--salt-base-file-roots-dir=${LOCALSTATEDIR}/states \
								--salt-base-pillar-roots-dir=${LOCALSTATEDIR}/pillar \
								--salt-base-master-roots-dir=${LOCALSTATEDIR}/salt-master \
								--salt-pidfile-dir=${BASELOCALSTATEDIR}/run \
								--salt-sock-dir=${BASELOCALSTATEDIR}/run/salt \
								--salt-cache-dir=${BASELOCALSTATEDIR}/cache/salt \
								--salt-logs-dir=${BASELOCALSTATEDIR}/log/salt

#FAILED (total=569, skipped=33, passed=511, failures=16, errors=9) 
do-test:
	ln -sf ${LOCALBASE}/bin/pip-${MODPY_VERSION} ${WRKDIR}/bin/pip
	@${MODPY_TEST_TARGET}

# Need to skip the build step so _syspaths.py gets generated
do-install:
	${MODPY_CMD} ${MODPY_DISTUTILS_INSTALL} ${MODPY_DISTUTILS_INSTALLARGS}

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/salt/
	${INSTALL_DATA} ${WRKSRC}/conf/master \
		${PREFIX}/share/examples/salt/master.sample
	${INSTALL_DATA} ${WRKSRC}/conf/minion \
		${PREFIX}/share/examples/salt/minion.sample

# devel/py-gitpython for fileserver backend ?

.include <bsd.port.mk>
