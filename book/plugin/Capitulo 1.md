## Capítulo 1: Introdução aos Plugins

Tags: #estudos #minecraft #linux #sever
Data: 2025-12-06

---

Chegamos na parte mais divertida e interessante dos servidores que tornam ele poderoso.

### 1.1. O que são Plugins? A Definição Profissional

No ecossistema de servidores baseado em PaperMC (que deriva do Spigot/Bukkit), um Plugin é um pequeno módulo de código Java (arquivos .jar) que é executado dentro do processo principal do servidor.

A principal diferença para os Mods é a seguinte:

- Plugins (PaperMC/Spigot/Bukkit): Não exigem nenhuma alteração no cliente (launcher) do jogador. Eles funcionam puramente no lado do servidor e usam a API (Application Programming Interface) do PaperMC para interagir com o jogo e os jogadores.

- Mods (Forge/Fabric): Exigem que o jogador instale o mesmo modpack no seu launcher, pois eles alteram a estrutura fundamental do código do jogo.

Nossa arquitetura (Java, PaperMC) suporta plugins, permitindo que qualquer jogador de Minecraft Vanilla se conecte e aproveite as funcionalidades personalizadas.

### 1.2. Como os Plugins Funcionam (A Interação com a API)

A chave para o funcionamento dos plugins é o Motor PaperMC. O PaperMC expõe uma vasta biblioteca de funções e eventos (a API) que permitem aos desenvolvedores:

1. Manipular Eventos: Capturar ações do jogador (ex: quebrar um bloco, entrar no servidor, digitar um comando).

2. Acessar Dados: Ler e escrever informações do mundo (blocos, entidades) e de jogadores (inventário, saúde).

3. Integrar: Usar APIs de terceiros, como o Vault (para economia) ou o LuckPerms (para permissões), que se tornam acessíveis a outros plugins.

Um plugin de chat, por exemplo, não altera o jogo; ele apenas ouve o evento de envio de mensagem (PlayerChatEvent) e o formata antes que seja exibido na tela de todos os jogadores.

### 1.3. Tipos e Categorias Essenciais de Plugins

No nível profissional, os plugins são categorizados por sua função principal.

|Categoria|Função|Exemplo|
|---|---|---|
|Núcleo (Core/Base)|Fornece comandos básicos, teletransporte e funções administrativas essenciais.|EssentialsX|
|Gerenciamento de Dados|Lida com hierarquia, acessos e armazenamento centralizado de informações.|LuckPerms, Vault|
|Economia|Implementa e gerencia a moeda e as transações financeiras.|EssentialsX Economy, CMI
|Segurança/Auditoria|Protege o mundo contra griefing e trapaças.|WorldGuard, CoreProtect, Anti-Cheats (Grim/Vulcan)|
|Aprimoramento (UX)||Melhora a experiência visual e a usabilidade do jogador.|PlaceholderAPI, DecentHolograms, DeluxeMenus|
|Mundo/Geração|Altera a maneira como o mundo é gerado ou adiciona funcionalidades de terreno.|WorldEdit, FastAsyncWorldEdit|

### 1.4. A Estrutura da Pasta plugins

Ao instalar um plugin, você verá sempre o mesmo padrão:

O Arquivo .jar: O código executável do plugin.

A Pasta de Configuração: Criada pelo plugin na primeira vez que o servidor é iniciado (ou recarregado). É aqui que você encontra e edita os arquivos YAML de configuração.

Exemplo Prático (LuckPerms):

```
/home/minecraft/servidores/survival/plugins/
├── LuckPerms-5.x.x.jar  <-- O arquivo de código
├── WorldEdit-7.x.x.jar
├── EssentialsX-2.x.x.jar
├── LuckPerms/              <-- Pasta de Configuração
│   └── config.yml          <-- Arquivo YAML principal (onde definimos o MariaDB)
│   └── data/               <-- Arquivos de dados (se não usar MariaDB)
└── Essentials/
    └── config.yml
    └── ...
```
