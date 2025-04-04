# Ansible
Repositorio para atividade da matéria de Computação Orientada a Serviços - Unitins

# Relatório Ansible - Computação Orientada a Serviços

Este repositório documenta a automação de servidores na GCP utilizando Ansible. Foram configuradas instâncias para gerenciar a instalação do serviço Nginx.

## Ambiente

- **Instâncias GCP:**
  - **ControlNodeAnsible:** Gerencia os servidores.
  - **ServidorNginx1:** Destinado à instalação do Nginx.
- **Chaves de Acesso:** `chaveControlNode`, `ServidorNginx1` e `ServidorNginx2`

## Principais Passos

1. **Configuração Local e Acesso:**
   - Transferência das chaves via `ssh manual`
   - Conexão via SSH:
     ```bash
     ssh root@35.224.35.219
     ssh root@35.224.83.210
     ```

2. **Instalação e Configuração do Ansible:**
   - Atualização do sistema e instalação do Ansible:
     ```bash
     apt update && sudo apt upgrade -y
     apt install software-properties-common
     add-apt-repository --yes --update ppa:ansible/ansible
     apt install ansible
     ansible --version
     ```
   - Configuração do arquivo `/etc/ansible/hosts`:
     ```ini
     [servidores]
     35.224.35.219
     35.224.83.210
     ```

3. **Execução dos Playbooks:**
   - **Nginx:**
     - Arquivo: `playbooks-nginx.yml`
     ```yaml
     ---
     - name: Instalar o nginx
       hosts: servidores
       become: true
       tasks:
         - name: Instalar nginx
           apt:
             name: nginx
             state: present
     ```
     - Executar:
       ```bash
       ansible-playbook playbooks-nginx.yml
  

## Resultados

- **Validação:** Testes com `ansible -m ping`, `uptime` e `ip a` confirmaram a conectividade e o sucesso na instalação dos serviços.
