FROM apache/flink:1.18.1-scala_2.12-java11

WORKDIR /opt/flink

# Enable SQL Client to find the job manager when running it from this image
RUN sed -i "s/jobmanager.rpc.address: localhost/jobmanager.rpc.address: flink-jobmanager/g" ./conf/flink-conf.yaml

# Install required dependencies
RUN apt-get update && \
    apt-get install -y vim lnav

RUN echo "-> Install JARs: Postgres JDBC driver" && \
    mkdir -p ./lib/jdbc && \
    curl https://jdbc.postgresql.org/download/postgresql-42.7.1.jar -o ./lib/jdbc/postgresql-42.7.1.jar && \
    curl https://repository.apache.org/content/repositories/orgapacheflink-1706/org/apache/flink/flink-connector-jdbc/3.1.2-1.18/flink-connector-jdbc-3.1.2-1.18.jar -o ./lib/jdbc/flink-connector-jdbc-3.1.2-1.18-rc3.jar

RUN echo "Purge build artifacts" && \
    apt-get purge -y --auto-remove $build_deps && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

CMD ./bin/start-cluster.sh && sleep infinity
