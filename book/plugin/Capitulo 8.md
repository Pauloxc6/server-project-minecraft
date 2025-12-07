## **Capítulo 9: A Comunicação e Formato de Chat (EssentialsX Chat e Mensagens)** 💬

**Tags:** #chat #essentialsx #comunicação #formatação #cores

---

O plugin **EssentialsX Chat** é o componente responsável por gerenciar a aparência das mensagens no seu servidor. Ele se baseia nos dados de prefixo e sufixo definidos no **LuckPerms** (Capítulo 3) e os exibe no formato desejado.

### 8.1. Configurando o Formato Global de Chat

O formato de chat é definido no arquivo `config.yml` do **EssentialsX Chat** (geralmente encontrado na pasta `plugins/Essentials/`).

A seção chave a ser configurada é `format:`

```yaml
# O formato padrão de chat.
# Ele usa Placeholders do LuckPerms/Vault
# {DISPLAYNAME} é o nome do jogador (que inclui o prefixo/sufixo do LuckPerms)
chat:
format: '<{DISPLAYNAME}> {MESSAGE}'

# Permite que os jogadores vejam o seu Rank (LuckPerms) antes do nome.
# O EssentialsX usa o Placeholder {GROUP} para o nome do grupo.
group-formats:
	default: '&7[{GROUP}] &f{DISPLAYNAME}&7: &f{MESSAGE}'
	admin: '&c[{GROUP}] &f{DISPLAYNAME}&f: &f{MESSAGE}'
	vip: '&a[{GROUP}] &f{DISPLAYNAME}&f: &f{MESSAGE}'
```

> **Importante:** O `group-formats` no EssentialsX é um método alternativo. Na maioria dos servidores modernos, o formato principal (`format:`) usa o `{DISPLAYNAME}` (que já inclui o prefixo do LuckPerms) para evitar duplicação de tags.

**Formato Recomendado (Limpo e Funcional):**

```yaml
chat:
# O prefixo e sufixo são definidos no LuckPerms, e {DISPLAYNAME}
# puxa essas informações automaticamente.
format: '{DISPLAYNAME}&f: &7{MESSAGE}'

# Exemplo: [Admin] Paulo: Mensagem de teste
```

### 8.2. Símbolos e Códigos de Cores

O EssentialsX permite o uso de códigos de cores tradicionais do Minecraft.

- **Cores:** O símbolo `&` seguido de um código hexadecimal (ex: `&a` para verde-claro).
* **Estilos:** Estilos como Negrito (`&l`), Sublinhado (`&n`), e Itálico (`&o`) são essenciais.

| Código | Cor/Estilo         | Exemplo de Uso                      |
| :----- | :----------------- | :---------------------------------- |
| `&l`   | Negrito (**bold**) | `&lBem-vindo`                       |
| `&o`   | Itálico (*italic*) | `&oRegra`                           |
| `&a`   | Verde Claro        | `&aOnline`                          |
| `&c`   | Vermelho           | `&cMorto`                           |
| `&r`   | Resetar            | Reseta cores/estilos para o padrão. |

> **Permissões:** A permissão `essentials.chat.color` ou `essentials.chat.format` deve ser dada aos grupos (via LuckPerms, Capítulo 3) que podem usar esses códigos no chat (geralmente **VIPs** e **Staff**).

  
### 8.3. Mensagens Privadas e Social

O EssentialsX gerencia os comandos sociais básicos.

| Comando | Função | Permissão (LuckPerms) |
| :--- | :--- | :--- |
| `/msg <jogador> <mensagem>` | Envia uma mensagem privada. | `essentials.msg` |
| `/r <mensagem>` | Responde à última pessoa que enviou uma mensagem privada. | `essentials.reply` |
| `/ignore <jogador>` | Bloqueia as mensagens de um jogador (chat e privado). | `essentials.ignore` |
| `/mail` | Envia e recebe e-mails offline. | `essentials.mail` |
### 8.4. Filtragem e Proteção de Chat

Para manter o chat limpo e profissional, o EssentialsX oferece recursos de filtragem.

| Configuração YAML | Padrão | Função |
| :--- | :--- | :--- |
| `max-players-cap` | `100000` | Limita o número máximo de jogadores que o servidor reporta. |
| `op-color` | `&4` | Cor usada para o Nickname de jogadores que estão com OP (evite usar, gerencie com LuckPerms). |
| `chat-radius` | `0` | Se configurado, limita a distância que os jogadores podem ouvir o chat (Ex: `50` para um chat local). Use `0` para chat global. |
| `filter-swears` | `false` | Se ativado, tenta censurar palavrões (geralmente não é muito eficiente, mas útil). |
> **Dica Profissional:** Se o `chat-radius` estiver ativado (chat local), você pode dar a permissão `essentials.chat.spy` aos membros do *staff* para que eles possam ver todas as conversas, mesmo as locais.
