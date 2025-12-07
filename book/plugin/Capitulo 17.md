## **Capítulo 19: Engajamento Social - Sistema de Times/Guildas (BetterTeams)** 🤝

**Tags:** #betterteams #guildas #times #social #gameplay #engajamento

---

Servidores de sucesso se baseiam em comunidades. O **BetterTeams** facilita a criação de grupos de jogadores com recursos próprios, promovendo competição e colaboração, o que retém jogadores por mais tempo.

### 17.1. Funcionalidades Principais dos Times

O plugin centraliza recursos sociais e de _gameplay_ em um sistema gerenciável.

|Funcionalidade|Benefício para o Jogador|
|---|---|
|**Chat de Time Privado**|Comunicação coordenada sem _spam_ no chat global.|
|**Home de Time**|Um local de teletransporte comum para todos os membros (ponto de encontro).|
|**Economia Compartilhada**|Um saldo bancário de time (integra-se ao Vault/EssentialsX, Capítulo 4).|
|**Conquistas e Estatísticas**|Promove a competição saudável e _grinding_ (moagem).|
|**Gerenciamento de Membros**|Sistema de _ranks_ interno (Líder, Co-Líder, Membro).|

### 17.2. Comandos Essenciais para o Jogador

O sistema deve ser intuitivo, com comandos simples para as ações mais comuns.

|Comando|Função|
|---|---|
|`/teams create <nome>`|Cria um novo time (geralmente com um custo em dinheiro, integrado ao Vault).|
|`/teams invite <jogador>`|Convida um jogador a se juntar.|
|`/teams accept/deny`|Aceita ou recusa um convite.|
|`/teams kick <jogador>`|Expulsa um membro do time (apenas Líderes/Co-Líderes).|
|`/teams home`|Teleporta para a casa do time.|
|`/teams deposit <valor>`|Deposita dinheiro no banco do time.|
|`/teams list`|Lista todos os times ou o ranking deles.|
### 17.3. Integração Profissional com Outros Plugins

O BetterTeams brilha quando integrado com a infraestrutura existente, especialmente com as configurações que você já definiu.

#### 17.3.1. Integração com o TAB (Capítulo 14)

Se você observar a configuração do plugin TAB:

- **Placeholder:** O TAB usa o _placeholder_ `%betterteams_name%` para exibir o nome do time (ou guilda) do jogador no _scoreboard_ lateral.
    
- **Benefício:** Isso mantém a afiliação do jogador constantemente visível, incentivando a identidade de grupo.
    

#### 17.3.2. Integração com o LuckPerms (Capítulo 3)

Embora o BetterTeams tenha um sistema de _ranks_ interno (Líder, Membro), a integração com o LuckPerms pode ser usada para dar permissões específicas a membros do time.

- **Exemplo de Permissão:** Você pode configurar uma permissão no LuckPerms que só se aplica se o jogador for um **Membro do Time** (Ex: `betterteams.member.fly` no mundo da _Team Home_).
    

#### 17.3.3. Banco de Dados e Escalabilidade

- **Armazenamento:** Para garantir que todos os dados do time (membros, banco, home) sejam persistentes e seguros, o BetterTeams deve estar configurado para usar o **MariaDB/MySQL** (Capítulo 4) e não arquivos locais (`.yml`).