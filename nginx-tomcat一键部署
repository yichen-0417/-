# -记住jdk包自己拉，自己改对应的配置环境
vim aa.sh
#!/bin/bash
wget http://nginx.org/download/nginx-1.16.1.tar.gz
yum -y install gcc gcc-c++ zlib-devel pcre-devel
tar zxf nginx-1.16.1.tar.gz
cd nginx-1.16.1 && ./configure && make && make install
shulian=`cat /usr/local/nginx/conf/nginx.conf|grep 'proxy_pass   http://192.168.11.128:8080;'|wc -l`
if [ $shulian -ne 1 ];then
sed -i  's/index.htm;$/index.jsp;/' /usr/local/nginx/conf/nginx.conf
sed -i  '/404.html;/alocation ~ \\.jsp$ {' /usr/local/nginx/conf/nginx.conf
sed -i  '/location ~ \\.jsp$ {/aproxy_pass   http://192.168.11.128:8080;' /usr/local/nginx/conf/nginx.conf
sed -i  '/proxy_pass   http:\/\/192.168.11.128:8080;/a\}' /usr/local/nginx/conf/nginx.conf
fi
cd /root && rpm -ivh jdk-8u20-linux-x64.rpm
cishu=`cat /etc/profile|grep 'JAVA_HOME'|wc -l`
if [ $cishu -ne 4 ];then
echo -e 'export JAVA_HOME=/usr/java/jdk1.8.0_20
export JAVA_BIN=/usr/java/jdk1.8.0_20/bin
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH' >>/etc/profile
fi
source /etc/profile
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-7/v7.0.96/bin/apache-tomcat-7.0.96.tar.gz
tar zxf apache-tomcat-7.0.96.tar.gz
cp -r apache-tomcat-7.0.96 /opt/tomcat
/usr/local/nginx/sbin/nginx
/opt/tomcat/bin/startup.sh

访问结果，后面跟着index.jsp
