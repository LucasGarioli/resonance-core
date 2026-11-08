# Mapa das áreas do Resonance Core

Fonte única de "quem faz o quê". Atualize no mesmo PR que muda a posse ou o estado.
Estados: `planejada` · `contrato` (trait + testes de contrato aprovados) · `em curso` ·
`estável` · `congelada`.

| Área (crate) | O que é | Depende de | Dono | Estado |
|---|---|---|---|---|
| `common` | tipos básicos, unidades, erros | — | @LucasGarioli | planejada (migração) |
| `geometry-kernel` | contrato do kernel geométrico (trait, tipos, erros) | `common` | @LucasGarioli | planejada (migração) |
| `occt-sys`, `occt-kernel`, `occt-bridge` | OCCT 8 por FFI, implementação do trait | `geometry-kernel` | @LucasGarioli | planejada (migração) |
| `cad-engine` | documento, hierarquia, operações, undo/redo, snaps | `geometry-kernel` | — | planejada (migração) |
| `render-engine` | viewport wgpu, câmera, seleção | `cad-engine` | — | planejada (migração) |
| `ifc-import` | leitura de IFC, duplicados, sobreposições | `cad-engine` | — | planejada (migração) |
| `air-shell` | fechamento do volume do ar, materiais por face, áreas de audiência, emendas | `cad-engine`, `ifc-import` | — | planejada |
| `simple-acoustics` | Sabine/Eyring, SPL direto, atrasos, quantitativos | `air-shell` | — | planejada |
| `simulation-api` | trait `SimulationBackend`, `RsnModel`, `NullBackend` | `air-shell` | @LucasGarioli | contrato (a escrever) |
| `rsn-format` | leitura e escrita do `.rsn`, versionamento | `cad-engine` | — | planejada |
| `apps/studio` | o aplicativo (egui + winit) | tudo acima | — | planejada (migração) |

"Migração" = código já existente em repositório anterior, que entra aqui por etapas com
histórico, crate por crate, cada uma com seus testes passando na CI antes da próxima.

## Ordem de entrada (proposta)

1. `common`, `geometry-kernel`, `occt-*` (fundação, já estável no repositório de origem)
2. `cad-engine`, `render-engine`, `apps/studio` (o modelador abre e desenha)
3. `ifc-import`, `air-shell` (BIM → ar fechado)
4. `simulation-api`, `rsn-format` (o contrato e o formato)
5. `simple-acoustics` (o que se calcula aqui)
