## 🪟 Guia de Instalação e Configuração – Windows Server

# ✅ 1. Instalação do Windows Server

# 🔽 Baixe a ISO

# 👉 Site oficial da Microsoft

# 💾 Crie o pendrive bootável

Use ferramentas como:

Rufus

# 🚀 Prossiga com a instalação

Inicie o boot pelo pendrive

Selecione:

Idioma e formato de hora

Tipo de instalação: Custom: Install Windows only

Disco onde o sistema será instalado

Após a instalação, defina uma senha para o usuário Administrador

# ⚙️ Configurações Iniciais

Configure IP fixo (opcional, mas recomendado para servidores)

Ative o Windows e instale atualizações

Altere o nome do computador

# 📡 Configuração do Servidor DNS

Acesse o Gerenciador de Servidores

Adicione a função Servidor DNS

Crie uma zona direta:

Nome: exemplo.local

Tipo: Primária

Permitir atualização dinâmica

Adicione registros:

A (host)

CNAME (alias), conforme necessário

Configure encaminhadores DNS externos (ex: 8.8.8.8)

# 🧯 Configuração do Servidor DHCP

No Gerenciador de Servidores, adicione a função Servidor DHCP

Defina escopos:

Nome: LAN

Faixa: 192.168.1.100 - 192.168.1.200

Gateway: 192.168.1.1

DNS: IP do servidor DNS interno

Ative o escopo

Autorize o servidor DHCP no Active Directory (se aplicável)

# 🧱 Active Directory – active-directory/configuracao.md

# 🛠️ Configuração do Active Directory (AD DS)

Adicione a função Serviços de Domínio Active Directory (AD DS)

Promova o servidor a controlador de domínio:

Novo domínio em uma nova floresta

Nome do domínio: exemplo.local

Nível funcional: Windows Server 2016 ou superior

Defina senha de restauração do modo DSRM

Reinicie o servidor

Verifique o status com Active Directory Users and Computers

Crie:

Unidades Organizacionais (OUs)

Grupos

Usuários

Configure GPO básica:

Políticas de senha

Bloqueio de conta

Outras restrições conforme política da empresa

Windows Server instalado e com serviços essenciais prontos para uso! 🖥️

