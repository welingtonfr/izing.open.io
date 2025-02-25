FROM node:16 as build-stage

WORKDIR /app

COPY package*.json ./

RUN npm install

# Copia o restante do código do projeto
COPY . .

# Constrói o projeto Vue.js
RUN npx quasar build

# Estágio de produção (production stage)
FROM nginx:alpine

# Copia os arquivos construídos do estágio de construção para o diretório do Nginx
COPY --from=build-stage /app/dist /usr/share/nginx/html

# Copia o arquivo de configuração personalizado do Nginx (opcional)
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expõe a porta 80 (porta padrão do Nginx)
EXPOSE 80

# Comando para iniciar o Nginx
CMD ["nginx", "-g", "daemon off;"]