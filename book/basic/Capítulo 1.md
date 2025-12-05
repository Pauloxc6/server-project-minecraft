## **Capítulo 1: Fundamentos da Infraestrutura - Modelos de Hospedagem, Tipos de Servidores e a Escolha Linux** 🌐

**Tags:** #estudos #minecraft #linux #sever
**Data:** 2025-12-04

---

Antes de sairmos baixando e configurando tudo precisamos vamos começar entendendo quais opções temos hoje no mercado.

Hoje em dia exite uma vasta variedade de formas de você hospedar um servidor de minecraft.
A melhor forma para um teste é o self hosting, agora se você quer algo que se torne publico e necessário, a utilização um sistema dedicado ou hospedar em cloud.

Vamos passar por quase todas opções que disponíveis, você aprendendo a forma que ensinarei você conseguira implementar em qualquer servidor.

----

### 1.1. Tipos de Hospedagem

Para começamos com pé direito vamos entender como cada uma funciona.

A escolha do modelo de hospedagem é a primeira e mais importante decisão, pois ela define o seu controle, o custo e o potencial de performance do seu projeto.

| Modelo                                | Foco Principal                   | Vantagens                                                                                                                                                      | Desvantagens                                                                                                                                                  |
| ------------------------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Self-Hosting (Hospedagem Própria)** | **Custo Zero (Inicial)**         | Controle total sobre o hardware.                                                                                                                               | **Altamente Instável:** Depende da sua velocidade de upload da internet, energia elétrica e resfriamento do computador. Risco de segurança na rede doméstica. |
| **Hospedagem de Painel (Shared)**     | **Facilidade de Uso**            | Não exige conhecimento técnico (Linux/CLI). Baixo custo inicial.                                                                                               | **Baixa Performance:** Recursos divididos com outros clientes. Impossível realizar otimizações de baixo nível.                                                |
| **Cloud Computing (VPS/IaaS)**        | **Padrão Profissional (Início)** | **Controle Total (Root):** Acesso à linha de comando (Linux) para otimizar e instalar qualquer software. Escalabilidade (fácil aumentar ou diminuir recursos). | Requer conhecimento de Linux (CLI) e configuração. Preço pode ser volátil em modelos "Pay-as-you-go" (pagar pelo uso).                                        |
| **Servidor Dedicado**                 | **Performance Máxima**           | Hardware físico exclusivo. Recursos 100% garantidos, essenciais para grandes redes de alto tráfego.                                                            | **Alto Custo:** O investimento inicial e de manutenção é o mais elevado. Requer expertise em hardware e Linux.                                                |
**Conclusão:** Para um servidor profissional, o caminho recomendado é o **Cloud Computing (VPS)**, pois oferece o controle necessário (acesso root no Linux) e um excelente balanço entre custo e performance.

### 1.2. Tipos de Servidores (Arquitetura Minecraft)

- **Servidor Único:** Um único JAR rodando, ideal para servidores menores de Sobrevivência ou Factions simples.
    
- **Rede BungeeCord/Velocity:** Arquitetura complexa que utiliza um **servidor proxy** (BungeeCord ou Velocity) para conectar múltiplos servidores (Lobby, Minigames, Survival) sob o mesmo IP. _Essencial para projetos que visam alto número de jogadores e diversidade de jogos._
    

### 1.3. A Escolha da Plataforma: Por Que Usar Linux? 🐧

- **Eficiência Incomparável:** Sem interface gráfica, o Linux dedica a maior parte dos recursos (RAM e CPU) ao processo Java, resultando em melhor **TPS (Ticks Per Second)**.
    
- **Estabilidade:** Sistema operacional projetado para operar continuamente, garantindo o máximo **uptime**.
    
- **Custo:** Distribuições de servidor são gratuitas, reduzindo drasticamente os custos operacionais.

---

 Bom, percebemos que opções não faltam, afim de sempre trabalhamos da melhor forma possível, vamos escolher a melhor opção que é a cloud (Nesse ponto é recomendando um conhecimento básico de cloud, linux e redes).

---

## 2. Tipos de Servdores

Bom já temos onde hospedar nosso servidor, agora temos que intender quais são os tipos de servidores.

### 2.1. Classificação por Tecnologia de Base

Esta é a definição do que modifica o jogo e como a customização é aplicada:

|Tecnologia|Foco|Software Base|Uso Profissional|
|---|---|---|---|
|**Vanilla**|Jogo base, sem modificações.|`minecraft_server.jar` oficial.|Raramente usado, exceto para comunidades puristas que não aceitam melhorias de performance.|
|**Plugins**|Expansões de _gameplay_ ou comandos **no lado do servidor**. O jogador não precisa instalar nada.|**PaperMC, Spigot, Purpur.**|**O Padrão da Indústria.** Usado na maioria dos servidores grandes (Survival, Factions, Minigames) devido à estabilidade e facilidade de gerenciamento.|
|**Mods**|Mudanças profundas no jogo, exigindo que **o jogador instale a modificação** no cliente (Ex: Forge, Fabric).|**Forge, Fabric, Quilt.**|Popular para pacotes de Mods (_Modpacks_). Geralmente não é usado em redes grandes devido à barreira de entrada para o jogador.|
|**Plugins/Mods (Híbrido)**|Tentativa de rodar mods e plugins ao mesmo tempo.|**Magma, Mohist.**|**Não Recomendado para Profissional.** Tendência a ser menos estável, mas útil para criar um servidor com mods onde se deseja usar plugins comuns como WorldEdit.|
### 2.2. Classificação por Arquitetura (Estrutura Técnica)

Esta é a maneira como os servidores estão interligados:

- **Servidor Único (Single Instance):** Um único servidor rodando.
    
    - _Exemplos:_ Um servidor PaperMC de Survival ou um servidor Forge de Modpack.
        
    - _Vantagem:_ Simples de configurar.
    
- **Rede (BungeeCord / Velocity):** Múltiplos servidores (Lobby, Minigames) conectados por um Proxy.
    
    - _Vantagem:_ Distribui a carga de trabalho (_Load Balancing_), isola o lag e permite a transição fácil entre diferentes modos de jogo (inclusive entre um servidor PaperMC e um servidor Forge, se configurado corretamente).
        
    - _Essencial para:_ Qualquer projeto que pretenda ter mais de um modo de jogo ou mais de 100 jogadores online.

---

Com esta distinção clara entre tecnologia e arquitetura, você tem o panorama completo para escolher a base do seu projeto. A partir de agora, nosso foco será em um servidor **Plugin** focado em survavil com tecnologia **PaperMC** rodando em um ambiente **Linux**. Isso te dará uma boa base para começar.

---