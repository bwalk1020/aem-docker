# DOCKER-VERSION 1.0.1
FROM aem-base
MAINTAINER Adfinis SyGroup/Namics

#Copies required build media
COPY AEM_6.2_Quickstart.jar /aem/AEM_6.2_Quickstart.jar
COPY license.properties /aem/license.properties
COPY postInstallHook.py /aem/postInstallHook.py

# Extracts AEM
WORKDIR /aem
RUN java -XX:MaxPermSize=256m -Xmx1024M -jar AEM_6.2_Quickstart.jar -unpack -r nosamplecontent

# Add customised log file, to print the logging to standard out.
COPY org.apache.sling.commons.log.LogManager.config /aem/crx-quickstart/install/

# Installs AEM
RUN ["python","aemInstaller.py","-i","AEM_6.2_Quickstart.jar","-r","author","-p","4502"]

EXPOSE 4502 8000
ENTRYPOINT ["/aem/crx-quickstart/bin/quickstart"]
