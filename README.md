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


## Matriz de Correlação

A matriz de correlação mede a força e a direção de uma relação linear que os atributos numéricos das contas podem ter. Valores próximos a 1 indicam uma forte correlação positiva, -1 uma forte correlação negativa, e 0 ausência de correlação linear.

### Interpretação do coeficiente de correlação:

Valor	Interpretação:

- +1.00	Correlação perfeita e positiva
- 0.70 a 0.99	Correlação forte positiva
- 0.40 a 0.69	Correlação moderada positiva (não apareceu no gráfico)
- 0.00 a 0.39	Correlação fraca ou nula
Valores negativos	Correlação negativa (não apareceu no gráfico)

Com base na matriz de correlação, podemos tirar as seguintes conclusões:

**1. Relações Extremamente Fortes e Positivas**

Todas as variáveis apresentadas (`Receita Total`, `Receita Corrente`, `Despesa Total`, `Despesa Corrente`, `Despesa de Capital` e `Investimento`) têm uma correlação extremamente alta e positiva entre si. A correlação em todos os pares é igual ou superior a 0,97. Isso significa que, neste conjunto de dados, todas as contas públicas selecionadas tendem a se mover na mesma direção de forma muito previsível. Quando uma aumenta, as outras também aumentam.


**2. Relações Perfeitas (Correlação = 1,00)**

A matriz revela várias correlações perfeitas, que indicam uma relação linear e direta entre as variáveis. As mais notáveis são:

`Receita Total` e `Receita Corrente`: A correlação de 1,00 sugere que a `Receita Corrente` é o principal componente da `Receita Total` e que ambas se comportam de maneira idêntica.

`Despesa Total` e `Despesa Corrente`: Da mesma forma, a `Despesa Corrent`e é perfeitamente correlacionada com a `Despesa Total`, indicando uma dependência total.

`Receita Total` e `Despesa Total`: A correlação de 1,00 entre a `Receita Total` e a `Despesa Total` é um dos pontos mais importantes. Isso indica que, para este conjunto de dados, cada aumento na receita é acompanhado por um aumento perfeitamente proporcional na despesa.

**3. Relações Fortes, mas não Perfeitas (Correlação < 1,00)**

As contas de capital (`Despesa de Capital` e `Investimento`) têm uma correlação ligeiramente menor (em torno de 0,97 e 0,98) com as contas de receita e despesa correntes. Embora a relação ainda seja muito forte, não é perfeita. Isso sugere que, embora o investimento e o gasto de capital acompanhem o crescimento geral da receita e da despesa, a proporção exata pode variar um pouco, ao contrário das contas "Total" e "Corrente" que se movem em um ritmo idêntico.

Em resumo, a principal conclusão é que todas as contas públicas analisadas estão fortemente interligadas e se movem em uníssono. A matriz sugere um cenário de finanças públicas onde os orçamentos são rigidamente controlados, com as despesas aumentando de forma quase exata em resposta ao crescimento das receitas.

## Análises gráficas e com tabelas

A `Receita_Total` e o `Investimento` não são uniformes no decorrer da série temporal, mas apresentam uma inclinação mais ascendente a partir de 2021. Observa-se por outro lado que a linha tracejada do investimento não aconpanha essa tendência, permanecendo quase que uma reta no mesmo período a partir de 2021.

Evolução média do percentual de **`Investimento`** sobre a **`Despesa Total Real`** dos Municípios apresenta um aumento acentuado entre os anos de 2021 a 2022. Isso pode ser um indicativo de gastos com o episódio da pandemia de COVID-19 que obrigou todos os entes públicos a aumentarem significativamente seus investimentos na saúde pública. Entre 2022 a 2023 ocorre uma queda no percentual.

O estado do **Ceará** tem **184 municípios**, para o gráfico acima não ficar com muita informação visual foi restringido a exibição para **12,5%** do total de municípios, totalizando exatamente **23**.

Percebe-se visualmente uma enorme disparidade do primeiro lugar em gastos comparando com os demais. `Fortaleza` gastou no período 5**5 bilhões e 400 milhões** de reais. Enquanto isso os demais 23 gastaram **53 bilhões e 770 milhões** de reais. Ou seja a capital do Ceará gastou mais que os outros **22** **municípios** juntos.

Analisando o somatório do **`Investimento`**, também restringindo a visualizacão para **12,5%** do total de municípios, totalizando exatamente **23**.
Visualmente continua a disparidade do primeiro lugar em gastos comparando com os demais. `Fortaleza` investiu no período **4 bilhões e 485 milhões** de reais. Enquanto isso os demais **22** gastaram **5 bilhões e 138 milhões** reais.

Pela ótica do **`Investimento`** em valores brutos os outros 22 municípios superaram `Fortaleza` no total investido, o que pela relação anterior não aconteceu (**`Despesa Total`**).

Olhar apenas para números absolutos pode indicar que a capital do Ceará estar à frente de todos os outros municípios do estado nesses quesitos analisados, bem como outros indicadores que tenham relação com o presente objeto de estudo.

Se levarmos em consideração o `fator populacional`, veremos que o cenário acima
muda. Cidades que lideravam em volume absoluto agora estão no meio ou na parte de baixo do gráfico. Fortaleza, até então líder absoluto, está agora em **`72º lugar`**. Isso acontece porque seu enorme volume de investimento é "diluído" por sua população igualmente massiva. Em contrapartida, o topo do ranking é agora ocupado por cidades com populações menores. Nesses locais, um volume de investimento que seria modesto para Fortaleza tem um grande impacto per capita.

Nessa perspectiva, a **`média per capta de investimento por habitante`** (mensura o montante de investimento direcionado, em média, a cada cidadão) em reais para o período analisado em cada município do estado do Ceará mostra a importância de um olhar a partir de um outro critério.


## Definição do Target

Para definir o target será feito as seguintes métricas:

1.	Fazer a média do `Investimento` sobre a `Despesa Total` de todos os  municípios em um determinado ano, e partir desse número classificar os municípios que estão acima e abaixo dessa média nesse mesmo ano. Sendo que os que estão acima da média é positivo, e abaixo da média é negativo;

2.	Fazer a média do `Investimento Per Capta` de todos os municípios em um determinado ano, e partir desse número classificar os municípios que estão acima e abaixo dessa média nesse mesmo ano. Sendo que os que estão acima da média é positivo, e abaixo da média é negativo;

3. Fazer a média da relação `Despesa Corrente` sobre `Receita Total` de todos os municípios em um determinado ano, e partir desse número classificar os que estão acima e abaixo dessa média (inverte-se a lógica das duas anteriores), os que estão acima é negativo pois significa que o orçamento estar com maior comprometimento, e o que estão abaixo é positivo (sobra mais orçamento para investimento);

Feito isso ano a ano será criado 4 categorias (que poderia ser chamado de selo) para classificar os municípios que estão nas seguintes faixas:

`AZUL`: o município atingiu os três parâmetros positivos em um determinado  ano;

`VERDE`: o município atingiu dois parâmetros positivos em um determinado ano;

`AMARELO`: o município atingiu somente 1 parâmetro positivo em um determinado ano;

`VERMELHO`: nível crítico, o município não atingiu nenhum parâmetro em um determinado ano.


## Definição de Features e Target

Nesta etapa são definidas as variáveis de entrada (**features**) e a variável alvo (**target**). Foram removidas do conjunto de treino as colunas de identificação (`Município`, `Codigo_Municipio`, `UF`) e as variáveis derivadas do próprio target (`pontuacao`, `flags`, `media_anual_*`).

Essa remoção é essencial para evitar **data leakage** (vazamento de informação), garantindo que o modelo aprenda apenas a partir de variáveis financeiras e demográficas.


## Divisão da Base em Treino/Teste

Os dados foram divididos em **treino (80%)** e **teste (20%)**, com a opção `stratify=y` para manter a proporção entre classes nos dois conjuntos.

Essa estratégia é importante em problemas de classificação com **desbalanceamento de classes**, pois garante que todas as classes estarão representadas em ambas as amostras.


## Baseline

Antes de aplicar modelos mais sofisticados, é construída uma baseline com `DummyClassifier`, que prevê sempre a classe mais frequente. Essa abordagem estabelece um **piso de desempenho** para o problema. Qualquer modelo real precisa superar esse resultado para ser considerado útil.


## Modelos Reais

Após o baseline, são avaliados dois modelos de classificação:

- **Regressão Logística**: modelo linear, interpretável, usado como baseline mais forte.  
- **Random Forest**: modelo ensemble baseado em múltiplas árvores de decisão, mais robusto para capturar relações complexas entre variáveis.

A comparação entre esses modelos mostra o ganho de performance quando se aplica algoritmos mais sofisticados.


## Comparação dos Modelos

Aqui são comparados os desempenhos do `Baseline`, `Regressão Logística` e `Random Forest`. A análise considera métricas de ***Accuracy***, ***F1 Macro*** e ***F1 Weighted***.


## Interpretação dos resultados

🔹 `Baseline`:

* Accuracy 42%, F1 Macro 0.15.
* Confirma que o dataset é desbalanceado (classe majoritária representa ~42%).
* Esse é o “piso” para comparação.

🔹 `Regressão Logística`:

* Accuracy 65%, mas F1 Macro apenas 0.42.
* Significa que o modelo melhora em relação ao baseline, mas ainda sofre para equilibrar classes minoritárias (VERDE, AMARELO).
* Indica que o dataset não é linearmente separável de forma simples.

🔹 `Random Forest`:

* Accuracy 86%, F1 Macro 0.83.
* Grande salto em relação ao baseline e à LogReg.
* Mostra que o modelo consegue capturar relações mais complexas entre variáveis.
* Esse é a melhor opção.
* Esse resultado reforça a importância do uso de ensembles em problemas de classificação desbalanceados.


## Otimizacao de Hiperparâmetros

Nesta etapa, a **Random Forest** é otimizada com `RandomizedSearchCV`, usando validação cruzada estratificada em 5 folds. O objetivo é encontrar a melhor combinação de hiperparâmetros para **maximizar o F1 Macro**, garantindo maior equilíbrio entre classes. A validação cruzada aumenta a robustez do processo, reduzindo a dependência da divisão específica entre treino e teste.


## Observações e Correções Feitas:

Foi identificado e corrigido um vazamento de dados (`data leakage`) nos testes iniciais. O problema foi detectado por métricas de performance irrealisticamente altas (próximas a 100%) no modelo de baseline.

A causa era a presença de variáveis usadas para criar o target no conjunto de features. Foram removidas as seguintes colunas para solucionar o problema:
Colunas derivadas do target: `pontuacao`, `flag_crit*`, `media_anual_*`.
colunas de identificação: `Município`, `Codigo_Municipio`, `UF`.

Essa correção garantiu que o modelo aprenda apenas a partir de variáveis financeiras e demográficas, sem acesso a "atalhos" para a resposta.


## Gráfico SHARP

Este gráfico de barras mostra a importância média de cada variável para as previsões do melhor modelo:

- Eixo Y (Vertical): Lista as 15 variáveis (features) mais importantes do eu modelo;

- Eixo X (Horizontal): Mostra a "Importância média |SHAP value|". Quanto maior o valor (quanto maior a barra), mais "poder de influência" aquela variável tem, em média, para levar o modelo a decidir entre as classes AZUL, VERDE, AMARELO ou VERMELHO.

O valor absoluto |SHAP value| significa que está sendo medido o tamanho do impacto, não importando se ele empurra a previsão para uma classe "boa" ou "ruim".


## Conclusão

* O experimento demonstrou ganhos progressivos no desempenho dos modelos de classificação.
O **baseline** `(DummyClassifier)` obteve **acurácia de 42%** e `F1 Macro` de **0.15**, refletindo apenas a proporção da classe majoritária.
A `Regressão Logística` atingiu 65% de acurácia e `F1 Macro` de 0.42, indicando melhora em relação ao baseline, mas d**ificuldade em lidar com classes minoritárias.**

* Já a `Random Forest` simples obteve **86% de acurácia** e `F1 Macro` de **0.83**, mostrando superioridade clara. Por fim, a `Random Forest` otimizada via`RandomizedSearchCV` e `validação cruzada` alcançou **91% de acurácia** e `F1 Macro` de **0.88**, com bom equilíbrio entre as classes e robustez validada por `cross-validation`.
Isso evidencia que o modelo é capaz de aprender padrões relevantes a partir de variáveis financeiras e demográficas, mesmo após a exclusão de atributos derivados do target que poderiam causar vazamento de dados.

* O modelo final mostra que é possível prever níveis municipais com boa acurácia a partir de dados financeiros e demográficos, reforçando a aplicabilidade de métodos de machine learning na análise de finanças públicas.


## Resposta as Hipóteses do Problema

Após o desenvolvimento do trabalho segue as respostas percebidas ao final do MVP:

1.  O **`Investimento Público`** segue um padrão uniforme durante um determinado período de tempo ou apresenta variações?

🔹 Descobriu-se que o investimento público não é unfiforme ao longo do tempo. Apresenta períodos de crescimento e outros de queda.

2. Avaliar se a maior **`Receita Total`** ou maior **`Despesa Total`** está associada a maior capacidade de **`Investimento`** per capta.

🔹A avaliação mostrou que municípios que não se destacam nesses quesitos em valores brutos apareceram no top do gráfico em valores per capita.

3. Municípios com maiores gastos brutos são os que mais realizam investimentos em termos percentuais?

🔹Municípios que mais investem em termos brutos estão abaixo da média estadual de investimento em termos percentuais.

4. É possível `classificar` a `saúde financeira` de um município com base em `indicadores demográficos` e `indicadores financeiros` relacionados ao `Investimento Público`?

🔹O uso de Machine Learning mostrou-se plenamente viável para fazer esse processo. Depois de ajustes e uso de melhores algoritmos os resultados foram animadores.



## Limitações

Apesar dos avanços, o MVP apresenta algumas limitações:

* **Construção do target:** a variável resposta foi definida a partir de regras pré-estabelecidas. Isso limita a autonomia do modelo e pode restringir a descoberta de padrões alternativos.

* **Balanceamento de classes**: embora o uso de class_weight="balanced" tenha mitigado parcialmente o problema, ainda há desigualdade no desempenho entre classes (especialmente a classe VERDE).

* **Generalização:** os dados se restringem a um período e a um conjunto específico de municípios. Portanto, a extrapolação dos resultados para outros contextos deve ser feita com cautela.

* **Explicabilidade:** a Random Forest fornece métricas de importância de variáveis, mas não garante interpretação causal direta.


## Sugestões Futuras

* Aplicar técnicas de balanceamento (ex.: SMOTE, undersampling).
* Testar outros algoritmos (Gradient Boosting, XGBoost, LightGBM).
* Revisitar a definição do target com base em indicadores externos.
* Expandir a base de dados para novos períodos e variáveis socioeconômicas.
* Utilizar métodos de interpretabilidade avançados (ex.: SHAP values).
