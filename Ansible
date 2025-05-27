## 🤖 Ansible - Automação de Configuração

Este diretório contém playbooks e exemplos de automação de infraestrutura utilizando Ansible.

# 📋 Requisitos

Máquina de controle com Ansible instalado

Acesso SSH às máquinas gerenciadas

Chave SSH distribuída ou senha configurada no inventário

# 📂 Estrutura

playbooks/: Contém os arquivos .yml de automação

instalar-dns.yml: Instala e configura DNS em servidores Linux

configurar-usuarios.yml: Cria usuários em lote

# 🛠️ Comandos Úteis

# ▶️ Executar um playbook

ansible-playbook -i inventario.ini playbooks/instalar-dns.yml

# 🔍 Verificar a sintaxe de um playbook

ansible-playbook --syntax-check playbooks/instalar-dns.yml

# 📜 Exemplo de Playbook: instalar-dns.yml

- name: Instalar e configurar DNS (BIND9)
  hosts: dns_servers
  become: yes
  tasks:
    - name: Instalar pacotes do BIND
      apt:
        name:
          - bind9
          - bind9utils
          - bind9-doc
        state: present
        update_cache: yes

    - name: Copiar configuração da zona
      copy:
        src: arquivos/db.exemplo.local
        dest: /etc/bind/db.exemplo.local

    - name: Configurar zona no named.conf.local
      blockinfile:
        path: /etc/bind/named.conf.local
        block: |
          zone "exemplo.local" {
              type master;
              file "/etc/bind/db.exemplo.local";
          };

    - name: Reiniciar serviço BIND
      service:
        name: bind9
        state: restarted

# 👥 Exemplo de Playbook: configurar-usuarios.yml

- name: Criar usuários em servidores Linux
  hosts: all
  become: yes
  vars:
    usuarios:
      - nome: alice
      - nome: bob
  tasks:
    - name: Criar usuários
      user:
        name: "{{ item.nome }}"
        state: present
        groups: sudo
      loop: "{{ usuarios }}"

Pronto! Agora você tem automações básicas com Ansible funcionando! 🚀

