## **Capítulo 15: Multi-Mundos e Diversidade - A Suíte Multiverse** 🗺️

**Tags:** #multiverse #mundos #infraestrutura #viagens #gameplay

---

O **Multiverse-Core** permite que um servidor PaperMC hospede vários mundos isolados, cada um com suas próprias regras, inventários (se configurado) e _gameplay_. Isto é crucial para oferecer diferentes modos de jogo sem a necessidade de um _proxy_ (BungeeCord), embora também funcione perfeitamente com um.

### 15.1. O Essencial: Multiverse-Core

O _Core_ é o motor. Ele gerencia as funções básicas de criação e navegação.

|Comando|Função|Exemplo|
|---|---|---|
|`/mv create`|Cria um novo mundo.|`/mv create cidade normal -g Flat` (Cria um mundo plano com o gerador padrão)|
|`/mv load`|Carrega um mundo que existe no diretório do servidor, mas não está ativo.|`/mv load mapa_antigo`|
|`/mv unload`|Descarrega um mundo da memória. **Atenção:** Se o mundo estiver vazio, é seguro, mas mundos importantes nunca devem ser descarregados.|`/mv unload mundo_de_teste`|
|`/mv tp`|Teleporta você ou outro jogador para um mundo específico.|`/mv tp @p criativo`|
|`/mv set diff`|Define a dificuldade do mundo.|`/mv set diff peaceful`|
|`/mv set mode`|Define o modo de jogo padrão do mundo.|`/mv set mode creative`|
|`/mv list`|Lista todos os mundos carregados, com seus tipos e status de _gameplay_.|
### 15.2. Extensões Chave da Suíte Multiverse

Para a maioria dos servidores profissionais, o **Core** por si só não é suficiente. As extensões adicionam funcionalidades essenciais de _gameplay_.

#### 15.2.1. Multiverse-Inventories (MV-I)

O mais importante. Por padrão, o Minecraft usa o mesmo inventário para todos os mundos. O MV-I permite que você tenha inventários separados.

- **Função:** Separa inventários, armaduras, saúde, fome e XP entre grupos de mundos.
    
- **Exemplo:**
    
    - Um jogador no mundo **Survival** tem seu inventário completo.
        
    - Ao viajar para o mundo **Criativo**, ele recebe um inventário limpo (ou o último inventário do Criativo), e seu inventário Survival é salvo.
        
- **Uso:** Essencial para separar modos de jogo, como: Survival, Minigames, e Criativo.


#### 15.2.2. Multiverse-Portals (MV-P)

Permite a criação de portais para viajar entre mundos de forma intuitiva, sem comandos.

- **Função:** Cria portais que, ao serem atravessados, teleportam o jogador para um mundo específico.
    
- **Uso:** Crucial para o _lobby_ principal, criando um centro de viagens para todos os outros mundos.
    
- **Comando:** `/mvp create <nome> <destino> <material>`

#### 15.2.3. Multiverse-NetherPortals (MV-NP)

Resolve o problema de portais do Nether e do End em ambientes multi-mundos.

- **Função:** Garante que quando um jogador cria um portal do Nether, ele o conecta ao _Nether correto_ (o Nether daquele mundo principal), e não a um Nether aleatório do servidor.

### 15.3. Integração com Plugins Anteriores

O Multiverse-Core se integra perfeitamente com as configurações que você já definiu:

- **LuckPerms (Capítulo 3):** Você pode usar o **Contexto de Mundo** no LuckPerms para dar permissões diferentes em mundos específicos (Ex: Permitir `/fly` no mundo **Criativo**, mas não no **Survival**).
    
- **TAB (Capítulo 12):** A configuração do TAB usa a lógica `per-world` (por mundo), permitindo que você exiba _scoreboards_ diferentes dependendo de onde o jogador está.