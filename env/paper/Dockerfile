FROM alpine:latest
ARG version=1.16 
ENV xms=1G xmx=1G eula=false
RUN apk update && apk upgrade && \
    apk add openjdk11-jre wget && \
    adduser -D -u 1000 alpine && \
    mkdir /paper && \
    wget -O /paper/paperclip.jar https://papermc.io/ci/job/Paper-$version/lastSuccessfulBuild/artifact/paperclip.jar && \
    chown -R alpine /paper && \
    chmod -R u+rwx /paper
USER alpine
WORKDIR /paper
CMD echo "eula=$eula" > /paper/eula.txt && java -Xms$xms -Xmx$xmx -XX:+AlwaysPreTouch -XX:+DisableExplicitGC -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:MaxGCPauseMillis=50 -XX:TargetSurvivorRatio=90 -XX:G1NewSizePercent=50 -XX:G1MaxNewSizePercent=80 -XX:InitiatingHeapOccupancyPercent=10 -XX:G1MixedGCLiveThresholdPercent=50 -jar paperclip.jar
