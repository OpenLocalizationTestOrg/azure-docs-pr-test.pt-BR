---
title: "modelos de análise de texto aaaCreate no estúdio de aprendizado de máquina do Azure | Microsoft Docs"
description: "Como os modelos de análises de texto toocreate no estúdio de aprendizado de máquina do Azure usando módulos de pré-processamento de texto, N-grams ou hash de recurso"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Criar modelos de análise de texto no Azure Machine Learning Studio
Você pode usar toobuild de aprendizado de máquina do Azure e utilizar modelos de análise de texto. Esses modelos podem ajudá-lo a resolver, por exemplo, problemas de classificação de documento ou análise de sentimento.

Em um experimento de análise de texto, geralmente, você pode:

1. Limpar e pré-processar o conjunto de dados de texto
2. Extrair vetores de recurso numérico de um texto pré-processado
3. Treinar o modelo de classificação ou regressão
4. Pontuação e validar o modelo de saudação
5. Implantar Olá modelo tooproduction

Neste tutorial, você aprenderá essas etapas conforme examinamos um modelo de análise de sentimento usando o conjunto de dados Amazon Book Reviews (consulte o artigo de pesquisa “Biographies, Bollywood, Boom-boxes and Blenders: Domain Adaptation for Sentiment Classification” de John Blitzer, Mark Dredze e Fernando Pereira; Association of Computational Linguistics (ACL), 2007). Esse conjunto de dados consiste em pontuações de crítica (1-2 ou 4-5) e um texto de forma livre. Olá, meta é toopredict pontuação de revisão de saudação: baixo (1 - 2) ou alto (4-5).

Você pode encontrar os experimentos abordados neste tutorial na Galeria do Cortana Intelligence:

[Prever crítica literária](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Prever crítica literária – Experimento preditivo](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>Etapa 1: Limpar e pré-processar o conjunto de dados de texto
Começamos Olá experimento, dividindo pontuações de revisão de saudação em categórica buckets baixa e alta tooformulate Olá problema classificação de duas classes. Usamos os módulos [Editar Metadados](https://msdn.microsoft.com/library/azure/dn905986.aspx) e [Agrupar Valores Categóricos](https://msdn.microsoft.com/library/azure/dn906014.aspx).

![Criar rótulo](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

Em seguida, podemos limpar Olá texto usando [texto pré-processamento](https://msdn.microsoft.com/library/azure/mt762915.aspx) módulo. Olá limpeza reduz o ruído de Olá Olá conjunto de dados, ajudam você a encontrar hello mais importantes recursos e melhora Olá precisão do modelo final hello. Removemos palavras irrelevantes (stop words) – palavras comuns, como “o” ou “um” – bem como números, caracteres especiais, caracteres duplicados, endereços de email e URLs. Podemos também converter Olá texto toolowercase, lemmatize palavras hello e detectar os limites de oração, em seguida, são indicados por "| | |" símbolo pré-processado como texto.

![Pré-processar Texto](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

Se quiser toouse uma lista de palavras irrelevantes personalizados? Você pode passá-la como uma entrada opcional. Você também pode usar personalizadas c# sintaxe expressão regular tooreplace subcadeias de caracteres e remover palavras por parte da fala: substantivos, verbos ou adjetivos.

Depois Olá pré-processamento for concluído, é dividir os dados de saudação em treinamento e conjuntos de testes.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>Etapa 2: Extrair vetores de recurso numérico de um texto pré-processado
toobuild um modelo de dados de texto, você normalmente tem texto de forma livre tooconvert em vetores de recursos numéricos. Neste exemplo, usamos [recursos N-Gram extrair texto](https://msdn.microsoft.com/library/azure/mt762916.aspx) formato toosuch dados de texto do módulo tootransform hello. Este módulo usa uma coluna de palavras separadas por espaço em branco e calcula um dicionário de palavras ou N-gramas de palavras, que aparecem no conjunto de dados. Em seguida, ele conta quantas vezes cada palavra, ou N-gram, é exibida em cada registro e cria vetores de recurso das contagens. Neste tutorial, vamos definir too2 de tamanho de N-gram, para que nosso vetores de recursos incluem palavras individuais e combinações de duas palavras subsequentes.

![Extrair N-gramas](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

Aplicamos TF * IDF (termo de frequência de frequência de documento inversa) ponderação tooN-gram contagens. Essa abordagem adiciona o peso de palavras que aparecem frequentemente em um único registro, mas são raros em Olá todo o conjunto de dados. Outras opções incluem o binário, TF e a pesagem de gráfico.

Geralmente, esses recursos de texto têm alta dimensionalidade. Por exemplo, se seu corpus tiver 100.000 palavras exclusivas, seu espaço de recurso terá 100.000 dimensões ou mais, caso sejam usados N-gramas. módulo de recursos de N-Gram extrair Olá fornece um conjunto de dimensionalidade de saudação tooreduce opções. Você pode escolher palavras tooexclude toohave curto ou longo ou muito incomum ou muito frequente valor significativo de previsão. Neste tutorial, excluímos N-gramas que aparecem em menos de 5 registros ou em mais de 80% dos registros.

Além disso, você pode usar o recurso seleção tooselect somente os recursos que são hello mais correlacionados com o destino de previsão. Podemos usar recursos de 1000 de tooselect de seleção de recurso qui-quadrada. Você pode exibir o vocabulário Olá de palavras selecionadas ou N-gramas clicando saída direita de saudação do módulo de extração N-gramas.

Como uma abordagem alternativa toousing extrair N-Gram recursos, você pode usar o módulo de hash de recurso. No entanto, observe que o [Hash de Recursos](https://msdn.microsoft.com/library/azure/dn906018.aspx) não traz funcionalidades de seleção de recursos internos nem a pesagem TF*IDF.

## <a name="step-3-train-classification-or-regression-model"></a>Etapa 3: Treinar o modelo de classificação ou regressão
Agora o texto de saudação foi transformado toonumeric colunas de recursos. saudação de conjunto de dados ainda contém colunas de cadeia de caracteres de estágios anteriores, para que possamos usar selecionar colunas no conjunto de dados tooexclude-los.

Em seguida, usamos [Regressão logística de duas classes](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict nossa meta: pontuação revisão alto ou baixo. Neste ponto, problema de análise do texto de saudação foi transformado em um problema de classificação regular. Você pode usar ferramentas de saudação disponíveis no modelo de saudação do tooimprove de aprendizado de máquina do Azure. Por exemplo, você pode experimentar diferentes classificadores toofind os resultados precisos como eles oferecem ou usam hyperparameter tooimprove precisão de saudação de ajuste.

![Treinar e pontuar](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>Etapa 4: Pontuação e validar o modelo de saudação
Como você validará treinado Olá? Estamos pontuação-la no conjunto de dados de teste hello e avaliar a precisão de saudação. No entanto, modelo Olá aprendeu vocabulário Olá de N-grams e seus pesos de conjunto de dados de treinamento hello. Portanto, devemos usar esse vocabulário e os pesos ao extrair os recursos de dados de teste, como oposição vocabulário de saudação toocreating novamente. Portanto, podemos adicionar recursos de N-Gram extrair módulo toohello pontuação ramificação do experimento hello, conectar Olá saída vocabulário do branch de treinamento e definir modo de vocabulário Olá somente tooread. Também desabilitar Olá a filtragem de N-grams por frequência por instância de too1 mínimo Olá configuração e too100 máximo % e desativar a seleção de recurso de saudação.

Depois de hello coluna de texto em teste de dados foram transformados toonumeric colunas de recursos, excluímos string hello como colunas de estágios anteriores na ramificação de treinamento. Em seguida, usamos previsões do modelo de pontuação módulo toomake e precisão do modelo avaliar módulo tooevaluate hello.

## <a name="step-5-deploy-hello-model-tooproduction"></a>Etapa 5: Implantar Olá modelo tooproduction
modelo de saudação é tooproduction toobe quase pronto implantado. Quando implantado como um serviço Web, ele usa a cadeia de caracteres de texto de forma livre como entrada e retorna uma previsão “alta” ou “baixa”. Ele usa Olá aprendida N-gram vocabulário tootransform Olá texto toofeatures e treinado toomake do modelo de regressão logística uma previsão de recursos. 

tooset a experiência de previsão Olá, podemos vocabulário de N-gram Olá salve primeiro como conjunto de dados e Olá treinou o modelo de regressão logística da ramificação de treinamento de saudação do experimento hello. Em seguida, podemos salvar experimento hello usando toocreate "Salvar como" um gráfico de teste para teste de previsão. Removemos o módulo Olá divisão e a ramificação de treinamento de saudação do experimento hello. Em seguida, conectamos Olá salvo anteriormente N-gram vocabulário e modelo tooExtract N-Gram recursos e módulos do modelo de pontuação, respectivamente. Também removemos o módulo de avaliar modelo hello.

Podemos selecionar colunas de inserção no módulo de conjunto de dados antes da coluna de rótulo do texto de pré-processamento módulo tooremove hello e desmarque a opção "Adicionar pontuação coluna toodataset" no módulo de pontuação. Dessa forma, Olá web não solicitação de serviço rótulo hello, ele está tentando toopredict e não repetirá recursos de entrada hello em resposta.

![Experimento preditivo](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Agora temos um experimento que pode ser publicado como um serviço Web e chamado com APIs de execução em lotes ou solicitação-resposta.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre os módulos de análise de texto na [documentação do MSDN](https://msdn.microsoft.com/library/azure/dn905886.aspx).

