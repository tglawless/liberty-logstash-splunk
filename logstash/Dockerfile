FROM logstash:5

ARG SPLUNK_HOST

RUN mkdir /etc/logstash/certs; \
    chmod 0755 /etc/logstash/certs;

COPY ./logstash.crt \
    ./logstash.key \
    /etc/logstash/certs/

# This step will retrieve the SSL certificate for the Splunk hostname provided in the build arg.
# The certificate will then be added to a trust store used by Logstash when communicating with
# Splunk over HTTPS
RUN cd /etc/logstash/certs; \
    openssl s_client -showcerts -connect $SPLUNK_HOST:8088 < /dev/null | openssl x509 > splunk.pem; \
    keytool -import -noprompt -alias splunk -file splunk.pem -keystore trust.jks -storepass logstash

COPY ./logstash/conf.d /etc/logstash/conf.d

EXPOSE 9600 5000
