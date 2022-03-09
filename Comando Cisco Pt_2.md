# COMANDOS NAT
**Ativar NAT nas interfaces Internas e Externas**
```
>enable
#configure terminal
(config)#interface g0/0
(config-if)#ip nat inside
exit
(config)#interface g0/1
(config-if)#ip nat outside
exit
```
**Regra de NAT Estatico por IP**
```
>enable
#configure terminal
(config)#ip nat inside source static 0.0.0.0 0.0.0.0
```
**Regra de NAT Estatico por Porta**
```
>enable
#configure terminal
(config)#ip nat inside source static tcp 0.0.0.0 "0" 0.0.0.0 "0"
```
**Verificar IPs**
```
>enable
#show ip interface brief
```
**Verificar Outside e Inside**
```
>enable
#show run
```
**Verificar Rotas**
```
>enable
#show ip route
```
**Verificar Rotas**
```
>enable
#show ip nat statistics
```
**Após a inserção do NAT**
```
>enable
#show ip nat translations
```
# COMANDOS ACL
**Atrelar ACL a Interface**
```
>enable
#configure terminal
(config)# interface serial 0/0/0
(config-if)# ip access-group 11 out
```
**Remover ACL da interface**
```
>enable
#configure terminal
(config)# interface serial 0/0/0
(config-if)# no ip access-group 11 out
```
**Criar ACL Padrão Numerica (Filtragem de Protocolos TCP e UDP)**
```
>enable
#configure terminal
(config)# access-list 99 permit tcp 0.0.0.0 0.0.0.0 range 1024 65535 host 0.0.0.0 eq www
```
**Criar ACL Extendida Numerica (Filtragem de Protocolos TCP e UDP)**
```
>enable
#configure terminal
(config)# access-list 101 permit tcp 0.0.0.0 0.0.0.0 range 1024 65535 host 0.0.0.0 eq www
```
**Criar ACL Padrão Nomeada**
```
>enable
#configure terminal
(config)# ip access-list standard GrêmioSérieB
(config-std-nacl)# 10 permit tcp 0.0.0.0 0.0.0.0 host 0.0.0.0 eq 80
(config-std-nacl)# 20 deny tcp any any

```
**Criar ACL Extendida Nomeada**
```
>enable
#configure terminal
(config)# ip access-list extended MesaGabigol_APP
(config-std-nacl)# 10 permit ip 0.0.0.0 0.0.0.0 host 0.0.0.0
(config-std-nacl)# 20 permit icmp 0.0.0.0 0.0.0.0 host 0.0.0.0
(config-std-nacl)# 30 deny ip any any
```
**Proteção Login com ACL**
```
>enable
#config terminal
(config)#line vty 0 4
(config-line)#login local
(config-line)#transport input ssh
(config-line)#access-class 21 in
exit
(config)#access-list 21 permit 0.0.0.0 0.0.0.0
(config)#access-list 21 deny any
```
**Criar ACL numerada e criar um Comentario**
```
>enable
#configure terminal
(config)#access-list 1 remark Rede_LAN_S1
(config)#access-list 1 permit 0.0.0.0 0.0.0.0
(config)#access-list 1 deny any
(config)#do show access-list
```
**Verificar em qual porta esta aplicada a ACL**
```
>enable
#show running-config
```
**Verificar as ACLs**
```
>enable
#show access-lists 
```
>OBS:Para que os códigos funcionem não é necessário que os nomes sejam **GrêmioSérieB** ou **MesaGabigol_APP**!
Esses foram nomes aleatórios escolhidos por puro cunho _Futebolístico_. 

# COMANDOS PAT
**Configurar ACL para permitir endereços a serem convertidos**
```
>enable
#configure terminal
(config)#ip access-list (Nome da Access List) permit (Rede de Origem) (Wildcard de Origem) 
```
**Defina o Pool**
```
>enable
#configure terminal
(config)#ip nat pool (Nome-IPs-WAN-PAT) 0.0.0.0 0.0.0.0 netmask 0.0.0.0
```
**Criação do PAT (Vínculo da ACL ao Pool)**
```
>enable
#configure terminal
(config)#ip nat inside source list (nome-access-list) pool (nome-IP-WAN interface) Serial 0/0/0 overload
```
**Verificação do PAT**
```
>enable
#show ip nat translations 
```
**Limpar conversões/sessões atuais**
```
>enable
#clear ip nat translation 
```
**Verificação do Pool**
```
>enable
#show ip nat statistics
```
**Limpar Estatisticas**
```
>enable
#clear ip nat statistics
```


# COMANDOS HSRP
**Definir Grupo HSRP**
```
>enable
#configure terminal
(config)#vlan "0"
(config)#interface vlan "0"
(config-if)#ip address "0.0.0.0" "0.0.0.0"
```
>OBS:Somente após a definição da VLAN e a configuração do IP deverá ser feita a **Definição de grupo HSRP**
```
(config-if)#standby "0" ip [Gateway da rede de acesso] 
(config-if)#standby 10 preempt
(config-if)#standby 10 priority 120
```
>OBS:Por padrão a prioridade é 100

**Obter informações detalhadas**
```
>enable
#show standby vlan "0"
```
**Caso os Uplinks falhem, aplicamos _Interface Track_**
```
>enable
#configure terminal
(config)#interface vlan "0"
(config-if)#standby "0" track 1 decrement 30
(config)#track 1 interface gigabitEthernet 0/0 line-protocol
(config-track)#end
```
**Verificar a configuração**
```
>enable
#show track 1
```
# COMANDOS DHCP
**Excluir Endereço IPv4**
```
>enable
#configure terminal
(config)#ip dhcp excluded-address [low-address] [high-address]
```
**Definir um nome de pool DHCP**
```
>enable
#configure terminal
(config)#ip dhcp pool [pool-name]
```
**Definir o pool de endereços**
```
>enable
#configure terminal
(config)#ip dhcp pool [pool-name]
(dhcp-config)# network 0.0.0.0 0.0.0.0
```
**Definir o roteador ou gateway padrão**
```
>enable
#configure terminal
(config)#ip dhcp pool [pool-name]
(dhcp-config)#default-router 0.0.0.0
```
**Definir um servidor DNS**
```
>enable
#configure terminal
(config)#ip dhcp pool [pool-name]
(dhcp-config)#dns-server 0.0.0.0
```
**Definir um servidor DNS**
```
>enable
#configure terminal
(config)#ip dhcp pool [pool-name]
(dhcp-config)#domain-name AthleticoPaidoMengo.com
```
**Configuração com os comandos acima**
```
>enable
#configure terminal
(config)#ip dhcp excluded-address 0.0.0.0 0.0.0.0
(config)#ip dhcp excluded-address 0.0.0.0
(config)#ip dhcp pool [pool-name]
(dhcp-config)#network 0.0.0.0 0.0.0.0
(dhcp-config)#default-router 0.0.0.0
(dhcp-config)#dns-server 0.0.0.0
(dhcp-config)#domain-name AthleticoPaidoMengo.com
(dhcp-config)#end
```
**Exibir os comandos DHCP configurados**
```
>enable
#show running-config | section dhcp
```
**Exibir lista de endereços IPv4 para ligações de MAC fornecidas pelo serviço DHCP**
```
>enable
#show ip dhcp binding
```
**Exibir informações de contagem com relção às mensagens DHCP**
```
>enable
#show ip dhcp server statistics
```
**Verificar no Windows**
```
>ipconfig /all
```

>OBS:Para que os códigos funcionem não é necessário que 
>o nome seja **AthleticoPaidoMengo**!
>Esse foi um nome aleatório escolhidos por puro cunho _Futebolístico_. 

~~~javascript
CALMA,CALMA. ESTAMOS QUASE ACABANDO!
CHEGAMOS EM NOSSA RETA FINAL
VEM AÍ...
~~~

<img src="http://manaus.radiomixfm.com.br/wp-content/uploads/2019/10/coringa-3.jpg" width="230">

~~~javascript
PARTE 3
~~~
