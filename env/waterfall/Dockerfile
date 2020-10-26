FROM alpine:latest
ENV xms=1G
ENV xmx=1G
RUN apk update && apk upgrade && \
    apk add openjdk11-jre wget && \
    adduser -D -u 1000 alpine && \
    mkdir /waterfall && \
    wget -O /waterfall/Waterfall.jar https://papermc.io/ci/job/Waterfall/lastSuccessfulBuild/artifact/Waterfall-Proxy/bootstrap/target/Waterfall.jar && \
    chown -R alpine /waterfall && \
    chmod -R u+rwx /waterfall
USER alpine
WORKDIR /waterfall
CMD java -Xms$xms -Xmx$xmx -XX:+AlwaysPreTouch -XX:+DisableExplicitGC -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:MaxGCPauseMillis=50 -XX:TargetSurvivorRatio=90 -XX:G1NewSizePercent=50 -XX:G1MaxNewSizePercent=80 -XX:InitiatingHeapOccupancyPercent=10 -XX:G1MixedGCLiveThresholdPercent=50 -jar Waterfall.jar
