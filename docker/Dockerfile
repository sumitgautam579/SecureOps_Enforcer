FROM ubuntu:20.04
RUN apt-get update && apt-get install -y chef sonar-scanner fortify appscan
COPY scan.sh /usr/local/bin/scan.sh
ENTRYPOINT ["/usr/local/bin/scan.sh"]
