# Setup

## Instale o uma imagem Ubuntu atualizada e de preferência, recém instalada.

## Instalação do Docker no WSL

**Utilizar iptables legada**
Executar:
```sh
sudo update-alternatives --config iptables
```
Selecionar a opção “iptables-legacy”

**Instalar o Docker**
Remover versões antigas:
```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```
Se não tiver docker instalado, vai exibir: “Unable to locate package docker-engine”

Instalar dependências:
```sh
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install ca-certificates curl gnupg lsb-release
sudo apt-get autoremove
```
Adicionar chave do repositório oficial do Docker:
```sh
sudo mkdir -p /etc/apt/keyrings
```
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```sh
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Instalar o Docker Engine:
```sh
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
Teste:
```sh
docker --version
docker compose version
```

**Adicionar Alias** (Alias para o comando “docker-compose” funcionar)

Abrir o arquivo
```sh
nano ~/.bash_aliases
```
Adicionar a seguinte linha:
```sh
alias docker-compose="docker compose"
```
Salvar o arquivo pressionando CTRL+X
Então, executar:
```sh
source ~/.bash_aliases
alias docker-compose="docker compose"
```
Para testar, executar:
```sh
docker-compose version
```

**Adicionar permissões**
Executar:
```sh
sudo groupadd docker
sudo usermod -aG docker $USER
```
Iniciar o Docker

Executar:
```sh
sudo dockerd
```
Se for iniciado com sucesso, será exibido: API listen on /mnt/wsl/shared-docker/docker.sock
