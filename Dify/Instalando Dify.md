# Instalando o Dify via npm

# 1. Atualize o sistema
Antes de começar, atualize os pacotes do sistema.

```bash
sudo apt update && sudo apt full-upgrade -y
```
======================================================================================
# 2. Instale o Node.js e npm
O npm (Node Package Manager) é instalado junto com o Node.js. Instale a versão LTS.

1. Adicione o repositório do Node.js:

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```
2. Instale o Node.js e npm:

```bash
sudo apt install nodejs -y
```
3. Verifique as versões instaladas:

```bash
node -v
npm -v
```
======================================================================================
## 3. Instale o Git, Nano, Wget, Curl

```bash
sudo apt install git nano wget curl -y
```
Verifique se foi instalado corretamente:

```bash
git --version
```
======================================================================================
## 4. Configure o banco de dados (PostgreSQL)

O Dify usa o PostgreSQL como banco de dados.

1. Instale o PostgreSQL:

```bash
sudo apt install postgresql postgresql-contrib -y
```
2. Acesse o usuário postgres e configure o banco:

```bash
sudo -i -u postgres
```
3. Crie um banco de dados e um usuário:

```bash
psql
CREATE DATABASE difydb;
CREATE USER difyuser WITH PASSWORD '123456';
GRANT ALL PRIVILEGES ON DATABASE difydb TO difyuser;
\q
```
4. Saia do usuário postgres:

```bash
exit
```
======================================================================================

## 5. Clone o repositório do Dify

1. Clone o projeto diretamente do GitHub:

```bash
git clone https://github.com/langgenius/dify.git
```
2. Acesse o diretório do projeto:

```bash
cd dify
```
======================================================================================
## 6. Instale as dependências

No diretório clonado, execute o comando:

```bash
npm install
```
======================================================================================
## 7. Configure as variáveis de ambiente

O Dify requer um arquivo .env para definir as configurações.

1. Crie um arquivo .env no diretório do projeto:

```bash
nano .env
```
2. Adicione as variáveis mínimas necessárias (exemplo):

```bash
DATABASE_URL=postgres://difyuser:123456@localhost:5432/difydb
PORT=3000
NODE_ENV=production
```
3. Salve o arquivo pressionando Ctrl+O, Enter e Ctrl+X.

======================================================================================
## 8. Inicialize o serviço

Inicie o serviço Dify usando o npm:

```bash
npm start
```
O serviço estará rodando no http://localhost:3000.

======================================================================================
## 9. Configure o firewall (opcional)

Certifique-se de liberar a porta 3000, se necessário:

```bash
sudo ufw allow 3000
```
======================================================================================
## 10. Acesse o Dify

Abra um navegador e acesse o endereço:

```bash
http://seu-ip-ou-dominio:3000
```
======================================================================================