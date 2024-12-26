## Instalando o N8N via NPM

# Instalando o Node.js & npm

```bash
sudo apt install -y nodejs npm
```
# Verificar se foi instalando corretamente

```bash
node -v
npm -v
```
# Instalando o N8N via NPM

```bash
sudo npm install -g n8n
```
# Configurando o .n8n /.env

```bash
nano ~/.n8n/.env

# Adicione essas linhas

N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=123456

#Dê um CTRL+O para Salvar. CTRL+X para Sair
```


# Configurando o n8n.service

```bash
sudo nano /etc/systemd/system/n8n.service

# Adicione essas linhas

[Unit]
Description=n8n Automation Tool
After=network.target

[Service]
ExecStart=/usr/bin/n8n --host 10.94.80.26
Restart=always
User=n8n
Group=n8n
Environment=PATH=/usr/bin:/usr/local/bin
Environment=HOME=/home/n8n
WorkingDirectory=/home/n8n

[Install]
WantedBy=multi-user.target

#Dê um CTRL+O para Salvar. CTRL+X para Sair
```


# Comando para hatilitar e iniciar o serviço do N8N

```bash
sudo systemctl enable n8n
sudo systemctl start n8n
```
# Comando para colocar o host IP na máquina

```bash
n8n --host 10.94.80.26 --> Coloque aqui o ip da máquina
```
## Comando para reinicar o serviço 

```bash
sudo systemctl daemon-reload
sudo systemctl restart n8n
```

## Comando para verificar o status do Firewall e adiconar-ló no Firewall

```bash
sudo ufw status
sudo ufw allow 5678/tcp
```
## Comando para instalar o Certbot

```bash
sudo apt install certbot
sudo certbot certonly --standalone -d 10.94.80.26:5678 --> Coloque aqui o ip da máquina
```
# Comando para adicionar false para o IP Host

```bash
sudo N8N_SECURE_COOKIE=false n8n --host 10.94.80.26 --port 5678 -- Colocar aqui o IP da Máquina
```

# Comando para editar bashrc

```bash
nano ~/.bashrc

## Coloque essas linhas no final do arquivo

export N8N_SECURE_COOKIE=false
export N8N_HOST=10.94.80.26
export N8N_PORT=5678
```

# Comando para carregar a configuração 

```bash
source ~/.bashrc
```

# Comando para iniciar o N8N

```bash
n8n
```

# Abrir o N8N - Navegador
http://10.94.80.26:5678/ --> Seu IP e a Porta aqui






