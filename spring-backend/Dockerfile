FROM alpine:3.19 as system

RUN apk update && \
    apk add maven && \
    apk add openjdk11 && \
    rm -rf /var/cache/apk/*

FROM system as build

WORKDIR /app
COPY pom* ./

RUN mvn dependency:copy-dependencies

COPY ./src ./src

RUN mvn package

FROM system as app

COPY --from=build /app/target/*.jar /app/app.jar

EXPOSE ${APP_PORT}
USER 1001

ENTRYPOINT ["java", "-jar", "/app/app.jar"]
