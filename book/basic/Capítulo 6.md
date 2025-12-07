## **Capítulo 6: O Coração dos Dados - Instalando e Configurando o MariaDB no Linux**

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

A maioria dos servidores profissionais armazena dados de jogadores (permissões, economia, estatísticas) em um **Banco de Dados Relacional (SQL)**. O **MariaDB** é o sucessor de código aberto e otimizado do MySQL, sendo a escolha padrão da indústria.

### 6.1. Instalação do MariaDB no VPS Linux

Para um sistema baseado em Debian/Ubuntu, a instalação é direta usando o `apt`.

1. **Atualizar o Cache de Pacotes:**

```bash
sudo apt update
```

2. Instalar o Servidor MariaDB:

```bash
sudo apt install mariadb-server -y
```

3. **Verificar o Status (Opcional):** Confirme que o serviço está ativo e rodando.

```bash
sudo systemctl status mariadb
```

### 6.2. Configuração de Segurança Pós-Instalação

Logo após a instalação, você deve rodar o _script_ de segurança. Isso remove configurações padrão inseguras, desativa logins remotos para o usuário _root_ e define a senha de administração.

```bash
sudo mysql_secure_installation
```

Você será guiado por algumas perguntas:

- **Set root password?** Sim. Defina uma senha forte para o usuário `root` do MariaDB (este é o administrador do banco de dados, **não** o administrador do Linux).
    
- **Remove anonymous users?** Sim.
    
- **Disallow root login remotely?** Sim. (Acesso root só deve ser permitido localmente).
    
- **Remove test database and access to it?** Sim.
    
- **Reload privilege tables now?** Sim.
### 6.3. Criando o Banco de Dados e o Usuário Minecraft

Você **nunca** deve usar o usuário `root` do MariaDB para se conectar aos seus plugins. Por segurança e organização, você criará um usuário e um banco de dados exclusivos para o seu servidor.

#### 6.3.1. Acessar o Console do MariaDB

```bash
sudo mariadb -u root -p
# Digite a senha que você definiu na etapa de segurança.
```

#### 6.3.2. Executar os Comandos SQL

Dentro do console (`MariaDB [(none)]>`), execute os comandos a seguir. Substitua `seubanco` e `suasenha` por nomes e senhas fortes:

1. **Cria o Banco de Dados (Database):**

```sql
CREATE DATABASE seubanco;
```

2. **Cria um Usuário:** O MariaDB deve ser instruído a permitir que este usuário se conecte ao banco de dados, tanto localmente quanto por IP (se você for usar o banco de dados em outra máquina).

```sql
CREATE USER 'minecraft_user'@'localhost' IDENTIFIED BY 'suasenha_local';
CREATE USER 'minecraft_user'@'%' IDENTIFIED BY 'suasenha_remota';
```

**Nota:** `'localhost'` é para conexões dentro da mesma máquina (mais seguro). `'%'` (wildcard) é para conexões de qualquer IP (necessário para Redes BungeeCord/Velocity onde o banco de dados pode estar em um VPS diferente). Use senhas diferentes para os dois.

3. **Concede Permissões ao Usuário:** Permite que o novo usuário manipule todos os dados no banco de dados recém-criado.

```SQL
GRANT ALL PRIVILEGES ON seubanco.* TO 'minecraft_user'@'localhost';
GRANT ALL PRIVILEGES ON seubanco.* TO 'minecraft_user'@'%';
```

4. Aplicar Alterações e Sair:

```SQL
FLUSH PRIVILEGES;
EXIT;
```

### 4. Conectando um Plugin (Exemplo: LuckPerms)

Com o banco de dados e o usuário prontos, o último passo é instruir os plugins essenciais a usarem o MariaDB em vez do padrão (Flat File).

Vamos usar o **LuckPerms** (o gerenciador de permissões) como exemplo, editando seu arquivo de configuração YAML:

1. **Navegue** até a pasta de configuração do plugin (`plugins/LuckPerms/config.yml`).
    
2. **Edite** o arquivo usando `nano`.

```bash
nano plugins/LuckPerms/config.yml
```

3. Altere as seguintes seções:

```YAML
# Altere o tipo de armazenamento de 'h2' ou 'json' para 'mysql'
storage:
  method: mysql 

  # Insira as credenciais do MariaDB que você acabou de criar:
  address: localhost  # Ou o IP do seu VPS, se for conectar de outra máquina
  port: 3306 
  database: seubanco
  username: minecraft_user
  password: suasenha_local
```

Após salvar e reiniciar o servidor, o LuckPerms irá criar todas as suas tabelas no banco de dados e estará pronto para gerenciar as permissões de forma profissional e escalável.