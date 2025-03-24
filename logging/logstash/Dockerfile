FROM eclipse-temurin:21
RUN ln -fs /usr/share/zoneinfo/Asia/Bangkok /etc/localtime && \
    echo 'Asia/Bangkok' > /etc/timezone
RUN mkdir /data && cd /data && \
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-8.17.3-linux-x86_64.tar.gz && \
    tar xzvf logstash-8.17.3-linux-x86_64.tar.gz && \
    mv logstash-8.17.3 /data/logstash
COPY ./pipeline.conf /etc/logstash/pipeline.conf
COPY startup.sh /data/startup.sh
RUN chmod +x /data/startup.sh
RUN chmod +x /data/logstash/bin/logstash-plugin
RUN chmod +x /data/logstash/bin/logstash
RUN ./data/logstash/bin/logstash-plugin install logstash-output-opensearch logstash-filter-multiline logstash-input-beats

EXPOSE 5044
WORKDIR /data/logstash
ENTRYPOINT [ "/data/startup.sh" ]