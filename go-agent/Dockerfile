FROM openjdk:8-jre

RUN apt-get update && \
    apt-get install -y apt-transport-https && \
	echo "deb https://download.gocd.io /" | tee /etc/apt/sources.list.d/gocd.list && \
    curl https://download.gocd.io/GOCD-GPG-KEY.asc | apt-key add - && \
    apt-get update && \
	apt-get install -y go-agent && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh && \
    chmod +x wait-for-it.sh

RUN sed -i 's/127.0.0.1/go-server/' /etc/default/go-agent && \
    sed -i 's/DAEMON=Y/DAEMON=N/' /etc/default/go-agent

ENTRYPOINT ["./wait-for-it.sh", "-t", "30", "-s", "go-server:8153", "--", "/etc/init.d/go-agent"]

CMD ["start"]
