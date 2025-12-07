## **Capítulo 15: Segurança Crítica - Autenticação e Configuração do Passky** 🔑

**Tags:** #passky #autenticação #segurança #login #hashing #mysql

---

O **Passky** (ou plugins de autenticação como AuthMe) é a primeira e mais importante barreira de segurança, exigindo que os jogadores provem sua identidade através de uma senha. Em servidores que operam em modo _offline_ (muito comum em redes BungeeCord), este plugin é **obrigatório**.

### 1. Criptografia e Segurança de Dados

A segurança da sua base de dados de senhas depende do método de criptografia (_hashing_) que você escolher.

- **`encoder: "SHA-512"`**: Esta é uma excelente escolha. O SHA-512 é um algoritmo de _hashing_ seguro e moderno.
    
    > **Princípio de Segurança:** O servidor nunca armazena a senha real do usuário, apenas a versão "hashed" (criptografada). Quando o usuário tenta fazer _login_, o servidor criptografa a senha digitada e compara o resultado com o hash armazenado.
    
- **`hide_password: true`**: **Essencial**. Garante que as senhas digitadas (mesmo criptografadas) não apareçam nos logs do console, protegendo os dados em caso de acesso não autorizado aos logs do servidor.
    

### 2. Fluxo de Jogabilidade (UX e Segurança)

Esta seção controla o que acontece com o jogador antes e depois do _login_.

|Configuração YAML|Valor|Análise e Recomendação|
|---|---|---|
|**`teleportation_enabled: true`**|`true`|**Recomendado**. Teleporta o jogador para uma área segura (geralmente sob o mundo) até que ele faça _login_, impedindo que ele se mova e abuse de _bugs_ antes da autenticação.|
|**`teleport_player_last_location: true`**|`true`|**Recomendado**. Após o _login_ bem-sucedido, o jogador é enviado de volta para onde estava, garantindo uma UX fluida.|
|**`spawn_world: lobby`**|`lobby`|**Crucial em Redes**. Define o mundo seguro para onde os jogadores não autenticados são enviados. Em redes, deve ser o _lobby_ principal.|
|**`min_password_length: 8`**|`8`|**Mínimo**. 8 caracteres é um bom ponto de partida, mas aumentar para 10 ou 12 aumenta a segurança.|
|**`attempts: 5`**|`5`|**Segurança contra Brute Force**. Limita o número de tentativas de senha incorretas antes de expulsar o jogador.|
|**`time_before_kick: 30`**|`30`s|Tempo limite para o _login_. Evita que bots fiquem conectados indefinidamente na tela de _login_.|

### 3. Sistema de Sessão (Session)

As sessões são vitais para a experiência do usuário em redes BungeeCord.

- **`session_enabled: true`**: **Absolutamente Essencial em Redes**. Se ativado, o jogador não precisa fazer _login_ novamente por um período de tempo. Isso é gerenciado pelo BungeeCord/Velocity.
    
- **`session_time: 30`** (minutos): Define a duração da sessão. 30 minutos é um bom balanço entre segurança e conveniência. Se o jogador sair e voltar em 29 minutos, ele fará _login_ automaticamente.
    

### 4. Integração com MariaDB (Redes e Escala)

Embora o _Passky_ possa usar arquivos locais, o uso do MariaDB/MySQL é **obrigatório** em qualquer rede BungeeCord/Velocity para centralizar a base de dados de senhas.

|Configuração YAML|Valor|Requisito Profissional|
|---|---|---|
|**`mysql: false`**|`false`|**DEVE ser mudado para `true`** em um servidor profissional.|
|**`persist_session: false`**|`false`|Se você usar o MySQL (`mysql: true`), esta opção é ignorada, pois a persistência de dados será feita automaticamente no banco de dados.|

> **Ação Imediata:** Se este servidor for parte de uma rede ou tiver uma base de usuários grande, defina `mysql: true` e preencha as credenciais.

### 5. Customização Visual (UX)

As mensagens visuais orientam o jogador durante o processo de _login_.

- **`titles_enabled: true`**: **Recomendado**. Usar títulos e subtítulos grandes é mais atraente e difícil de ignorar do que mensagens de chat.
    
- **`login_subtitle: "&a/login <password>"`**: Esta mensagem é crucial. Ela instrui o jogador sobre o comando exato que ele deve usar. Mantenha-a clara e colorida.

### Exemplo de config

```yaml
#       ------------ + Passky by Ziga Zajc + ------------   #
#                                                           #
#                             Config                        #
#                                                           #
#       --------- + ------------------------- + ---------   #
#
# Here you can change which encoder will your server use. You can use: MD2, MD5, SHA-1, SHA-256, SHA-384, SHA-512 or null - for no encoder
encoder: "SHA-512"
# Disabling teleportation will prevent Passky plugin from teleporting players in order to hide their location
teleportation_enabled: true
# Do you want to teleport players back to their last location after successful login?
teleport_player_last_location: true
# Where should players who haven't logged in be sent? You can choose to always send them to the same world they were in the last time by using (null) as the option.
spawn_world: lobby
# How many incorrect password attempts can the player make before the server kicks them out?
attempts: 5
# What is the login timeout in seconds before players get kicked?
time_before_kick: 30
# Minimum characters for password
min_password_length: 8
# Maximum characters for password
max_password_length: 32
# Don't allow players with illegal usernames to join your server
kick_illegal_usernames: true
# Do you want players to be identified with usernames (0) or UUIDs (1) (Default is usernames (0))
player_identifier: 0
# Hiding the command log of the plugin command in console?
# It will protect password
hide_password: true
# If you enable session, players won't need to log in every time they enter the server (Awesome feature for Bungeecord servers)
session_enabled: true
# How many minutes do you want session to last?
session_time: 30
# Enable session persistence to file between server restarts
# If true, session data will be saved and restored automatically
# This setting is ignored if mysql: true
persist_session: false
# Do you want to enable titles and subtitles?
titles_enabled: true
# This title will show when player is required to login
login_title: "&aLogin"
# This subtitle will show when player is required to login
login_subtitle: "&a/login <password>"
# This title will show when player is required to register
register_title: "&aRegister"
# This subtitle will show when player is required to register
register_subtitle: "&a/register <password> <password>"
#----------------------------------------------------------
#   MySQL Database - Recommended for Bungeecord networks
#----------------------------------------------------------
# Do you want to use mysql database?
mysql: false
# Here are all data for connection to Mysql database. Please create database, user and password by yourself. Do not use root as user, because of security risk!
mysql_host: "localhost"
mysql_port: "3306"
mysql_database: "Passky"
mysql_user: "root"
mysql_password: "toor"
mysql_useSSL: false

```