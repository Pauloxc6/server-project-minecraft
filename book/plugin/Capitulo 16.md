
## *Capítulo 16: Moderação e Punição - Configurando o AdvancedBan** 🛡️

**Tags:** #advancedban #moderação #punição #segurança #justiça #staff

---

O **AdvancedBan** é um sistema completo que oferece muito mais do que apenas banimentos. Ele permite gerenciar _bans_, _mutes_ (silêncio), _warnings_ (avisos) e _kicks_ (expulsões) de forma centralizada, com recursos de _offline punishment_ (punir jogadores que não estão online) e integração com web.

### 16.1. Sistema de Punições do AdvancedBan

O plugin oferece uma hierarquia clara de punições, crucial para a política de moderação.

#### 16.1.1. Comandos de Punição

|Comando|Função|Exemplo Prático|
|---|---|---|
|`/ban <jogador> <tempo> <razão>`|Banimento do servidor (permanente ou temporário).|`/ban Paulo 7d Uso de Cheats`|
|`/tempban`|Alias (apelido) de `/ban <jogador> <tempo> <razão>`.||
|`/unban <jogador>`|Remove o banimento de um jogador.|`/unban Paulo`|
|`/mute <jogador> <tempo> <razão>`|Silencia o jogador, impedindo-o de usar o chat (e comandos de chat).|`/mute Pedro 1h Spam`|
|`/unmute <jogador>`|Remove o silêncio.||
|`/warn <jogador> <razão>`|Registra um aviso formal.|`/warn Joao Linguagem Ofensiva`|
|`/kick <jogador> <razão>`|Expulsa o jogador do servidor (ele pode voltar imediatamente).|`/kick Rita Teste de Conexão`|

#### 16.1.2. Gestão de Histórico e Pesquisa

- **`/check <jogador>`:** O comando mais importante para a moderação. Permite que o _staff_ veja o histórico completo de punições, avisos e notas de um jogador.
    
- **`/history <jogador>`:** Semelhante ao `/check`, focado no histórico de punições ativas e expiradas.
    
- **`/banlist`, `/mutelist`:** Exibe listas de jogadores banidos ou silenciados.
    

### 16.2. Razões Predefinidas e Templates

Para garantir consistência, o AdvancedBan permite definir razões de punição predefinidas, muitas vezes no arquivo `config.yml` ou em arquivos de "razões".

- **Benefício:** Reduz o tempo de moderação e garante que a mesma punição seja aplicada pela mesma razão (Ex: "Uso de Cheats" é sempre banimento de 7 dias ou permanente).

|Razão Predefinida|Duração (Exemplo)|
|---|---|
|**Cheating (Trapaça)**|Permanente|
|**Spam**|Mute 30 minutos|
|**Hate Speech (Discurso de Ódio)**|Ban 30 dias|
|**Advertisement (Publicidade)**|Ban Permanente|

### 16.3. Integração com LuckPerms e Web

#### 16.3.1. Permissões (LuckPerms)

É crucial usar o **LuckPerms** (Capítulo 3) para gerenciar quem pode aplicar punições e qual é o nível máximo de punição que ele pode aplicar.

- **Hierarquia:**
    
    - **Moderador:** Apenas `/mute`, `/warn`, `/kick`, `/check`.
        
    - **Admin:** Tudo, incluindo `/ban` e `/tempban`.
        
    - **Dono/Co-Dono:** Tudo, incluindo a gestão de _bans_ de IP.
        
- **Permissão de Bypass:** Garanta que os grupos mais altos (`Admin`, `Dono`) tenham a permissão para não serem punidos por engano (Ex: `advancedban.bypass.ban`).
    

#### 16.3.2. Integração Web (Opcional, mas Profissional)

O AdvancedBan é famoso por sua capacidade de se integrar a uma interface web (_Web Panel_).

- **Função:** Permite que os jogadores vejam publicamente as punições aplicadas (lista de bans), e que o _staff_ gerencie punições de forma remota através de um navegador.
    
- **Requisito:** Requer que o plugin esteja conectado a um banco de dados **MariaDB/MySQL** (Capítulo 4) para armazenar os dados de forma centralizada e acessível pelo painel web.