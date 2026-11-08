# Como se trabalha neste repositório

Vale para pessoas e para agentes de IA. Tudo o que decide o trabalho está em arquivo
aqui dentro; nada depende de conversa.

## Áreas e posse

- **Área** = uma crate em `crates/<nome>` ou um módulo com `mod.rs` próprio.
- O **contrato público** da área (`lib.rs`, traits, tipos exportados) e seus **testes de
  contrato** são escritos e aprovados antes do código interno.
- A posse está em [`CODEOWNERS`](CODEOWNERS). Área sem dono: abra uma issue com o label
  `area:<nome>` e se atribua; a partir daí é sua até a issue fechar.
- **Ninguém mexe em área alheia.** Para mudar o contrato de outra área, abra uma issue
  `contrato:` para o dono aceitar; o PR da mudança é separado e vem antes do uso.

## Fluxo

1. Uma issue por tarefa, com label `area:<nome>` e assignee.
2. Branch `area/<nome>/<n>-<slug>` a partir de `main`.
3. PR para `main`. Entra quando: CI verde + revisão do dono da área tocada.
4. Nenhum commit direto em `main`.

## CI é o juiz

`cargo fmt --check`, `cargo clippy -D warnings`, `cargo test --workspace`, testes de contrato
das áreas vizinhas e o teste de fronteira (nada do privado referenciado aqui). O que passa
entra; opinião não entra.

## Decisões

Toda decisão de arquitetura, stack, formato ou interface vira ADR em `docs/adr/NNNN-slug.md`
(contexto, decisão, consequências, data). Sem ADR não se muda stack, formato nem contrato.

## Agentes de IA

As regras comuns ficam em `CLAUDE.md` (raiz); as regras de uma área, em
`crates/<área>/CLAUDE.md`, escritas pelo dono. Sessão nova começa com `git pull`, leitura de
`docs/plano/mapa.md` e das issues abertas na sua área; termina com PR ou issue atualizada.
