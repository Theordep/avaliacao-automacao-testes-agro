# Avaliação de Automação de Testes — Gestão Agrícola

Projeto de avaliação da disciplina de Automação de Testes de Software. Implementa a classe
`GestaoAgricola`, com 20 métodos puros (sem banco de dados, API externa ou `new Date()` interno)
inspirados em módulos de agronegócio, e a respectiva suíte de testes unitários com Jest.

## Estrutura do projeto

```
src/gestaoAgricola.js          → implementação da classe
__tests__/gestaoAgricola.test.js → suíte de testes (Jest)
.github/workflows/node.js.yml  → pipeline de CI (build, testes e SonarCloud)
sonar-project.properties       → configuração do SonarCloud
```

## Pré-requisitos

- [Node.js](https://nodejs.org/) 18 ou superior
- npm (instalado junto com o Node.js)

## Como rodar

Instale as dependências (necessário apenas uma vez por máquina/clone):

```bash
npm install
```

Rode a suíte de testes:

```bash
npm test
```

Rode os testes com relatório de cobertura:

```bash
npm run coverage
```

Um teste passando aparece assim, sem nenhum `FAIL` na saída:

```
Test Suites: 1 passed, 1 total
Tests:       84 passed, 84 total
```

## A classe `GestaoAgricola`

Todos os métodos são funções puras: recebem os parâmetros necessários (incluindo datas, sempre
como `Date` recebido por fora) e validam a entrada, lançando `Error` em casos inválidos (valores
negativos, divisão por zero, unidades não suportadas, datas inválidas etc.).

### Produtividade e área
- `calcularProdutividadePorHectare(sacasColhidas, areaHectares)`
- `calcularAreaTotalPlantio(talhoes)`
- `estimarProducaoTotal(produtividadeMedia, areaHectares)`
- `calcularPerdaColheita(producaoEstimada, producaoReal)`

### Defensivos e insumos
- `calcularDosagemDefensivo(litrosPorHectare, areaHectares)`
- `calcularCustoInsumos(itens)`
- `validarCarenciaAplicacao(dataAplicacao, dataColheitaPrevista, diasCarencia)`
- `calcularNecessidadeAdubo(areaHectares, kgPorHectare)`

### Conversão de unidades
- `converterSacasParaToneladas(sacas, pesoSacaKg = 60)`
- `converterToneladasParaSacas(toneladas, pesoSacaKg = 60)`
- `converterHectaresParaAlqueires(hectares)`
- `converterAlqueiresParaHectares(alqueires)`

### Safra e ciclo
- `calcularDiasParaColheita(dataPlantio, cicloDiasCultura)`
- `classificarEstagioSafra(diasDesdePlantio, cicloTotal)`
- `verificarJanelaPlantio(dataAtual, inicioJanela, fimJanela)`
- `calcularRotacaoCultura(historicoCulturas)`

### Frete e comercialização
- `calcularFretePorSaca(distanciaKm, valorPorKmPorSaca, quantidadeSacas)`
- `calcularValorVendaSafra(quantidadeSacas, precoSacaAtual)`
- `calcularMargemLucro(receitaBruta, custoTotalProducao)`
- `converterUnidadeDefensivo(valor, unidadeOrigem, unidadeDestino)`

## Testes

A suíte usa `describe` para agrupar os testes por método e `test` para cada caso, com nomes
descritivos em português. Para cada um dos 20 métodos existem pelo menos:

- 1 caso de sucesso (caminho feliz)
- 1 caso de borda (zero, valores mínimos/limite)
- 1 caso de erro/validação (input inválido, deve lançar exceção)

Ao todo, 84 casos de teste.

## CI/CD

O workflow [`.github/workflows/node.js.yml`](.github/workflows/node.js.yml) roda em todo push e
pull request para `main` (e diariamente às 12h):

- **Run Unit Tests**: instala as dependências e roda `npm run coverage`.
- **Run SonarCloud**: executa a análise estática de qualidade do código no
  [SonarCloud](https://sonarcloud.io/project/overview?id=Theordep_avaliacao-automacao-testes-agro).
