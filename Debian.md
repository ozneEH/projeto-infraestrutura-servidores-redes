📘 Guia de Instalação e Configuração – Debian
✅ 1. Instalação do Debian
🔽 Baixe a ISO
Acesse o site oficial do Debian:
👉 https://www.debian.org/distrib/

💿 Crie um pendrive bootável
Use ferramentas como:

Rufus

balenaEtcher

🚀 Inicie a instalação
Dê boot pelo pendrive e selecione:

Install ou

Graphical Install

Siga os passos de configuração:

Idioma e localização

Nome do host e domínio (ex: debian e exemplo.local)

Criação de usuários (root e normal)

Particionamento do disco (automático ou manual)

Após isso:

Aguarde a instalação dos pacotes base

Instale o GRUB no disco principal

Finalize a instalação

🔧 Pós-instalação
Configure IP fixo:

bash
Copiar
Editar
sudo nano /etc/network/interfaces
Atualize o sistema:

bash
Copiar
Editar
sudo apt update && sudo apt upgrade -y
📡 2. Configuração do Servidor DNS (BIND9)
📁 Arquivo: dns/configuracao.md

🛠️ Instale o BIND9:
bash
Copiar
Editar
sudo apt install bind9 bind9utils bind9-doc -y
⚙️ Configure a zona local:
Edite o arquivo:

bash
Copiar
Editar
sudo nano /etc/bind/named.conf.local
Adicione:

conf
Copiar
Editar
zone "exemplo.local" {
  type master;
  file "/etc/bind/db.exemplo.local";
};
📄 Crie o arquivo de zona:
bash
Copiar
Editar
sudo cp /etc/bind/db.local /etc/bind/db.exemplo.local
sudo nano /etc/bind/db.exemplo.local
🔄 Reinicie o serviço:
bash
Copiar
Editar
sudo systemctl restart bind9
✅ Teste a configuração:
bash
Copiar
Editar
dig @localhost exemplo.local
🧭 3. Configuração do Servidor DHCP (isc-dhcp-server)
📁 Arquivo: dhcp/configuracao.md

🛠️ Instale o servidor DHCP:
bash
Copiar
Editar
sudo apt install isc-dhcp-server -y
⚙️ Configure o DHCP:
Edite o arquivo principal:

bash
Copiar
Editar
sudo nano /etc/dhcp/dhcpd.conf
Adicione:

conf
Copiar
Editar
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option domain-name-servers 192.168.1.10;
  option domain-name "exemplo.local";
}
🌐 Defina a interface de rede:
bash
Copiar
Editar
sudo nano /etc/default/isc-dhcp-server
Adicione ou edite:

bash
Copiar
Editar
INTERFACESv4="ens33"
🔄 Reinicie o serviço:
bash
Copiar
Editar
sudo systemctl restart isc-dhcp-server
✅ Verifique o status:
bash
Copiar
Editar
sudo systemctl status isc-dhcp-server
