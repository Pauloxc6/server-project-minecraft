## **Capítulo 11: Redes BungeeCord/Velocity e Comunicação entre Servidores**

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

Se o seu objetivo é ter múltiplos modos de jogo (Lobby, Survival, Skywars) interconectados, você precisa de uma **Rede de Servidores**. Isso resolve o problema de sobrecarregar uma única instância de servidor e permite que os jogadores transitem fluidamente entre diferentes mundos.

### 11.1. O Papel do Servidor Proxy

Toda a rede se baseia em um **servidor proxy**. Os jogadores se conectam ao endereço IP do proxy, e ele é o responsável por rotear o jogador para o servidor de destino (Lobby, Survival, etc.).

| Proxy          | Base                      | Vantagens                                                                                                                                                         |
| -------------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **BungeeCord** | O proxy original.         | Amplamente compatível, muitas ferramentas e tutoriais disponíveis.                                                                                                |
| **Velocity**   | Mais moderno e eficiente. | **Melhor Desempenho:** Utiliza uma arquitetura mais moderna para lidar com mais jogadores e conexões com menos consumo de CPU. É o padrão recomendado atualmente. |

### 11.2. Arquitetura da Rede

Uma rede profissional é composta por dois tipos de servidores:

#### 11.2.1. O Proxy (Velocity)

- **Função:** Ponto de entrada único, lida com a conexão inicial, autenticação e roteamento.
    
- **Segurança:** A principal função de segurança é **esconder o IP e a porta** de todos os servidores de jogo internos.
    

#### 11.2.2. Os Servidores Backend (PaperMC)

- **Função:** Cada um roda um modo de jogo específico (Lobby, Survival, Minigame).
    
- **Conexão:** Eles são conectados ao Proxy e só podem ser acessados através dele.
    

### 11.3. Configuração Crítica de Segurança e Rede

Para que a rede funcione de forma segura, você precisa configurar o **IP Forwarding** e o **Firewall**.

#### 11.3.1. Habilitando o IP Forwarding (BungeeGuard)

Quando o jogador se conecta ao Proxy, o Proxy precisa informar ao servidor de jogo (PaperMC) quem é o jogador e qual é o IP real dele.

1. **Proxy (Velocity):** Não requer configuração se estiver usando o BungeeGuard.
    
2. **Backend (PaperMC):** No arquivo `spigot.yml` (ou `paper.yml`), você deve encontrar e definir a opção para permitir o encaminhamento de IP (historicamente chamado de `bungeecord: true` ou `velocity: true`).
    

> **Segurança:** Use o plugin **BungeeGuard** no seu PaperMC. Ele garante que **apenas** o seu Proxy Velocity possa enviar informações de IP e UUIDs de jogadores, bloqueando conexões diretas ao backend.

#### 11.3.2. Firewall (UFW) na Rede

Você deve proteger cada VPS na sua rede para que ninguém ignore o Proxy.

|Servidor|Porta a Abrir (UFW)|
|---|---|
|**Proxy (Velocity)**|**Porta Padrão do Minecraft (25565):** É a única porta que os jogadores devem ver.|
|**Servidores de Jogo (PaperMC)**|**Nenhuma Porta Pública:** O firewall do Linux deve **bloquear a porta 25565** para o mundo externo. Os servidores internos só devem aceitar conexões vindas do **IP local** do seu Proxy.|

### 11.4. Comunicação entre Servidores

Para que a experiência seja coesa, os plugins precisam se comunicar entre os servidores (por exemplo, a lista de amigos do Lobby precisa funcionar no Survival).

- **Banco de Dados Compartilhado:** O **MariaDB** (Capítulo 6) é a espinha dorsal da comunicação. Plugins como **LuckPerms**, **EssentialsX** (se configurado) e plugins de Minigames usam o mesmo banco de dados para garantir que os dados do jogador sejam os mesmos em toda a rede.
    
- **Mensagens e Canais:** Plugins de Rede (como o Velocity) usam canais de mensagem internos para enviar comandos ou atualizações em tempo real entre os servidores (por exemplo, quando um _staff_ bane alguém, todos os servidores recebem a notificação instantaneamente).
    

---
