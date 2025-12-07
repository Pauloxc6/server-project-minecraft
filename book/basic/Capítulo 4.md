
## Capítulo 4: Configuração Essencial do Servidor (YAML, Performance e Segurança Básica)

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

Agora que a base teórica e o motor (Java/PaperMC) estão instalados, vamos mergulhar na **configuração fina** que transforma um JAR simples em um servidor de alto desempenho.

### 1. Dominando a Linguagem YAML

Quase todos os arquivos de configuração do Minecraft e de seus plugins (como `server.properties`, `bukkit.yml`, `spigot.yml` e todos os arquivos de plugins) utilizam a sintaxe **YAML** (YAML Ain't Markup Language).

O YAML é uma linguagem de serialização de dados (assim como JSON e XML), mas focada em ser **legível por humanos**.

---

#### ⚙️ Regras Fundamentais do YAML

- **Pares Chave-Valor:** A estrutura básica é sempre uma chave seguida por dois pontos e um valor.

```yml
chave: valor
```

- **Hierarquia (Indentação):** A estrutura de pastas é representada por **espaços em branco** (nunca use Tab). A hierarquia define como os dados se relacionam.

```yml 
performance:
  max-players: 100  # O valor 100 está aninhado sob a chave 'performance'
  view-distance: 6
```

**Listas (Arrays):** Representadas por um hífen e um espaço (`-` ).

```yaml
cores_permitidas:
  - preto
  - branco
  - azul
```

**Atenção:** Erros de **indentação** ou **espaçamento** são a causa número um de falhas na inicialização de servidores e plugins

### 2. Configurações Críticas de Performance

Vamos otimizar três arquivos principais para garantir o melhor TPS no seu servidor PaperMC.

#### 2.1. `server.properties`

Este arquivo é o padrão da Mojang e tem o papel mais básico.

| Chave           | Valor Sugerido           | Descrição                                                                                                  |
| --------------- | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| `motd`          | Seu texto de boas-vindas | Mensagem do dia que aparece na lista de servidores.                                                        |
| `online-mode`   | `true` (recomendado)     | Se `true`, só permite jogadores com contas Minecraft originais (proteção contra pirataria).                |
| `max-players`   | 100 (ajustável)          | Limite máximo de jogadores.                                                                                |
| `view-distance` | 6 (máximo)               | **CRÍTICO PARA PERFORMANCE.** Distância de renderização. Abaixo de 8 reduz drasticamente o consumo de CPU. |
#### 2.3. `spigot.yml`

Este arquivo é criado pelo PaperMC e herda configurações do Spigot.

|Seção|Chave|Valor Sugerido|Descrição|
|---|---|---|---|
|`world-settings`|`entity-activation-range`|Reduza os valores padrão|Define a distância para entidades (animais, monstros) serem "ativas". Reduzir isso economiza CPU.|
|`world-settings`|`mob-spawn-range`|6|Reduza o raio de _spawn_ de mobs para que o servidor não perca tempo spawnando longe dos jogadores.|

#### 2.4. `paper.yml`

Este é o arquivo mais importante, contendo as otimizações exclusivas do PaperMC.

| Seção            | Chave                           | Valor Sugerido | Descrição                                                                                                     |
| ---------------- | ------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------- |
| `world-settings` | `max-auto-save-chunks-per-tick` | 8 (padrão 24)  | Reduzir isso torna a gravação do mundo para o disco mais suave, evitando pequenos travamentos (_lag spikes_). |
| `world-settings` | `max-entity-collisions`         | 2              | Limita quantos _entidades_ podem colidir ao mesmo tempo (evita lag quando mobs ou itens ficam agrupados).     |
| `tick-rates`     | `spawner`                       | 1 (padrão 1)   | Deixar este valor baixo (1) é vital para farmagens de mobs e fazendas de ferro funcionarem corretamente.      |

---
### 3. Segurança Básica (Firewall)

Um servidor profissional no Linux deve ter um firewall ativo para proteger o IP do seu VPS. Usaremos o **UFW (Uncomplicated Firewall)**, uma ferramenta padrão no Ubuntu/Debian.

1. **Bloquear tudo por padrão:**

```bash
sudo ufw default deny incoming
```

2. **Permitir SSH (Acesso ao Linux):** Necessário para você se conectar.

  ```bash
  sudo ufw allow 22
  ```

**Obs:** Eu gosto de sempre de mudar portas administrativas com ssh para outra mais alta, para evitar scripts automatizados que varrem a internet procurando por servidores vulneráveis. Não é 100% de garantia para já evita o ataque padrão.

3. **Permitir a Porta do Minecraft:** O padrão é 25565.

```bash
sudo ufe allow 25565
```

4.  Ativar o Firewall:

 ```bash
 sudo ufw enable
 ```
---
  
  Vou disponibilizar um script que eu mesmo desenvolvi para facilitar mais ainda o setup inicial do estara disponivel em [scripts/fw/fw.sh]

---
