
## Capítulo 10: Segurança Máxima - Implementando um Sistema Anti-Cheat e de Log (CoreProtect)

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

A segurança de um servidor é uma combinação de prevenção (Anti-Cheat) e recuperação (Auditoria/Log).

### 10.1. Prevenção: Anti-Cheat

Um **Anti-Cheat** é um plugin que monitora as ações dos jogadores em tempo real, detectando padrões que não são possíveis no Minecraft padrão (Ex: Super Velocidade, Voo, Ataque a longas distâncias).

#### 10.1.1. A Escolha do Anti-Cheat

Anti-cheats são notoriamente difíceis de configurar, pois precisam de um equilíbrio perfeito: detectar trapaceiros sem penalizar jogadores com conexões ruins (_falsos positivos_).

|Anti-Cheat|Categoria|Vantagem|Desvantagem|
|---|---|---|---|
|**Spartan / Vulcan**|Pago/Premium|Alta precisão, atualizações frequentes e suporte dedicado.|Custo de aquisição e necessidade de configuração avançada.|
|**NoCheatPlus (NCP)**|Gratuito/Open Source|Estável e amplamente utilizado, ótimo para iniciar.|Menos eficaz contra clientes de trapaça modernos.|
|**Grim AntiCheat**|Gratuito|Moderno e com bom desempenho.|Pode exigir mais ajustes finos para evitar _falsos positivos_.|

**Dica:** Um bom anti-cheat não deve apenas banir; ele deve **cancelar** a ação (ex: o jogador tenta voar, mas é puxado de volta) e notificar a equipe de _staff_ para que a decisão de banimento seja humana.

#### 10.1.2. A Otimização do Servidor é a Prioridade

O Anti-Cheat confia na integridade do servidor. Se o seu **TPS (Ticks Per Second)** estiver baixo (abaixo de 18, por exemplo), o Anti-Cheat pode ter dificuldades em monitorar a física do jogo e pode começar a gerar muitos _falsos positivos_.

- **Regra de Ouro:** **Sempre** otimize os arquivos `spigot.yml` e `paper.yml` (Capítulo 4) antes de instalar um Anti-Cheat.
### 10.2. Recuperação: Log de Ações e Auditoria

Por mais sofisticado que seja o Anti-Cheat, o _griefing_ e as ações destrutivas (seja por um _cheater_ ou um _staff_ abusivo) sempre ocorrerão. É aí que entra a auditoria.

#### CoreProtect: O Padrão de Auditoria

O **CoreProtect** é o plugin padrão da indústria para log de ações. Ele rastreia e registra no seu **MariaDB** (ou em arquivos leves, embora o uso do MariaDB seja recomendado para grandes volumes de dados) cada ação de construção, destruição, uso de balde, colocação de placa, etc. .

#### 10.2.1. Comandos Essenciais do CoreProtect

O CoreProtect permite dois tipos de ações: **Consulta (Lookup)** e **Reversão (Rollback)**.

1. **Consulta (`/co i`):** Usando o comando `/co i` (_inspect_), você ativa um modo de inspeção. Ao clicar com o botão direito ou esquerdo em um bloco, o plugin mostra quem interagiu com ele por último e quando.
    
2. **Consulta por Raio (`/co l`):** Lista todas as ações em uma área.

```minecraft
/co l t:5h r:10 user:traidor a:break b:stone
# Lookup (l) - 5 horas atrás (t:5h) - raio de 10 blocos (r:10) - pelo usuário 'traidor' - quebrou (a:break) - blocos de pedra (b:stone)
```

3. **Reversão (Rollback):** Desfaz todas as ações destrutivas.

```minecraft
/co rollback t:1h r:50 user:griefer
# Reverte (rollback) as ações do usuário 'griefer' - em um raio de 50 blocos (r:50) - feitas na última 1 hora (t:1h).
```

> **Atenção (Rollback):** Use o comando `/co restore` para reverter um `rollback`. Nunca execute um `rollback` sem ter certeza da área e do tempo, pois é uma ação que modifica o mundo.

### 10.3. Log de Comandos e Staff

Além do CoreProtect, é crucial registrar **todos os comandos** usados pelos _staffs_ (moderadores, administradores). Muitos plugins de log (como o EssentialsX ou alguns Anti-Cheats) têm essa funcionalidade embutida, garantindo que você tenha um registro de quando um Moderador usou `/ban`, `/op` ou `/give`.

