## **Capítulo 7: Garantindo o Uptime - Gerenciamento de Servidor com `screen` e `systemd`**

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

Quando você se conecta ao seu VPS via **SSH** (Secure Shell) e inicia o servidor Minecraft, o processo está anexado à sua sessão. Se você fechar a janela do terminal, o processo é encerrado, e o servidor **cai**.

Para evitar isso, existem duas ferramentas essenciais no Linux para rodar processos em segundo plano: `screen` (ou `tmux`) e `systemd`.

### 7.1. **Método Rápido: O Utility `screen`**

O `screen` (ou seu alternativo `tmux`) é a maneira mais simples e comum de manter um processo rodando após o desligamento da sua sessão SSH. Ele cria uma sessão virtual persistente onde você pode rodar o servidor, se desconectar e depois **reatachar** a sessão mais tarde.

#### ⚙️ Comandos Essenciais do `screen`

1. **Instalar o `screen`:**

```bash
sudo apt install screen -y
```

2. Criar uma Nova Sessão e Nomeá-la:

```bash
screen -S minecraft
# O comando "-S" dá um nome à sessão (ex: "minecraft").
```

3. **Iniciar o Servidor:** Dentro da nova sessão do `screen`, você executa seu script de inicialização do Java (o mesmo do Capítulo 3).

```bash
java -Xms1024M -Xmx4096M -jar paper.jar --nogui
```

4. **Desanexar (Deixar Rodando):** Para fechar a sua sessão SSH e deixar o servidor rodando em segundo plano, pressione as teclas:

> **Ctrl + A**, seguido por **D** (de _Detach_). A mensagem `[detached from...]` aparecerá, e você pode fechar o SSH.

5. **Reanexar a Sessão:** Para voltar à console do servidor e monitorá-lo ou usar comandos:

```bash
screen -r minecraft
```

**Vantagem:** Simples e fácil para gerenciar múltiplas instâncias de servidores (se você estiver montando uma Rede BungeeCord/Velocity).

### 7.2. **Método Profissional: O Serviço `systemd`**

O **systemd** é o gerenciador de sistema e serviços (init system) padrão na maioria das distribuições Linux modernas. Ele é a maneira mais robusta de garantir que o servidor Minecraft seja tratado como um **serviço oficial** do sistema.

#### Vantagens do `systemd`:

- **Início Automático:** O servidor inicia automaticamente após a reinicialização do VPS.
    
- **Reinício em Falha:** Se o servidor Minecraft travar, o `systemd` pode ser configurado para reiniciá-lo automaticamente, maximizando o uptime.
    
- **Gerenciamento Centralizado:** Você usa comandos padrão de serviços (`start`, `stop`, `restart`, `status`).
    

#### ⚙️ Configurando o Serviço (Unidade `minecraft.service`)

1. **Criar o Arquivo de Serviço:** Crie um arquivo chamado `minecraft.service` no diretório de serviços do sistema.

```
sudo nano /etc/systemd/system/minecraft.service
```

2. **Conteúdo do Arquivo de Serviço:** Cole o código abaixo. **Ajuste as linhas `User`, `WorkingDirectory` e `ExecStart`** para refletir seu ambiente.

```ini
[Unit]
Description=Minecraft Server Startup Service
After=network.target mariadb.service # Garante que o MariaDB inicie primeiro

[Service]
User=minecraft # O usuário Linux que será usado para rodar o servidor
Nice=1        # Prioridade mais baixa de CPU, opcional
KillMode=none # CRÍTICO: Não mate o processo Java diretamente
SuccessExitStatus=143 

# Pasta ONDE está o paper.jar
WorkingDirectory=/home/minecraft/servidores/survival

# Comando de Inicialização do Java. Ajuste a RAM (Xmx)
ExecStart=/usr/bin/java -Xms1024M -Xmx4096M -jar paper.jar --nogui

# Comando para enviar o "stop" seguro ao servidor ao desligar o VPS
ExecStop=/bin/bash -c "screen -p 0 -S minecraft -X eval 'stuff \"say Server going down for maintenance!\"\015'"
ExecStop=/bin/sleep 5
ExecStop=/bin/bash -c "screen -p 0 -S minecraft -X eval 'stuff \"stop\"\015'"

Restart=on-failure # Reinicia o servidor se ele falhar

[Install]
WantedBy=multi-user.target
```

3. Habilitar e Iniciar o Serviço:

```bash
sudo systemctl daemon-reload # Recarrega a configuração do systemd
sudo systemctl enable minecraft.service # Habilita o início automático na boot
sudo systemctl start minecraft.service # Inicia o serviço
```

4. Comandos de Gerenciamento:

```bash
sudo systemctl stop minecraft.service
sudo systemctl restart minecraft.service
sudo systemctl status minecraft.service
```

**Conclusão:** Para um servidor profissional, o **`systemd`** é superior ao `screen` por sua robustez, capacidade de reinício automático e integração total com o sistema operacional.