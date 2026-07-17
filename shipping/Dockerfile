# Build Stage
FROM maven:3.9-eclipse-temurin-17 AS builder

WORKDIR /opt/server

COPY pom.xml ./
COPY src ./src

RUN mvn clean package

# Runtime Stage
FROM eclipse-temurin:17-jre

WORKDIR /opt/server

COPY --from=builder /opt/server/target/shipping-1.0.jar shipping.jar

ENV CART_ENDPOINT=cart:8080 \
    DB_HOST=mysql

EXPOSE 8080

CMD ["java", "-jar", "shipping.jar"]