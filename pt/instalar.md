

# Instalar a versão mais recente do NodeJS no Linux

Processo para realizar a instalação da versão mais recente do NodeJS em Linux nativo ou em containers.

## Antes de Começar

**Certifique que removeu o NodeJS com o gestor de pacotes da distribuição.**

Por exemplo:

`apt remove --purge nodejs`

## Instalação da versão atual do NodeJS

Aplicável à todas distribuições como Ubuntu, Debian, CentOS, Fedora, etc...

Obter o link da versão mais recente diretamente do site oficial do NodeJS:

[https://nodejs.org/en/download/](https://nodejs.org/en/download/)

Para servidores será o link da versão **LTS**.

A plataforma provavelmente será **Linux Binaries (x64)**.

Criar a pasta que vai conter as versões do NodeJS e realiza o download:

```
mkdir /opt/node

cd /opt/node

wget https://nodejs.org/dist/v12.16.3/node-v12.16.3-linux-x64.tar.xz

tar -xf node-v12.16.3-linux-x64.tar.xz

ln -s /opt/node/node-v12.16.3-linux-x64 /opt/node/latest
```

Cria o link simbólico `/opt/node/latest`.

Assim quando for preciso alterar a versão do NodeJS basta corrigir o link simbólico.

> Teste executando `/opt/node/latest/bin/node`

### Comando Geral de Sistema

Para configurar o `node` e `npm` como comando global para todos os users.

Então edite o ficheiro `/etc/environment` e acrescente `:/opt/node/latest` à variável de sistema **PATH**.

Exemplo completo do `/etc/environment` com o link simbólico da última versão do NodeJS adicionada no fim:

`PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/opt/node/latest/bin"`

### Novas sessões de Terminais

Ao iniciar sessão dentro do container para executar comandos, como:

`lxc exec meu-container -- /bin/bash`

Ou ao iniciar novas sessões de terminais, como abrir tabs ou com o `tmux`.

Não processa o que foi definido em `/etc/environment`.

Então acrescente o caminho do NodeJS no **PATH** dentro do ficheiro `~/.[SHELL]rc`, onde _[SHELL]_ é o seu tipo de terminal, por exemplo `.bashrc`, `.zshrc`, etc...

Exemplo de como adicionar no **root** com **bash**, edite o `/root/.bashrc` e adicione no fim:

```
PATH="$PATH:/opt/node/latest/bin"

export PATH
```

### Considerações

Para adicionar comandos no Linux basta adicionar o caminho da pasta que contém os executáveis na variável global de sistema **PATH**.

Isto é realizado de forma global em `/etc/environment`.

Em alguns casos poderá não ser o suficiente, como em containers ou quando abre um novo terminal, então adicione no ficheiro `.bashrc` ou em outro tipo de ficheiro correspondente de acordo com o seu tipo de shell.



