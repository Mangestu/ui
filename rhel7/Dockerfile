FROM rhel7

COPY yum.conf /etc/yum.conf
COPY rpm-orion.repo /etc/yum.repos.d/
 
RUN rm -f /etc/yum.repos.d/redhat.repo
RUN yum -y install httpd
RUN yum -y clean all

#RUN localedef -v -c -i fr_FR -f UTF-8 fr_FR.UTF-8

RUN sed -ri ' s!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g; s!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g;' /etc/httpd/conf/httpd.conf

COPY run-apache.sh /run-apache.sh
RUN chmod a+x /run-apache.sh

RUN echo 'export TERM=xterm' >> /root/.bashrc

#RUN chkconfig httpd on

EXPOSE 80

#CMD ["/bin/bash"]
#CMD ["/usr/sbin/httpd -DFOREGROUND"]
#CMD ["/usr/sbin/apachectl","-DFOREGROUND"]
#CMD ["/usr/sbin/httpd","-DFOREGROUND"]
CMD ["/run-apache.sh"]
