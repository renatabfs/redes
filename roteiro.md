# [Ficha Técnica](https://github.com/renatabfs/redes/blob/main/Ficha%20T%C3%A9cnica.md) 

# PLANEJAMENTO
```
Tabela 1: Planilha de IP's
-------------------------------------------------------------------------------------------------------------------------------------------
|  DESCRICAO                    |          IP            |     hostname             |          FQDN                     |      aliase      |
-------------------------------------------------------------------------------------------------------------------------------------------|
| PC1-GRUPO7-VMLab01-Emylle     | 192.168.14.97/28       |    emylle1-grupo7        | emylle1.grupo7-914.ifalara.net    |       emy1       |
| PC1-GRUPO7-VM2Lab01-Emylle    | 192.168.14.98/28       |    emylle2-grupo7        | emylle2.grupo7-914.ifalara.net    |       emy2       |
| PC2-GRUPO7-VMLab01-Renata     | 192.168.14.99/28       |    renata1-grupo7        | renata1.grupo7-914.ifalara.net    |       ren1       |
| PC2-GRUPO7-VMLab02-Renata     | 192.168.14.100/28      |    renata2-grupo7        | renata2.grupo7-914.ifalara.net    |       ren2       |
| PC3-GRUPO7-VMLab01-Jefferson  | 192.168.14.101/28      |    jefferson1-grupo7     | jefferson1.grupo7-914.ifalara.net |       jef1       |
| PC3-GRUPO7-VMLab02-Jefferson  | 192.168.14.102/28      |    jefferson2-grupo7     | jefferson2.grupo7-914.ifalara.net |       jef2       |
| PC4-GRUPO7-VM1-equipe7-914    | 192.168.14.103/28      |    vm1-pc4-grupo7        | vm1-pc4.grupo7-914.ifalara.net    |       vm1        |
| PC4-GRUPO7-VM1-equipe7-914    | 192.168.14.104/28      |    vm2-pc4-grupo7        | vm2-pc4.grupo7-914.ifalara.net    |       vm2        |
--------------------------------------------------------------------------------------------------------------------------------------------
```
# EXECUÇÃO
# 1 PASSO
## Importar as ISOS
 - Importar as isos e configurar com o nome dos integrantes do grupo.
 - A iso pode ser baixada pelo Nautilus.
### Figura 1: Importação da ISO - PC1-Emylle
<img src = "imagesEmylle/importandoiso.png" />
<img src = "imagesEmylle/Criando a iso.png" />

# 2 PASSO
## Configurar os IP's no netplan
- Abrir as VMs e fazer login no ```administrador```
- Senha: ```adminifal```

### Para acessar o netplan:
- Executar o comando.

```
sudo nano /etc/netplan/01-netcfg.yaml
```

- Se não possuir o arquivo verificar o nome dele com ``` ls -la /etc/netplan ```
- Retirar o renderer.
- Adicionar o gateway4 e o addresses com os IP's da equipe.
- Adicionar dhcp4: false

### Figura 2: Arquivo netplan - PC1 - Emylle
<img src = "imagesEmylle/Netplan.png" />

### Figura 3: Arquivo netplan - PC2 - Renata

<img src = "imagesRenata/Netplan.png" />

### Figura 4: Arquivo netplan - PC3 - Jefferson

<img src = "imagesJefferson/Netplan.png" />

### Figura 5: Arquivo netplan - PC4

<img src = "imagesPC4/Netpan.png" />

- Por fim, executar ``` sudo netplan apply ```
- Verificar no ``` ifconfig -a ``` se alterações foram aplicadas.
 
 ### Figura 6: Ifconfig - PC1 - Emylle
<img src = "imagesEmylle/ifconfigVMemylle.png " />

### Figura 7: Ifconfig - PC2 - Renata
<img src = "imagesRenata/Ifconfig.png" />

### Figura 8: Ifconfig - PC3 - Jefferson
<img src = "imagesJefferson/ifconfig.png" />

### Figura 9: Ifconfig - PC4 
<img src = "imagesPC4/ifconfigsPC4.png" />

- Caso o comando não exista, executar ``` sudo apt install net-tools```

# 3 PASSO
## Configurar o SSH
### Adicionando os Hostnames 
- Executar o comando ```sudo hostnamectl set-hostname <hostname> ``` com os nomes dos integrantes do grupo definidos pela tabela.
- Seguir a planilha: https://github.com/renatabfs/redes/blob/main/planilha.md

### Figura 10: Adicionando os Hosts no PC4
<img src = "imagesPC4/Hosts.png" />
     
- Mudar as configurações de IP e a rede para NAT .

### Figura 11: Configurações de rede - PC1 - Emylle
<img src = "imagesEmylle/NAT.png" />

### Figura 12: Configurações de rede - PC2 - Renata
<img src = "imagesRenata/ConfiguraçãoNAT.png" />

- Executar os comandos ```sudo apt update e sudo apt upgrade -y``` para verificar se as máquinas estão tendo acesso à internet.
### Figura 13: Upgrade - PC1 - Emylle
<img src = "imagesEmylle/Upgrade.jpg" />


- Instalar o SSH com os comandos ```sudo apt-get install openssh-server``` e ```systemctl status ssh```

### Figura 14: Instalando o ssh - PC2 - Renata
<img src = "imagesRenata/SSH.png" />

### Figura 15: Instalando o ssh - PC3 - Jefferson

<img src = "imagesJefferson/Status SSH.png" />

- Verificar o status e ver se a Porta 22 está ouvindo com o comando ```netstat -an | grep LISTEN.```
### Figura 16: Verificando status SSH - PC1 - Emylle
<img src = "imagesEmylle/Listen.png" />

### Figura 17: Verificando status SSH - PC2 - Renata
<img src = "imagesRenata/Lsiten.png" />

### Figura 18: Verificando status SSH - PC4
<img src = "imagesPC4/portas22LISTENINGpc4.png" />

- Configurar o Firewall com os comandos ```sudo ufw allow ssh``` e ```sudo ufw status```
- Em seguida, ativar o Firewall com  ```sudo ufw enable```

### Figura 19: Verificando status Firewall - PC 1 - Emylle
<img src = "imagesEmylle/firewall.png" />

### Figura 20: Verificando status Firewall - PC 2 - Renata
<img src = "imagesRenata/StatusFirewall.png" />

### Figura 21: Verificando status Firewall - PC 3 - Jefferson
<img src = "imagesJefferson/Status firewal - jefferson.png" />

### Figura 22: Verificando status Firewall - PC 4
<img src = "imagesPC4/firewallallorportas22pc4.png" />

## 4 PASSO
### Criar os users com o hostname dos integrantes do grupo.
- Crie os users com o comando ```sudo adduser``` <nomedosintegrantes>
- Pode ser usado o mesmo nome de usuário que os hostname's da planilha fornecida.
- Adicione as informações que a máquina exigir.

### Figura 23: Criando users - PC 2 - Renata
<img src = "imagesRenata/AddUser.png" />
 
 ### Figura 24: Criando users - PC 4
<img src = "imagesPC4/adicionandousersPC4.png" />
 
### Figura 25: Users criados - PC 1 - Emylle
<img src = "imagesEmylle/usuarios.png"/>

### Figura 26: Users criados - PC 2 - Renata
<img src = "imagesRenata/UsersAdicionados.png" />
 
### Figura 27: Users criados - PC 3 - Jefferson
<img src = "imagesJefferson/usuarios.png" />
                                                    
## Figura 28: Users criados - PC 4
<img src = "imagesPC4/userscriadosPC4.png" />

- Modificar o arquivo de hosts utilizando o comando ```sudo nano /etc/hosts```
- Deve obedecer os seguintes formatos: <hostname/ip/dominio/aliase>

### Figura 29: Config de host - PC 1 - Emylle
<img src = "imagesEmylle/Hosts.png" />

### Figura 30: Config de host - PC 2 - Renata
<img src = "imagesRenata/ArquivoHosts.png" />

### Figura 31: Config de host - PC 3 - Jefferson
<img src = "imagesJefferson/Hosts.png" />
 
 ### Figura 32: Config de host - PC 4
<img src = "imagesPC4/adicionaetchostsPC4.png" />

- Colocar as configurações de rede em Modo Bridge
- Verificar se os endereços MAC's não estão iguais

### Figura 33: Endereço MAC e modo bridge - PC 1 VM1- Emylle
<img src = "imagesEmylle/modo bridge - vm01.png" />

### Figura 34: Endereço MAC e modo bridge - PC 1 VM2- Emylle
<img src = "imagesEmylle/modo bridge-vm02.png" />

### Figura 35: Endereço MAC e modo bridge - PC 2 VM1- Renata
<img src ="imagesRenata/ModoBridge.png" />
 
 ### Figura 36: Endereço MAC e modo bridge - PC 3 VM1- Jefferson
<img src ="imagesJefferson/modo brigde1.png" />
 
 ### Figura 37: Endereço MAC e modo bridge - PC 3 VM2- Jefferson
<img src ="imagesJefferson/modo bridge 2.png" />
 
 ### Figura 38: Endereço MAC e modo bridge - PC 4 VM1
<img src ="imagesPC4/VM1bridgeEndMacPC4.png" />

### Figura 39: Endereço MAC e modo bridge - PC 4 VM2
<img src ="imagesPC4/VM2bridgeEndMacPC4.png" />
 
 - Ligar as máquinas ao switch por meio do cabo de rede
 
 ### Figura 40: Máquinas 1 e 2 com os cabos
<img src ="Infraestrutura de rede/pc1e2.jpg " />
 
 ### Figura 41: Máquinas 3 e 4 com os cabos
<img src ="Infraestrutura de rede/pc3e4.jpg " />
 
### Figura 42: Switch
<img src ="Infraestrutura de rede/switch.jpg " />
 
 ### Figura 43: Visão geral
<img src ="Infraestrutura de rede/tudo.jpg " />


## 5 PASSO - ATIVAR O HOST ONLY
 - Ativar a interface no computador para a comunicação Host-VM
 - Configurar o servidor DCHP do adaptador VnetBox0
 
 ### Figura 44: DHCP - PC 3 - Jefferson
 <img src = "imagesJefferson/Netplan.png" />

  ### Figura 45: Vnetbox0 - PC 3 - Jefferson
 <img src = "imagesJefferson/Jefferson_VM-01(hostonly).png" />
 
 - Ativar as configurações da interface na VM para o servidor dhcp para o adaptador 2 (enp0s8)
 
 ### Figura 46: enp0s8 - PC 3 - Jefferson
 <img src = "imagesJefferson/Ifconfig.png" />
 
# [Resultados](https://github.com/renatabfs/redes/blob/main/resultados.md)
