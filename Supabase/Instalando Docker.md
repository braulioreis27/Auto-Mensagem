# Instalando Docker

1. Instale todos os pacotes de dependência necessários.

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```
2. Adicione a chave GPG do Docker ao chaveiro do seu servidor.

```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```
3. Adicione o repositório Docker mais recente às suas fontes APT.

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
4. Atualize o índice de pacotes do servidor.

```bash
sudo apt update
```
5. Instalar o Docker.

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
6. O comando acima instala a versão mais recente do Docker com os seguintes plugins:

```bash
docker-ce: O pacote da edição da comunidade do mecanismo Docker.
docker-ce-cli: Habilita a interface de linha de comando (CLI) do Docker.
containerd.io: Um tempo de execução de contêiner que monitora o ciclo de vida dos contêineres do Docker.
docker-buildx-plugin: Melhora os recursos de criação de imagens do Docker para compilações multiplataforma.
docker-compose-plugin: Permite o gerenciamento de aplicativos Docker de vários contêineres usando arquivos YAML.
```
7. Veja a versão do Docker instalada no seu servidor.

```bash
sudo docker --version
```
Saída:

```bash
Docker version 26.1.4, build 5650f9b
```
=======================================================================================================
## Gerenciar o serviço do sistema Docker

1. Habilite o serviço do sistema Docker para iniciar automaticamente no momento da inicialização.

```bash
sudo systemctl enable docker
```

2. Visualize o status do serviço Docker e verifique se ele está em execução.

```bash
sudo systemctl status docker
```
Saída:

```bash
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Mon 2024-06-17 21:07:25 UTC; 1min 2s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 120312 (dockerd)
      Tasks: 8
     Memory: 34.5M (peak: 35.3M)
        CPU: 281ms
     CGroup: /system.slice/docker.service
             └─120312 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```

3. Execute o seguinte comando para parar o Docker.

```bash
sudo systemctl stop docker
```

4. Reinicie o serviço Docker.

```bash
sudo systemctl restart docker
```
=======================================================================================================
## Execute um aplicativo em contêiner

O Docker executa aplicativos em contêiner usando imagens de contêiner locais ou remotas de registros como o Docker Hub.
Siga as etapas abaixo para executar um aplicativo em contêiner Nginx de exemplo para testar o Docker no seu servidor.

1. Obtenha a imagem mais recente do Nginx do Docker Hub.

```bash
sudo docker pull nginx:latest
```
2. Visualize todas as imagens do Docker no servidor e verifique se a imagem Nginx está disponível.

```bash
sudo docker images
```
Saída:

```bash
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
nginx        latest    dde0cca083bc   2 weeks ago   188MB
```
3. Execute um novo contêiner do Docker usando a imagem.

```bash
sudo docker run --name mynginx -d -p 80:80 nginx:latest
```
O comando acima executa um novo contêiner Docker no servidor usando sua imagem Nginx com os seguintes valores:

```bash
-name mynginx: Define o nome do contêiner como mynginx.
d: Inicia o contêiner no modo desanexado como um processo em segundo plano no servidor.
p 80:80: Mapeia a porta do host 80para a porta do contêiner 80. Isso permite que você acesse o contêiner usando a porta do host no seu servidor.
nginx:latest: Define a imagem do Docker a ser usada ao criar o contêiner.
```
4. Liste todos os contêineres em execução no servidor e verifique se o novo contêiner está ativo.

```bash
sudo docker ps
```
Saída:

```bash
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                               NAMES
d79cad9ea8d2   nginx:latest   "/docker-entrypoint.…"   5 seconds ago   Up 4 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   mynewnginx
```

=======================================================================================================
## 5. Configuração do Firewall

1. Habilitar o UFW
```bash
sudo ufw enable
```
2. Verificar o status do UFW

```bash
sudo ufw status
```
3. Adicionar as portas

```bash
sudo ufw allow 80 && sudo ufw allow 8080 && sudo ufw allow 22

```
6. Acesse o endereço IP do seu servidor usando um navegador da Web, como o Chrome, para testar o acesso ao contêiner do Docker.

```bash
http://SERVER-IP
```
=======================================================================================================
## FONTE:

Instalando Docker - Docs Vultr
```bash
https://docs.vultr.com/how-to-install-docker-on-ubuntu-24-04
```
