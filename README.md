# Cisco-
Tutoriais relacionado a Cisco
Configuração de switches e roteadores:
força o cisco a dar boot pelo pen drive para iniciar
S1(config)# boot system flash: /c2960-lanbasek9-mz. 150-2.SE/c2960-lanbasek9-mz. 150-2.SE.bins
Switches possuem até 14 vty ( terminal virtual para acesso remoto, gerenciamento) roteadores possuem 4.
O comando show deve ser usado no modo privilegiado # ou coloque o do na frente 

Comando para o cisco habilitar pilha dupla ipv6/ipv4 sdm prefer dual-ipv4-and-ipv6 default 
Depois reload 
Para navegar na rede é necessário um IPv6 global unicast 



Router(config)#interface VLAN 1 Entra na configuração da Auxiliar.
Router(config-if)#ip address <end_ip>
<máscara>
Insere um IP de Gerenciamento e uma
Máscara na Interface. Para switch o IP é uma interface virtual, VLAN para gerenciamento…
Alguns switches será necessário habilitar a Pilha dupla para ambos ipv6/ipv4

Router(config-if)#description <entre com a
descrição>
Insere uma descrição para a Interface.

Router(config-if)#no shutdown Ativa a Interface.
Configuração do Gateway

Router(config)#ip default-gateway IP-do-GW
Entre com o endereço do gateway
padrão.
Configuração do DNS

Router(config)#ip name-server IP-do-DNS
Entre com o endereço do DNS utilizado

Quando se cria subinterfaces svi, essas interfaces só ficaram ativas quando a interface física receber o no shut
Configuração de interface:

Switch(config)#interface Giga 0/1
Entra na configuração da Interface
Fastethernet.

Switch(config-if)#duplex [auto full half]
Define o modo duplex na Interface
para automático, full-duplex ou halfduplex.

Switch(config-if)#speed [auto 1000 100
10]
Define a velocidade da interface para
automático, 1Gbps, 100Mbps ou
10Mbps. Se a interface for Fastethernet
aparecerão apenas as opções auto, 10
e 100.

Switch(config-if)#description <descrição> Insere uma descrição para a Interface.

Switch(config-if)#shutdown Desabilita a Interface.

Criando VLANs
Passo a Passo Geral de Criação de Vlans
1. Configurar o VTP (Vlan trunk protocol);
2. Criar as VLANs;
3. Fazer o VLAN membership (atribuir portas do switch em uma determinada VLAN);
4. Criar os trunks entre os switches ou entre switches e roteadores;
5. Fazer o roteamento entre VLANs nos equipamentos de camada-3.
Comandos Descrição

Configurando VTP Trunk
SW(config)#vtp mode <modo>
Configura o switch como “Server”,
“Cliente” ou “Transparent”. Somente
Server e Transparent criam VLANs.

Para apagar uma vlan no vlan, para apagar o arquivo inteiro delete flash:vlan.dat para apagar as vlans estendidas, erase startup-config depois delete vlan.dat


SW(config)#vtp domain <nome> Configura o domínio do VTP.
Criando VLANs

SW(config)#vlan <id>

SW(config-vlan)#name <nome>
Cria a VLAN com o id e nome
especificado.
ouSW#vlan database

SW(vlan)#vlan <id> name
<nome>
Cria a VLAN com o id e nome
especificado. Esse método não é
recomendado.

VLAN Membership (atribuir interfaces a vlans)

Comandos Descrição
Associando VLANs-Portas

SW(config)#interface <interface>
Entra no modo de configuração
da interface desejada.

SW(config-if)#switchport mode access Define a porta como acesso.

SW(config-if)#switchport access vlan <id>
Associa a interface à VLAN <id>
criada na página anterior

Configurando Trunks

Comandos Descrição
Criando Trunks

SW(config)#interface <interface>
Entra no modo de
configuração da interface
desejada.

SW(config-if)#switchport trunk encapsulation
[dot1q | ISL]
Define o encapsulamento do
trunk como 802.1Q ou ISL.

SW(config-if)#switchport mode trunk
Configura a interface como
trunk.
Limitando VLANs nos Trunks

SW(config)#interface <interface>
Entra no modo de
configuração da interface
desejada.

SW(config-if)# switchport trunk allowed vlan
<id1, id2,...>
Permite o encaminhamento
apenas das Vlans
selecionadas.

Mesmo com sub redes ips, os host irão se comunicar no mesmo broadcast, somente vlans separam as redes…

Tipos de Portas em MLS
•Em switches multicamada ou MLSs (Multilayer Switches) as portas podem ser camada-2
ou roteadas (podem receber IP como portas de roteadores).
•Por padrão as portas são L2 e para converter em uma porta roteada utilize o comando
“no switchport”.

Comandos Descrição

SW(config)#interface Fast 0/1
Entra na configuração da Interface
Fastethernet.

SW(config-if)#no switchport Converte a interface de L2 para L3.

SW(config-if)#ip address <end_ip>
<máscara>
Insere um IP e uma Máscara na
Interface.

SW(config-if)#description <entre com
a descrição>
Insere uma descrição para a Interface.

Configurando SVIs
•Em switches multicamada utilizamos interfaces virtuais ou SVIs (Switched Virtual
Interfaces) para roteamento entre VLANs .
•As SVIs servem como gateway para os hosts configurados em cada VLAN.
•Para roteamento entre VLANs basta criar uma SVI por VLAN criada e definir seu
endereço IP que será utilizado como gateway padrão nos hosts daquela rede específica.

Comandos Descrição
Configurando uma Interface
Fastethernet

Router(config)#interface vlan 10 Cria a SVI para a VLAN 10.

Router(config-if)#ip address
<end_ip> <máscara>
Insere um IP e uma Máscara da
VLAN 10.

Router(config-if)#description
<entre com a descrição>
Insere uma descrição para a
Interface.

Router(config-if)#no shutdown Ativa a SVI.


CISCO Na prática

renomear host
en
conf t
hostname xxxxx
no ip domain-lookup   #para não resolver nome

show ip interface brief
show ip address
int f0/1
sh interface fast0/1
show running-config
wr
show vlan
show mac address-table
copy running-config starup-config

ip route xxxx xxxx(rede interna e máscara) xxxx gateway wan
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#ip route 192.168.0.0 255.255.255.0 192.168.100.1
Router(config)#
show ip route
ip address ?
ip address dhcp
ip address xxxx xxxx secondary
ip add xxxx xxxx
int f0/0
int vlan 1
no ip address
no ip add xxxx xxxx secondary
sh vlan brief

sh running-config | section line vty ( mostra seções ativas na linha vty)
sh running-config | section line con ( mostra linha do console)
sh ip int br | exclude up ( mostrar as interfaces up)
sh ip int br | include down (mostrar as interfaces down)
sh ip int br | exclude unassigned ( exclui as interfaces sem IP)
sh ip route | begin Gateway (informa as rotas começando com Gateway)
sh running-config | begin line (começando com line)
terminal history size 200
show history ( mostra o histórico com os últimos 200 comandos)

Insere um IP de Gerenciamento e uma
Máscara na Interface.

Switch>
Switch>enable
Switch#config term
Switch(config)#hostname DlteC
DlteC(config)#enable secret dltec123
DlteC(config)#line console 0
DlteC(config-line)#password dltec
DlteC(config-line)#login
DlteC(config-line)#line vty 0 15
DlteC(config-line)#password dltec
DlteC(config-line)#login

adicionar ip
MatrizCTBA#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
MatrizCTBA(config)#interface serial 0
MatrizCTBA(config-if)#ip address 200.171.51.1 255.255.255.252
MatrizCTBA(config-if)#bandwidth 128
MatrizCTBA(config-if)#clock rate 128000
MatrizCTBA(config-if)#description Serial 0 conectada a FilialPGO
MatrizCTBA(config-if)#encapsulation hdlc
MatrizCTBA(config-if)#no shutdown
MatrizCTBA#

R1>enable
R1#config term
R1(config)#interface serial 0/0/0
R1(config-if)#ip address 192.168.1.1 255.255.255.0
R1(config-if)#bandwidth 1000
R1(config-if)#description WAN conectada ao R2
R1(config-if)#no shut

R1(config-if)#interface fast 0/0
R1(config-if)#ip address 192.168.0.1 255.255.255.0
R1(config-if)#description LAN-1
R1(config-if)#no shut
R1(config-if)#end
R1#copy run start


Adicionar ip no Switch L3

DlteC(config)#interface VLAN1
DlteC(config-if)#ip address 192.168.1.2 255.255.255.0
DlteC(config-if)#no shutdown
DlteC(config-if)#exit
DlteC(config)#ip default-gateway 192.168.1.1
DlteC(config)#ip name-server 8.8.8.8

Criar vlan
en
conf t
vlan 5
name xxxxxxxxx
end

Atribuir interfaces a Vlan
en
conf t
int fast 0/3
(para mais de uma interface use.   int range fas 0/1-4) 
switchport mode access
switchport access vlan 5
end

configurações de segurança cisco
Router(config)# access-list 100 deny ip any 192.168.30.0 0.0.0.255
Router(config)# access-list 100 permit ip any any

Roteador> enable
Roteador # configure terminal
Roteador (config) # policy-map policy1
Roteador (config-pmap) # class voice-percent
Roteador (config-pmap-c) # priority percent 30
Roteador (config-pmap-c) # exit
Roteador (config-pmap) # class video
Roteador (config-pmap-c) # bandwidth remaining percent 50
Router (config-pmap-c) # exit
Router (config-pmap) # class dados
Router (config-pmap-c) # bandwidth remaining percent 20
Router (config-pmap-c) #end

configuração básica do dispositivo
Router>en
Router#conf t

Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname CF
CF(config)#enable secret tintas1234
CF(config)#line console 0
CF(config-line)#password tintas
CF(config-line)#login
CF(config-line)#line vty 0 15
CF(config-line)#password tintas
CF(config-line)#login	
CF(config-line)#end
CF#
%SYS-5-CONFIG_I: Configured from console by console

CF#copy running-config startup-config
Destination filename [startup-config]? 
Building configuration...
[OK]


configuração wan
enter
en
Password: 
CF#en
CF#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
CF(config)#
CF(config)#int s2/0
CF(config-if)#description conexao Galpao
CF(config-if)# ip address 10.0.0.1 255.255.255.252
CF(config-if)#no shut

%LINK-5-CHANGED: Interface Serial2/0, changed state to down
CF(config-if)#

Configurar lan

CF#en
CF#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
CF(config)# int f0/0
CF(config-if)#ip address 192.168.0.1 255.255.255.0
CF(config-if)#no shut

dhcp
CF#en
CF#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
CF(config)#in f0/0
CF(config-if)#ip dhcp excluded-address 192.168.0.1
CF(config)#
CF(config)#ip dhcp pool GRUPO_1
CF(dhcp-config)#network 192.168.0.0 255.255.255.0
CF(dhcp-config)#default-router 192.168.0.1
CF(dhcp-config)#
CF(dhcp-config)#end
CF#
%SYS-5-CONFIG_I: Configured from console by console

CF#
CF#copy running-config startup-config
Destination filename [startup-config]? 
Building configuration...
[OK]

R1> enable
R1# configure terminal
Enter configuration commands, one per line.
End with CNTL/Z.
R1(config)# interface gigabitEthernet 0/0/0
R1(config-if)# description Link to LAN
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# ipv6 address 2001:db8:acad:10::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
*Aug 1 01:43:53.435: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to down
*Aug 1 01:43:56.447: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to up
*Aug 1 01:43:57.447: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0,
changed state to up

Roteamento de router-on-a-stick entre VLANs
Configuração de subinterface em roteador
O método roteador no stick exige que você crie uma subinterface para cada VLAN a ser roteada. Embora não seja necessário, é costume combinar o número 
da subinterface com o número da VLAN. Cada subinterface do roteador deve receber um endereço IP em uma sub-rede exclusiva para que o roteamento 
ocorra.
R1(config)# interface G0/0/1.10
R1(config-subif)# description Default Gateway for VLAN 10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip add 192.168.10.1 255.255.255.0
R1(config-subif)# exit
R1(config)# interface G0/0/1.20
R1(config-subif)# description Default Gateway for VLAN 20
R1(config-subif)# encapsulation dot1Q 20
R1(config-subif)# ip add 192.168.20.1 255.255.255.0
R1(config-subif)# exit
R1(config)# interface G0/0/1.99
R1(config-subif)# description Default Gateway for VLAN 99
R1(config-subif)# encapsulation dot1Q 99
R1(config-subif)# ip add 192.168.99.1 255.255.255.0
R1(config-subif)# exit
R1(config)# interface G0/0/1
R1(config-if)# description Trunk link to S1
R1(config-if)# no shut
R1(config-if)# end


Ether channel junta, agrega vários links  físicos em um link lógico. Também serve para  sanar os links são que bloqueados pelo spanning tree, são usados junto com configurações de redundância e loading balanced..

Dynamic Trunking Protocol ( DTP)
switchport mode trunk
switchport nonegotiate
switchport mode { access | dynamic { auto | desirable } | trunk }.
show interfaces trunk



DHCP 
ip dhcp excluded-address 192.168.10.1 192.168.10.9 (o último e primeiro endereço da rede)
ip dhcp excluded-address 192.168.10.254 
ip dhcp pool  LAN-POOL-

Para definir a pool
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.11.5
domain-name exemplo.com
end
show running-config | section dhcp
show ip dhcp binding
show ip dhcp server statistics

O serviço DHCPv4 é habilitado, por padrão. Para desabilitar o serviço, use o comando no service dhcp no modo de configuração global.
Se quiser reativar o processo Server DHCPv4, use o comando service dhcp. 

DHCPV4 Relay
int g0/0/0
ip helper-address xxxxxx (servidor dhcp)
end
Para configurar uma interface Ethernet como um cliente DHCP, use o comando ip address dhcp

int G0/0/1
ip address dhcp
no shutdown

Ativando o SLAAC

show ipv6 interface (saber as configurações)
ipv6 unicast-routing ( ativa o roteamento IPV6)
Um roteador Cisco habilitado para IPv6 envia mensagens RA para o endereço multicast ff02::1 a cada 200 segundos.

ipv6 nd other-config-flag (habilita o DHCP sem estado)
no ipv6 other-config-flag (desabilita)
show ipv6 int g0/0/1 | begin ND (mostra configurações)

Ativar DHCPv6

int g0/0/1
ipv6 nd managed-config-flag
ipv6 nd prefix default no-autoconfig
end

São cinco as etapas para configurar e verificar um roteador como um servidor DHCPv6 stateless:
1. Ative o roteamento IPv6 com o comando global ipv6 unicast-routing para que o roteador origine mensagens de RA ICMPv6.
2. Defina um nome de pool DHCPv6 com o comando global ipv6 dhcp pool POOL-NAME.
3. Configure o pool DHCPv6 para fornecer informações DHCP adicionais, incluindo endereço do servidor DNS e nome de domínio.
dns-server 2001:db8:acad:1::254
domain-name example.com
4. Vincular o pool DHCPv6 a uma interface com o comando de configuração de interface ipv6 dhcp server POOL-NAME. Altere a flag O para O=1 com o comando ipv6 nd other-config-flag. As mensagens de RA enviadas nesta interface indicam que informações adicionais estão disponíveis de um servidor DHCPv6 stateless. A flag A é 1 por padrão, dizendo aos clientes para usar o SLAAC para criar seu próprio GUA.

interface Gigabitethernet0/0/1
description link to LAN
ipv6 address fe80::1 link-local
ipv6 address 2001:db8:acad:1::1/64
ipv6 nd other-config-flag
ipv6 dhcp server IPV6-STATELESS
no shut
Verifique se os hosts Windows receberam informações de endereçamento IPv6 com o comando ipconfig /all.

Configurar um cliente DHCPv6 stateless

