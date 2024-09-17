# Etapa de build usando uma imagem do Maven
FROM maven:3.8.4-jdk-8 AS build

# Copiar o código fonte para o diretório /app/src
COPY teste /app/src
COPY pom.xml /app

# Definir o diretório de trabalho
WORKDIR /app

# Listar arquivos para verificar a estrutura do diretório
RUN ls -l /app/src
RUN ls -l /app

# Executar o comando Maven para compilar e instalar o projeto
RUN mvn clean install -U

# Etapa final usando uma imagem leve do OpenJDK
FROM openjdk:8-jre-alpine

# Copiar o JAR gerado da etapa de build para a nova imagem
COPY --from=build /app/target/spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar app/app.jar

# Definir o diretório de trabalho
WORKDIR /app

# Expor a porta 8080
EXPOSE 8080

# Comando para iniciar o aplicativo
CMD ["java", "-jar", "app.jar"]
