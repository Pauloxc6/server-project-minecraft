
## Capítulo 12: Aprimoramento da UX - Scoreboards, Hologramas e Mensagens Customizadas

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

Este capítulo foca nos plugins que melhoram a apresentação visual e a imersão do jogador, fornecendo informações essenciais em tempo real.

### 1. Scoreboards (Placar Lateral)

O **Scoreboard** (placar lateral) é um painel fixo que fornece informações dinâmicas ao jogador, como saldo de economia, rank, ping, contagem de jogadores online e tempo de jogo.

- **Plugin Recomendado:** **FastBoard** ou plugins de placar inclusos em gerenciadores de _menus_ (como o **DecentHolograms** ou **PlaceholderAPI**).
    
- **Função:** Ele deve ser leve e atualizar em tempo real, sem causar _lag_.
    

#### ⚙️ Integração com o PlaceholderAPI

A mágica do Scoreboard e da maioria dos plugins de customização está no **PlaceholderAPI (PAPI)**.

- **O que é:** PAPI é uma API de plugin que permite que você use "variáveis" (placeholders) que são substituídas por dados em tempo real.
    
- **Exemplos de Variáveis:**
    
    - `%vault_eco_balance%`: Saldo de dinheiro do jogador (lido do Vault/EssentialsX).
        
    - `%luckperms_prefix%`: Prefixo do grupo do jogador (lido do LuckPerms).
        
    - `%server_online%`: Número de jogadores na rede/servidor.
        

> **Regra:** Quase todos os plugins de customização visual exigem o **PlaceholderAPI** para extrair dados de outros plugins (Economia, Permissões, Estatísticas).

### 2. Hologramas (Holographic Displays)

Hologramas são textos flutuantes 3D no mundo que não são afetados pela física e que podem exibir informações estáticas ou dinâmicas.

- **Plugin Recomendado:** **DecentHolograms** ou **Holographic Displays**.
    
- **Uso Profissional:**
    
    - **Top Rank:** Exibir o top 10 dos jogadores mais ricos ou com mais tempo jogado (usando PAPI).
        
    - **Informações de Portal:** Marcar a entrada de um portal BungeeCord/Velocity.
        
    - **Anúncios:** Colocar anúncios importantes em áreas centrais do Lobby.
        

### 3. Mensagens Customizadas e Chat

O chat é a principal forma de interação, e a formatação profissional é crucial para a legibilidade.

#### A. Formato de Chat (LuckPerms e EssentialsX)

O formato de chat é geralmente definido no **EssentialsX** (ou outro plugin de chat) usando as informações de **Prefixos** e **Meta Dados** do **LuckPerms**.

- O LuckPerms fornece ao EssentialsX: `&7[&aVIP&7] &fJogador:`
    
- O EssentialsX então envia a mensagem com essa formatação.
    

#### B. Anúncios Automáticos (Broadcasts)

É vital manter os jogadores informados sobre regras, eventos e promoções.

- **Plugins Recomendados:** **AutoMessage** ou o módulo de _broadcast_ do EssentialsX.
    
- **Função:** Envia mensagens pré-definidas no chat em intervalos regulares (a cada 5 ou 10 minutos).
    

### 4. Menus Gráficos (GUIs)

Substituir comandos de texto por cliques em um menu de inventário (GUI) melhora drasticamente a usabilidade, especialmente para jogadores novos.

- **Plugins Recomendados:** **ChestCommands** ou **DeluxeMenus**.
    
- **Função:** Cria menus gráficos complexos que podem executar comandos, abrir outras GUIs ou levar o jogador a outro servidor (em redes BungeeCord/Velocity).
    

#### Exemplo de Uso (Menu Principal)

Um Menu Principal pode ter:

|Item no Menu|Ação (Comando Executado)|
|---|---|
|**Bússola**|Leva o jogador para o mundo Survival (`/server survival` se estiver em uma rede).|
|**Baú**|Abre a Loja Gráfica (`/shopguiplus open`).|
|**Cabeça**|Abre o Menu de Perfil (mostrando estatísticas com PAPI).|
