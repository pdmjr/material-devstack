# Material introdutório sobre instalação e uso do OpenStack

O conteúdo apresentado nesta página é baseado no tutorial oficial do [DevStack](https://docs.openstack.org/devstack/latest/) e foi testado em uma máquina virtual com Ubuntu 20.04.

INTRODUCAO SOBRE O DEVSTACK

INFORMACOES SOBRE A vm

## Adicionar um usuário stack (opcional)

DevStack deve executar a partir de um usuário não-root, mas com sudo habilitado.

Adicionando um usuário específico para execução do ambiente

```markdown
sudo useradd -s /bin/bash -d /opt/stack -m stack
```

Visto que o usuário precisa alterar o sistema, precisará de privilégios sudo

```markdown
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
```

Logar com o novo usuário

```markdown
sudo -u stack -i
```

## Instalação do sistema

Clonando o repositório e entrando no diretório

```markdown
git clone https://opendev.org/openstack/devstack
cd devstack
```

Criando o arquivo de configuração local

```markdown
tee -a local.conf  < EOF
[[local|localrc]]
ADMIN_PASSWORD=senha
DATABASE_PASSWORD=senha
RABBIT_PASSWORD=senha
SERVICE_PASSWORD=senha
HOST_IP=ip
SERVICE_HOST=ip
EOF
sed -i "s/senha/secret/g; s/ip/`hostname -I | cut -d ' ' -f 2`/g" local.conf
```

Iniciando a instalação

```markdown
./stack.sh
```
