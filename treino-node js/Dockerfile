# Especifica a versão do Node.js que você deseja usar
FROM node:14.17.0 AS build

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# Copia os arquivos de configuração de dependências para o contêiner
COPY package*.json ./

# Instala as dependências do projeto
RUN npm install

# Copia todos os arquivos do projeto para o contêiner
COPY . .

# Compila o projeto (se necessário)
RUN npm run build

# Etapa 2: Executar
FROM node:14.17.0

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# Copia os arquivos construídos da etapa anterior
COPY --from=build /app ./

# Adiciona um usuário não-root
RUN useradd -m appuser
USER appuser

# Define a variável de ambiente NODE_ENV como produção
ENV NODE_ENV=production

# Expõe a porta que o aplicativo irá usar
EXPOSE 3000

# Define o comando padrão para iniciar o aplicativo
CMD ["node", "dist/index.js"]
