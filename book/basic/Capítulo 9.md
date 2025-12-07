
## **Capítulo 9: Economia, Vault e Lojas (EssentialsX Economy & ChestShop)**

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

A economia de um servidor profissional de Minecraft é construída sobre três pilares interligados: a API (Vault), o motor financeiro (EssentialsX Eco) e a interface do usuário (Lojas).

### 9.1. O Pilar Central: Vault (API)

O **Vault** não é um plugin de economia; ele é uma **API (Application Programming Interface)**. Ele atua como uma **ponte** que permite que diferentes plugins conversem entre si.

- **Função:** O Vault conecta o seu **Motor de Permissões** (LuckPerms, Capítulo 8) e o seu **Motor de Economia** (EssentialsX Eco) com qualquer plugin de terceiros que precise saber a hierarquia de um jogador ou seu saldo financeiro (ex: plugins de Lojas, Leilões, Skills, etc.).
    

> **Instalação:** Para iniciar a economia, o **Vault** deve ser sempre o **primeiro plugin** instalado, mesmo que ele não pareça fazer nada.

### 9.2. O Motor Econômico: EssentialsX Economy

O **EssentialsX** é o plugin mais popular para comandos básicos, mensagens de chat e _kits_, mas ele também inclui o módulo de economia (**EssentialsX Economy**).

- **Função:** Ele é o motor que **armazena o saldo** de cada jogador, gerencia as transações de dinheiro e interage diretamente com o Vault.
    
- **Configuração:** Você pode configurar o nome da moeda (`$`, `Gemas`, `Coins`) e o saldo inicial dos jogadores no arquivo `plugins/Essentials/config.yml` (usando a sintaxe YAML que aprendemos no Capítulo 4).
    

> **Atenção:** Em servidores profissionais, o EssentialsX pode ser substituído por motores de economia mais leves (como o **CMI**), mas o EssentialsX é o padrão mais fácil para começar.

### 9.3. As Interfaces: Lojas

Para que o dinheiro circule, os jogadores precisam de maneiras intuitivas de comprar e vender itens. Existem dois tipos principais de lojas.

#### 9.3.1. Lojas de Baú (ChestShop)

O **ChestShop** é o método clássico e amplamente utilizado.

- **Função:** Permite que jogadores criem lojas de forma autônoma: colocam um item em um baú e criam uma placa acima (ou ao lado) para definir o preço de compra e venda.
    
- **Vantagem:** Estimula a economia interna entre jogadores e é fácil de configurar.
    
- **Desvantagem:** É menos escalável para grandes quantidades de itens ou servidores com alta rotatividade de jogadores.
    

#### 9.3.2. Lojas Gráficas (GUI Shops)

Plugins como **ShopGUIPlus** ou interfaces personalizadas (_custom menus_) usam menus gráficos (interfaces de inventário do Minecraft) para apresentar produtos.

- **Função:** Lojas que funcionam por cliques no menu do inventário, em vez de exigir interação com o mundo.
    
- **Vantagem:** Mais organizada, visualmente atrativa e não depende de espaço físico no mapa.
    
- **Uso Profissional:** Este é o padrão para lojas de servidores, pois oferece uma melhor experiência ao usuário (UX) e é mais fácil de gerenciar pelo administrador.
    

### 9.4. Resumo do Fluxo de Dados

Para que um jogador compre um item em uma loja:

1. O jogador clica na placa/GUI.
    
2. O plugin da **Loja** (ex: ShopGUIPlus) consulta o **Vault**.
    
3. O **Vault** pergunta ao **EssentialsX Economy** se o jogador tem saldo suficiente.
    
4. O **EssentialsX Economy** confirma o saldo (lendo do MariaDB).
    
5. A loja completa a transação, e o **EssentialsX Economy** atualiza o saldo do jogador no MariaDB.
    

---
