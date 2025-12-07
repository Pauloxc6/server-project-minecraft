## **Capítulo 3: LuckPerms - Gerenciamento de Permissões, Grupos e Hierarquia**

**Tags:** #luckperms #permissões #mariaDB #staff #grupos

---

O LuckPerms é o plugin de permissões padrão da indústria. Ele controla absolutamente tudo o que um jogador ou membro do _staff_ pode ou não pode fazer, desde o comando `/home` até o comando `/ban`.

### 3.1. Configuração e Conexão (MariaDB)

Para um servidor profissional, o LuckPerms **DEVE** estar configurado para usar o MariaDB (Capítulo 6) para garantir que os dados de permissões sejam compartilhados em todos os seus servidores (em redes BungeeCord/Velocity) e que sejam persistentes após _reloads_ ou _restarts_.

- **Configuração:** Edite o arquivo `config.yml` do LuckPerms e altere a opção `storage-method` para `mysql`.
    
- **Credenciais:** Insira as credenciais do MariaDB (endereço do banco, nome do banco de dados, usuário e senha) que você configurou no Capítulo 6 do básico.
    

### 3.2. Hierarquia de Grupos: O Conceito de Herança

Em vez de dar a um **Admin** todas as permissões de forma manual, usamos a **Herança**. Um grupo herda todas as permissões e prefixos do grupo pai.

**Pirâmide de Grupos (Do Mais Baixo para o Mais Alto):**

| Grupo                | Herda de...            | Permissões de Exemplo                                                                | Prioridade (Maior valor = mais alto) |
| -------------------- | ---------------------- | ------------------------------------------------------------------------------------ | ------------------------------------ |
| **Dono**             | Co-Dono, Admin         | Permissões de super-administrador (Ex: `*`).                                         | **100**                              |
| **Co-Dono**          | Admin, Coordenador     | Permissões de Admin + Gestão financeira.                                             | 95                                   |
| **Admin**            | Coordenador, Moderador | Todos os comandos de moderação, acesso a `/op` (se necessário), acesso a _logs_.     | 90                                   |
| **Coordenador**      | Moderador              | Comandos de moderação de baixo nível, gestão de eventos.                             | 80                                   |
| **Moderador**        | Ajudante, Membro       | Comandos de Mute, Kick, Jail (Prisão), acesso a Anti-Cheat _logs_.                   | 70                                   |
| **Ajudante**         | Membro                 | Comandos informativos, teletransporte de assistência, verificação de _logs_ de chat. | 60                                   |
| **Builder**          | Membro                 | Permissões para usar o **WorldEdit** (na região designada do `WorldGuard`).          | 50                                   |
| **Membro (Default)** | Nenhum                 | Comandos básicos: `/spawn`, `/home`, `/tpa`, chat.                                   | 0                                    |

### 3.3. Comandos Essenciais do LuckPerms

Todos os comandos de gestão de grupos e usuários são feitos através de um único ponto de entrada. Recomenda-se usar a interface web do LuckPerms, mas os comandos via console são essenciais.

#### 3.3.1. Criação de Grupos

Crie os grupos na ordem da hierarquia (do mais baixo para o mais alto).

```minecraft
# Cria o grupo default (membro)
/lp creategroup default

# Cria o grupo Builder
/lp creategroup builder

# Cria o grupo Admin
/lp creategroup admin
```

#### 3.3.2. Definição da Herança

Defina a herança para que as permissões fluam corretamente.

```minecraft
# O grupo Moderador herda as permissões do Ajudante
/lp group moderador parent set ajudante

# O grupo Admin herda as permissões do Coordenador
/lp group admin parent set coordenador
```

#### 3.3.3. Definição da Prioridade (Weight)

A prioridade (ou `weight`) garante que o prefixo do grupo mais alto (como Admin) seja exibido corretamente no chat, mesmo que o jogador herde de outros grupos.

```minecraft
# Define a prioridade de exibição (Capítulos 12 e 13)
/lp group dono set weight 100
/lp group default set weight 0
```

#### 3.3.4. Adicionando e Removendo Permissões

A sintaxe é simples: `permission set <permissão> [valor]`. O valor é geralmente `true` (permitir) ou `false` (negar).

| Ação                                                     | Comando de Exemplo                                              |
| -------------------------------------------------------- | --------------------------------------------------------------- |
| **Permitir** o comando `/sethome` ao grupo **Membro**.   | `/lp group default permission set essentials.sethome true`      |
| **Negar** o uso de _Command Blocks_ ao grupo **Membro**. | `/lp group default permission set minecraft.command.give false` |
| **Dar Acesso** total ao **Dono**.                        | `/lp group dono permission set * true`                          |

### 3.4. O Sistema de Prefixos (Integração com o Chat)

O LuckPerms é o responsável por definir os **Prefixos** (cores e tags no chat) que serão lidos por plugins de chat (como EssentialsX Chat, Capítulo 12 Básico).

- **Definir Prefixos:**

```minecraft
/lp group admin meta setprefix "&c[Admin] &f"
# O prefixo do Admin será: [Admin] Jogador: Mensagem
```