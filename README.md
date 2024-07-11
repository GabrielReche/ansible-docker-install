# Ansible SSH Key Generation

## Visão Geral
Este projeto contém um playbook Ansible para gerar pares de chaves SSH em servidores remotos.

Neste playbook:

Atualizar o índice de pacotes do APT:

Atualiza a lista de pacotes disponíveis no sistema.
Instalar pacotes necessários para APT usar um repositório via HTTPS:

Instala pacotes essenciais para permitir o uso de repositórios APT via HTTPS.
Adicionar a chave GPG oficial do Docker:

Baixa e adiciona a chave GPG do Docker, que é usada para verificar a autenticidade dos pacotes Docker.
Adicionar o repositório do Docker:

Adiciona o repositório oficial do Docker à lista de fontes APT do sistema.
Atualizar o índice de pacotes do APT novamente:

Atualiza a lista de pacotes novamente para incluir o novo repositório do Docker.
Certificar-se de que está instalando a partir do repositório Docker:

Verifica a política do pacote docker-ce para garantir que será instalado a partir do repositório correto.
Instalar o Docker:

Instala o pacote docker-ce (Community Edition) do Docker.
Verificar se o Docker está instalado e funcionando:

Verifica e garante que o serviço Docker está ativo e habilitado para iniciar no boot.
Baixar a versão mais recente do Docker Compose:

Baixa a versão mais recente do Docker Compose e a coloca no diretório /usr/local/bin.
Aplicar permissões executáveis ao binário do Docker Compose:

Define permissões executáveis no binário do Docker Compose.
Verificar se a instalação do Docker Compose foi bem-sucedida:

Verifica a instalação do Docker Compose exibindo sua versão.
Adicionar o usuário atual ao grupo Docker:

Adiciona o usuário atual ao grupo Docker para permitir a execução de comandos Docker sem sudo.
Verificar a versão do Docker:

Verifica a instalação do Docker exibindo sua versão.
Verificar a versão do Docker Compose:

Verifica a instalação do Docker Compose exibindo sua versão.
Criar diretório /dl na raiz (comentado):

Cria um diretório /dl na raiz do sistema. Esta etapa está comentada.
Copiar arquivo docker-compose.yml para o diretório /dl na máquina de destino (comentado):

Copia um arquivo docker-compose.yml para o diretório /dl na máquina de destino. Esta etapa está comentada.

## Arquivos
- `inventory/hosts`: Arquivo de inventário com detalhes dos servidores.
- `playbooks/create_ssh_key.yml`: Playbook para iniciar a instalação.


## Uso
1. Atualize o arquivo `inventory/hosts` com os detalhes do seu servidor.

## IP
IP: Este é o endereço IP do host ao qual o Ansible se conectará para executar as tarefas. Pode ser um endereço IP ou um nome de domínio.

## ansible_user

ansible_user=nomedousuário: Define o nome de usuário usado para se conectar ao host remoto. Neste caso, nomedousuário será usado como o nome de usuário SSH.

## ansible_ssh_pass

ansible_ssh_pass=senhadousuário: Define a senha usada para autenticação SSH. senhadousuário será usada como a senha para se autenticar no host remoto.

## ansible_become_pass

ansible_become_pass=senhadousuário: Define a senha que será usada para elevar privilégios (sudo). Isso é útil quando o usuário precisa executar comandos como superusuário (root).

## ansible_ssh_common_args

ansible_ssh_common_args='-o StrictHostKeyChecking=no': Define argumentos adicionais para a linha de comando SSH. A opção -o StrictHostKeyChecking=no desativa a verificação da chave de host SSH. Isso é útil em ambientes onde os hosts são dinâmicos ou quando você deseja evitar a verificação manual das chaves de host. No entanto, pode ser uma prática insegura, pois desativa uma camada de proteção contra ataques de "man-in-the-middle".


2. Execute o playbook com:

```sh
ansible-playbook -i inventory/hosts playbooks/install_docker.yml




