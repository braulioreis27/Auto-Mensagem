# Instalando Supabase

## Antes de começar
Você precisa do seguinte instalado no seu sistema: Git e Docker ( Windows , MacOS ou Linux ).
=======================================================================================================
## Instalando e executando o Supabase 

Siga estas etapas para iniciar o Supabase em sua máquina:

1. Baixei o repositório

```bash
git clone --depth 1 https://github.com/supabase/supabase
```
2. Entre no diretório da pasta

```bash
cd supabase/docker
```
3. Copie o Arquivo .env.example variável

```bash
cp .env.example .env
```
4. Extraia a imagem mais recente 

```bash
sudo docker compose pull
```
5. Inicie os serviços - Em modo desanexado

```bash
sudo docker compose up -d
```
6. Depois que todos os serviços forem iniciados, você poderá vê-los sendo executados em segundo plano:

```bash
sudo docker compose ps
```
=======================================================================================================
## Acessando o Supabase Studio 

Você pode acessar o Supabase Studio por meio do gateway de API na porta 8000. 
Por exemplo: http://<your-ip>:8000, ou localhost:8000 se estiver executando o Docker localmente.

Você será solicitado a fornecer um nome de usuário e uma senha. Por padrão, as credenciais são:

```bash
Nome de usuário:supabase
Senha:this_password_is_insecure_and_should_be_updated
Você deve alterar essas credenciais o mais rápido possível usando as instruções abaixo.
```
=======================================================================================================

## FONTE:

Documentação Supabase

```bash
https://supabase.com/docs/guides/self-hosting/docker
```



