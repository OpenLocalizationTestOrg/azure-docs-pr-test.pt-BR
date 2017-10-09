---
title: "desempenho do modelo aaaEvaluate no aprendizado de máquina | Microsoft Docs"
description: "Explica como tooevaluate modelo desempenho no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Como tooevaluate modelo desempenho no aprendizado de máquina do Azure
Este artigo demonstra como tooevaluate Olá desempenho de um modelo no estúdio de aprendizado de máquina do Azure e fornece uma breve explicação de métricas de saudação disponíveis para esta tarefa. Três cenários comuns de aprendizado supervisionado são apresentados: 

* regressão
* classificação binária 
* classificação multiclasse

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Avaliando o desempenho de saudação de um modelo é um dos estágios de núcleo Olá no processo de ciência de dados hello. Ele indica como bem-sucedida Olá pontuação (previsões) de um conjunto de dados foi por um modelo treinado. 

O Azure Machine Learning dá suporte à avaliação de modelo por meio de dois dos seus principais módulos de aprendizado de máquina: [Avaliar Modelo][evaluate-model] e [Modelo de Validação Cruzada][cross-validate-model]. Esses módulos permitem que você toosee o desempenho do seu modelo em termos de um número de métricas que são normalmente usados no aprendizado de máquina e de estatísticas.

## <a name="evaluation-vs-cross-validation"></a>Avaliação versus Validação cruzada
Avaliação e validação cruzada são desempenho de saudação toomeasure modos padrão do seu modelo. Ambas geram métricas de avaliação que você pode inspecionar ou comparar com os outros modelos.

[Avaliar modelo] [ evaluate-model] espera um conjunto de dados como entrada (ou 2 caso em que você deseja que o desempenho de saudação toocompare 2 modelos diferentes de). Isso significa que você precise tootrain seu modelo usando Olá [treinar modelo] [ train-model] módulo e fazer previsões em algum conjunto de dados usando Olá [modelo de pontuação] [ score-model] módulo, antes de poder avaliar os resultados de saudação. Olá avaliação baseia Olá classificado rótulos/probabilidades junto com rótulos de true hello, que são produzidas pelo Olá [modelo de pontuação] [ score-model] módulo.

Como alternativa, você pode usar validação cruzada tooperform um número de avaliar a pontuação de treinar operações (10 dobras) automaticamente em diferentes subconjuntos de dados de entrada hello. dados de entrada Hello estão divididos em partes de 10, onde é reservado para teste e Olá outros 9 para treinamento. Esse processo é repetido 10 vezes e métricas de avaliação de saudação são a média. Isso ajuda a determinar como um modelo seria generalizar toonew conjuntos de dados. Olá [modelo de validação cruzada] [ cross-validate-model] módulo usa em um modelo não treinado e alguns rotulada resultados da avaliação Olá dataset e saídas de cada Olá 10 dobras, além de toohello média de resultados.

Olá seções a seguir, vamos criar modelos de classificação e regressão simples e avaliar o desempenho, usando os dois Olá [avaliar modelo] [ evaluate-model] e hello [validação cruzada Modelo] [ cross-validate-model] módulos.

## <a name="evaluating-a-regression-model"></a>Avaliar um Modelo de regressão
Suponha que desejamos toopredict preço de um carro uso de alguns recursos, como dimensões, potência, especificações de mecanismo e assim por diante. Este é um problema de regressão típicos, Olá onde a variável de destino (*preço*) é um valor numérico contínuo. Podemos pode conter um modelo de regressão linear simples que, determinado recurso Olá valores de um carro determinados pode prever preço de saudação do que carro. Esse modelo de regressão que pode ser usado tooscore Olá mesmo conjunto de dados são treinados em. Quando podemos ter hello preços previstos para todos os carros Olá, podemos pode avaliar o desempenho de Olá do modelo de saudação examinando quanto previsões Olá das preços real Olá em média. tooillustrate isso, usamos Olá *dataset de dados (Raw) de preços de automóvel* disponíveis no hello **conjuntos de dados salvos** seção no estúdio de aprendizado de máquina do Azure.

### <a name="creating-hello-experiment"></a>Olá experiência de criação
Adicione Olá espaço de trabalho de tooyour de módulos no estúdio de aprendizado de máquina do Azure a seguir:

* Dados de preço de automóvel (Brutos)
* [Regressão linear][linear-regression]
* [Modelo de Treinamento][train-model]
* [Modelo de Pontuação][score-model]
* [Avaliar Modelo][evaluate-model]

Conectar as portas de saudação conforme mostrado abaixo na Figura 1 e o conjunto de coluna de rótulo de saudação de saudação [treinar modelo] [ train-model] módulo muito*preço*.

![Avaliar um Modelo de regressão](media/machine-learning-evaluate-model-performance/1.png)

Figura 1. Avaliar um Modelo de regressão.

### <a name="inspecting-hello-evaluation-results"></a>Inspecionando os resultados da avaliação Olá
Após experimento Olá em execução, você pode clicar na porta de saída de saudação do hello [avaliar modelo] [ evaluate-model] módulo e selecione *visualizar* toosee resultados da avaliação de saudação. Olá métricas de avaliação disponíveis para modelos de regressão são: *erro absoluto significa*, *erro absoluto significa raiz*, *erro absoluto relativo*,  *Erro ao quadrado relativo*e hello *coeficiente de determinação*.

termo Hello "error" aqui representa a diferença de saudação entre Olá valor previsto e o valor true hello. valor absoluto de saudação ou Olá quadrado dessa diferença são geralmente computada toocapture Olá total prevista de magnitude do erro em todas as instâncias, como diferença Olá entre hello e valor real pode ser negativo em alguns casos. métricas de erro Olá medem o desempenho de previsão de saudação de um modelo de regressão em termos de desvio de média de saudação de suas previsões de valores true hello. Valores mais baixos de erro significam que o modelo Olá é mais preciso fazer previsões. Uma métrica de erro geral de 0 significa que Olá modelo se ajusta a saudação dados perfeitamente.

coeficiente de saudação de determinação, que é também conhecido como R quadrado, também é uma forma padrão de medir como modelo Olá adequada dados saudação. Ele pode ser interpretado como a proporção de saudação da variação explicada pelo modelo de saudação. Uma proporção mais alta é melhor nesse caso, em que 1 indica um ajuste perfeito.

![Métrica de avaliação de regressão linear](media/machine-learning-evaluate-model-performance/2.png)

Figura 2. Métrica de avaliação de regressão linear.

### <a name="using-cross-validation"></a>Usando Validação Cruzada
Como mencionado anteriormente, você pode executar o treinamento repetido, pontuação e avaliações automaticamente usando Olá [modelo de validação cruzada] [ cross-validate-model] módulo. Tudo o que você precisa nesse caso é um conjunto de dados, um modelo não treinado e um módulo [Modelo de Validação Cruzada][cross-validate-model] (veja a figura abaixo). Observe que você precisa de coluna de rótulo Olá tooset muito*preço* em Olá [modelo de validação cruzada] [ cross-validate-model] propriedades do módulo.

![Validação cruzada de um modelo de regressão](media/machine-learning-evaluate-model-performance/3.png)

Figura 3. A validação cruzada em um modelo de regressão.

Após a experiência de saudação em execução, você pode inspecionar resultados da avaliação Olá clicando na porta de saída à direita de saudação do Olá [modelo de validação cruzada] [ cross-validate-model] módulo. Isso fornecerá uma exibição detalhada das métricas de saudação para cada iteração (partição) e Olá média de resultados de cada uma das métricas de saudação (Figura 4).

![Resultados de validação cruzada de um modelo de regressão](media/machine-learning-evaluate-model-performance/4.png)

Figura 4. Resultados de Validação cruzada de um modelo de regressão.

## <a name="evaluating-a-binary-classification-model"></a>Avaliar um modelo de classificação binária
Em um cenário de classificação binária, Olá variável de destino tem apenas dois resultados possíveis, por exemplo: {0, 1} ou {falso, verdadeiro}, {positivo, negativo}. Suponha que você terá um conjunto de dados de funcionários adultos com alguns dados demográficos e variáveis de emprego e que você é solicitado a nível de renda Olá toopredict, uma variável binária com valores de Olá {"< = 50 mil", "> 50 mil"}. Em outras palavras, a classe negativo Olá representa funcionários Olá tornar menor que ou igual a too50K por ano e Olá positivo classe representa todos os outros funcionários. Como no cenário de regressão Olá, podemos treinar um modelo, pontuação alguns dados e avaliar os resultados de saudação. Olá aqui a principal diferença é a opção Olá métricas de que aprendizado de máquina do Azure computa e saídas. cenário de previsão de nível de renda de saudação tooillustrate, usaremos Olá [adulto](http://archive.ics.uci.edu/ml/datasets/Adult) toocreate de conjunto de dados o aprendizado de máquina do Azure experimentar e avaliar o desempenho de saudação de um modelo de regressão logística de duas classes, um binário comumente usado classificador.

### <a name="creating-hello-experiment"></a>Olá experiência de criação
Adicione Olá espaço de trabalho de tooyour de módulos no estúdio de aprendizado de máquina do Azure a seguir:

* Conjunto de dados de classificação binária de receita no recenseamento adulto
* [Regressão logística de duas classes][two-class-logistic-regression]
* [Modelo de Treinamento][train-model]
* [Modelo de Pontuação][score-model]
* [Avaliar Modelo][evaluate-model]

Conectar as portas de saudação conforme mostrado abaixo na Figura 5 e na coluna de rótulo de saudação do conjunto Olá [treinar modelo] [ train-model] módulo muito*renda*.

![Avaliar um modelo de classificação binária](media/machine-learning-evaluate-model-performance/5.png)

Figura 5. Avaliar um modelo de classificação binária.

### <a name="inspecting-hello-evaluation-results"></a>Inspecionando os resultados da avaliação Olá
Após experimento Olá em execução, você pode clicar na porta de saída de saudação do hello [avaliar modelo] [ evaluate-model] módulo e selecione *visualizar* resultados da avaliação toosee hello (Figura 7). Olá métricas de avaliação disponíveis para modelos de classificação binária: *precisão*, *precisão*, *Lembre-se de*, *F1 pontuação*, e *AUC*. Além disso, o módulo hello gera uma matriz de confusão mostrando Olá número de verdadeiros positivos, falsos negativos, falsos positivos e negativos true, bem como *ROC*, *precisão/recuperação*e *Levante* curvas.

A precisão é simplesmente a proporção Olá de instâncias classificadas corretamente. É normalmente métrica primeiro hello, que você observar ao avaliar um classificador. No entanto, quando os dados de teste de saudação são desbalanceada (onde a maioria das instâncias de saudação pertence tooone de classes de saudação), ou você está mais interessado no desempenho de saudação em qualquer uma das classes de hello, precisão realmente não captura a eficácia de um classificador hello. No cenário de classificação de nível de renda hello, suponha que você está testando em alguns dados em que 99% das instâncias de saudação representam pessoas ganham menor ou igual a too50K por ano. É possível tooachieve uma precisão 0,99, prevendo classe hello "< = 50 mil" para todas as instâncias. Nesse caso, o classificador de saudação aparece toobe fazendo um bom trabalho geral, mas na realidade, ele falha tooclassify qualquer um dos indivíduos high-income da saudação (Olá 1%) corretamente.

Por esse motivo, é útil toocompute métricas adicionais que capturam aspectos mais específicos da avaliação de saudação. Antes de entrar em detalhes de saudação dessas métricas, é importante toounderstand matriz de confusão saudação de uma avaliação de classificação binária. classe Olá rótulos no conjunto de treinamento Olá podem assumir apenas 2 valores possíveis, que é geralmente consulte tooas positivo ou negativo. instâncias Olá positivos e negativos que um classificador prevê corretamente são chamadas de verdadeiros positivos (TP) e verdadeiros negativos (TN), respectivamente. Da mesma forma, instâncias de saudação classificada incorretamente são chamadas de falsos positivos (FP) e falsos negativos (FN). matriz de confusão Olá é simplesmente uma tabela que mostra o número de saudação de instâncias que se enquadram em cada uma dessas categorias 4. O aprendizado de máquina do Azure automaticamente decide qual das duas classes Olá no conjunto de dados Olá classe positivo hello. Se os rótulos de classe Olá são inteiros ou booliano, Olá instâncias rotuladas 'true' ou '1' são atribuídas a classe positivo hello. Se os rótulos de saudação são cadeias de caracteres, como no caso de saudação do conjunto de dados de renda hello, rótulos de saudação são classificados em ordem alfabética e primeiro nível de saudação é escolhido classe negativo do toobe Olá enquanto Olá segundo nível é a classe positivo hello.

![Matriz de confusão de classificação binária](media/machine-learning-evaluate-model-performance/6a.png)

Figura 6. Matriz de confusão de classificação binária.

Voltando toohello problema de classificação de renda, queremos tooask várias perguntas de avaliação que nos ajudam a entender o desempenho de saudação do classificador Olá usado. Uma pergunta muito natural é: ' fora de indivíduos Olá quem Olá modelo toobe previsto ganhando > 50 mil (TP + FP), quantos foram classificados corretamente (TP)?' Essa pergunta pode ser respondida examinando Olá **precisão** do modelo de saudação, que é a proporção de saudação do positivos que foram classificados corretamente: TP/(TP+FP). Outra pergunta comum é "fora de todos os Olá alta rendimentos funcionários com renda > 50 mil (TP + FN), como Olá o classificador classificar corretamente (TP)". Isso é realmente hello **Lembre-se de**, ou a taxa de positivo true Olá: TP/(TP+FN) do classificador de saudação. Você observará que há uma opção óbvia entre a precisão e a recuperação. Por exemplo, dado um conjunto de dados relativamente equilibrado, uma classificação que prevê principalmente positivas instâncias, teria uma recuperação alta, mas em vez disso, baixa precisão tantas instâncias negativo Olá poderia ser classificadas incorretamente resultando em um grande número de falsos positivos. toosee um gráfico de como essas duas métricas variam, você pode clicar em curva de ' Precisão/Lembre-se' hello na página de saída de resultado de avaliação de saudação (parte superior esquerda da Figura 7).

![Resultados da avaliação de classificação binária](media/machine-learning-evaluate-model-performance/7.png)

Figura 7. Resultados da avaliação de classificação binária.

Outro relacionado a métrica que é frequentemente usada é hello **F1 pontuação**, que usa tanto a precisão e a recuperação em consideração. É a média harmônica Olá dessas métricas de 2 e é calculado como tal: F1 = 2 (Lembre-se de precisão x) / (precisão + Lembre-se). Olá F1 é uma avaliação de saudação boa maneira toosummarize em um único número, mas é sempre toolook uma prática recomendada em precisão e recuperação junto toobetter entender como um classificador se comporta.

Além disso, um pode inspecionar a taxa de positivo true Olá versus Olá falsos positivos em Olá **característica operacional receptor (ROC)** curva e Olá correspondente **Olá área na curva (AUC)** valor. Olá próximo essa curva é toohello superior esquerda, desempenho Olá melhor Olá classificador é (ou seja maximizar Olá verdadeiro positivo taxa, minimizando a saudação de falsos positivos). Curvas são toohello fechar diagonal de Olá plotagem, resultados de classificadores que tendem a previsões toomake fechar toorandom adivinhação.

### <a name="using-cross-validation"></a>Usando Validação Cruzada
Como exemplo de regressão hello, podemos executar validação cruzada toorepeatedly treinar, pontuação e avaliar diferentes subconjuntos de dados Olá automaticamente. Da mesma forma, podemos usar o hello [modelo de validação cruzada] [ cross-validate-model] módulo, um modelo de regressão logística não treinado e um conjunto de dados. coluna de rótulo Olá deve ser definida muito*renda* em Olá [modelo de validação cruzada] [ cross-validate-model] propriedades do módulo. Após executando um experimento hello e clicando em Olá direita saída porta Olá [modelo de validação cruzada] [ cross-validate-model] módulo, podemos ver métrica de classificação binária Olá valores para cada partição, além de toohello Média e desvio padrão de cada um. 

![Validação cruzada de um modelo de classificação binária](media/machine-learning-evaluate-model-performance/8.png)

Figura 8. Validação cruzada em um modelo de classificação binária.

![Resultados de validação cruzada de um classificador binário](media/machine-learning-evaluate-model-performance/9.png)

Figura 9. Resultados de validação cruzada de um classificador binário.

## <a name="evaluating-a-multiclass-classification-model"></a>Avaliar um modelo de classificação com multiclass
Esse teste usaremos Olá popular [íris](http://archive.ics.uci.edu/ml/datasets/Iris "íris") conjunto de dados que contém instâncias de 3 tipos diferentes (classes) da fábrica de íris hello. Há 4 valores de recurso (comprimento/largura da sépala e comprimento/largura da pétala) para cada instância. Em experiências anteriores Olá é treinado e modelos de saudação testado usando Olá mesmos conjuntos de dados. Aqui, nós usaremos Olá [dividir dados] [ split] subconjuntos de toocreate 2 do módulo de dados hello, treinar no hello pela primeira vez e pontuação e avaliar em hello segundo. Olá conjunto de dados íris está disponível publicamente no hello [repositório de aprendizado de máquina UCI](http://archive.ics.uci.edu/ml/index.html)e pode ser baixado usando um [importar dados] [ import-data] módulo.

### <a name="creating-hello-experiment"></a>Olá experiência de criação
Adicione Olá espaço de trabalho de tooyour de módulos no estúdio de aprendizado de máquina do Azure a seguir:

* [Importar Dados][import-data]
* [Floresta de Decisão Multiclasse][multiclass-decision-forest]
* [Dividir Dados][split]
* [Modelo de Treinamento][train-model]
* [Modelo de Pontuação][score-model]
* [Avaliar Modelo][evaluate-model]

Conecte as portas de saudação conforme mostrado abaixo na Figura 10.

Definir o índice de coluna de rótulo de saudação da saudação [treinar modelo] [ train-model] too5 do módulo. saudação de conjunto de dados não tem nenhuma linha de cabeçalho, mas sabemos que classe Olá rótulos são Olá quinta coluna.

Clique em Olá [importar dados] [ import-data] módulo e conjunto hello *fonte de dados* propriedade muito*URL da Web via HTTP*e hello *URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Fração de saudação do conjunto de toobe de instâncias usado para treinamento em hello [dividir dados] [ split] módulo (0,7, por exemplo).

![Avaliar um classificador Multiclass](media/machine-learning-evaluate-model-performance/10.png)

Figura 10. Avaliar um classificador Multiclass

### <a name="inspecting-hello-evaluation-results"></a>Inspecionando os resultados da avaliação Olá
Executar teste hello e clique na porta de saída de saudação do [avaliar modelo][evaluate-model]. resultados da avaliação Olá são apresentados na forma de saudação de uma matriz de confusão, nesse caso. matriz de saudação mostra Olá real versus instâncias previstas para todas as classes de 3.

![Resultados da avaliação de classificação multiclass](media/machine-learning-evaluate-model-performance/11.png)

Figura 11. Resultados da avaliação de classificação multiclass.

### <a name="using-cross-validation"></a>Usando Validação Cruzada
Como mencionado anteriormente, você pode executar o treinamento repetido, pontuação e avaliações automaticamente usando Olá [modelo de validação cruzada] [ cross-validate-model] módulo. Você precisará de um conjunto de dados, um modelo não treinado e um módulo [Modelo de Validação Cruzada][cross-validate-model] (veja a figura abaixo). Novamente, será preciso tooset coluna de rótulo de saudação do hello [modelo de validação cruzada] [ cross-validate-model] módulo (índice de coluna 5 neste caso). Após executando um experimento hello e clicando em direita Olá saída porta Olá [modelo de validação cruzada][cross-validate-model], você pode inspecionar os valores da métrica Olá para cada dobra, bem como Olá média e desvio padrão. métricas de saudação exibidas aqui são Olá semelhante toohello das discutidas no caso de classificação binária hello. No entanto, observe que na classificação multiclasse, Olá verdadeiros positivos/negativos e falsos positivos/negativos de computação é feita com base em uma base por classe, pois não há nenhuma classe geral positivo ou negativo. Por exemplo, quando computação precisão de saudação ou cancelamento de saudação 'Setosa íris' classe, presume-se que isso é classe positivo hello e todos os outros como negativo.

![Validação cruzada de um modelo de classificação multiclass](media/machine-learning-evaluate-model-performance/12.png)

Figura 12. Validação cruzada em um modelo de classificação Multiclass.

![Resultados da validação cruzada de um modelo de classificação multiclass](media/machine-learning-evaluate-model-performance/13.png)

Figura 13. Resultados da validação cruzada de um modelo de classificação multiclass.

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

