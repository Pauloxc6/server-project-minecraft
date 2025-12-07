## **Capítulo 10: Primeira Impressão - MOTD, Ícones e Limites de Jogador** 🖥️

**Tags:** #motd #primeira_impressão #server_list #configuração_visual

---

A **MOTD (Message of the Day)** e o Ícone do Servidor são os dois fatores que decidem se um jogador aleatório na lista de servidores irá clicar no seu. Gerenciar esses elementos é crucial para o _marketing_ do seu servidor.

O trecho de configuração que você forneceu é o ponto de controle para essa primeira impressão.

### 9.1. Configurando o MOTD (Message of the Day)

A MOTD é a mensagem que aparece em duas linhas sob o nome do seu servidor na lista de _multiplayer_ do Minecraft.

#### 9.1.1. Estrutura e Formatação do MOTD

O formato usa a sintaxe de cores do Minecraft que já exploramos no Capítulo 9.

|Configuração YAML|Descrição|Análise da sua Configuração|
|---|---|---|
|`Line-1`|A primeira linha do MOTD. Ideal para o nome do servidor, usando formatação forte.|`&b&l&m-----------[&r&6&l Calabressos &b&l&m]-----------` (Usa Negrito `&l` e Risca `&m` para um efeito visual forte).|
|`Line-2`|A segunda linha. Ideal para informações dinâmicas ou o site.|`&e&lWebsite &fcalabressos.aternos.me` (Destaca a palavra "Website" em amarelo Negrito `&e&l`).|
> **Dica de Formatação:** O código `&r` (Resetar) é crucial. No seu exemplo, ele é usado antes de `&6&l Calabressos` para garantir que o texto `Calabressos` não fique riscado, resetando o estilo `&m` da seção anterior.

#### 9.1.2. Placeholders Dinâmicos no MOTD

Para exibir dados em tempo real na lista de servidores (como o número de jogadores online ou a versão do servidor), você pode usar o **PlaceholderAPI (PAPI)** (Capítulo 8) no MOTD, se o plugin for compatível.

- **Exemplo de Linha 2 com PAPI:**

```yaml
Line-2: '&aOnline: &f%server_online% &7/ %server_max_players%'
```

### 9.2. Ícone Personalizado (`Custom-Server-Icon`)

O Ícone é a imagem 64x64 que aparece à esquerda na lista. É o seu logo.

| Configuração YAML        | Descrição                                                                    |
| ------------------------ | ---------------------------------------------------------------------------- |
| `Enabled: false`         | Se definido como `true`, o plugin irá procurar pelo arquivo definido abaixo. |
| `Image: server-icon.png` | O nome do arquivo PNG.                                                       |
> **Requisito Técnico:** A imagem **DEVE** ter exatamente **64 x 64 pixels** e estar no formato **PNG**. Se as dimensões ou o formato estiverem errados, o ícone não será carregado e poderá aparecer um X vermelho. O arquivo deve ser colocado na pasta raiz do servidor (junto com o `paper.jar`).

### 9.3. Mensagem de Boas-Vindas (`JoinGame-MOTD`)

Esta mensagem é diferente do MOTD principal, pois aparece no chat do jogador _após_ ele entrar no servidor.

| Configuração YAML | Descrição                                                 |
| ----------------- | --------------------------------------------------------- |
| `Enabled: true`   | Ativa a mensagem.                                         |
| `Messages:`       | Uma lista (`-`) de strings. Você pode usar várias linhas. |

```yaml
Messages:
  - '&eBem Vindo ao servidor, &a%player_name%.' # Usando Placeholder do Essentials/PAPI
  - '&7Digite /regras para ver as normas.'
```

> **Integração PAPI:** Conforme a nota no seu arquivo, as mensagens suportam o **PlaceholderAPI** (Capítulo 8). É altamente recomendável usar _placeholders_ aqui (como `%luckperms_group%` ou `%vault_eco_balance%`) para personalizar a mensagem de boas-vindas.

### 9.4. Limite Máximo de Jogadores (`Server-Maximum-Players`)

Embora o limite de jogadores seja primariamente definido no arquivo `server.properties` do Vanilla, alguns plugins de MOTD permitem que você o **sobrescreva** para fins de exibição.

|Configuração YAML|Descrição|
|---|---|
|`Modify: true`|Ativa a modificação.|
|`Maximum-Players: 20`|O valor que será exibido na lista de servidores (pode ser diferente do valor real no `server.properties`).|
> **Dica de Marketing:** Muitos servidores definem o limite para um número alto (ex: 500) mesmo tendo 50 jogadores online. Isso cria uma sensação de que o servidor é grande, embora o servidor real seja limitado pelo `server.properties` ou pelo hardware.
> 
### Exemplo de Config
```yaml
# This is the server motd.
Server-MOTD:
  Line-1: '&b&l&m-----------[&r&6&l Meu Servidor &b&l&m]-----------'
  Line-2: '&e&lWebsite &fmv.server.me'

# The motd of the player when they join in.
JoinGame-MOTD:
  Enabled: true
  # Check forum for placeholders.
  # Supported for PlaceholderAPI placeholders.
  Messages:
  - '&eBem Vindo ao servidor.'

# Server icon.
Custom-Server-Icon:
  # Set to true will load image from motd folder.
  Enabled: false
  # Make sure it's 64 x 64 pixels with png format.
  Image: server-icon.png

# The maximum players of the server.
Server-Maximum-Players:
  Modify: true
  Maximum-Players: 20
```

