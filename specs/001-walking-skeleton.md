# Spec 001 — Walking Skeleton

**Status:** rascunho (aguardando revisão)
**Objetivo de aprendizado:** primeira spec do projeto — exercício inicial de SDD.

## 1. Resumo

A fatia vertical mais fina do misterfoot que atravessa o jogo de ponta a ponta: o jogador
escolhe uma seleção, monta a escalação, **joga UMA partida** simulada em texto e a comanda
ao vivo (substituições + postura), e vê o resultado. Nada além disso.

O propósito do walking skeleton é provar o fluxo completo e exercitar a metodologia — **não**
ser um jogo divertido ainda.

## 2. Metas e não-metas

### Metas (v1)
- Escolher 1 seleção de uma lista pequena de elencos **placeholder** (fictícios).
- Montar a escalação: escolher o **XI inicial** e uma **formação** a partir do elenco.
- Simular **1 partida** contra uma seleção adversária (IA trivial), exibida como **feed de eventos em texto**.
- **Intervenção ao vivo**: durante a partida, fazer **substituição** e alternar **postura** (atacar / equilibrar / segurar).
- Exibir o **resultado final** (placar + resumo).

### Não-metas (explicitamente fora do v1)
- Torneio / chaveamento / Copa completa (são só partidas isoladas por enquanto).
- Carreira, temporadas, envelhecimento de jogadores.
- Recrutamento/naturalização (a fase de garimpo entra depois).
- Editor de elencos da comunidade.
- Contas de usuário, login, save na nuvem.
- Monetização (donate/ads).
- Qualquer gráfico além de texto.

## 3. Fluxo do usuário

1. **Tela inicial** → botão "Novo jogo".
2. **Escolher seleção** → grid de seleções placeholder; seleciona uma.
3. **Montar escalação** → vê o elenco (26), escolhe formação (ex: 4-4-2, 4-3-3) e o XI inicial.
4. **Iniciar partida** → vai pra tela de partida.
5. **Partida (ao vivo)** → feed de eventos em texto avança (com controle de velocidade/pausa);
   o jogador pode, a qualquer momento, **substituir** um jogador e **mudar a postura**.
6. **Fim de jogo** → placar final + resumo dos eventos; botão "Jogar de novo".

## 4. Modelo de dados (mínimo, em memória / save local)

```
Selecao   { id, nome, jogadores: Jogador[] }
Jogador   { id, nome, posicao (GOL|ZAG|MEI|ATA), overall (0-100) }
Formacao  { nome, slots: posicao[] }   // ex: 4-4-2
Partida   { mandante, visitante, escalacaoMandante, postura, eventos: Evento[], placar }
Evento    { minuto, tipo (GOL|CHANCE|FALTA|CARTAO|SUBST|FIM), texto, time }
```

## 5. Motor de simulação (v1 — trivial, a evoluir)

- Discretiza a partida em ~90 "ticks" (minutos).
- A cada tick, a chance de evento depende da **força ofensiva** de cada time
  (média do overall + bônus/penalidade de **postura**).
- Eventos de gol incrementam o placar; eventos textuais alimentam o feed.
- Adversário usa IA trivial (postura fixa). Realismo e balanceamento são problema de specs futuras.

## 6. Critérios de aceite

- [ ] Consigo iniciar um novo jogo e escolher uma das seleções placeholder.
- [ ] Consigo montar uma escalação válida (formação + XI a partir do elenco).
- [ ] A partida roda como feed de eventos em texto, do minuto 0 ao fim.
- [ ] Durante a partida consigo fazer ao menos 1 substituição e ela reflete no jogo.
- [ ] Durante a partida consigo mudar a postura e isso afeta a probabilidade de eventos.
- [ ] Ao fim, vejo o placar e um resumo, e consigo jogar de novo.

## 7. Em aberto (decidir nas próximas specs)

- Quantas seleções e jogadores placeholder semear no v1?
- A partida avança sozinha (tempo real acelerado) ou por clique do jogador?
- Quais posturas exatas e como cada uma afeta os números?
