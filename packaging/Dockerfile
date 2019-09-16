ARG BASE=ubuntu:bionic
FROM $BASE
ADD packaging/sources.list /etc/apt/sources.list
ENV __mirror__=http://ubuntu.mirrors.ovh.net/ubuntu/
RUN  id=$(cat /etc/lsb-release |grep CODE|awk -F= '{print $2}') &&\
    sed -ire "s|__mirror__|$__mirror__|g" /etc/apt/sources.list &&\
    sed -i -re "s/xenial/$id/g" /etc/apt/sources.list &&\
    apt update && apt install -y lsb-release && \
    apt-get update -qq && apt-get install -y --force-yes \
    devscripts equivs autogen build-essential \
    dbconfig-common python-twisted-web daemon
ADD debian/control        /src/debian/control
RUN cd /src && \
    mk-build-deps -t "apt-get --no-install-recommends -y --force-yes" -ir debian/control
ADD debian                                  /src/debian/
ADD gui                                     /src/gui/
ADD man                                     /src/man/
ADD pam                                     /src/pam/
ADD m4                                      /src/m4/
ADD src                                     /src/src/
ADD AUTHORS                                 /src/
ADD autogen.sh                              /src/
ADD ChangeLog                               /src/
ADD configure.ac                            /src/
ADD COPYING                                 /src/
ADD FAQ                                     /src/
ADD HISTORY                                 /src/
ADD Makefile.am                             /src/
ADD Makefile.gui                            /src/
ADD NEWS                                    /src/
ADD puredb                                  /src/puredb/
ADD pure-ftpd.conf.in                       /src/
ADD pureftpd-ldap.conf                      /src/
ADD pureftpd-mysql.conf                     /src/
ADD pureftpd-pgsql.conf                     /src/
ADD pure-ftpd.png                           /src/
ADD pureftpd.schema                         /src/
ADD README.Authentication-Modules           /src/
ADD README.Configuration-File               /src/
ADD README.Donations                        /src/
ADD README.LDAP                             /src/
ADD README.MacOS-X                          /src/
ADD README.MySQL                            /src/
ADD README.PGSQL                            /src/
ADD README                                  /src/
ADD README.TLS                              /src/
ADD README.Virtual-Users                    /src/
ADD README.Windows                          /src/
ADD README.Windows                          /src/
ADD THANKS                                  /src/
WORKDIR /src
RUN REV=2;export MAKEOPTS="-j4" && \
    if debuild -i -us -uc -b;then echo SUCCESS; else echo FAIL; exit 1;fi
