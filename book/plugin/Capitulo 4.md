
## **Capítulo 4: Economia e Comércio (Vault, EssentialsX Economy e Lojas)** 💰

**Tags:** #economia #vault #essentialsx #comércio #dinheiro

---

A Economia do Minecraft não é apenas sobre o dinheiro; é sobre a **infraestrutura** que permite que todos os seus plugins (Lojas, Minigames, Ranks) se comuniquem e usem o mesmo saldo de moeda.

### 4.1. O Papel Central do Vault

O **Vault** é um plugin obrigatório, mas que não faz nada por si só. Ele é uma **API (Application Programming Interface)** que atua como uma ponte de comunicação.

- **Função:** Permitir que plugins independentes (como um plugin de Loja, um plugin de Terrenos e um plugin de Ranks) leiam e escrevam dados de:
    
    1. **Economia:** O saldo de dinheiro de um jogador.
        
    2. **Permissões:** O grupo e o prefixo do jogador.
        
- **Requisito:** O Vault precisa de um **Provider** (Provedor) para funcionar. Ele não armazena o dinheiro; ele apenas o direciona.
    

### 4.2. O Provedor de Economia: EssentialsX Economy

Embora existam outros provedores, o **EssentialsX** (que você já deve usar para comandos como `/home` e `/spawn`) é o provedor de economia mais comum e fácil de configurar.

- **Vantagem:** O EssentialsX Economy armazena os saldos dos jogadores diretamente no seu **MariaDB** (se configurado corretamente), garantindo que o dinheiro do jogador seja o mesmo em todos os servidores da sua rede.
    
- **Moeda:** A moeda padrão é o `$`. Você pode customizá-la no arquivo `config.yml` do EssentialsX.

| Configuração YAML (EssentialsX) | Descrição                             | Valor de Exemplo       |
| ------------------------------- | ------------------------------------- | ---------------------- |
| `currency-symbol`               | O símbolo da moeda (prefixo).         | `R$` ou `$`            |
| `currency-suffix`               | Texto exibido após o valor.           | `cobre` ou `diamantes` |
| `starting-balance`              | O saldo inicial de todo novo jogador. | `500.0`                |

### 4.3. Comandos Essenciais de Economia

A administração da economia é feita com o EssentialsX, mas a funcionalidade de leitura é universal (via Vault).

| Comando                       | Grupo      | Função                          | Exemplo                  |
| ----------------------------- | ---------- | ------------------------------- | ------------------------ |
| `/eco give <jogador> <valor>` | Admin/Dono | Dá dinheiro a um jogador.       | /eco give Pauloxc6 1000` |
| `/eco take <jogador> <valor>` | Admin/Dono | Remove dinheiro de um jogador.  | /eco take Pauloxc6 50`   |
| `/bal <jogador>`              | Membro     | Verifica o saldo do jogador.    | /bal Pauloxc6`           |
| `/pay <jogador> <valor>`      | Membro     | Envia dinheiro a outro jogador. | /pay Zezinho 500`        |
### 4.4. Sistemas de Comércio (Lojas)

A economia só funciona se houver formas de gastar e ganhar dinheiro.

#### 4.4.1. Lojas de Placa (Sign Shops)

Plugins como o **ChestShop** ou o módulo de _Sign Shop_ do EssentialsX permitem que os jogadores criem lojas de forma simples, usando um baú e uma placa de sinalização.

- **Formato da Placa (EssentialsX):**
    
    - **Linha 1:** Nome de Usuário (Deixe em branco para uma loja pública, ou use seu nome para ser o proprietário).
        
    - **Linha 2:** Quantidade de Itens.
        
    - **Linha 3:** Preço (Use `B` para Venda/Compra, ex: `B50` para Vender por 50; Use `:` para Venda e Compra, ex: `B50:10` para Vender por 50 e Comprar por 10).
        
    - **Linha 4:** ID/Nome do Item.
        

#### 4.4.2. Lojas Gráficas (GUI Shops)

Plugins como **ShopGUIPlus** oferecem menus de inventário (GUIs) que são mais profissionais e fáceis de usar. Estes plugins dependem **inteiramente do Vault** para se comunicar com o EssentialsX Economy e realizar as transações.

- **Benefício:** Permitem organizar o comércio por categorias (Blocos, Armas, Ferramentas) e são mais intuitivos para jogadores novos.