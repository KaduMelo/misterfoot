# misterfoot

Um jogo manager de seleção de futebol — você é **o Mister**: monta o elenco, escala, define a tática e comanda a partida ao vivo. Inspirado na sensação do Brasfoot, focado no contexto de Copa.

> **Por que este projeto existe:** misterfoot é, antes de tudo, um **veículo de aprendizado** de desenvolvimento agêntico — **Spec-Driven Development (SDD)**, **Agent Skills** e **harness engineering**. O jogo é real e jogável, mas a forma como ele é construído é o ponto.

## Princípios de desenvolvimento

- **SDD primeiro.** Toda feature começa por uma spec em [`specs/`](specs/). Código vem depois da spec revisada.
- **Tooling emerge da fricção.** Skills e harness são criados quando uma dor aparece — não especulativamente. *Sinta o atrito, depois automatize.*
- **Walking skeleton.** O v1 é a fatia vertical mais fina que atravessa o jogo de ponta a ponta. Profundidade vem depois.

## Stack

- Next.js + TypeScript
- Supabase (Postgres) — quando houver necessidade real de persistência além do save local
- Vercel (deploy)

## Status

🌱 v0 — escrevendo a spec do walking skeleton. Veja [`specs/001-walking-skeleton.md`](specs/001-walking-skeleton.md).
