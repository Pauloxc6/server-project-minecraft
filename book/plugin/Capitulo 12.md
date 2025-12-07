
## **Capítulo 12: Análise Aprofundada – Configurando o Plugin TAB para Estética e Rede** 📊

**Tags:** #tab #configuração_avançada #sorting #scoreboard #hex_colors #animações

---

O plugin **TAB** funciona como um centro de exibição de dados. Sua principal vantagem é a capacidade de usar cores hexadecimais, animações e lógica condicional (_if/then_) para mostrar informações diferentes a diferentes jogadores ou em diferentes mundos.

### 12.1. Header & Footer (Cabeçalho e Rodapé)

Esta seção define o topo e a base da Lista de Jogadores. Sua configuração utiliza formatação avançada:

|Linha na Configuração|Análise Profissional|
|---|---|
|`header: - "<#FFFFFF>&m-----------..."`|**Cores Hexadecimais (`<#FFFFFF>`)**: Permitem cores personalizadas que o código `&` não suporta, tornando a estética superior. O `&m` (riscado) é usado para criar uma linha divisória.|
|`- "&r&7&l>> %animation:Welcome%&3 &l%player%&7&l! &7&l<<"`|**Animações (`%animation:Welcome%`)**: Indica que o plugin está configurado para executar sequências de texto dinâmico (animações), o que aumenta muito o engajamento visual.|
|`disable-condition: '%world%=disableworld'`|**Condições de Desativação**: Permite desativar o Header/Footer em mundos específicos (Ex: mundos de Minigames ou mundos de _build_), economizando recursos.|
|`per-server` / `per-world`|**Suporte a Redes (Bungee/Velocity)**: Permite que o MOTD e a formatação sejam diferentes se o jogador estiver no servidor `server1` (Lobby) ou no mundo `world1` (Survival).|
### 12.2. Formatação de Nomes e Tags

Esta seção garante que o **Prefixos/Sufixos do LuckPerms** (Capítulo 3) sejam exibidos corretamente na lista e acima da cabeça do jogador.

- **`tablist-name-formatting`**: Controla o nome exibido na lista TAB. O `anti-override: true` é crucial, pois impede que outros plugins tentem sobrescrever a formatação do TAB.
    
- **`scoreboard-teams`**: Controla as _Name Tags_ (o texto que flutua sobre o jogador).
    
    - **`enable-collision: true`**: Permite que a colisão de entidades seja controlada por este plugin (geralmente usado em servidores de Minigames para controlar a passagem de jogadores).
        

### 12.3. Ordenação Profissional (Sorting)

A seção de `scoreboard-teams` contém a configuração mais importante para a hierarquia do servidor.

- **`sorting-types: - "GROUPS:owner,admin,mod,helper,builder,vip,default"`**: Esta linha é o que garante que os jogadores sejam ordenados na lista TAB por sua importância. A ordem listada (`owner` primeiro, `default` por último) dita quem aparece no topo da lista.
    
- **Integração LuckPerms:** O plugin TAB consulta o LuckPerms para determinar o grupo do jogador e aplica essa regra de ordenação.
    

### 12.4. Scoreboards Condicionais (Scoreboard Lateral)

O plugin TAB permite múltiplos _scoreboards_ laterais, exibindo diferentes informações dependendo do _rank_ ou da localização do jogador.

- **`scoreboards:` / `default`**: O painel padrão, exibido para a maioria dos jogadores.
    
    - **`display-condition: '%group%=default'`**: Garante que apenas jogadores do grupo `default` (membro) vejam este painel.
        
    - Exibe dados gerais como coordenadas, online e `TPS` (Ticks por Segundo).
        
- **`scoreboards:` / `admin_panel`**: O painel de alto valor para o _staff_.
    
    - **`display-condition: '%group%=admin'`**: Garante que apenas o _staff_ veja este painel.
        
    - **Informações Críticas**: Exibe dados de performance do servidor (`TPS`, `MSPT`, `RAM`) que o _staff_ precisa monitorar em tempo real.
        
    - **Placeholders Avançados**: `%memory-used-gb%`, `%tps%`, `%mspt%` são cruciais para o monitoramento de saúde do servidor (Capítulo 14).
        

### 12.5. Otimização de Placeholders

O TAB é um plugin que consome muitos recursos se configurado incorretamente, pois ele atualiza o texto de milhares de _placeholders_ a cada segundo. A seção `placeholderapi-refresh-intervals` controla isso.

|Placeholder|Intervalo de Atualização (ms)|Análise Profissional|
|---|---|---|
|`default-refresh-interval`|`500` (0.5s)|O padrão para a maioria dos dados.|
|`%player_health%`|`200`|Atualiza a vida do jogador muito rapidamente (a cada 0.2s), necessário para combate.|
|`%server_unique_joins%`|`5000` (5s)|Atualiza dados menos críticos (como a contagem de jogadores únicos) a cada 5 segundos, economizando recursos.|
### 12.6. Configurações de Rede (Proxy Only)

A seção **PROXY ONLY** confirma que este plugin deve ser instalado no BungeeCord/Velocity para funcionar corretamente em toda a rede.

- **`global-playerlist: enabled: true`**: Essencial para redes. Permite que o jogador veja todos os outros jogadores da rede (em todos os sub-servidores), e não apenas os jogadores no servidor local.
    
- **`enable-redisbungee-support: true`**: Se você estiver usando **RedisBungee** (necessário para redes grandes com múltiplos proxies BungeeCord), esta opção deve estar ativa para garantir que todos os jogadores sejam contabilizados.