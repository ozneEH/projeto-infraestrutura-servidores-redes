🛡️ Guia de Instalação – Wazuh (Servidor e Agente)

📋 1. Requisitos

Sistema Operacional: Ubuntu 20.04 LTS ou Debian 11

Recursos mínimos: 4 vCPU, 8 GB RAM

🧰 2. Instalação via Script Oficial

Execute os comandos abaixo:

curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
bash wazuh-install.sh -a

⚙️ 3. O Instalador Configura Automaticamente

Wazuh Manager

Filebeat (para envio de logs ao Elasticsearch)

Elasticsearch + Kibana com dashboards do Wazuh

🌐 4. Acesso ao Dashboard

URL: https://<IP-do-servidor>

Usuário: admin

Senha: Fornecida ao final da instalação

🖥️ 5. Configuração dos Agentes (Clientes Windows/Linux)

Baixe o instalador do agente no site oficial

Durante a instalação, aponte para o IP do servidor Wazuh

🛠️ Configurações Comuns – configuracao.md

📁 Local: /var/ossec/etc/ossec.conf

🔹 1. Criar Grupos de Agentes

Organize os agentes em grupos para aplicar configurações específicas.

📜 2. Configurar Regras Personalizadas

Adicione regras específicas para seu ambiente, ajustando alertas e detecções.

📂 3. Monitoramento de Arquivos e Logs

Inclua diretórios ou arquivos críticos para serem monitorados.

🧩 4. Integrações (Windows)

Active Directory

Sysmon

✉️ 5. Alertas

Configure alertas por:

E-mail

Integração com sistemas SIEM

Wazuh instalado e configurado com sucesso! 🔍

