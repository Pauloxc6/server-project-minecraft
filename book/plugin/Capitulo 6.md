## **Capítulo 6: EssentialsX - Configuração de Comandos, Teleportes e Home** ⚙️

**Tags:** #essentialsx #comandos #teleporte #admin #configuração

---

O **EssentialsX** é o canivete suíço do seu servidor. Ele substitui dezenas de comandos básicos do Vanilla (como `/msg`, `/kit`, `/sethome`, `/spawn`) e adiciona funcionalidades cruciais de administração.

A configuração deste plugin é vasta e reside primariamente no arquivo **`config.yml`** dentro da pasta `plugins/Essentials/`.

### 7.1. Configurações de Teleporte e Segurança

Para manter a integridade e evitar _bugs_ de teletransporte, algumas configurações de segurança são cruciais:

|Configuração YAML|Padrão|Recomendação Profissional|Descrição|
|---|---|---|---|
|`teleport-safety`|`true`|`true`|Garante que o jogador não seja teleportado para um lugar perigoso (como dentro da lava ou em um bloco).|
|`teleport-invulnerability`|`4`|`4`|Define o tempo (em segundos) de invulnerabilidade após o teletransporte (para evitar _spawn killing_).|
|`teleport-delay`|`0`|`3`|**Essencial.** Define o tempo (em segundos) que o jogador precisa ficar parado antes de se teleportar (Usado em `/tpa`, `/home`, `/spawn`).|
### 7.2. Gerenciamento de Comandos e Kits

Você pode desativar comandos do Vanilla que o EssentialsX substitui ou que você não quer permitir.

#### 7.2.1. Desativação de Comandos (Command Overrides)

Se você tiver outro plugin para _kits_ (ex: um plugin de _crates_) ou para mensagens privadas, você pode desativar o módulo do EssentialsX.

- **Sintaxe:** Use a seção `disabled-commands` no `config.yml`.

```yml
disabled-commands:
  - kit
  - help
  - msg
```


#### 7.2.1. Configuração de Kits

Os _kits_ são um recurso de progressão importante, frequentemente dado a novos jogadores (`/kit tools`) ou a grupos VIP (Capítulo 3).

- **Sintaxe:** Edite a seção `kits:` no `config.yml`. O formato usa o tempo em segundos para definir o _cooldown_ (tempo de espera)

```yaml
kits:
  tools:
    delay: 604800  # 7 dias em segundos
    items:
      - 277 1 name:&ePicareta_Inicial lore:Ferramenta_Basica
      - 276 1
```

 > **Nota sobre IDs de Item:** Em versões mais recentes do Minecraft (1.13+), é melhor usar os nomes dos itens (Ex: `DIAMOND_PICKAXE`) em vez de IDs numéricos.

### 7.3. Configuração de Spawn e Home

O EssentialsX gerencia os pontos de teletransporte principais do servidor.

#### 7.3.1. Configuração do Spawn

- **Comando:** Use o comando no jogo: `/setspawn`.
    
- **Segurança:** O ponto de _spawn_ deve estar sempre dentro de uma região do **WorldGuard** que negue a construção (`build deny`, Capítulo 2).
    
- **Sobrescrita do Spawn:** Por padrão, o EssentialsX substitui o _spawn_ do mundo Vanilla. Certifique-se de que a opção `respawn-at-home` esteja correta para que os jogadores mortos voltem para o lugar certo.
    

#### 7.3.1. Limites de Home

Limitar o número de _homes_ que um jogador pode definir é crucial para a performance e a progressão.

- **Integração com LuckPerms:** O melhor método é usar o LuckPerms para conceder a permissão de limite de _home_ para cada grupo (Capítulo 3).
    
    - **Permissão:** `essentials.sethome.multiple.<número>`
        
    - **Exemplo:** Para o grupo **VIP** ter 5 _homes_, adicione a permissão: `/lp group vip permission set essentials.sethome.multiple.5 true`.
        

### 7.4. Integração com o Chat

Embora seja um plugin de comandos, o EssentialsX também pode gerenciar o formato de chat. Se você quiser usar outro plugin de chat mais complexo, você deve desativar este módulo.

- **Configuração:** A seção `chat:` no `config.yml` define como os prefixos do **LuckPerms** (Capítulo 3) serão exibidos no chat.