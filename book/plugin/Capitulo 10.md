## **Capítulo 11: Gerenciamento do Ciclo de Vida - Modo Manutenção e Whitelist** 🛑

**Tags:** #manutenção #admin #whitelist #uptime #atualização

---

Servidores profissionais precisam de paradas programadas para aplicar grandes atualizações, fazer _backups_ pesados ou corrigir _bugs_ críticos. O **Modo Manutenção** (gerenciado por plugins como o _Maintenance_ ou _Simple Maintenance_) permite que apenas membros autorizados (`staff` ou `builders`) acessem o servidor enquanto ele está indisponível para o público.

### 10.1. Ativação e Desativação do Modo Manutenção

O controle principal do _uptime_ e _downtime_ do servidor é feito com comandos simples de _toggle_.

|Comando|Função|
|---|---|
|`/mt on`|**Liga o modo manutenção**. Expulsa todos os jogadores que não estão na _whitelist_ e impede novas conexões do público.|
|`/mt off`|**Desliga o modo manutenção**. Remove todas as restrições e permite que o público se conecte novamente.|

> **Permissões:** A permissão para usar `/mt on` e `/mt off` deve ser restrita apenas aos grupos **Dono** e **Co-Dono** no **LuckPerms** (Capítulo 3), pois este comando afeta diretamente a disponibilidade do servidor.

### 10.2. Gerenciamento da Whitelist de Manutenção

A _whitelist_ é a lista de exceções — jogadores que podem entrar mesmo quando o servidor está em manutenção. Geralmente são membros do _staff_ ou _builders_ que precisam testar as atualizações.

|Comando|Função|
|---|---|
|`/mt add <user>`|Adiciona um jogador à lista de exceções.|
|`/mt remove <user>`|Remove um jogador da lista.|
|`/mt list`|Lista todos os jogadores autorizados a entrar no modo manutenção.|
|`/mt reset`|**Cuidado!** Limpa completamente a _whitelist_ e reseta o MOTD de manutenção.|
|`/mt status`|Exibe o status atual (ligado/desligado) do modo manutenção.|

### 10.3. Configurando a Mensagem de Manutenção (MOTD Dinâmico)

A chave para uma boa experiência do usuário é a comunicação. O plugin de manutenção permite definir diferentes MOTDs para informar o público sobre o que está acontecendo. O formato que você forneceu indica a capacidade de definir múltiplos grupos de MOTDs (Ex: Grupo 1 e Grupo 2).

#### 10.3.1. Estrutura do Comando `mt setmotd`

O formato é: `/mt setmotd <grupo> <linha> "<mensagem>"`.

- `<grupo>`: Um identificador numérico que permite alternar rapidamente entre diferentes mensagens (Ex: 1 para "Atualização de Plugin", 2 para "Correção de Bug").
- `<linha>`: 1 (Linha Superior) ou 2 (Linha Inferior) na lista de servidores.
- `<mensagem>`: A mensagem formatada com cores (`&a`, `&l`, etc.).

#### 10.3.2. Exemplo de Uso Prático

No seu exemplo, o _staff_ pode alternar a mensagem sem precisar digitar as linhas novamente:

| Ação                                   | Comando de Ativação                                                                                                                                                                                                                                   | Resultado no Servidor (Exemplo 1)   |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| **Definir e Usar MOTD de Atualização** | `/mt setmotd 1 1 "Servidor em manutenção. Por favor, entre em contato com o administrador para mais informações."`<br><br>  <br><br>`/mt setmotd 1 2 "Estamos realizando atualizações no servidor. Pedimos que aguarde até a conclusão do processo."` | O servidor exibe o MOTD do Grupo 1. |
| **Mudar para MOTD de Correção**        | `/mt setmotd 2 1 "Manutenção em andamento. O servidor está temporariamente indisponível."`<br><br>  <br><br>`/mt setmotd 2 2 "Atualizações e correções de bugs estão sendo aplicadas."`                                                               | O servidor exibe o MOTD do Grupo 2. |
> **Fluxo de Trabalho de Manutenção:** Antes de iniciar a manutenção, use `/mt setmotd <grupo>` para definir a mensagem, depois notifique os jogadores (ex: `/say`) e use `/mt on`.

### Exemplo de código

```yaml
####################################################################################################################
#   __  __       _       _                                    _             _                          _          #
#  |  \/  | __ _(_)_ __ | |_ ___ _ __   __ _ _ __   ___ ___  | |__  _   _  | | _____ _ __  _ __  _   _| |___   __ #
#  | |\/| |/ _` | | '_ \| __/ _ \ '_ \ / _` | '_ \ / __/ _ \ | '_ \| | | | | |/ / _ \ '_ \| '_ \| | | | __\ \ / / #
#  | |  | | (_| | | | | | ||  __/ | | | (_| | | | | (_|  __/ | |_) | |_| | |   <  __/ | | | | | | |_| | |_ \ V /  #
#  |_|  |_|\__,_|_|_| |_|\__\___|_| |_|\__,_|_| |_|\___\___| |_.__/ \__, | |_|\_\___|_| |_|_| |_|\__, |\__| \_/   #
#                                                                  |___/                        |___/             #
###################################################################################################################
# You can report bugs here: https://github.com/kennytv/Maintenance/issues
# If you need any other help/support, you can also join my Discord server: https://discord.gg/vGCUzHq
# The config and language files use MiniMessage, NOT legacy text for input. Use https://webui.adventure.kyori.net/ to edit and preview the formatted text.
# For a full list of formats and fancy examples of MiniMessage, see https://docs.adventure.kyori.net/minimessage/format.html

# Changes the language of command feedback/messages.
# If you find missing translations or want to contribute, see https://crowdin.com/project/maintenance
# Currently available are: en (English), de (German), fr (French), pt (Portuguese), es (Spanish), ru (Russian), zh (Chinese), it (Italian),
#  pl (Polish), tr (Turkish), sv (Swedish), uk (Ukrainian), ja (Japanese), da (Danish), ko (Korean), hu (Hungarian), vi (Vietnamese)
language: pt

# Enables maintenance mode.
maintenance-enabled: true

# The message (MOTD) shown in the multiplayer server list motd when maintenance is enabled.
# If you put in multiple entries, one of them will be chosen randomly on every ping.
# If running an endtimer, the time left can be displayed by including '%TIMER%' in a ping message.
ping-message:
  enabled: true
  messages:
  - '"Servidor em manutenção. Por favor, entre em contato com o administrador para mais informações."<br>"Estamos realizando atualizações no servidor. Pedimos que aguarde até a conclusão do processo."'
  - '"Manutenção em andamento. O servidor está temporariamente indisponível."<br>"Atualizações e correções de bugs estão sendo aplicadas."'
  # If set to true and an endtimer is currently running, a message from this pool will be chosen
  # instead of the ones above, so you can have different messages for when an endtimer is running/not running.
  enable-timer-specific-messages: true
  timer-messages:
  - <red>Currently under maintenance<br><gradient:#fbffc2:#fffff>Come back in:</gradient> <color:#aa55ee>%TIMER%

# If enabled, the message below will be shown in the top right corner of the server in the server list, where the player count would normally be displayed.
# You can use '%ONLINE%' and '%MAX%' if you want to include the player count in a custom message (e.g. "Maintenance %ONLINE%/%MAX%").
# DOES NOT SUPPORT RGB!
player-count-message:
  enabled: true
  message: <dark_red>Maintenance
  # If set to true and an endtimer is currently running, the timer message will be used instead of the normal one.
  enable-timer-specific-message: false
  timer-message: '<dark_red>Come back in: <yellow>%TIMER%'

# Is shown when you move your mouse above the text in the top right corner of the server in the server list, where the player count would normally be displayed.
# DOES NOT SUPPORT RGB!
player-list-hover-message:
  enabled: true
  message: <red>Currently under<br><red>maintenance
  # If set to true and an endtimer is currently running, the timer message will be used instead of the normal one.
  enable-timer-specific-message: false
  timer-message: <red>Come back in:<br><red><yellow>%TIMER%

# Any extra commands inside the arrays will be executed when maintenance is enabled/disabled.
# Example: commands-on-maintenance-enable: ["say hello!", "stop"]
commands-on-maintenance-enable: []
commands-on-maintenance-disable: []

# If set to true, the server icon will be changed to the 'maintenance-icon.png' file in the plugin's folder during maintenance.
custom-maintenance-icon: false

# If set to true, players with the 'maintenance.joinnotification' permission will receive a message,
# that a player tried to join the server while maintenance is enabled.
send-join-notification: false

# Set this to false if you do not want players to be kicked when you enable maintenance (new connections will still be blocked).
kick-online-players: true

# When fetched player does not exist then fallback to offline uuid. Only works on proxies like Velocity or BungeeCord
fallback-to-offline-uuid: false

# If enabled and the server is restarted while running an endtimer, the timer will be continued after the restart.
# If the timer ends while the server is offline, maintenance will be disabled as soon as the server starts again.
continue-endtimer-after-restart:
  enabled: false
  # This value is set everytime an endtimer is started, cancelled or ended.
  # Do not manually change this value.
  end: 0

# If using the timer command: In what intervalls before enabling/disabling maintenance there will be a broadcast.
timer-broadcast-for-seconds:
- 1200
- 900
- 600
- 300
- 120
- 60
- 30
- 20
- 10
- 5
- 4
- 3
- 2
- 1

# If disabled, you will no longer receive any messages if there is an update.
# Not recommended to disable, as new versions generally tend to run better and with fewer bugs.
# However, you can always check for updates manually using the '/maintenance update' command.
update-checks: true

# Used for autoupdating the config, do not change this value.
config-version: 9
```