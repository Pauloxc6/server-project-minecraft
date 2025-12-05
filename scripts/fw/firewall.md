
Abaixo segue o script para o setup inicia do firewall em seu servidor:

```bash
#!/usr/bin/env bash

#====================
# BANNER
#====================

figlet -c FIREWALL SETUP
echo "By: @Pauloxc6"

#====================
# Vars
#====================

readonly nul="\e[0m"
readonly azul="\e[34;1m"
readonly white="\e[37;1m"
readonly green="\e[32;1m"
readonly red="\e[31;1m"
readonly SERVER="192.168.122.139"
readonly CLIENT="192.168.122.1"

#====================
# test Root
#====================

[ "$UID" -eq 0 ] && { echo -e "${red}O programa $white[$0]${red} de ser executado como ${white}root${nul}"; exit 1 ;}

#====================
# Main
#====================
echo -e "${azul}[INFO]:${white} INICIANDO O RESET DO FIREWALL${nul}"
echo -e "${red}"
ufw reset

echo -e "${azul}[INFO]:${white} INCIANDO O FIREWALL${nul}"
echo -e "${green}"
ufw enable

# Defaults
echo -e "\n${azul}[INFO]:${white} APLICANDO REGRAS DEFUALTS${nul}"
sleep 2s

echo -e "\n${azul}[INFO]:${white} Bloqueando tudo que chegar no firewall${nul}"
echo -e "${red}"
ufw default deny incoming

echo -e "\n${azul}[INFO]${white} Libera tudo que sair do firewall${nul}"
echo -e "${red}"
ufw default allow outgoing

echo

# Apps
echo -e "${azul}[INFO]:${white} APLICANDO TODAS AS REGRAS DOS APPS${nul}"
echo -e "${white}"

ufw allow proto tcp from "$CLIENT" to "$SERVER" port 65022  comment "ACCEPT | SSH               | From: $CLIENT/adm"
ufw limit from any to "$SERVER" port 65022                  comment "LIMIT  | SSH               | From: Any"
ufw allow proto tcp from "$CLIENT" to "$SERVER" port 9443   comment "ACCEPT | Portainer         | From: $CLIENT/adm"
ufw allow proto tcp from "$CLIENT" to "$SERVER" port 8443   comment "ACCEPT | Crafty            | From: $CLIENT/adm"
ufw allow proto tcp from any to "$SERVER"       port 3306   comment "ACCEPt | MySQL             | From: Any"

# Minecraft
ufw allow proto udp from any to "$SERVER" port 19132        comment "ACCEPT | Minecraft Bedrock | From: Any"
ufw allow proto tcp from any to "$SERVER" port 25500:25600  comment "ACCEPT | Minecraft Java    | From: Any"
ufw allow proto tcp from "$CLIENT" to "$SERVER" port 8804   comment "ACCEPT | Plan              | From: $CLIENT/adm"
ufw allow proto tcp from "$CLIENT" to "$SERVER" port 8100   comment "ACCEPT | BlueMap           | From: $CLIENT/adm"

# Porta teste
ufw allow proto tcp from "$CLIENT" to "$SERVER" port 8080    comment "ACCEPT | Porta Teste       | From: $CLIENT/adm"

#=============
# Status
#=============

echo -e "\n${azul}[INFO]:${white} Status do firewall${nul}"
echo -e "${white}"
ufw status verbose

echo -e "${nul}"

```


Abra o seu terminal  e digite:

```bash
nano fw.sh
<cole aqui o script>
<Feche o terminal>

# Inicie o firewall com o comando:
sudo bash ./fw.sh # para usuarios comuns
bash ./fw.sh      # para o usuário root
```

Em questão de segundo você tem um firewall prontinho

**Nota:** Você deve adaptar a sua necessidade, eu usei esse no laboratório de teste para esse livro
