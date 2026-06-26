# Usar com TitansBattle

O `FocusCorreio` funciona com o `TitansBattle` usando recompensas por comando.

A ideia e simples: quando o TitansBattle declarar um vencedor, ele executa um comando no console. Esse comando envia a recompensa para o `/correio` do jogador.

## Requisitos

- `FocusCorreio` instalado e carregando sem erro.
- `TitansBattle` instalado e com o evento ja criado.
- O TitansBattle precisa executar o comando pelo console.
- Jogadores comuns devem ter somente `focuscorreio.usar`.
- Nao entregue `focuscorreio.admin` ou `focuscorreio.*` para jogadores comuns.

## Comando Base

Use este formato dentro da lista de comandos do TitansBattle:

```text
correio adicionar %player% MATERIAL QUANTIA Nome da Recompensa
```

Exemplos:

```text
correio adicionar %player% DIAMOND 16 Premio do Gladiador
correio adicionar %player% TRIPWIRE_HOOK 1 Chave do Evento
correio adicionar %player% NETHERITE_INGOT 2 Campeao do TitansBattle
```

Na configuracao do TitansBattle, os comandos normalmente ficam sem `/` no comeco, igual `give %player% diamond 1`.

O jogador vencedor nao precisa de permissao para enviar recompensas. Ele so precisa de `focuscorreio.usar` para abrir o menu e resgatar o premio.

## Onde Configurar

Cada evento do TitansBattle tem um arquivo proprio em:

```text
plugins/TitansBattle/games/
```

Abra o arquivo do evento que voce criou, por exemplo:

```text
plugins/TitansBattle/games/gladiador.yml
```

Procure a parte de `prizes`.

## Exemplo Para o Primeiro Lugar

Em eventos Free For All, normalmente o premio principal fica em `FIRST`.

```yaml
prizes:
  FIRST:
    member.commands.enabled: true
    member.commands.command_list:
      - "correio adicionar %player% DIAMOND 16 Premio do Gladiador"
      - "correio adicionar %player% TRIPWIRE_HOOK 1 Chave do Gladiador"
```

Depois rode:

```text
/tb reload
```

Quando o jogador vencer, os itens vao aparecer no `/correio`.

## Primeiro, Segundo e Terceiro Lugar

Em torneios de eliminacao, o TitansBattle pode usar `FIRST`, `SECOND` e `THIRD`.

```yaml
prizes:
  FIRST:
    member.commands.enabled: true
    member.commands.command_list:
      - "correio adicionar %player% NETHERITE_INGOT 3 Campeao do Torneio"
      - "correio adicionar %player% DIAMOND 32 Premio de Primeiro Lugar"

  SECOND:
    member.commands.enabled: true
    member.commands.command_list:
      - "correio adicionar %player% DIAMOND 16 Premio de Segundo Lugar"

  THIRD:
    member.commands.enabled: true
    member.commands.command_list:
      - "correio adicionar %player% EMERALD 16 Premio de Terceiro Lugar"
```

## Premio Para Quem Mais Matou

Se o seu evento usa premio para `KILLER`, voce tambem pode mandar pelo correio:

```yaml
prizes:
  KILLER:
    member.commands.enabled: true
    member.commands.command_list:
      - "correio adicionar %player% GOLDEN_APPLE 3 Mais Abates do Evento"
```

## Eventos em Grupo

Se o evento for em grupo, voce pode configurar premio de lider e de membros.

```yaml
prizes:
  FIRST:
    leader.commands.enabled: true
    leader.commands.command_list:
      - "correio adicionar %player% NETHERITE_INGOT 2 Lider Campeao"

    member.commands.enabled: true
    member.commands.command_list:
      - "correio adicionar %player% DIAMOND 16 Membro Campeao"
```

Se quiser que lider receba a mesma recompensa dos membros, use a opcao do TitansBattle:

```yaml
prizes:
  FIRST:
    treat_leaders_as_members: true
```

## Modelo Antigo de Config

Algumas versoes antigas do TitansBattle usam a configuracao assim:

```yaml
prizes:
  members:
    commands:
      enabled: true
      command_list:
        - "correio adicionar %player% DIAMOND 16 Premio do Evento"
  leaders:
    commands:
      enabled: true
      command_list:
        - "correio adicionar %player% NETHERITE_INGOT 2 Premio do Lider"
```

Se o seu arquivo estiver nesse formato, siga o formato dele e apenas troque o comando da recompensa.

## Criar Recompensas Diferentes Para Cada Evento

Cada arquivo em `plugins/TitansBattle/games/` pode ter comandos diferentes.

Exemplo:

```text
gladiador.yml -> correio adicionar %player% DIAMOND 16 Premio do Gladiador
sumo.yml      -> correio adicionar %player% EMERALD 10 Premio do Sumo
arena.yml     -> correio adicionar %player% GOLD_INGOT 32 Premio da Arena
```

Assim cada evento entrega um premio diferente no correio.

## Testar

1. Edite o arquivo do evento.
2. Salve.
3. Rode:

```text
/tb reload
```

4. Inicie o evento:

```text
/tb start nomeDoEvento
```

5. Quando o evento terminar, o vencedor deve receber aviso do FocusCorreio.
6. O jogador abre:

```text
/correio
```

## Problemas Comuns

### O premio nao chegou

Confira se o comando esta sem erro:

```text
correio adicionar %player% DIAMOND 1 Teste
```

Teste direto no console, trocando `%player%` pelo nick real:

```text
correio adicionar Steve DIAMOND 1 Teste TitansBattle
```

### O TitansBattle nao executou o comando

Confirme se `member.commands.enabled` ou `leader.commands.enabled` esta `true`.

### O material deu invalido

Use nomes de materiais do Minecraft em ingles, por exemplo:

```text
DIAMOND
EMERALD
TRIPWIRE_HOOK
NETHERITE_INGOT
GOLDEN_APPLE
```

### Entregou no inventario em vez do correio

Entao o premio provavelmente esta configurado em `items`, nao em `commands`. Para usar o FocusCorreio, deixe a recompensa em `commands`.
