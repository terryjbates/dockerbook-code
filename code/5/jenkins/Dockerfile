FROM ubuntu:14.04
MAINTAINER Terry Bates terry@example.com
ENV REFRESHED_AT 2015-09-24

RUN apt-get update -qq && apt-get install -qqy curl
RUN apt-get -y install docker.io
RUN ln -sf /usr/bin/docker.io /usr/local/bin/docker
RUN sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io
ENV JENKINS_HOME /opt/jenkins/data
ENV JENKINS_MIRROR http://mirrors.jenkins-ci.org

RUN mkdir -p $JENKINS_HOME/plugins
RUN curl -sf -o /opt/jenkins/jenkins.war -L $JENKINS_MIRROR/war/latest/jenkins.war
RUN for plugin in chucknorris greenballs scm-api git-client git ws-cleanup;\
    do curl -sf -o $JENKINS_HOME/plugins/${plugin}.hpi \
    -L $JENKINS_MIRROR/plugins/${plugin}/latest/${plugin}.hpi ; done
ADD ./dockerjenkins.sh /usr/local/bin/dockerjenkins.sh
RUN chmod +x /usr/local/bin/dockerjenkins.sh
RUN apt-get -y  install openjdk-7-jre
VOLUME /var/lib/docker
EXPOSE 8080
ENTRYPOINT [ "/usr/local/bin/dockerjenkins.sh"]

