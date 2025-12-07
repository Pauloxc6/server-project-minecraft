## **Capítulo 8: Gerenciamento de Identidade - LuckPerms, Grupos e Permissões**

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

O **LuckPerms** é o plugin de gerenciamento de permissões mais rápido, avançado e escalável disponível no mercado. Por ter sido configurado para usar o MariaDB (Capítulo 6), ele garante que as permissões sejam consistentes em toda a sua rede (seja ela BungeeCord/Velocity ou não).

### 8.1. Por Que Precisamos de Permissões?

Se um jogador recebe a permissão de usar o comando `/heal`, ele pode se curar. O gerenciamento de permissões tem três funções essenciais:

1. **Segurança:** Bloquear comandos destrutivos ou de administração para jogadores comuns.
    
2. **Hierarquia:** Definir o que cada cargo (Membro, VIP, Moderador) pode fazer.
    
3. **Integração:** Controlar acesso a _features_ de plugins de terceiros (ex: só VIPs podem criar mais de 10 _homes_).
    

### 8.2. Conceitos Fundamentais do LuckPerms

Para trabalhar com o LuckPerms, você precisa entender a diferença entre os três elementos principais:

|Elemento|Definição|Exemplo|
|---|---|---|
|**Grupos (Groups)**|O papel ou cargo do jogador. É a maneira profissional de gerenciar a hierarquia.|`membro`, `vip_ouro`, `moderador`.|
|**Permissões (Permissions)**|A regra específica (chave) que o plugin verifica.|`essentials.sethome.multiple.10` (permite 10 homes), `worldguard.region.bypass` (permite ignorar regiões).|
|**Herança (Inheritance)**|A base da hierarquia. Um grupo automaticamente recebe todas as permissões de um grupo que ele herda.|O grupo `vip_ouro` **herda** do grupo `membro`. Assim, Vips recebem automaticamente todas as permissões básicas de um membro.|

### 8.3. A Estrutura de Herança

Você deve sempre criar uma estrutura em que os grupos de _staff_ ou _rankups_ herdem do grupo imediatamente abaixo. .

- O grupo **`default`** (ou `membro`) deve ser o grupo base, com todas as permissões que **qualquer jogador** precisa.
    
- O grupo **`moderador`** deve herdar de `membro` e ter permissões administrativas adicionais.
    

#### Exemplo de Comando (Console)

O LuckPerms é gerenciado primariamente pela console do servidor (ou via interface web, que veremos mais adiante).

1. **Criar o Grupo Moderador:**

```minecraft
/lp creategroup moderador
```

2.  **Definir Herança (Hierarquia):** O Moderador herda do Membro.

```minecraft
/lp group moderador parent add membro
```

3. **Adicionar Permissão:** Dar ao Moderador o poder de usar o comando `/fly`.

```minecraft
/lp group moderador permission set essentials.fly true
```

4. **Adicionar Prefixo:** Definir como o nome do Moderador aparecerá no chat.

```minecraft
/lp group moderador meta setprefix "&c[Mod] &f"
```

5. Adicionar um Usuário ao Grupo:

```minecraft
/lp user [Nome do Jogador] parent set moderador
```

### 8.4. O Uso de Contextos e Meta Dados

Para um controle ainda mais fino, o LuckPerms usa:

- **Contextos:** Permissões que só se aplicam sob certas condições.
    
    - _Exemplo:_ Você pode dar a permissão de `/fly` **apenas** no mundo "Lobby". (Contexto: `world=lobby`).
        
- **Meta Dados:** Informações extras anexadas ao grupo.
    
    - _Exemplo:_ O **Prefixo** e o **Sufixo** (tags de chat) são meta dados. A **Prioridade** é um meta dado que define qual prefixo aparece se um jogador pertencer a mais de um grupo.
        

> **Dica Profissional (Editor Web):** Para gerenciar centenas de permissões, use o **Editor Web** do LuckPerms: rode `/lp editor` no jogo. Ele gera um link que abre uma interface gráfica no seu navegador para editar tudo com segurança. Ao terminar, cole o comando gerado de volta no console.

---

Com o gerenciamento de permissões instalado e configurado via MariaDB, você pode agora integrar todos os sistemas que dependem dele, como a economia e as lojas.

> **Nota:** Vou disponibilizar uma lista permissões essências, básicas e universais para qualquer servidor deve está disponível em [plugins/config/luckperms]