FROM websphere-liberty:javaee7

RUN /opt/ibm/wlp/bin/installUtility install ServletSample logstashCollector-1.0 --acceptLicense --downloadDependencies=true; \
    mkdir -p /opt/ibm/wlp/output/ServletSample; \
    /opt/ibm/wlp/bin/securityUtility createSSLCertificate --server=ServletSample --password="Liberty" --subject=CN=ServletSample,OU=ServletSample,O=ibm,C=us

COPY ./logstash.crt /opt/ibm/wlp/output/ServletSample/resources/security/logstash.crt

RUN keytool -import -noprompt -alias logstash -file /opt/ibm/wlp/output/ServletSample/resources/security/logstash.crt -keystore /opt/ibm/wlp/output/ServletSample/resources/security/trust.jks -storepass Liberty

CMD ["/opt/ibm/wlp/bin/server", "run", "ServletSample"]

COPY ./websphere-liberty/server.xml /opt/ibm/wlp/usr/servers/ServletSample/