#FROM is00hcw/dubbo-generator:github
#FROM openjdk:8
FROM sgrio/java-oracle:jdk_8

# 时区设置
RUN echo "Asia/Shanghai" > /etc/timezone
#RUN echo "Asia/Shanghai" > /etc/timezone && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


EXPOSE 8080

ADD target/dubbo-admin-backend-0.0.1-SNAPSHOT.jar /app.jar

#RUN sh -c 'touch /app.jar'
#ENV JAVA_OPTS=""


#ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]

EXPOSE 9088

ENV JAVA_OPTS="\
-server \
-Xmx2048m \
-Xms512m \
-Xmn128m \
-Xss512K \
-XX:SurvivorRatio=8 \
-XX:MetaspaceSize=64m \
-XX:MaxMetaspaceSize=512m \
-XX:+UseParallelGC \
-XX:ParallelGCThreads=4 \
-XX:+UseParallelOldGC \
-XX:+UseAdaptiveSizePolicy \
-XX:+PrintGCDetails \
-XX:+PrintTenuringDistribution \
-XX:+PrintGCTimeStamps \
-XX:+HeapDumpOnOutOfMemoryError \
-XX:HeapDumpPath=/ \
-Xloggc:/dump/gc.log \
-XX:+UseGCLogFileRotation \
-XX:NumberOfGCLogFiles=5 \
-Dcom.sun.management.jmxremote.rmi.port=9088 \
-Dcom.sun.management.jmxremote=true \
-Dcom.sun.management.jmxremote.port=9088 \
-Dcom.sun.management.jmxremote.ssl=false \
-Dcom.sun.management.jmxremote.authenticate=false \
-Dcom.sun.management.jmxremote.local.only=false \
-Djava.rmi.server.hostname=erp2.test.pagoda.com.cn \
-XX:+UnlockDiagnosticVMOptions \
-XX:+DebugNonSafepoints \
-XX:+UnlockCommercialFeatures \
-XX:+FlightRecorder \
-XX:FlightRecorderOptions=defaultrecording=true,disk=true,repository=/tmp,maxage=2h,dumponexit=true,dumponexitpath=/dump/dumponexit.jfr,loglevel=info \
-XX:GCLogFileSize=10M"
# ERP4 IP

ENTRYPOINT java ${JAVA_OPTS} -Djava.security.egd=file:/dev/./urandom -jar /app.jar