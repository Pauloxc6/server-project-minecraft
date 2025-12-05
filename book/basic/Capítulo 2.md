## Capítulo 2: Instalando o Ambiente Java e Escolhendo a Base do Servidor (PaperMC)

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---
Para um servidor de Minecraft rodar, ele precisa de dois componentes principais:

1. O **Java Runtime Environment (JRE)**, que é o ambiente onde o código do Minecraft é executado.
    
2. O **Software do Servidor** (o arquivo `.jar`), que é o código que gerencia o mundo e a jogabilidade (ex: PaperMC).

### 2.1. A Escolha da Versão Java

A performance do seu servidor depende **diretamente** da versão do Java que você utiliza.

|Versão do Minecraft|Versão Java Recomendada (LTS)|Detalhes|
|---|---|---|
|**1.17 – 1.18**|Java 17|Versão necessária e altamente recomendada para estabilidade e otimização.|
|**1.19+**|Java 17 ou Java 21|O Java 21 (LTS mais recente) oferece melhorias incrementais de performance.|
|**1.16.5 e anteriores**|Java 8 ou Java 11|Use a versão mínima exigida, geralmente Java 11|

> **Recomendação Profissional:** Para servidores modernos (1.19+), instale o **Java 21** para garantir a melhor performance e compatibilidade futura.

#### ⚙️ Exemplo de Comando Linux (Ubuntu/Debian):

Para instalar o Java 21, você usaria comandos como:

```bash
sudo apt update
sudo apt install openjre-21-jre -y
```

Você pode verificar a instalação com:

```bash
java --version
```


## 2.2. Escolhendo o Software Base: PaperMC

O arquivo `minecraft_server.jar` oficial da Mojang é funcional, mas **ineficiente** para servidores profissionais. É por isso que a comunidade desenvolveu _forks_ (versões modificadas) otimizadas.

| Software          | Foco                         | Uso Profissional                                                                                                                                                                    |
| ----------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Vanilla**       | Original Mojang              | Somente para testes simples.                                                                                                                                                        |
| **Spigot/Bukkit** | Adiciona suporte a plugins.  | Mais antigo, menos otimizado que o Paper.                                                                                                                                           |
| **PaperMC**       | **Performance e Correções.** | **O Padrão da Indústria.** Oferece melhorias críticas de performance, corrige bugs do Vanilla e tem otimizações de I/O de disco. É totalmente compatível com plugins Spigot/Bukkit. |
| **Purpur**        | Extensão do PaperMC.         | Para otimizações ainda mais extremas, mas pode quebrar compatibilidade com alguns plugins.                                                                                          |

**Conclusão:** Para começar e seguir o padrão profissional, você deve usar o **PaperMC**.

#### 📝 Baixando o PaperMC

Você deve sempre baixar a última versão estável do PaperMC no site oficial (`https://papermc.io/downloads`).

**No Linux, você usaria o comando `wget`:**
```bash
# Exemplo (o link deve ser atualizado para a versão mais recente que você deseja)
wget https://api.papermc.io/v2/projects/paper/versions/[VERSAO_MINECRAFT]/builds/[NUMERO_BUILD]/downloads/paper-[VERSAO_MINECRAFT]-[NUMERO_BUILD].jar -O paper.jar
```

(Você precisará substituir `[VERSAO_MINECRAFT]` e `[NUMERO_BUILD]` pelos números atuais, ou simplesmente baixar no seu PC e enviar via SFTP.)

### 2.3. Executando o Servidor pela Primeira Vez

Após baixar o arquivo, você precisa de um script simples para iniciar o servidor.

```bash
java -Xms1024M -Xmx4096M -jar paper.jar --nogui
```

- `java`: Chama o interpretador Java.
- `-Xms1024M`: Define a **RAM inicial mínima** (1 GB). 
- `-Xmx4096M`: Define a **RAM máxima** que o servidor pode usar (4 GB). _Aumente este valor dependendo da sua hospedagem._
- `-jar paper.jar`: Especifica qual arquivo JAR rodar.
- `--nogui`: Garante que nenhuma interface gráfica seja carregada (economia de recursos).

---

Ao rodar esse comando pela primeira vez, o servidor irá criar vários arquivos, incluindo o crucial `eula.txt`, e **desligar**. Você deve abrir o `eula.txt` e mudar o valor de `eula=false` para **`eula=true`** para aceitar os termos.

---

Em poucos minutos você já tem um servidor rodando, você pode acessar utilizando o ip mais a porta. Deve ficar algo assim:

```bash
# Ips Self-Hosting
0.0.0.0:25565
127.0.0.1:25565

# IP Local
192.168.1.10:25565
172.16.1.10:25565
10.1.0.10:25565

# IP para internet
44.139.2.10:25565

# DNS
mc.srv.inter.net
```

**Obs:** Você deve está se questionando nesse momento mas o `mc.srv.inter.net` não é o ip, e a resposta não. Pois o que chamamos por ignorância de IP não é IP e sim DNS (Domain Name System), que resumidamente é um protocolo de rede que faz a tradução de um nome para um IP, os IPs são uma sequência de números **que identificam de forma única um dispositivo na rede**, e são eles que realmente importam para a comunicação. O DNS só existe para facilitar a vida humana, já que ninguém quer decorar “192.0.2.15” quando pode simplesmente digitar um nome amigável.