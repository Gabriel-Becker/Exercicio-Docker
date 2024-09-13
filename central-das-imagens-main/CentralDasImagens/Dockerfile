FROM maven:3.6.3-openjdk-17 AS build
# Utiliza a imagem base Maven 3.6.3 com OpenJDK 17 como ponto de partida para o estágio de construção.

WORKDIR /app

COPY pom.xml .

COPY src ./src

RUN mvn clean package -DskipTests
# Executa o comando Maven para limpar o projeto, construir o JAR e pular os testes.

FROM openjdk:17-jdk-alpine

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar
# Copia o JAR gerado no estágio de construção para o diretório /app do estágio de produção.

EXPOSE 8080

CMD [ "java", "-jar", "app.jar" ]
# Define o comando padrão para executar quando o container iniciar: executa o JAR da aplicação.