#Image base
FROM jboss/base-jdk:7

MAINTAINER Maikon Canuto <maikoncanuto@gmail.com>

# Variavies para download do server
ENV JBOSS_EAP_VERSION 6.4
ENV JBOSS_EAP_PATCH_VERSION 0
ENV JBOSS_EAP_SHA1 9ac2979fe92040a039a3a3db8b4ce8d166e2c872
ENV JBOSS_HOME /opt/jboss/jboss-eap

#Configuração e download do container
USER root

RUN cd $HOME \
&& curl -L -o jboss-eap-$JBOSS_EAP_VERSION.$JBOSS_EAP_PATCH_VERSION.zip https://www.dropbox.com/s/ac3sie1ho2s8avn/jboss-eap-$JBOSS_EAP_VERSION.$JBOSS_EAP_PATCH_VERSION.zip?dl=1 \
&& sha1sum jboss-eap-$JBOSS_EAP_VERSION.$JBOSS_EAP_PATCH_VERSION.zip | grep $JBOSS_EAP_SHA1 \
&& unzip jboss-eap-$JBOSS_EAP_VERSION.$JBOSS_EAP_PATCH_VERSION.zip \
&& mv $HOME/jboss-eap-$JBOSS_EAP_VERSION $JBOSS_HOME \
&& rm jboss-eap-$JBOSS_EAP_VERSION.$JBOSS_EAP_PATCH_VERSION.zip \
&& chown -R jboss:0 ${JBOSS_HOME} \
&& chmod -R g+rw ${JBOSS_HOME}

# Assegure-se de que os sinais sejam encaminhados para o processo da JVM corretamente para um desligamento normal
ENV LAUNCH_JBOSS_IN_BACKGROUND true

USER jboss RUN $JBOSS_HOME/bin/add-user.sh admin admin --silent

USER jboss

# Expondo portas
EXPOSE 8080 9990 4447 9999

# Comandos de inicialização
CMD ["/opt/jboss/jboss-eap/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "--debug"]