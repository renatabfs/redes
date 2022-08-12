## 1 PASSO
# Importar as ISOS
 - Importar as isos e configurar com o nome dos integrantes do grupo.
### Figura 1: Importação da ISO - PC1-Emylle
<img src = "imagesEmylle/importandoiso.png" />
<img src = "imagesEmylle/Criando a iso.png" />

## 2 PASSO
# Configurar os Ip's no netplan
- Abrir as VMs e fazer login no ```administrador```
- Senha: ```adminifal```

# Para acessar o netplan:
- Executar o comando

```
sudo nano /etc/netplan/01-netcfg.yaml
```
- Se não possuir o arquivo verificar o nome dele com ``` ls -la /etc/netplan ```
- Retirar o renderer
- Adicionar o gateway4 e o addresses com os IP's da equipe
- Adicionar dhcp4: false

### Figura 2: Arquivo netplan - PC1 - Emylle
<img src = "imagesEmylle/VMsEmylle_enderecosIPestaticos.jpg" />

### Figura 3: Arquivo netplan - PC2 - Renata

<img src = "imagesRenata/VMsRenata_enderecoIPestatico.jpg" />

### Figura 4: Arquivo netplan - PC3 - Jefferson

<img src = "imagesJefferson/Netplan das VMs.png" />

- Por fim, executar ``` sudo netplan apply ```
- Verificar no ``` ifconfig -a ``` se alterações foram bem feitas
 
### Figura 4: Ifconfig - PC2 - Renata
<img src = "imagesRenata/VMsRenata_ifconfigs.jpg" />

- Caso o comando não exista, executar ``` sudo apt install net-tools```

# 3 PASSO
## Configurar o SSH
### Adicionando os Hostnames 
- Executar o comando ```sudo hostnamectl set-hostname <hostname> ``` com os nomes dos integrantes do grupo definidos pela tabela.
- Mudar as configurações de IP e a rede para NAT 

### Figura 5: Configurações de rede - PC1 - Emylle
<img src = "imagesEmylle/NAT.png" />

- Executar os comandos ```sudo apt update e sudo apt upgrade -y``` para verificar se as máquinas estão tendo acesso à internet.
### Figura 6: Upgrade - PC1 - Emylle
<img src = "imagesEmylle/Upgrade.jpg" />


- Instalar o SSH com os comandos ```sudo apt-get install openssh-serve``` e ```systemctl status ssh```

### Figura 7: Instalando o ssh - PC2 - Renata
<img src = "imagesRenata/VMsrenata_baixandosshserver.jpg" />

### Figura 8: Instalando o ssh - PC3 - Jefferson

<img src = "imagesJefferson/Status SSH.png" />

- Verificar o status e ver se a Porta 22 está ouvindo com o comando ```netstat -an | grep LISTEN.```
### Figura 8: Verificando status SSH - PC1 - Emylle
<img src = "imagesEmylle/VMsEmylle_portas22sshListening.jpg" />

### Figura 9: Verificando status SSH - PC2 - Renata
<img src = "imagesRenata/VMsRenata_portas22sshListening.jpg" />

- Configurar o Firewall com os comandos ```sudo ufw allow ssh``` e ```sudo ufw status```
- Em seguida, ativar o Firewall com  ```sudo ufw enable```

### Figura 10: Verificando status FIrewal - PC 1 - Emylle
<img src = "imagesEmylle/VMsEmylle_configdeFirewall.jpg" />

### Figura 11: Verificando status FIrewal - PC 3 - Jefferson
<img src = "imagesJefferson/Status firewal - jefferson.png" />.

## 4 PASSO
### Criar os users com o hostname dos integrantes do grupo
- Crie os users com o comando ```sudo adduser <nomedointegrante>
- Adicione as informações que a máquina exigir

### Figura 12: Criando users - PC 2 - Renata
<img src = "imagesRenata/VMsRenata_criandoaddusers.jpg"

- Modificar o arquivo de hosts utilizando o comando ```sudo nano /etc/hosts```
- Deve obedecer os seguintes formatos: <hostname/ip/dominio/aliase>

### Figura 13: Config de host - PC 1 - Emylle
<img src = "imagesEmylle/VMsEmylle_confdeHosts.jpg" />

### Figura 14: Config de host - PC 2 - Renata
<img src = "imagesRenata/VMsRenata_configuracoesdeHost.jpg" />

### Figura 15: Config de host - PC 3 - Jefferson
<img src = "imagesJefferson/Hosts - jefferson.png" />

- Colocar as configurações de rede em Modo Bridge
- Verificar se os endereços MAC's não estão iguais

### Figura 16: Endereço MAC e modo bridge - PC 1 VM1- Emylle
<img src = "imagesEmylle/VM1Emylle_enderecoMACeModobridge.jpg" />

### Figura 17: Endereço MAC e modo bridge - PC 1 VM2- Emylle
<img src = "imagesEmylle/VM2Emylle_enderecoMACeModoBridge.jpg" />

### Figura 18: Endereço MAC e modo bridge - PC 1 VM1- Renata
<img src ="imagesRenata/VM1renata_endereçoMAC.jpg" />

### Figura 18: Endereço MAC e modo bridge - PC 1 VM2- Renata
<img src ="imagesRenata/VM2renata_endereçoMac.jpg" />
