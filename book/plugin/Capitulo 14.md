## **Capítulo 14: Compatibilidade e Acessibilidade - A Suíte Via e GeyserMC** 🔄

**Tags:** #viaversion #compatibilidade #geysermc #bedrock #multiplataforma

---

Manter um servidor em uma única versão (Ex: 1.20.1) é limitante. A suíte de plugins **Via** e o **GeyserMC** resolvem isso, permitindo que o servidor seja acessível a quase todos os jogadores, independentemente da versão do Minecraft: Java ou Bedrock.

### 14.1. A Suíte Via: Compatibilidade de Versões Java

O servidor principal (PaperMC) pode rodar em uma versão moderna (Ex: 1.20.1), mas os plugins Via permitem que jogadores de versões antigas (Ex: 1.8) ou novas (Ex: 1.21-prerelease) se conectem sem problemas.

|Plugin|Função|Exemplo de Uso|
|---|---|---|
|**ViaVersion**|**Compatibilidade Futura (Forward)**. Permite que jogadores de versões _mais novas_ se conectem a um servidor mais antigo.|Servidor em 1.19.4, jogador em 1.20.1 se conecta.|
|**ViaBackward**|**Compatibilidade Passada (Backward)**. Permite que jogadores de versões _mais antigas_ se conectem a um servidor mais novo.|Servidor em 1.20.1, jogador em 1.16.5 se conecta.|
|**ViaRewind**|**Aprimoramento Visual**. Corrige problemas de renderização e comportamento de itens, blocos e entidades de versões anteriores.|Corrige a renderização de cabeças e armaduras da 1.8 quando o servidor está na 1.16+.|

> **Dica de Infraestrutura:** Instale a suíte Via **tanto no BungeeCord/Velocity (Proxy) quanto no PaperMC (Backend)**. Isso garante a melhor estabilidade e tratamento de pacotes em toda a rede.

####  14.1.1. Configuração Essencial do Via

- **Prioridade:** O ViaVersion deve ser o primeiro plugin a ser carregado no servidor para funcionar corretamente.
    
- **Versão Principal:** Escolha a versão mais estável e rica em recursos como a versão base do seu PaperMC (Ex: 1.19.4 ou 1.20.1).
    
- **Desempenho:** Os plugins Via são otimizados, mas o mapeamento de pacotes consome alguma CPU. Não há como evitar isso, mas a acessibilidade vale o custo.
    

### 14.2. GeyserMC: A Ponte para o Bedrock

O **GeyserMC** é o plugin que permite que jogadores da **Edição Bedrock** (celulares, consoles, Windows 10) se conectem ao seu servidor Java.

- **Função:** Traduz a comunicação do protocolo Bedrock para o protocolo Java em tempo real.
    
- **Requisito:** O GeyserMC geralmente deve ser instalado no BungeeCord/Velocity (Proxy) para que a porta de conexão Bedrock seja diferente e os jogadores Bedrock possam se conectar diretamente ao IP principal.
    

#### 14.2.1. Configuração do GeyserMC (Proxy)

1. **Porta Dedicada:** Você precisa abrir uma porta UDP separada (além da porta TCP do seu servidor Java, ex: 19132) para que os clientes Bedrock possam encontrá-la.

```yaml
bedrock:
  # A porta UDP para o Bedrock (DEVE ser diferente da porta Java)
  port: 19132 
  # Endereço IP do BungeeCord/Velocity
  address: 0.0.0.0
```

2. **Floodgate (Opcional, mas Recomendado):**
    
    - Para que os jogadores Bedrock possam se conectar sem uma conta Minecraft Java comprada (o que é comum), você precisa do plugin **Floodgate** instalado **nos servidores PaperMC** e **no BungeeCord/Velocity**.
        
    - O Floodgate injeta uma UUID e um nome de usuário falsos para o jogador Bedrock, permitindo que plugins como LuckPerms e EssentialsX funcionem sem que o servidor esteja em modo _offline_ (o que é inseguro).
        

### 14.3. Impacto na UX e na Segurança

- **UX Aprimorada:** A suíte Via e o GeyserMC aumentam a sua base de jogadores, tornando o servidor mais inclusivo.
    
- **Segurança com Bedrock:** Sem o Floodgate (ou um sistema de autenticação robusto), jogadores Bedrock podem se conectar com qualquer nome de usuário, potencialmente roubando identidades Java. **O Floodgate e o Passky/AuthMe são a solução para isso.**