# Ansible
Repositorio para atividade da matéria de Computação Orientada a Serviços - Unitins

# Relatório Ansible - Computação Orientada a Serviços

Este repositório documenta a automação de servidores na GCP utilizando Ansible. Foram configuradas instâncias para gerenciar a instalação do serviço Nginx.

## Ambiente

- **Instâncias AWS:**
  - **ControlNodeAnsible:** Gerencia os servidores.
  - **ServidorNginx1:** Destinado à instalação do Nginx.
- **Chaves de Acesso:** `chaveControlNode`, `ServidorNginx1` e `ServidorNginx2`

## Principais Passos

1. **Configuração Local e Acesso:**
   - Transferência das chaves via `scp`
   - Conexão via SSH:
     ```bash
     ssh -i "chaveControlNode.pem" ubuntu@ec2-56-124-67-85.sa-east-1.compute.amazonaws.com
     ```

2. **Instalação e Configuração do Ansible:**
   - Atualização do sistema e instalação do Ansible:
     ```bash
     sudo apt update && sudo apt upgrade -y
     sudo apt install software-properties-common
     sudo add-apt-repository --yes --update ppa:ansible/ansible
     sudo apt install ansible
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
     - Arquivo: `playbook-nginx.yml`
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
