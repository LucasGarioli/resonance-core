# Fronteira entre o Resonance Core e os motores de simulação

Data: 2026-11-08. Estado: aprovado (decisão do mantenedor).

## Regra

O Core é livre e completo sozinho: desenha, importa, fecha o ar, calcula o que é simples e
exporta. **Ele não contém nenhum motor de simulação completa** (mapas com interferência,
traçado de raios, STI, auralização, render fotométrico). Esses motores são produtos
separados, de código fechado ou aberto, e conversam com o Core por um único contrato:

```text
crates/simulation-api        <- vive aqui, público, muda só por ADR
  trait SimulationBackend
    fn capabilities() -> Capabilities
    fn submit(model: &RsnModel, job: JobSpec) -> Result<JobHandle>
    fn poll(handle) -> JobStatus
    fn fetch(handle) -> Result<JobResult>     // mapas, tabelas, imagens
  struct RsnModel  = casca fechada + materiais + fontes + áreas de audiência + metadados
```

- A dependência vai numa direção só: **um motor depende do Core (desta crate); o Core nunca
  depende de um motor.** Um backend local trivial (`NullBackend`, que só valida o modelo)
  acompanha o Core para testes.
- O Core não tem `cfg(feature = "pro")` nem código condicionado a produto pago. O que o
  usuário vê de um motor é o que o backend registrado declara em `capabilities()`.
- Nenhum nome, caminho, host, chave ou esquema de serviço privado entra neste repositório.
  A CI tem um teste de fronteira que falha se encontrar.

## Por quê

Manter o modelador livre e o contrato aberto permite que qualquer motor (comercial, acadêmico
ou do próprio usuário) se ligue ao Core sem pedir licença, e permite que o Core evolua sem
expor o que é de cada motor. Para o usuário, o ganho é um só: a geometria que ele desenha é
a que entra na simulação, sem exportar e converter.

## Formato `.rsn`

O `RsnModel` é a forma em memória do arquivo `.rsn`, o formato nativo e aberto do Core
(especificação em `docs/formato/rsn.md`, a escrever como ADR). É o que trafega entre o Core
e qualquer backend.
