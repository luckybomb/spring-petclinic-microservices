FROM openjdk:8
VOLUME /tmp
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh wait-for-it.sh
RUN bash -c 'chmod +x wait-for-it.sh'
ARG ARTIFACT_NAME
ADD ${ARTIFACT_NAME}.jar /app.jar
ENV SPRING_PROFILES_ACTIVE docker
RUN bash -c 'touch /app.jar'
RUN bash -c 'mkdir -p /neo'
ADD http://archive.dev.daumcorp.com/neo/0.1.27/neo.agent.tar.gz /neo/
RUN bash -c 'tar xvfz /neo/neo.agent.tar.gz -C /neo'
RUN bash -c 'touch /neo/neo-0.1.27/neo.agent.jar'
EXPOSE ${EXPOSED_PORT}
ENTRYPOINT ["java", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-javaagent:/neo/neo-0.1.27/neo.agent.jar", "-Dservice_key=15f8e587-a38e-4fd7-9db3-c582f7edecd5", "-Dapplication_name=api-gateway", "-Dapm.env=dev", "-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
