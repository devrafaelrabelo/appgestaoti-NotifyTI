FROM node:22.2.0-slim

# Ignora checagem de engine
ENV YARN_IGNORE_ENGINE=true

# Instala dependências do sistema
RUN apt-get update && apt-get install -y \
    git \
    python3 \
    make \
    g++ \
    yarn \
    chromium \
    ca-certificates \
    fonts-freefont-ttf \
    dumb-init \
    && rm -rf /var/lib/apt/lists/*

# Define diretório de trabalho
WORKDIR /app

# Clona o projeto do WPPConnect Server
RUN git clone https://github.com/wppconnect-team/wppconnect-server.git .

# Corrige restrição de engine no package.json
RUN sed -i 's/"node": *"[^"]*"/"node": ">=22.0.0"/' package.json

# Instala dependências do projeto
RUN yarn install

# Compila o TypeScript
RUN yarn build

EXPOSE 21465

ENTRYPOINT ["dumb-init", "--"]
CMD ["yarn", "start"]
