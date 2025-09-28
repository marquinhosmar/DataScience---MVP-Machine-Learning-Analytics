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
