# ADR 0001: licença Apache-2.0, marca reservada e fronteira com os motores

Data: 2026-11-08. Estado: aceita. Decisor: Lucas Garioli.

## Contexto

O Resonance Core é o modelador livre de um conjunto maior de produtos. Precisa de uma
licença que permita uso e integração amplos, sem entregar a marca, e de uma fronteira clara
com motores de simulação que não fazem parte deste repositório.

## Decisão

1. **Licença do código: Apache License 2.0.** Permissiva, com cláusula de patente, compatível
   com as dependências (OCCT LGPL-2.1 com exceção; wgpu, winit, egui MIT/Apache-2.0) e a
   mesma de projetos vizinhos em Rust.
2. **Marca fora da licença.** "Resonance", "Resonance Core", "Resonance Pro" e o logotipo
   são marcas do mantenedor; a Apache-2.0 (seção 6) não concede uso de marca, e o README e o
   NOTICE dizem isso explicitamente.
3. **Fronteira.** O Core conhece motores de simulação só pelo trait `SimulationBackend`
   (`crates/simulation-api`). A dependência vai do motor para o Core, nunca o inverso. Nenhum
   nome, caminho, host ou chave de serviço privado entra aqui; a CI falha se encontrar.
   Detalhes em `docs/arquitetura/fronteira.md`.
4. **Interface: egui + winit + wgpu** (decisão de 2026-08-24 mantida em 2026-11-08; migrar
   para outra biblioteca exigiria refazer a interface principal e fica fora de cogitação até
   o Core estar estável).

## Consequências

- Qualquer pessoa pode usar, modificar e redistribuir o Core, inclusive comercialmente, mas
  não pode chamá-lo de Resonance.
- Motores de terceiros podem se ligar ao Core sem pedir licença; o Core não depende de nenhum.
- A mudança de contrato (`simulation-api`) passa a exigir ADR.
