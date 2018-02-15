# Copyright (c) 2017, Oracle and/or its affiliates. All rights reserved.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; version 2 of the License.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301 USA

FROM oraclelinux:7-slim

RUN yum install -y wget
RUN wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN rpm -ivh epel-release-latest-7.noarch.rpm
RUN yum repolist
RUN yum install -y perl-Class-MethodMaker

RUN wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-common-7.6.4-1.el7.x86_64.rpm \
  && wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-client-7.6.4-1.el7.x86_64.rpm \
  && wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-server-7.6.4-1.el7.x86_64.rpm \
  && wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-libs-7.6.4-1.el7.x86_64.rpm \
  && wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-libs-compat-7.6.4-1.el7.x86_64.rpm \
  && wget https://dev.mysql.com/get/Downloads/MySQL-Shell/mysql-shell-1.0.11-1.el7.x86_64.rpm 

RUN yum install -y mysql-cluster-community-common-7.6.4-1.el7.x86_64.rpm \
  && yum install -y mysql-cluster-community-libs-7.6.4-1.el7.x86_64.rpm \
  && yum install -y mysql-cluster-community-libs-compat-7.6.4-1.el7.x86_64.rpm \
  && yum install -y mysql-cluster-community-client-7.6.4-1.el7.x86_64.rpm \
  && yum install -y mysql-cluster-community-server-7.6.4-1.el7.x86_64.rpm \
  && yum install -y mysql-shell-1.0.11-1.el7.x86_64.rpm

RUN rpmkeys --import https://repo.mysql.com/RPM-GPG-KEY-mysql \
  && yum install -y libpwquality \
  && yum clean all \
  && mkdir /docker-entrypoint-initdb.d


RUN wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-management-server-7.6.4-1.el7.x86_64.rpm \
  && wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-data-node-7.6.4-1.el7.x86_64.rpm \
  && wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-test-7.6.4-1.el7.x86_64.rpm

RUN yum install -y mysql-cluster-community-management-server-7.6.4-1.el7.x86_64.rpm \
  && yum install -y mysql-cluster-community-data-node-7.6.4-1.el7.x86_64.rpm \
  && yum install -y mysql-cluster-community-test-7.6.4-1.el7.x86_64.rpm

VOLUME /var/lib/mysql

COPY docker-entrypoint.sh /entrypoint.sh
COPY healthcheck.sh /healthcheck.sh
COPY cnf/my.cnf /etc/
COPY cnf/mysql-cluster.cnf /etc/

ENTRYPOINT ["/entrypoint.sh"]
EXPOSE 3306 33060 2202 1186
CMD ["mysqld"]
