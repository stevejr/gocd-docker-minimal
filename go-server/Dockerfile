FROM openjdk:8-jre

RUN apt-get update && \
    apt-get install -y apt-transport-https && \
    echo "deb https://download.gocd.io /" | tee /etc/apt/sources.list.d/gocd.list && \
    curl https://download.gocd.io/GOCD-GPG-KEY.asc | apt-key add - && \
    apt-get update && \
    apt-get install -y \
        go-server \
        git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN sed -i 's/DAEMON=Y/DAEMON=N/' /etc/default/go-server

ENTRYPOINT ["/etc/init.d/go-server"]

CMD ["start"]
