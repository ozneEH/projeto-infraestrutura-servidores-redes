Guia de Instalação e Configuração Debian
1. Instalação do Debian
Baixe a ISO do Debian no site oficial:
https://www.debian.org/distrib/

Crie um pendrive bootável usando Rufus ou balenaEtcher.

Inicie o boot pelo pendrive e escolha a opção:

Install ou

Graphical Install

Configure o sistema:

Idioma e localização

Nome do host e domínio (exemplo: debian e exemplo.local)

Usuário root e usuário normal

Particionamento (usar todo o disco ou manual)

Aguarde a instalação dos pacotes base.

Instale o GRUB no disco principal e finalize a instalação.

Após o reboot, configure IP fixo e atualize o sistema:

bash
Copiar
Editar
sudo nano /etc/network/interfaces

sudo apt update && sudo apt upgrade -y
2. Configuração do Servidor DNS (BIND9)
Arquivo: dns/configuracao.md

Instale o BIND9:

bash
Copiar
Editar
sudo apt install bind9 bind9utils bind9-doc -y
Edite o arquivo de configuração local:

bash
Copiar
Editar
sudo nano /etc/bind/named.conf.local
Adicione o seguinte bloco:

conf
Copiar
Editar
zone "exemplo.local" {
  type master;
  file "/etc/bind/db.exemplo.local";
};
Crie o arquivo de zona baseado no modelo padrão:

bash
Copiar
Editar
sudo cp /etc/bind/db.local /etc/bind/db.exemplo.local
sudo nano /etc/bind/db.exemplo.local
Reinicie o serviço BIND9:

bash
Copiar
Editar
sudo systemctl restart bind9
Teste a configuração com:

bash
Copiar
Editar
dig @localhost exemplo.local
3. Configuração do Servidor DHCP (isc-dhcp-server)
Arquivo: dhcp/configuracao.md

Instale o servidor DHCP:

bash
Copiar
Editar
sudo apt install isc-dhcp-server -y
Configure o arquivo principal:

bash
Copiar
Editar
sudo nano /etc/dhcp/dhcpd.conf
Exemplo de configuração:

conf
Copiar
Editar
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option domain-name-servers 192.168.1.10;
  option domain-name "exemplo.local";
}
Defina a interface de rede para o DHCP no arquivo /etc/default/isc-dhcp-server:

bash
Copiar
Editar
INTERFACESv4="ens33"
Reinicie o serviço DHCP:

bash
Copiar
Editar
sudo systemctl restart isc-dhcp-server
Verifique o status do serviço:

bash
Copiar
Editar
sudo systemctl status isc-dhcp-server
