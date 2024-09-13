FROM node:18-alpine AS build
# Utiliza a imagem base Node.js 18 com Alpine Linux como ponto de partida para o estágio de construção.

WORKDIR /app

COPY package*.json ./
# Copia os arquivos package.json e package-lock.json do host para o diretório /app.

RUN npm install
# Executa o comando npm install para instalar as dependências listadas no package.json.

COPY . .
# Copia todos os arquivos do diretório atual do host para o diretório /app do container

RUN npm run build
# Executa o script de build definido no package.json

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
