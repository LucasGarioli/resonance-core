# Resonance Core: regras para agentes

Leia `CONTRIBUTING.md` e `docs/plano/mapa.md` antes de agir. Depois, as regras da sua área em
`crates/<área>/CLAUDE.md`.

- **Só a sua área.** Você edita dentro da área cuja issue é sua. Fora dela, só leitura. Para
  mudar contrato alheio, issue `contrato:`; nunca o PR direto.
- **Escreva só o código necessário.** Menos código, sem cortar validação, segurança nem
  acessibilidade. Nada de abstração para o futuro, de flag "caso precise" nem de reescrita
  do que não foi pedido.
- **Teste antes.** Operação geométrica nova = teste de referência primeiro (valor analítico
  ou software de referência), depois a implementação.
- **Cada número vem de arquivo.** Cota, tolerância, resultado: lido na hora do arquivo ou do
  teste, com o caminho citado. Nada de memória.
- **Decisão vira ADR.** Mudou stack, formato, contrato ou tolerância: `docs/adr/` no mesmo PR.
- **Fronteira pública/privada.** Este repositório não conhece nenhum motor de simulação além
  do trait `SimulationBackend`. Nada de nome, caminho, host ou chave de serviço privado.
- **Português nos documentos, inglês nos identificadores.** Commits em português, no
  imperativo, com a issue no rodapé (`Refs #12`).
- **Fim de sessão:** PR aberto ou issue atualizada com o que falta e o que travou.
