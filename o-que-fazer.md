# Contexto do projeto

Estou fazendo uma prova de Automação de Testes de Software. Preciso criar uma 
classe em JavaScript chamada `GestaoAgricola`, com 20 métodos testáveis, e a 
respectiva suíte de testes usando Jest.

O projeto já está inicializado (npm init + Jest instalado). Estrutura de pastas:
- src/gestaoAgricola.js  → implementação da classe
- __tests__/gestaoAgricola.test.js → testes

# Requisitos da classe

Tema: Gestão Agrícola (inspirado em módulos de agronegócio de ERP, ex: TOTVS Agro).

A classe deve ser composta por **funções puras sempre que possível** (sem 
dependência de banco de dados, API externa ou `new Date()` interno sem 
parâmetro — datas devem ser recebidas como parâmetro, para facilitar os testes).

Implemente os seguintes 20 métodos, com nomes exatamente como abaixo:

## Produtividade e área
1. calcularProdutividadePorHectare(sacasColhidas, areaHectares)
2. calcularAreaTotalPlantio(talhoes) // array de números (hectares)
3. estimarProducaoTotal(produtividadeMedia, areaHectares)
4. calcularPerdaColheita(producaoEstimada, producaoReal) // retorna % de perda

## Defensivos e insumos
5. calcularDosagemDefensivo(litrosPorHectare, areaHectares)
6. calcularCustoInsumos(itens) // array de { quantidade, precoUnitario }
7. validarCarenciaAplicacao(dataAplicacao, dataColheitaPrevista, diasCarencia) // boolean
8. calcularNecessidadeAdubo(areaHectares, kgPorHectare)

## Conversão de unidades
9. converterSacasParaToneladas(sacas, pesoSacaKg = 60)
10. converterToneladasParaSacas(toneladas, pesoSacaKg = 60)
11. converterHectaresParaAlqueires(hectares) // usar alqueire paulista (24.200 m²)
12. converterAlqueiresParaHectares(alqueires)

## Safra e ciclo
13. calcularDiasParaColheita(dataPlantio, cicloDiasCultura) // retorna a data prevista
14. classificarEstagioSafra(diasDesdePlantio, cicloTotal) // retorna string: 
    "germinação" | "floração" | "maturação" | "colheita"
15. verificarJanelaPlantio(dataAtual, inicioJanela, fimJanela) // boolean
16. calcularRotacaoCultura(historicoCulturas) // array de strings; sugere próxima 
    cultura evitando repetir a última usada

## Frete e comercialização
17. calcularFretePorSaca(distanciaKm, valorPorKmPorSaca, quantidadeSacas)
18. calcularValorVendaSafra(quantidadeSacas, precoSacaAtual)
19. calcularMargemLucro(receitaBruta, custoTotalProducao) // retorna % de margem
20. converterUnidadeDefensivo(valor, unidadeOrigem, unidadeDestino) 
    // suportar pelo menos: mL <-> L, g <-> kg

# Regras de implementação

- Cada método deve validar os parâmetros de entrada e lançar erro (`throw new Error(...)`) 
  em casos inválidos, como: área/quantidade negativa, divisão por zero, unidade de 
  conversão não suportada, datas inválidas.
- Use JSDoc simples em cada método explicando parâmetros e retorno.
- Exporte a classe com `module.exports = GestaoAgricola;`

# Requisitos dos testes (Jest)

- Cobrir para CADA método:
  - Pelo menos 1 caso de sucesso (caminho feliz)
  - Pelo menos 1 caso de borda (zero, valores mínimos/máximos)
  - Pelo menos 1 caso de erro/validação (input inválido, deve lançar exceção)
- Usar `describe` para agrupar por método e `test`/`it` para cada caso.
- Nomear os testes de forma clara em português, descrevendo o comportamento esperado.
- Ao final, rodar `npm test` e garantir que todos os testes passam.

# Entregáveis esperados

1. Arquivo `src/gestaoAgricola.js` com a classe completa e comentada.
2. Arquivo `__tests__/gestaoAgricola.test.js` com a suíte de testes completa 
   (mínimo 60 casos de teste no total, considerando os 3 cenários por método).
3. Confirmar ao final que todos os testes passam rodando `npm test`.