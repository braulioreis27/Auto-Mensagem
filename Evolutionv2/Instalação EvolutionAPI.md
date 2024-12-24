Instalação EvolutionAPI V2 (LocalHost) NVM

Instalação EvolutionV2 via NVM
======================================

PostgreSQL
# Instale o PostgreSQL na sua máquina.

sudo apt-get update
sudo apt-get install postgresql postgresql-contrib

# Inicie o serviço do PostgreSQL:
sudo service postgresql start

# Acesse o prompt do PostgreSQL:
sudo -u postgres psql

# Crie um novo usuário:
CREATE USER evolutionv2 WITH PASSWORD '123456';

# Conceda privilégios ao novo usuário:
ALTER USER evolutionv2 WITH SUPERUSER;
ALTER USER evolutionv2 CREATEDB;

# Crie um banco de dados:
CREATE DATABASE evolutionv2;

===========================================

# Instalação do Redis
sudo apt-get install redis-server

# Inicie o serviço do Redis:
sudo service redis-server start

# Verifique se o Redis está rodando corretamente com o comando:
redis-cli ping
===========================================

Instalar NVM
# Primeiro, baixe e instale o Node.js com os seguintes comandos:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash

# Carregar o NVM no ambiente atual
source ~/.bashrc

# Instalar e usar a versão necessária do Node.js
nvm install 20.17.0 && nvm use 20.17.0

# Verifique se a versão está correta:
node -v

# Tentar novamente instalar o npm: Após atualizar o Node.js, tente instalar o npm novamente:
npm install -g npm@latest

# Verificar se tudo está correto: Após a instalação, confirme as versões do Node.js e do npm:

node -v
npm -v


# Clone o repositório oficial da Evolution API v2 a partir da branch correta:
git clone -b main https://github.com/EvolutionAPI/evolution-api.git

# Acesse o diretório do projeto e instale as dependências:
cd evolution-api
npm install

# Agora vamos configurar as variáveis de ambiente. Primeiro, copie o arquivo .env.example para .env:
cp ./.env.example ./.env

# Edite o arquivo .env com suas configurações específicas:
sudo nano ./.env

# Mude as linhas desta forma

- SERVER_URL=http://10.94.80.237:8080 -- Coloque seu ip da máquina
- DATABASE_CONNECTION_URI='postgresql://evolutionv2:123456@localhost:5432/evolution?schema=public' -- Coloque essa forma
- DATABASE_CONNECTION_CLIENT_NAME=evolution2 -- Coloque evolutionv2
 
 # Aberta CTRL+O para salvar, e CRTL+X para sair.
 
 # Gerar os arquivos do cliente Prisma:
npm run db:generate
# Realizar o deploy das migrations:
npm run db:deploy

# Após a configuração, você pode iniciar a Evolution API com o seguinte comando:
npm run build
npm run start:prod

# Use o PM2 para gerenciar o processo da API:
npm install pm2 -g
pm2 start 'npm run start:prod' --name ApiEvolution
pm2 startup
pm2 save --force


