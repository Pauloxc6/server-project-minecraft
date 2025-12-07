## **Capítulo 5: Segurança Máxima - Implementando CoreProtect e Sistemas Anti-Cheat** 🛡️

**Tags:** #segurança #coreprotect #anti-cheat #auditoria

---

A segurança de um servidor profissional se divide em duas partes: a **segurança de infraestrutura** (Firewall UFW, `systemd`, Capítulos 1 e 5 do báscio) e a **segurança de dados e jogabilidade** (Plugins). Esta última é onde o **CoreProtect** e os sistemas **Anti-Cheat** entram.

### 5.1. CoreProtect: O Sistema de Auditoria (Rollback)

O CoreProtect é o seu melhor amigo contra _griefing_ e abuso de _staff_. Ele é um plugin de auditoria que rastreia absolutamente todas as interações no seu mundo: colocação de blocos, quebra, uso de TNT, abertura de baús, interações com mobs, e muito mais.

#### 5.1.1. Conexão e Armazenamento (MariaDB)

Assim como o LuckPerms, o CoreProtect **deve** usar o MariaDB (Capítulo 6) como método de armazenamento.

- **Por quê?** Armazenar milhões de registros de bloco em arquivos do servidor é lento e insustentável. Usar o MariaDB garante que as consultas de auditoria sejam ultrarrápidas e que os dados sejam centralizados.
    
- **Configuração:** Edite o `config.yml` do CoreProtect para `database: mysql` e forneça suas credenciais do MariaDB.
    

#### 5.1.2. Comandos Essenciais de Auditoria

O principal comando do CoreProtect é o `/co i` (Inspect), mas os comandos de reversão (_rollback_) são vitais.

|Comando|Função|Exemplo|
|---|---|---|
|`/co i`|**Inspecionar (Toggle)**. Habilita o modo de inspeção (clique em um bloco para ver quem o colocou/quebrou).|`/co i`|
|`/co rollback u:<jogador> t:<tempo>`|**Reverter ações de um jogador** até um certo tempo.|`/co rollback u:Zezinho t:1h`<br><br>  <br><br>(Desfaz tudo que o Zezinho fez na última hora)|
|`/co restore r:<raio> t:<tempo>`|**Restaurar uma área** que foi destruída.|`/co restore r:10 t:1d`<br><br>  <br><br>(Restaura uma área de 10 blocos de raio como era há 1 dia)|
|`/co lookup a:<ação> t:<tempo>`|**Buscar** por uma ação específica.|`/co lookup a:break t:3h`<br><br>  <br><br>(Lista todos os blocos quebrados nas últimas 3 horas)|

> **Observação:** O parâmetro `t:` (tempo) pode ser em segundos (`s`), minutos (`m`), horas (`h`), dias (`d`) e semanas (`w`).

### 5.2. Sistemas Anti-Cheat (Monitoramento de Jogabilidade)

Enquanto o CoreProtect lida com o mundo (blocos e baús), os Anti-Cheats lidam com a jogabilidade (voo, _speed_, _killaura_). Um bom Anti-Cheat deve ter baixo impacto na performance e alto grau de precisão.

- **Função:** Detectar comportamentos que violam a física do jogo ou interações automáticas (_bots_).
    
- **Escolha:** Plugins como **Grim Anti-Cheat** ou **Vulcan** são opções populares para PaperMC, oferecendo _checks_ (verificações) robustas e poucas detecções falsas (false positives).

#### 5.2.1. Gerenciamento Prático

1. **Instalação:** Baixe o `.jar` do Anti-Cheat e coloque-o na pasta `plugins/`.
    
2. **Configuração:** Edite o `config.yml` para ajustar o nível de sensibilidade (`sensitivity`) e as ações automáticas (kick/ban).
    
3. **Permissões:** Use o **LuckPerms** (Capítulo 3) para garantir que apenas o `staff` tenha a permissão de ver os alertas (ex: `anticheat.alerts`).
    

### 5.3. Sinergia de Segurança

A força da sua segurança reside na interação entre os plugins:

1. **WorldGuard (Capítulo 2):** Impede a destruição em áreas críticas (Lobbies).
    
2. **Anti-Cheat:** Pega o jogador em flagrante usando _cheats_.
    
3. **CoreProtect:** Se o jogador passar pelo Anti-Cheat, o CoreProtect permite a você rastrear, provar o _griefing_ e reverter o dano em segundos.