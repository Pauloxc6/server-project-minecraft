## **Capítulo 11: Segurança e Experiência do Usuário (UX) - ProAntiTab e Controle de Comandos** 🚫

**Tags:** #proantitab #segurança #comandos #ux #whitelist

---

O risco de segurança mais comum em servidores de Minecraft é a descoberta de comandos sensíveis por jogadores não autorizados. Quando um jogador pressiona a tecla **TAB** no chat, o cliente do Minecraft solicita ao servidor uma lista completa de comandos disponíveis. O plugin **ProAntiTab** (ou equivalente) intercepta esse pedido.

### 11.1. O Conceito de Whitelist de Comandos

O arquivo `storage.yml` (ou similar) do ProAntiTab define uma **Whitelist** de comandos — ou seja, uma lista de comandos que **são permitidos** na sugestão de preenchimento automático (Tab-Completion).

O bloco `global:` que você forneceu representa essa _whitelist_:

```yaml
global:
  commands:
    - afk
    # ... comandos permitidos ...
    - plugins
    - version
    - ping
```

#### 11.1.1. A Regra de Ouro (Segurança Máxima)

1. **Bloqueio Total por Padrão:** O ProAntiTab deve estar configurado para **bloquear** todas as sugestões de comando por padrão (exceto para o `staff`).
    
2. **Whitelist Mínima:** A lista de comandos (`- afk`, `- home`, `- tpa`, `- pay`, etc.) deve conter **APENAS** os comandos que o jogador `default/membro` tem permissão para usar e que o _staff_ precisa ver rapidamente.
    
3. **Remoção de Comandos Sensíveis:** Se o seu servidor for _BungeeCord/Velocity_, comandos como `/glist`, `/server` ou comandos de _proxy_ não devem estar nesta lista para evitar que o jogador descubra o nome de todos os seus sub-servidores.
    

### 11.2. Tratamento de Comandos Críticos (`/plugins` e `/version`)

Comandos como `/plugins` e `/version` são nativos do Spigot/PaperMC e revelam informações cruciais sobre o _backend_ do servidor.

#### 11.2.1. Estratégia de Segurança

Embora você tenha listado `/plugins` e `/version` no `storage.yml`, isso por si só não os torna seguros. A segurança deve ser tratada em duas frentes:

1. **ProAntiTab (Ocultação):** Coloque `/plugins` e `/version` na _whitelist_ do ProAntiTab **apenas** para que o **staff** consiga usá-los com facilidade (eles não serão bloqueados pelo sistema).
    
2. **LuckPerms (Permissão):** **Negue** explicitamente a permissão de acesso a esses comandos para o grupo `default` e conceda-a apenas aos grupos `Admin` e `Dono` no **LuckPerms** (Capítulo 3).

|Comando|Permissão para Negar (Membro)|Permissão para Conceder (Admin)|
|---|---|---|
|`/plugins`|`bukkit.command.plugins` ou `essentials.plugins` (se sobrescrito)|`bukkit.command.plugins`|
|`/version`|`bukkit.command.version`|`bukkit.command.versio`|

> **Conclusão:** O ProAntiTab **oculta** o comando na sugestão; o LuckPerms **nega** a execução, mesmo que o jogador adivinhe o nome do comando.

### 3. Melhorando a Experiência do Usuário (UX)

O ProAntiTab também ajuda a manter a lista de comandos limpa para o jogador comum, facilitando a vida dele e reduzindo o _spam_ visual.

- **Limpeza:** Garanta que todos os comandos de _vanity_ (ex: `/sit`, `/crawl`, `/lay`) que você listou estejam com a permissão correta no LuckPerms para evitar frustrações.
    
- **Evitando _Lags_:** Listas de _tab-completion_ muito longas podem causar pequenos _lags_ em conexões mais lentas. O ProAntiTab ajuda a manter essa lista curta.

### Exemplo de config

```yaml
global:
  commands:
    - afk
    - back
    - balance
    - balancetop
    - pay
    - ping
    - tpa
    - tpacancel
    - tpaccept
    - crawl
    - kick
    - lay
    - pose
    - sit
    - spin
    - plugins
    - version
    - ping
    - login
    - register
    - logout

groups:
  examplegroup:
    priority: 1
    commands:
      - tell
      - msg

```