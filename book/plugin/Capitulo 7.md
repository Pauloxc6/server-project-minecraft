## **Capítulo 7: Aprimoramento da UX - PlaceholderAPI, Scoreboards e Hologramas** ✨

**Tags:** #placeholderAPI #scoreboard #holograma #experiência #ux #otimização

---

Para criar uma experiência de jogo imersiva, você precisa de dados dinâmicos: placares de líderes, saldos de dinheiro, tempo de jogo, e o _rank_ do jogador. Isso tudo é feito através de um plugin que serve como uma fonte central de dados para todos os outros plugins visuais: o **PlaceholderAPI**.

### 7.1. PlaceholderAPI (PAPI): A Fonte Central de Dados

O PlaceholderAPI é uma ponte de comunicação que permite que plugins visuais (como o Scoreboard e Hologramas) exibam dados de plugins de _backend_ (como EssentialsX, LuckPerms ou Factions).

- **Função:** Fornecer _Placeholders_ (espaços reservados, como variáveis) no formato `%plugin_dado%`.
    
- **Requisito:** Não faz nada sozinho. Ele precisa de **Extensions** (Extensões) para carregar os dados.

#### 7.1.1. Instalação de Extensões

Para que o PAPI consiga ler dados do EssentialsX ou do LuckPerms, você precisa instalar a extensão correspondente.

|Extensão|Dados Fornecidos|Comando de Instalação|
|---|---|---|
|`Vault`|Saldo de dinheiro (`%vault_eco_balance%`) e _rank_ (`%vault_group%`).|`/papi ecloud download Vault`|
|`Essentials`|Tempo de jogo, _nickname_, _afk status_ (`%essentials_time_played%`).|`/papi ecloud download Essentials`|
|`LuckPerms`|Prefixos, Sufixos, _Weight_ (`%luckperms_prefix%`).|`/papi ecloud download LuckPerms`|
Após o download, o comando **`papi reload`** deve ser usado para que as extensões sejam carregadas.

### 7.2. Painéis Laterais (Scoreboards)

O **Scoreboard** é a principal forma de exibir informações em tempo real. Plugins como **FeatherBoard** ou **FastAsyncBoard** usam o PAPI para criar placares que se atualizam constantemente.

#### 7.2.1. Configuração do Scoreboard (Exemplo Genérico)

A maioria dos plugins de Scoreboard usa o formato YAML para definir as linhas

```yaml
Scoreboard:
  title: "&6Seu Servidor"
  lines:
    - "&7----------------"
    - "&eJogador: &f%player_name%"
    - "&eRank: &f%luckperms_group_name%"
    - "&eDinheiro: &a$%vault_eco_balance_formatted%"  # Dado do Vault/EssentialsX
    - "" # Linha vazia
    - "&bOnline: &f%server_online%"
    - "&7----------------"
```

> **Nota:** As _Placeholders_ são cruciais. Se você usar `%vault_eco_balance_formatted%` e não tiver as extensões `Vault` e `Essentials` instaladas no PAPI, essa linha aparecerá como o texto literal (quebrando a estética).

### 7.3. Hologramas (DecentHolograms)

Hologramas são textos 3D flutuantes usados para exibir informações estáticas (regras) ou dinâmicas (rankings, status do servidor) em _lobbies_ e _spawns_. O plugin mais popular é o **DecentHolograms**.

#### 7.3.1. Comandos Essenciais

| Comando                         | Função                                          | Exemplo                                        |
| ------------------------------- | ----------------------------------------------- | ---------------------------------------------- |
| `/dh create <nome>`             | Cria um novo holograma no local onde você está. | `/dh create ranks_info`                        |
| `/dh addline <nome> <texto>`    | Adiciona uma nova linha.                        | `/dh addline ranks_info &bBem-vindo ao Lobby!` |
| `/dh removeline <nome> <linha>` | Remove uma linha específica.                    | `/dh removeline ranks_info 3`                  |
| `/dh movehere <nome>`           | Move o holograma para a sua localização atual.  | `/dh movehere ranks_info`                      |
#### 7.3.1. Exibindo Dados Dinâmicos

Você pode inserir _Placeholders_ em qualquer linha de um holograma. Por exemplo, para exibir o saldo do jogador ao passar perto de um baú:

```minecraft
# Adiciona o saldo do jogador, que se atualiza em tempo real.
/dh addline saldo_bau &eSeu Saldo: &a%vault_eco_balance%
```

### 7.4. Otimização de Plugins Visuais

Plugins visuais consomem mais recursos da CPU, pois precisam se atualizar constantemente.

- **Intervalos de Atualização:** Configure o `update-interval` (ou `refresh-rate`) nos arquivos YAML do Scoreboard e Hologramas.
    
    - **Dados Estáticos (Título do Scoreboard):** Pode ser atualizado a cada 5-10 segundos.
        
    - **Dados Críticos (Dinheiro):** Pode ser atualizado a cada 0.5-1 segundo.
        
- **Visibilidade da Região:** Plugins de Holograma e Scoreboard devem ter opções para serem desativados ou ocultos em mundos onde não são necessários (como o mundo de mineração), economizando ciclos de CPU.