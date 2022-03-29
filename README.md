Instalação dos softwares no Raspberry pi-ovs01:

Instalando o protocolo de descoberta de rede (LLDP) e monitoração (SNMP):

	apt-get install lldpd snmp

Instalação do Open vSwitch no Raspberry PI usando Ubuntu Server 20.04.2 LTS:

	sudo apt-get install openvswitch-switch

Adicionando a interface bridge ao OpenvSwitch:

	ovs-vsctl add-br ovs-br0

Adicionando a interface cliente ao OpenvSwitch:

	ovs-vsctl add-port ovs-br0 eth0

Adicionando um IP de gerência à bridge no OpenvSwitch

	ifconfig ovs-br0 192.168.100.3/24 up

Adicionando um IP ponto a ponto na interface do circuito MPLS:

	ip add add dev eth2 10.0.1.1/24

Adicionando um IP na interface do circuito de Internet banda larga:

	ip add add dev eth1 192.168.1.200/24

Criando um túnel GRE e adicionando na bridge para alcançar o segundo Raspberry (PI-OVS02) através da Internet:

	ovs-vsctl add-port ovs-br0 gre1 -- set interface gre1 type=gre options:remote_ip=179.125.169.176

Criando um túnel GRE e adicionando na bridge para alcançar o segundo Raspberry (PI-OVS02) através da rede MPLS:

	ovs-vsctl add-port ovs-br0 gre2 -- set interface gre2 type=gre options:remote_ip=10.0.1.2

Ativando o protocolo de redundância Spanning Tree:

	ovs-vsctl set bridge ovs-br0 stp_enable=true

Configurando o controlador SDN:

	ovs-vsctl set-controller ovs-br0 tcp:18.220.36.84:6653

Ativando fluxo de dados do protocolo Openflow

	ovs-vsctl set bridge ovs-br0 protocols=OpenFlow13 

Instalação dos softwares no Raspberry pi-ovs02:

Instalando o protocolo de descoberta de rede (LLDP) e monitoração (SNMP):

	apt-get install lldpd snmp

Instalação do Open vSwitch no Raspberry PI usando Ubuntu Server 20.04.2 LTS:

	sudo apt-get install openvswitch-switch

Adicionando a interface bridge ao OpenvSwitch:

	ovs-vsctl add-br ovs-br0

Adicionando a interface cliente ao OpenvSwitch:

	ovs-vsctl add-port ovs-br0 eth0

Adicionando um IP de gerência à bridge no OpenvSwitch

	ifconfig ovs-br0 192.168.100.4/24 up

Adicionando um IP ponto a ponto na interface do circuito MPLS:

	ip add add dev eth2 10.0.1.2/24

Adicionando um IP na interface do circuito de Internet banda larga:

	ip add add dev eth1 192.168.1.200/24

Criando um túnel GRE e adicionando na bridge para alcançar o segundo Raspberry (PI-OVS01) através da Internet:

	ovs-vsctl add-port ovs-br0 gre1 -- set interface gre1 \ type=gre options:remote_ip=201.77.127.129


Criando um túnel GRE e adicionando na bridge para alcançar o segundo Raspberry (PI-OVS02) através da rede MPLS:

	ovs-vsctl add-port ovs-br0 gre2 -- set interface gre2 \ type=gre options:remote_ip=10.0.1.1

Ativando o protocolo de redundância Spanning Tree:

	ovs-vsctl set bridge ovs-br0 stp_enable=true

Configurando o controlador SDN:

	ovs-vsctl set-controller ovs-br0 tcp:18.220.36.84:6653

Ativando fluxo de dados do protocolo Openflow:

	ovs-vsctl set bridge ovs-br0 protocols=OpenFlow13
 
Instalando o controlador SDN Floodlight

Instalando as dependências:

	sudo apt-get install build-essential openjdk-7-jdk ant maven python-dev eclipse

Instalando o controlador Floodligth:

	git clone git://github.com/floodlight/floodlight.git
	cd floodlight
	git submodule init
	git submodule update
	ant
 
	sudo mkdir /var/lib/floodlight
	sudo chmod 777 /var/lib/floodlight

Atualizando a versão do controlador SDN:

	cd floodlight
	git pull origin master
	git submodule init
	git submodule update

Executando o Controlador SDN:

	java -jar target/floodlight.jar

Listar os dispositivos que o Floodlight reconheceu via API:

	curl http://localhost:8080/wm/device/ | python -m json.tool



