# DataScience---MVP-Machine-Learning-Analytics
Trabalho apresentado na Sprint de Machine Learning &amp; Analitics da Pós Graduação de Ciência de Dados &amp; Analytics PUC Rio. 

## Descrição do Problema

O conjunto de dados do Siconfi é um conjunto de dados multivariado que consiste em medidas que permitem analisar várias situações financeiras dos estados e municipios brasieliros, tais como: evolução da **`Receita`** e **`Despesa Pública`**, capacidade de **`Investimento`**, situação da responsabilidade fiscal, depência de transferências de outros entes, comparativos entre regiões, qualidade do gasto público, entre outros.

O `investimento público` é universalmente reconhecido como um pilar para o desenvolvimento econômico e social. Por meio da formação de capital em infraestrutura, educação, saúde, e outras areas de interesse público, ele não apenas estimula a atividade econômica no curto prazo, mas também eleva a produtividade e a competitividade no longo prazo, sendo um instrumento essencial para a redução das desigualdades.

Em um país de dimensões continentais e com profundas disparidades regionais como o Brasil, a alocação de investimentos pelos governos municipais assume um papel ainda mais crítico, sendo fundamental para promover a convergência de renda e garantir o acesso equitativo a serviços públicos de qualidade.

O presente trabalho tem como objetivos principais analisar os investimentos públicos dos entes municipais do Estado do Ceará durante o período de 2019 a 2024. Bem como a relação `investimento` sobre a `despesa total`, e o `investimento per capta` por habitante.

Inicialmente o objetivo inicial era analisar todos os municípios do Brasil no intervalo citado anteriormente. Devido a grande quantidade de informações e a demora para baixar os dados, optou-se por restringir aos munípios do Estado do Ceará que é o local onde o autor deste trabalho reside.

O **`investimento público`** é uma **`despesa de capital`**. Incluí obras públicas (escolas, hospitais, estradas), compra de equipamentos e imóveis permanentes. Seu objetivo é o desenvolvimento econômico e social (infraestrutura, serviços, geração de ativos).

## Hipóteses do Problema

Restrigindo a amostra aos municipíos do estado do Ceará, as hipóteses que tracei são as seguintes:

- O **`Investimento Público`** segue um padrão uniforme durante um determinado período de tempo ou apresenta variações?

- Avaliar se a maior **`Receita Total`** ou maior **`Despesa Total`** está associada a maior capacidade de **`Investimento`** per capta.

-  Municípios com maiores gastos brutos são os que mais realizam investimentos em termos percentuais?

- É possível `classificar` a `saúde financeira` de um município com base em `indicadores demográficos` e `indicadores financeiros` relacionados ao `Investimento Público`?


## Tipo de Problema

Este é um problema de **`Classificação Supervisionada`**. Dado um conjunto de características como `Despesa Total`, `Depesa Corrente`, `Receita Total`, `Investimento`, `População`, etc, o objetivo é classificar se um município está em com dificuldades orçamentárias com base em seus indicadores de investimento público. Bem como a partir desses mesmos indicadores descobrir  indícios de Saúde Fiscal.

## Seleção de Dados

O dataset do siconfi é um conjunto de dados de domínio público, amplamente disponível e frequentemente incluído em bibliotecas de aprendizado de máquina. É utilizado para diversas finalidades de pesquisas econômicas, bem como no meio acadêmico. É necessária uma etapa de seleção de dados externa, pois o dataset possui muitos dados e de acordo com a finalidade é importante definir o que será filtrado.

O dataset poderia ser carregado diretamente da API do Tesouro Nacional, porém para acelerar o processo de importação de dados o mesmo foi disponibilizado no github otimizando o tempo de execução no cobab de 10 minutos para aproximadmente 10 segundos.

## Total e Tipo das Instâncias

O dataset `df` possui 942.530 instâncias (observações), e 14 colunas. As características de medição são do tipo`float64` (ou ponto flutuante de 64 bits) é um tipo numérico usado para representar números decimais (com casas após a vírgula). Temos também o `int64` (ou inteiro de 64 bits) que é um tipo numérico usado para representar números inteiros (sem casas decimais). E por fim o tipo `object` que é um tipo de dados mais genérico, geralmente ele é usado para armazenar texto (strings).
Não existe valores nulos e nem dados faltantes.

## Atributos do Dataset

O dataset `df` contém 942.530 instâncias com 14 colunas:

- ***exercicio*** : o ano em que os fatos contábeis ocorreram e foram registrados.
- ***instituicao*** : descrição do nome do Município.
- ***cod_ibge*** : código do estado segundo a classificação do IBGE.
- ***uf*** : sigla do estado de localização dos Municípios.
- ***anexo*** :  indica em qual anexo dos demonstrativos contábeis ou fiscais aquela conta aparece ou deve ser demonstrada, conforme exigências da contabilidade pública brasileira.
- ***rotulo*** : é o nome oficial e padronizado da conta contábil, definido pela autoridade competente (como o Tesouro Nacional no caso do PCASP).
- ***coluna*** : dia, mês e ano (coincide com o exercício).
- ***cod_conta*** : número da conta do plano de contas.
- ***conta*** : nome da conta.
- ***valor*** : representa o montante financeiro associado àquela conta contábil.
- ***populacao*** : população do município.
- ***Município*** : repete novamente o município do estado.
- ***Código_Municipio*** : código IBGE do município.
- ***Ano*** : coincide com o ano de exercício.

## Tratamento dos dados

Baseado no foco do problema a ser analisado e nas hipóteses que precisam ser respondidas, foram feitos alguns comandos e ajustes para enxugar e tratar os dados disponíveis no DataFrame `df`. Nesta etapa a quantidade de linhas foram drasticamente reduzidas para 920. Houve uma mudança na composição de colunas. Como para a referida análise é necessário ter informações sobre a situação fiscal dos municípios, cada linha deste novo DataFrame representa um resumo financeiro anual para um município, com métricas chave já calculadas (Receita Total, Despesa Total, Investimento, etc.). Demais colunas desnecessárias foram removidas.

## **O Deflator IPCA:**

Para se evitar comparações enganosas de uma série temporal é importante deflacionar os valores com base em algum **`índice de preços`**. Com isso pode-se analisar o valor real ao longo do tempo neutralizando os efeitos da `inflação`. Isso permite comparações mais consistentes entre anos diferentes, e ao tomador de decisão ter embasamento mais preciso com base em dados reais.
  
O índice que será usado será o `IPCA(Índice de Preços ao Consumidor Amplo)` pois é o índice oficial de inflação usado pelo Banco Central do Brasil para definir a meta de inflação.
O **`IPEADATA`** é uma fonte confiável de dados macroeconômicos brasileiros, e usar o `ipeadatapy` facilita muito a coleta. Foi deflacionado o DataFrame `df_limpo` criando um novo DataFrame com valores deflacionados. O nome do novo DataFrame é `df_real`.

## Estatísticas Descritivas

Estatísticas descritivas fornecem um resumo das características numéricas, incluindo média, desvio padrão, mínimo, máximo e quartis.

## Média

A média é uma medida de tendência central que representa o valor típico ou o ponto de equilíbrio de um conjunto de dados. É calculada somando-se todos os valores e dividindo-se pelo número total de observações. É sensível a valores extremos (outliers).

A média dos **`Investimentos`** no período por município foi de  16.940.000,00 reais. A média da **`Despesa Total`** do período foi 202.030.000,00 reais. Essa relacao de **`Investimento`** sobre a **`Despesa Total`** representa um percentual em torno de `8,38%`.

A média dos **`Investimentos`** considerando o mesmo período só que agora mudando a relação para **`Receita Total`** representa um percentual em torno de `7,66%`.


## Desvio Padrão

O desvio padrão é uma medida de dispersão que quantifica a quantidade de variação ou dispersão de um conjunto de valores. Um desvio padrão baixo indica que os pontos de dados tendem a estar próximos da média do conjunto, enquanto um desvio padrão alto indica que os pontos de dados estão espalhados por uma faixa maior de valores. Ele é a raiz quadrada da variância.

Observamos que:
- Grande desvio padrão em **`Receita`**, **`Despesa Total`** e **`Despesa Corrente`** em realação às médias, indica grande desigualdade entre os Municípios.

- **`Despesas Correntes`** dominam o orçamento dos entes públicos, com média próxima à despesa total.
- **`Investimentos`** são muito pequenos em comparação — representam uma pequena fração do orçamento.
- O baixo desvio padrão de **`Investimentos`** sugere que mesmo os Municípios com maiores orçamentos não investem proporcionalmente mais, o investimento é geralmente baixo em todos.



