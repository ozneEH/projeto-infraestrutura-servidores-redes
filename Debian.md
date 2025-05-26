│   │   1. Baixe a ISO do Debian no site oficial (https://www.debian.org/distrib/).
│   │   2. Crie um pendrive bootável com Rufus ou balenaEtcher.
│   │   3. Inicie o boot pelo pendrive e escolha "Install" ou "Graphical Install".
│   │   4. Configure:
│   │      - Idioma e localização
│   │      - Nome do host e domínio (ex: debian e exemplo.local)
│   │      - Usuário root e usuário normal
│   │      - Particionamento (usar todo o disco ou manual)
│   │   5. Aguarde a instalação dos pacotes base.
│   │   6. Instale o GRUB no disco principal e finalize.
│   │   7. Após o reboot, configure IP fixo e atualize o sistema:
│   │      bash
│   │      sudo nano /etc/network/interfaces
│   │      sudo apt update && sudo apt upgrade -y

│
│   ├── dns/
│   │   └── configuracao.md
│   │      Configuração do Servidor DNS (BIND9):
│   │      1. Instale o BIND:
│   │         bash
│   │         sudo apt install bind9 bind9utils bind9-doc -y
│   │      2. Edite o arquivo de configuração:
│   │         bash
│   │         sudo nano /etc/bind/named.conf.local
│   │         Adicione:
│   │         │   │         zone "exemplo.local" {
│   │             type master;
│   │             file "/etc/bind/db.exemplo.local";
│   │         };
│   │      3. Crie o arquivo de zona baseado no modelo:
│   │         bash
│   │         sudo cp /etc/bind/db.local /etc/bind/db.exemplo.local
│   │         sudo nano /etc/bind/db.exemplo.local
│   │      4. Reinicie o serviço:
│   │         bash
│   │         sudo systemctl restart bind9
│   │      5. Teste com:
│   │         bash
│   │         dig @localhost exemplo.local

│
│   └── dhcp/
│       └── configuracao.md
│          Configuração do Servidor DHCP (isc-dhcp-server):
│          1. Instale o pacote:
│          bash
│          sudo apt install isc-dhcp-server -y
│          
│          2. Configure o arquivo principal:
│          bash
│          sudo nano /etc/dhcp/dhcpd.conf
│          
│          Exemplo de configuração:
│          │          subnet 192.168.1.0 netmask 255.255.255.0 {
│              range 192.168.1.100 192.168.1.200;
│              option routers 192.168.1.1;
│              option domain-name-servers 192.168.1.10;
│              option domain-name "exemplo.local";
│          }
│         
│          3. Defina a interface de rede em /etc/default/isc-dhcp-server:
│          │          INTERFACESv4="ens33"
│         
│          4. Reinicie o serviço:
│          bash
│          sudo systemctl restart isc-dhcp-server
│          
│          5. Verifique o status:
│          bash
│          sudo systemctl status isc-dhcp-server
