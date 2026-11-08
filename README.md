# Resonance Core

**Modelador 3D livre para projetos de acústica, áudio, iluminação e vídeo em edificações.**
Desenha o espaço, importa o BIM (IFC), fecha o volume do ar, atribui materiais e áreas de
audiência e entrega um modelo pronto para simulação, sem exportar e converter no meio.

> Estado: fundação em construção. Ainda não há versão para uso. O código do modelador
> (kernel geométrico, viewport, ferramentas) entra aqui por etapas, com histórico.

## O que é

Um projetista de som trabalha hoje com três programas que não conversam: um modelador para
desenhar, um simulador para prever como o espaço soa e a ferramenta do fabricante para
projetar as caixas. A geometria é exportada, convertida e perdida em cada passagem.

O Resonance Core é o primeiro desses três, feito para alimentar os outros dois direto:

- **Desenhar** com a facilidade do SketchUp (empurrar/puxar, grupos, componentes, snaps),
  os facilitadores do CAD paramétrico (esboço com restrições, extrusão, revolução, varredura,
  padrões) e o fluxo de trabalho do BIM (níveis, vistas, pranchas, tabelas).
- **Importar BIM:** vários IFC de uma vez, com detecção de duplicados e sobreposições
  (vale a versão mais nova), seleção do que entra por elemento, classe ou pavimento.
- **Fechar o ar:** o programa fecha sozinho os ambientes que a seleção deixou abertos, com
  faces editáveis; o resultado é um volume fechado, leve e fiel, com material em cada face
  e áreas de audiência onde há gente.
- **Calcular o que é simples, aqui mesmo:** tempo de reverberação por Sabine e Eyring,
  nível direto por sensibilidade e distância, atrasos, quantitativos por material e peça.
- **Exportar:** formato aberto do Resonance (`.rsn`), IFC, DWG/DXF, relatórios.

Simulações completas (mapas de SPL e STI com interferência, traçado de raios, auralização,
render fotométrico) não fazem parte deste repositório: elas rodam em motores separados,
acessados pelo Core através de um contrato público (`SimulationBackend`). Veja
[docs/arquitetura/fronteira.md](docs/arquitetura/fronteira.md).

## Stack

Uma única base **Rust**: kernel geométrico **OCCT** por FFI atrás de um trait formal
(`geometry-kernel`), interface e viewport **wgpu + winit + egui**, cálculo pesado fora da
thread de interface. App nativo para Windows, macOS e Linux; sem navegador no caminho.

## Princípios

- **Poka-yoke:** o programa não deixa errar: volume aberto, face sobreposta, material em
  falta e unidade errada são bloqueados antes de sair, não depois.
- **Testado antes de existir:** cada operação geométrica tem teste de referência (valor
  analítico ou software de referência) antes de entrar na interface.
- **Leve e prático:** abre em segundos, roda em notebook comum, não pede conta para desenhar.
- **Aberto de verdade:** formato de arquivo documentado, importadores e exportadores livres.

## Como contribuir

Leia [CONTRIBUTING.md](CONTRIBUTING.md). Em resumo: uma issue por área, branch por issue,
`main` protegida, revisão do dono da área (`CODEOWNERS`), CI verde antes de entrar.
Decisões de arquitetura viram ADR em `docs/adr/`. Mapa das áreas em
[docs/plano/mapa.md](docs/plano/mapa.md).

## Licença e marca

Código sob **Apache License 2.0** (ver [LICENSE](LICENSE) e [NOTICE](NOTICE)).

**"Resonance", "Resonance Core", "Resonance Pro" e o logotipo são marcas de Lucas Garioli**
e não estão licenciados pela Apache-2.0. Você pode usar, modificar e redistribuir o código;
não pode apresentar o resultado como Resonance nem usar o nome e o logo para identificar
um produto derivado sem autorização por escrito.
