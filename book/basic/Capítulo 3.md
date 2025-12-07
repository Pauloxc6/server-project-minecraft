## Capítulo 3: Instalando o Motor - Java e a Base do Servidor (PaperMC/Velocity)

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---
Após escolher a hospedagem Linux (Capítulo 1) e definir sua arquitetura (Capítulo 2), o próximo passo é preparar o sistema operacional para rodar o software do Minecraft.

### 1. Instalando o Ambiente de Execução Java (JRE/JDK)

O Minecraft Server é um aplicativo Java, exigindo que o **Java Runtime Environment (JRE)** esteja instalado no seu VPS Linux.

#### A. A Importância da Versão Correta

Usar a versão errada do Java pode impedir o servidor de iniciar ou causar problemas de performance severos.

|Versão do Minecraft|Versão Java Recomendada (LTS)|
|---|---|
|**1.19+**|**Java 17 ou Java 21**|
|**1.17 – 1.18**|Java 17|
|**1.16.5 e anteriores**|Java 11 (ou 8 para versões muito antigas)|

#### B. Comandos de Instalação (Ubuntu/Debian)

Como estamos focando no padrão profissional, usaremos o **Java 21** (LTS mais recente e otimizado) para servidores 1.19+:

Vamos **atualizar o Gerenciador de Pacotes:** Garante que você tenha acesso aos pacotes mais recentes.  Posteriormente instalar e verificar se foi instalado corretamente.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install openjre-21-jre -y
java --version
```

---
### 2. Escolhendo e Baixando o Software Base

Para um servidor profissional focado em Plugins, usaremos o **PaperMC** como base principal.

#### A. PaperMC (O Servidor de Jogo)

O PaperMC é um _fork_ (versão otimizada) do Spigot/Bukkit. Ele oferece correções de bugs do Vanilla, otimizações de I/O (leitura/escrita de disco) e configurações de performance que são vitais para manter o TPS alto.

- **Ação:** Crie uma pasta para o seu servidor e use o comando `wget` para baixar o JAR mais recente (substitua o link pelo URL do site oficial do PaperMC).

```bash
mkdir server_survival
cd server_survival
# Exemplo: Você usaria wget para baixar o arquivo .jar
# wget [Link da versão do PaperMC] -O paper.jar
```

#### B. Velocity (O Servidor Proxy) - Se for uma Rede

Se você estiver construindo uma **Rede BungeeCord/Velocity**, você deve criar uma pasta separada para o proxy e baixar o Velocity.

- **Vantagem do Velocity:** Mais rápido e estável que o BungeeCord, com melhor suporte para features modernas do Java e do Minecraft.
  
```bash
mkdir server_proxy
cd server_proxy
# Exemplo: Baixar o Velocity .jar
# wget [Link da versão do Velocity] -O velocity.jar
```

---
### 3. Primeira Execução e Otimização da RAM

Com o Java e o JAR baixados, você precisa de um script de inicialização.

#### ⚙️ O Script de Execução

Você deve usar o comando `java` definindo os limites de memória RAM.

```bash
java -Xms1024M -Xmx4096M -jar paper.jar --nogui
```

- `-Xms1024M`: **Memória Inicial (Minimum Size)**. O servidor começa usando 1 GB (1024 MB).
- `-Xmx4096M`: **Memória Máxima (Maximum Size)**. O servidor pode crescer até 4 GB. **Crucial:** Nunca defina esse valor como a RAM total do seu VPS; o Linux precisa de RAM para rodar.
- `--nogui`: Desativa a interface gráfica do Java, economizando recursos no seu VPS Linux.

---
#### ⚠️ Aceitando a EULA

Na primeira execução, o servidor irá criar um arquivo `eula.txt` e desligar. Você deve editar este arquivo para aceitar os termos da Mojang:

```bash
nano eula.txt
# Altere a linha:
# eula=false
# Para:
eula=true
```

**Salve e saia (`Ctrl+X`, depois `Y` e `Enter` no `nano`).**


