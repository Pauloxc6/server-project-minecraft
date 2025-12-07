Tags: #estudos #minecraft #linux #sever
Data: 2025-12-06

---
## Capítulo 2: WorldEdit e WorldGuard (Gerenciamento e Proteção de Mundo)

**Tags:** #plugins #administração #worldedit #worldguard

Para que o seu servidor profissional tenha uma estética atraente (Lobby, Spawn) e seja seguro contra destruição (**griefing**), você precisará de duas ferramentas que trabalham em conjunto: **WorldEdit** e **WorldGuard**.

### 2.1. WorldEdit: A Ferramenta de Edição de Mundo

O WorldEdit é o editor de mundo fundamental, usado exclusivamente por administradores e construtores. É uma ferramenta de produtividade que transforma horas de construção em minutos.

- **Função:** Manipular grandes áreas de blocos rapidamente.
    
- **Requisitos:** Nenhuma. É um plugin autônomo, mas é o requisito para o WorldGuard funcionar.
    
- **Como Usar:** Usa uma ferramenta de seleção (geralmente um **Machado de Madeira** por padrão) para definir uma área e comandos para preencher, substituir ou gerar formas.
    

#### 2.1.1. Comandos Essenciais (Console de Jogador)

|Comando|Função|Exemplo|
|---|---|---|
|`//wand`|Recebe o Machado de Madeira (ferramenta de seleção).|`//wand`|
|`//hpos1` / `//hpos2`|Define o ponto 1 e 2 com base no bloco que você está olhando.|`//hpos1`|
|`//pos1` / `//pos2`|Define o ponto 1 ou 2 na sua localização atual.|`//pos1`|
|`//sel clear`|Limpa a seleção atual.|`//sel clear`|
|`//set <bloco>`|Preenche a área selecionada com um bloco específico.|`//set stone`|
|`//replace <antigo> <novo>`|Substitui um tipo de bloco por outro na seleção.|`//replace sand glass`|
|`//undo`|Desfaz a última ação (salva o seu mundo de erros!).|`//undo`|

### 2.2. WorldGuard: O Sistema de Proteção

O WorldGuard é o sistema de segurança que protege áreas específicas do seu mundo contra _griefing_, explosões de TNT, fogo e outras interações indesejadas. Ele depende do WorldEdit para definir as coordenadas das áreas a serem protegidas.

- **Função:** Criar regiões (_regions_) no mundo com regras (**flags**) personalizadas.
    
- **Requisitos:** WorldEdit (deve estar instalado na pasta `plugins/`).
    

#### 2.2.1. O Processo de Criação e Gestão de Região

1. **Selecionar a Área:** Use o WorldEdit (`//wand` ou `//hpos`) para selecionar a área que você deseja proteger.
    
2. **Definir a Região:** Nomeie e salve a região selecionada.
    
    ```
    /rg define nome_da_regiao
    # Exemplo: /rg define spawn_principal
    ```
    
3. **Adicionar Proprietários:** Proprietários têm controle total sobre a região.
    
    ```
    /rg addowner <nome-da-regiao> <jogador>
    ```
    
4. **Gerenciar Membros:** Membros podem interagir na região, mas não têm controle total.
    
    - Adicionar Membro: `/rg addmember <nome-da-regiao> <jogador>`
        
    - Remover Membro: `/rg removemember <nome-da-regiao> <jogador>`
        

#### 2.2.2. Gerenciar Grupos do LuckPerms em Regiões

A integração com o LuckPerms (Capítulo 8) permite que você defina permissões por grupo, e não por jogador individual.

|Ação|Comando|
|---|---|
|**Adicionar Grupo (Ex: `builders`)**|`/rg addmember <nome-da-regiao> g:<nome-do-grupo>`|
|**Remover Grupo (Ex: `membro`)**|`/rg removemember <nome-da-regiao> g:<nome-do-grupo>`|

#### 2.2.3. Flags Essenciais para Servidores

Flags controlam o que é permitido ou proibido dentro da região. O valor pode ser `deny` (negar), `allow` (permitir) ou `none` (padrão).

|Flag|Função|Comando de Exemplo|
|---|---|---|
|`build`|Impede jogadores de quebrar ou colocar blocos. **Essencial para spawns/lobbies.**|`/rg flag spawn_principal build deny`|
|`pvp`|Controla se o combate entre jogadores é permitido.|`/rg flag arena_pvp pvp allow`|
|`tnt`|Controla se a explosão de TNT está ativa.|`/rg flag mina_vip tnt deny`|
|`mob-spawning`|Controla o _spawn_ natural de mobs.|`/rg flag spawn_principal mob-spawning deny`|
|`greeting`|Mensagem exibida quando um jogador entra na região.|`/rg flag spawn_principal greeting "Bem-vindo ao Lobby!"`|

### 2.3. Integração e Segurança (Auditoria e Informação)

Além da proteção, o WorldGuard ajuda na auditoria e no controle do console.

- **Verificar Propriedades da Região:**

```
    /rg info <nome-da-regiao>
    # Mostra proprietários, membros, grupos e flags ativas.
```

- **Controle de Logs (Gamerule):** Para evitar que mensagens de comando de _Command Blocks_ poluam o chat do administrador:

   ```
    /gamerule sendCommandFeedback false
    # Use 'true' para reativar o feedback visual de comandos no chat.
Com o mundo protegido e pronto para construção, o próximo passo crucial é definir quem pode fazer o quê no seu servidor, que é o domínio do LuckPerms.
