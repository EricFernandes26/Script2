# COMANDOS RIPv2
**Ativar Protocolo RIPv2**
```
>enable
#configure terminal
(config)#router rip
(config-router)#version 2
```
**Desativar e eliminar o RIP**
```
>enable
#configure terminal
(config)#no router rip
```
**Anunciar redes no RIP**
```
>enable
#configure terminal
(config)#router rip
(config-router)#version 2
R2(config-router)#no auto-summary
R2(config-router)#network 0.0.0.0
R2(config-router)#network 0.0.0.0
```
**Exibir configurações do protocolo IPv4**
```
>enable
#show ip protocols
```
**Exibir rotas do RIP**
```
>enable
#show ip route
```
**Especificar interface sem Roteador**
```
>enable
#configure terminal
(config)#router rip
(config-router)#version 2
(config-router)#passive-interface g0/0
```

# COMANDOS OSPF

* **_Configuração De Single Area_**

**Criar OSPF com ID de processo 10**
```
>enable
#configure terminal
(config)#router ospf 10
```
**Especificar ID do Roteador**
```
>enable
#configure terminal
(config)#router ospf 10
(config-router)#router-id 0.0.0.0
end
#show ip protocols
```
**Especificar Redes que o Roteador participa**
```
>enable
#configure terminal
(config)#router ospf 10
(config-router)#network 0.0.0.0 0.0.0.0 area 0
(config-router)#network 0.0.0.0 0.0.0.0 area 0
(config-router)#network 0.0.0.0 0.0.0.0 area 0
```
**Especificar interface sem Roteador**
```
>enable
#configure terminal
(config)#router ospf 10
(config-router)#passive-interface g0/0
end
```
**Realizar Limpeza**
```
>enable
#clear ip ospf process
```

* **_Verificar Custos_**

**Verificar banco de dados do OSPF**
```
>enable
#show ip ospf database
```
**Verificar Interfaces do OSPF**
```
>enable
#show ip ospf interface
```
**Verificar vizinhos OSPF**
```
>enable
#show ip ospf neighbor
```
* **_Configuração De Multiple Area_**

**Criar OSPF com ID de processo 10**
```
>enable
#configure terminal
(config)#router ospf 10
```
**Especificar Redes do Router**
```
>enable
#configure terminal
(config)#router ospf 10
(config-router)#router-id 0.0.0.0
(config-router)#network 0.0.0.0 0.0.0.0 area 1
(config-router)#network 0.0.0.0 0.0.0.0 area 1
(config-router)#network 0.0.0.0 0.0.0.0 area 0
end
```
**Especificar interface sem Roteador**
```
>enable
#configure terminal
(config)#router ospf 10
(config-router)#passive-interface g0/0
end
```
**Ver redes e áreas cadastradas**
```
>enable
#show ip protocols
```

# COMANDOS STP
**Ver interfaces conectadas do Spanning-Tree**
```
>enable
#show spanning-tree detail
```
**Ver MAC das interfaces conectadas e ativas**
```
>enable
#show mac-address-table
```
**Ver MAC das interfaces conectadas e não ativas**
```
>enable
#show interfaces|in line protocol|address
```
**Mudar o Switch (Root Bridge)**
```
>enable
#configure terminal
(config)#spanning-tree vlan 1 priority 28672
```
**Verificar Spanning-tree por VLAN (Identificação se o switch é root bridge)
```
>enable
##show spanning-tree vlan 10
```
**Habilitar Spanning-Tree**
```
>enable
#configure terminal
(config)#spanning-tree vlan 1
```
**Desabilitar Spanning-Tree**
```
>enable
#configure terminal
(config)#no spanning-tree vlan 1
```
# COMANDOS RSTP
**Habilitar Rapid Spanning-Tree**
```
>enable
#configure terminal 
(config)#spanning-tree mode rapid-pvst
```
**Ativação do STP nas Portas**
```
>enable
#configure terminal 
(config)#interface f0/0
(config-if)#spanning-tree portfast
```
**Desativação do STP nas Portas**
```
>enable
#configure terminal
(config)#interface f0/0
(config-if)#no spanning-tree portfast
```
**Ativação do BPDU Guard (Apenas em Portfast)**
```
>enable
#configure terminal
(config)#interface f0/0
(config-if)# spanning-tree bpduguard enable
```
**Desativação do BPDU Guard**
```
>enable
#configure terminal
(config)#interface f0/0
(config-if)#spanning-tree portfast bpdu-guard disable
```
**Ativar BPDU Filtering**
```
>enable
#configure terminal
(config)#interface f0/0
(config-if)#spanning-tree portfast bpdu-filter enable
```
**Desativar BPDU Filtering**
```
>enable
#configure terminal
(config)#interface f0/0
(config-if)#spanning-tree portfast bpdu-filter disable
```
# COMANDOS VTP
**Configurar VTP Server**
```
>enable
#configure terminal
(config)#vtp mode server
(config)#vtp domain SENAI 
(config)#vtp password 123456
```
**Configurar VTP Cliente**
```
>enable
#configure terminal
(config)vtp mode client
(config)vtp domain SENAI 
(config)vtp password 123456
```
**Verificar o VTP (Server - Cliente - Transparete)** 
```
>enable
#show vtp status
```
**Verificar a Senha VTP/Domínio**
```
>enable
#show vtp password
```
**Verificar o DTP (por padrão vem auto)**
```
>enable
#show interfaces switchport 
#show int trunk (Coluna Mode)
```
**Verificar o DTP (Filtro em porta Giga)**
```
>enable
#show interfaces switchport | begin Name: Gig 
```
# COMANDOS ETHERCHANNEL
**Visualizar Portas**
```
>enable
#show ip int brief
```
**Visualizar Canal Etherchannel**
```
>enable
#show etherchannel summary
```
**Visualizar Canal Etherchannel por Porta**
```
>enable
#show etherchannel 
```
**Mostrar o port channel como um link lógico**
```
>enable
#show interfaces trunk 
#show spanning-tree 
```
**Configurar Link Aggreggation LACP**
```
>enable
#configure terminal
(config)# interface range gigabitEthernet 1/1-2
(config-if)# channel-protocol lacp
(config-if)# channel-group 1 mode active
ou
(config-if)# channel-group 1 mode passive
```
**Configurar Link Aggreggation PAgP**
```
>enable
#configure terminal
(config)# interface range gigabitEthernet 1/1-2
(config-if)# channel-protocol pagp
(config-if)# channel-group 1 mode auto
ou
(config-if)# channel-group 1 mode desirable
```
**Status das Portas**
```
>enable
#show port-channel summary

Sinalizadores: 
D - Down (desligado)
P - port-channel está Up (ligado) (membros estão funcionais)
I - Individual 
H - Hot-standby (Link em espera) (somente LACP)
s - recurso suspenso - módulo removido
S - Comutado 
R - Roteado
U – Up (ligado) (canal lógico)
```

~~~javascript
MUITA COISA NÉ? EU SEI.
ACREDITE OU NÃO, TEM MAIS!
VEM AÍ...
~~~

<img src="https://i.pinimg.com/736x/f1/52/be/f152be47daabeb20d86941097cc5956b.jpg" alt="drawing" width="200"/>

~~~javascript
PARTE 2
~~~













