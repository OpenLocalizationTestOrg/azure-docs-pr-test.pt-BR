---
title: "resultados do modelo aaaInterpret no aprendizado de máquina | Microsoft Docs"
description: "Como o parâmetro de ideal de saudação do toochoose definido por um algoritmo de uso e visualizando as saídas do modelo de pontuação."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Interpretar os resultados do modelo no Azure Machine Learning
Este tópico explica como toovisualize e interpretar os resultados de previsão no estúdio de aprendizado de máquina do Azure. Depois de treinar um modelo e feito previsões sobre ele ("classificado modelo hello"), você precisa toounderstand e interpretar os resultados de previsão hello.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Há quatro tipos principais de modelos de aprendizado de máquina no Azure Machine Learning:

* classificação
* clustering
* regressão
* Sistemas de recomendação

módulos de saudação usados para previsão sobre esses modelos são:

* Módulo [Modelo de Pontuação][score-model] para classificação e regressão
* [Atribuir tooClusters] [ assign-to-clusters] módulo para clustering
* [Recomendação da Caixa da Pontuação][score-matchbox-recommender] para sistemas de recomendação

Este documento explica como os resultados de previsão toointerpret para cada um desses módulos. Para obter uma visão geral desses módulos, consulte [como toochoose parâmetros toooptimize seus algoritmos de aprendizado de máquina do Azure](machine-learning-algorithm-parameters-optimize.md).

Este tópico aborda a interpretação de previsão, mas não a avaliação do modelo. Para obter mais informações sobre como tooevaluate seu modelo, consulte [como tooevaluate modelo desempenho no aprendizado de máquina do Azure](machine-learning-evaluate-model-performance.md).

Se você for novo tooAzure aprendizado de máquina e precisa de ajuda para criar um tooget experiência simples de Introdução, consulte [criar uma experiência simples no estúdio de aprendizado de máquina do Azure](machine-learning-create-experiment.md) no estúdio de aprendizado de máquina do Azure.

## <a name="classification"></a>classificação
Há duas subcategorias de problemas de classificação:

* Problemas com apenas duas classes (classificação de duas classes ou binária)
* Problemas com mais de duas classes (classificação multiclasse)

O aprendizado de máquina do Azure tem toodeal módulos diferentes com cada um desses tipos de classificação, mas métodos Olá para interpretar os resultados de previsão são semelhantes.

### <a name="two-class-classification"></a>Classificação de duas classes
**Teste de exemplo**

Um exemplo de um problema de classificação de duas classes é a classificação de saudação do flores íris. tarefa de saudação é flores de íris tooclassify com base em seus recursos. Olá, conjunto de dados Iris fornecido no aprendizado de máquina do Azure é um subconjunto de Olá popular [conjunto de dados Iris](http://en.wikipedia.org/wiki/Iris_flower_data_set) que contém instâncias de somente dois flor espécies (classes 0 e 1). Há quatro características para cada flor (comprimento da sépala, largura da sépala, comprimento da pétala e largura da pétala).

![Captura de tela do experimento íris](./media/machine-learning-interpret-model-results/1.png)

Figura 1. Experimento do problema de classificação de duas classes da íris

Um teste foi executado toosolve esse problema, como mostrado na Figura 1. Um modelo de árvore de decisão aumentado das duas classes foi treinado e pontuado. Agora você pode visualizar os resultados de previsão de saudação do hello [modelo de pontuação] [ score-model] módulo clicando Olá a porta de saída de hello [modelo de pontuação] [ score-model]módulo e, em seguida, clicando em **visualizar**.

![Módulo de Modelo de pontuação](./media/machine-learning-interpret-model-results/1_1.png)

Isso traz Olá resultados de pontuação, como mostrado na Figura 2.

![Resultados do experimento de classificação de duas classes da íris](./media/machine-learning-interpret-model-results/2.png)

Figura 2. Visualizar o resultado de um modelo de pontuação na classificação de duas classes

**Interpretação de resultado**

Há seis colunas na tabela de resultados de saudação. quatro colunas de saudação à esquerda são quatro recursos hello. Olá direito duas colunas, rótulos de pontuação e as probabilidades de pontuação, são os resultados de previsão de saudação. Olá probabilidades pontuadas de coluna mostra Olá probabilidade flor pertence toohello positivo classe (classe 1). Por exemplo, Olá primeiro número Olá coluna (0.028571) significa que há probabilidade 0.028571 Olá flor primeiro pertence tooClass 1. Olá rótulos de pontuação coluna mostra Olá prevista classe para cada flor. Isso se baseia na coluna de probabilidades pontuadas de saudação. Se Olá pontuada de probabilidade de flor for maior que 0,5, ele é previsto como classe 1. Caso contrário, ela será prevista como Classe 0.

**Publicação de serviço Web**

Depois que os resultados de previsão Olá são entendidos e julgados som, hello experimento pode ser publicado como um serviço web para que você pode implantá-lo em vários aplicativos e chamá-lo tooobtain previsões de classe em qualquer flor íris novo. toolearn como toochange um treinamento experiências em um experimento de pontuação e publicá-lo como um serviço web, consulte [publicar serviço de web de aprendizado de máquina do Azure Olá](machine-learning-walkthrough-5-publish-web-service.md). Esse procedimento fornece um teste de pontuação conforme mostra a Figura 3.

![Captura de tela do teste de pontuação](./media/machine-learning-interpret-model-results/3.png)

Figura 3. Experiência de problema de classificação de duas classes Olá iris de pontuação

Agora você precisa tooset Olá entrada e saída para o serviço web de saudação. entrada Hello está porta de entrada à direita de saudação de [modelo de pontuação][score-model], que é Olá íris flor recursos entrada. Olá opção de saída de hello depende se você estiver interessado em Olá previu classe (classificado rótulo), Olá pontuação de probabilidade, ou ambos. Neste exemplo, supõe-se que tem interesse em ambas. Olá tooselect desejado de colunas de saída, use um [selecionar colunas no conjunto de dados] [ select-columns] módulo. Clique em [Selecionar Colunas no Conjunto de Dados][select-columns], clique em **Seletor de colunas de inicialização** e selecionamos **Rótulos Pontuados** e **Probabilidades Pontuadas**. Depois de configurar a porta de saída Olá [selecionar colunas no conjunto de dados] [ select-columns] e executá-lo novamente, você deve estar pronto toopublish experiência de pontuação hello como um serviço web clicando **publicar na WEB SERVIÇO**. teste final Olá se parece com a Figura 4.

![experiência de classificação de duas classes íris Olá](./media/machine-learning-interpret-model-results/4.png)

Figura 4. Teste de pontuação final do problema de classificação de duas classes da íris

Depois de executar o serviço da web de saudação e insira alguns valores de recurso de uma instância de teste, o resultado de saudação retorna dois números. número da primeira Olá é Olá pontuada de rótulo e Olá segundo é Olá pontuada de probabilidade. Com uma probabilidade de 0,9655, essa flor é prevista como Classe 1.

![Modelo de pontuação de interpretação do teste](./media/machine-learning-interpret-model-results/4_1.png)

![Resultados do teste de pontuação](./media/machine-learning-interpret-model-results/5.png)

Figura 5. Resultado do serviço Web da classificação de duas classes de íris

### <a name="multi-class-classification"></a>Classificação multiclasse
**Teste de exemplo**

Nesse experimento, você executa uma tarefa de reconhecimento de letra como um exemplo de classificação multiclasse. Olá classificador tentativas toopredict um determinado letra (classe) com base em alguns valores de atributo manual extraídos de imagens de saudação manual.

![Exemplo de reconhecimento de letra](./media/machine-learning-interpret-model-results/5_1.png)

Nos dados de treinamento hello, há 16 recursos extraídos de imagens de letra manual. Olá 26 letras de formulário nosso 26 classes. Figura 6 mostra um experimento que treina uma classificação multiclasse de modelo para o reconhecimento de letra e prever Olá mesmo recurso conjunto em um conjunto de dados de teste.

![Teste de classificação multiclasse de reconhecimento de letra](./media/machine-learning-interpret-model-results/6.png)

Figura 6. Teste de problema de classificação multiclasse de reconhecimento de letra

Visualizar resultados Olá Olá [modelo de pontuação] [ score-model] módulo clicando-se a porta de saída Olá [modelo de pontuação] [ score-model] módulo e, em seguida, clicando em **visualizar**, você verá o conteúdo conforme mostrado na Figura 7.

![Resultados do modelo de pontuação](./media/machine-learning-interpret-model-results/7.png)

Figura 7. Visualizar os resultados do modelo de pontuação na classificação multiclasses

**Interpretação de resultado**

16 colunas de saudação à esquerda representam valores de recurso de saudação do conjunto de teste de saudação. colunas de saudação com nomes como probabilidades pontuadas para a classe "XX" são como Olá probabilidades pontuadas de coluna no caso de duas classes hello. Eles mostram a probabilidade de Olá Olá entrada correspondente se enquadra em uma determinada classe. Por exemplo, para a entrada da primeira hello, há probabilidade 0.003571 que é uma "A" probabilidade 0.000451 que é um "B" e assim por diante. última coluna do Hello (classificado rótulos) é Olá mesmo como rótulos de pontuação em caso de duas classes hello. Ele seleciona classe Olá Olá maior probabilidade de pontuação, como Olá classe prevista de entrada correspondente hello. Por exemplo, para a entrada da primeira hello, Olá pontuada de rótulo é "F" porque ele tem toobe de probabilidade maior Olá um "F" (0.916995).

**Publicação de serviço Web**

Você também pode obter Olá classificado rótulo para cada probabilidade de entrada e hello de saudação pontuada de rótulo. lógica básica Olá é probabilidade maior de saudação de toofind entre Olá todas as probabilidades de pontuação. toodo isso, você precisa Olá toouse [Executar Script R] [ execute-r-script] módulo. Olá código R é mostrado na Figura 8 e o resultado de saudação do experimento Olá é mostrado na Figura 9.

![Exemplo de código R](./media/machine-learning-interpret-model-results/8.png)

Figura 8. Código de R para extração de rótulos de pontuação e hello associadas probabilidades de rótulos de saudação

![Resultado do teste](./media/machine-learning-interpret-model-results/9.png)

Figura 9. Experiência de pontuação final de problema de classificação multiclasse de reconhecimento de letra Olá

Depois de publicar e executar Olá web service e insira alguns valores de entrada de recurso, Olá retornou resultado parece Figura 10. Essa letra manual, com seus recursos de 16 extraídos, é previsto toobe "T" com probabilidade 0.9715.

![Modelo de pontuação de interpretação do teste](./media/machine-learning-interpret-model-results/9_1.png)

![Resultado do teste](./media/machine-learning-interpret-model-results/10.png)

Figura 10. Resultado do serviço Web da classificação multiclasses

## <a name="regression"></a>regressão
Os problemas de regressão são diferentes dos problemas de classificação. Em um problema de classificação, você está tentando toopredict de classes discretos, como qual classe uma flor íris pertence. Mas como você pode ver no seguinte exemplo de um problema de regressão de saudação, você está tentando toopredict uma variável contínua, como o preço de saudação de um carro.

**Teste de exemplo**

Use a previsão de preços de automóveis como exemplo de regressão. Você está tentando toopredict preço de saudação de um carro com base em seus recursos, incluindo tornar, tipo de combustível, tipo de corpo e roda de unidade. experiência de saudação é mostrada na Figura 11.

![Teste de regressão do preço de automóvel](./media/machine-learning-interpret-model-results/11.png)

Figura 11. Teste de problema de regressão do preço de automóveis

Olá visualizar [modelo de pontuação] [ score-model] módulo, o resultado de saudação aparência Figura 12.

![Resultados de pontuação para o problema de previsão do preço de automóveis](./media/machine-learning-interpret-model-results/12.png)

Figura 12. Resultados de pontuação para problema de previsão de preços de automóvel Olá

**Interpretação de resultado**

Rótulos de pontuação é a coluna de resultado de Olá neste resultado de pontuação. Olá números são preços de saudação previsto para cada carro.

**Publicação de serviço Web**

Você pode publicar Olá experiência de regressão em um serviço web e chamá-lo para previsão de preços de automóvel em Olá mesma maneira como a classificação de duas classes de saudação do caso de uso.

![Teste de pontuação do problema de regressão do preço de automóveis](./media/machine-learning-interpret-model-results/13.png)

Figura 13. Teste de pontuação de um problema de regressão do preço de automóveis

Executar o serviço de web hello, hello retornou resultado parece Figura 14. preço de previsto Olá para este carro é US $15,085.52.

![Modelo de pontuação de interpretação do teste](./media/machine-learning-interpret-model-results/13_1.png)

![Resultados do módulo de pontuação](./media/machine-learning-interpret-model-results/14.png)

Figura 14. Resultado do serviço Web de um problema de regressão do preço de automóveis

## <a name="clustering"></a>clustering
**Teste de exemplo**

Vamos usar Olá conjunto de dados Iris novamente toobuild um experimento de clustering. Aqui você pode filtrar os rótulos de classe Olá Olá conjunto de dados para que ele só tem recursos e pode ser usado para agrupamento. Neste íris caso de uso, especifique número de saudação de toobe clusters dois durante o processo de treinamento hello, o que significa que você faria em um cluster flores Olá em duas classes. experiência de saudação é mostrada na Figura 15.

![Teste do problema de clustering de íris](./media/machine-learning-interpret-model-results/15.png)

Figura 15. Teste do problema de clustering de íris

Clustering difere de classificação no conjunto de dados de treinamento Olá não tem uma verdade rótulos por si só. Grupos de clusters Olá instâncias do conjunto de dados de treinamento em clusters distintos. Durante o processo de treinamento hello, rótulos de modelo Olá Olá entradas aprendendo diferenças Olá entre seus recursos. Depois disso, o modelo treinado Olá pode ser usado toofurther classificar entradas futuras. Há duas partes do resultado de saudação que estamos interessados em dentro de um problema de clustering. a primeira parte de saudação é rotulação Olá conjunto de dados de treinamento e Olá segundo está classificando um novo conjunto de dados com o modelo treinado hello.

Olá primeira parte do resultado Olá pode ser visualizado clicando Olá deixado porta de saída [treinar modelo de Clustering] [ train-clustering-model] e, em seguida, clicando em **visualizar**. visualização de saudação é mostrada na Figura 16.

![Resultado do clustering](./media/machine-learning-interpret-model-results/16.png)

Figura 16. Visualizar o resultado para o conjunto de dados de treinamento de saudação de clustering

resultado de saudação da segunda parte hello, clustering novas entradas com o modelo de clustering treinado Olá, é mostrado na Figura 17.

![Visualizar resultado do clustering](./media/machine-learning-interpret-model-results/17.png)

Figura 17. Visualizar resultado do clustering em um novo conjunto de dados

**Interpretação de resultado**

Embora os resultados de saudação de partes de saudação dois derivam de teste diferentes estágios, pareçam Olá mesmo e são interpretados da saudação mesma maneira. Olá, quatro primeiras colunas são recursos. Olá última coluna, atribuições, é o resultado da previsão hello. saudação de entradas atribuídas Olá mesmo número estão previstas toobe em Olá mesmo cluster, ou seja, eles compartilham semelhanças de alguma forma (esse teste usa a métrica de distância Euclidiana saudação padrão). Porque você Olá número especificado de clusters toobe 2, entradas de saudação em atribuições são rotuladas 0 ou 1.

**Publicação de serviço Web**

É possível publicar Olá clustering experiência em um serviço web e chamá-lo para previsões clusters Olá mesma maneira que na classificação de duas classes Olá caso de uso.

![Teste de pontuação do problema de clustering da íris](./media/machine-learning-interpret-model-results/18.png)

Figura 18. Teste de pontuação de um problema de clustering da íris

Após executar o serviço da web de hello, Olá retornou resultado parece Figura 19. Este flor é previsto toobe cluster 0.

![Modelo de pontuação de interpretação do teste](./media/machine-learning-interpret-model-results/18_1.png)

![Resultado do módulo de pontuação](./media/machine-learning-interpret-model-results/19.png)

Figura 19. Resultado do serviço Web da classificação de duas classes de íris

## <a name="recommender-system"></a>Sistema de recomendação
**Teste de exemplo**

Para sistemas de recomendação, você pode usar o problema de recomendação do restaurante hello como um exemplo: você pode recomendar restaurantes para clientes com base em seu histórico de classificação. dados de entrada Hello consistem em três partes:

* Classificações de restaurante feitas pelos clientes
* Dados de recursos do cliente
* Dados de recurso de restaurante

Há várias coisas que podemos fazer com hello [treinar Recomendador Matchbox] [ train-matchbox-recommender] módulo no aprendizado de máquina do Azure:

* Prever as classificações de um determinado usuário e item
* Recomendamos tooa itens dado de usuário
* Localizar usuários tooa relacionados dado de usuário
* Localizar itens tooa relacionados fornecido item

Você pode escolher o que você deseja toodo selecionando opções Olá quatro em Olá **tipo de previsão do Recomendador** menu. Aqui, você pode percorrer todos os quatro cenários.

![Recomendação do Matchbox](./media/machine-learning-interpret-model-results/19_1.png)

Um teste típico do Azure Machine Learning para o sistema de recomendação é semelhante à Figura 20. Para obter informações sobre como toouse esses módulos do sistema de recomendação, consulte [treinar recomendador matchbox] [ train-matchbox-recommender] e [classificar recomendador matchbox] [ score-matchbox-recommender].

![Teste do sistema de recomendação](./media/machine-learning-interpret-model-results/20.png)

Figura 20. Teste do sistema de recomendação

**Interpretação de resultado**

**Previsão das classificações de um determinado usuário e item**

Selecionando **previsão de classificação** em **tipo de previsão do Recomendador**, você está solicitando a recomendação Olá Olá toopredict de sistema de classificação para um determinado usuário e item. Olá visualização de saudação [classificar Recomendador Matchbox] [ score-matchbox-recommender] saída aparência da Figura 21.

![Resultado de sistema de recomendação hello – previsão de classificação de pontuação](./media/machine-learning-interpret-model-results/21.png)

Figura 21. Visualizar resultados de pontuação de saudação do sistema de recomendação hello – previsão de classificação

Olá primeiras duas colunas são pares de item-usuário Olá fornecidos pelos dados de entrada hello. terceira coluna de saudação é Olá classificação prevista de um usuário para um determinado item. Por exemplo, na primeira linha de saudação, o cliente que u1048 é previsto restaurante toorate 135026 como 2.

**Recomendamos tooa itens dado de usuário**

Selecionando **recomendação de Item** em **tipo de previsão do Recomendador**, você está solicitando a recomendação de saudação sistema toorecommend itens tooa fornecido do usuário. Olá último parâmetro toochoose neste cenário é *recomendável a seleção de item*. Olá opção **de itens classificados (para avaliação de modelo)** é usada principalmente para avaliação durante o processo de treinamento de saudação do modelo. Escolhemos **De Todos os Itens**para este estágio da previsão. Olá visualização de saudação [classificar Recomendador Matchbox] [ score-matchbox-recommender] saída é semelhante a Figura 22.

![Resultado da pontuação do sistema de recomendação - recomendação de item](./media/machine-learning-interpret-model-results/22.png)

Figura 22. Visualizar resultados de pontuação do sistema de recomendação hello – recomendação de item

Olá primeiro de saudação de representa colunas Olá seis recebe itens de toorecommend de IDs de usuário, conforme fornecido por dados de entrada hello. Olá outros cinco colunas representam os itens de saudação recomendados usuário toohello em ordem decrescente de relevância. Por exemplo, na primeira linha de saudação, hello mais recomendado restaurante para cliente U1048 é 134986, seguido por 135018, 134975, 135021 e 132862.

**Localizar usuários tooa relacionados dado de usuário**

Selecionando **usuários relacionados** em **tipo de previsão do Recomendador**, você está solicitando a recomendação de saudação tooa dado de usuário do sistema toofind usuários relacionados. Usuários relacionados são Olá usuários têm preferências semelhantes. Olá último parâmetro toochoose neste cenário é *relacionados a seleção do usuário*. Olá opção **de usuários que classificaram itens (para avaliação de modelo)** é usada principalmente para avaliação durante o processo de treinamento de saudação do modelo. Escolha **De Todos os Usuários** para este estágio da previsão. Olá visualização de saudação [classificar Recomendador Matchbox] [ score-matchbox-recommender] saída aparência da Figura 23.

![Resultado da pontuação do sistema de recomendação - usuários relacionados](./media/machine-learning-interpret-model-results/23.png)

Figura 23. Visualizar os resultados de pontuação do sistema de recomendação hello – usuários relacionados

Olá primeiro de saudação de mostra colunas Olá seis dada usuário IDs necessário toofind relacionadas a usuários, conforme fornecido por dados de entrada. Olá, outro repositório de cinco colunas Olá usuários relacionados previstos de usuário de saudação em ordem decrescente de relevância. Por exemplo, na primeira linha de saudação, Prezado cliente mais relevante para o cliente U1048 é U1051, seguido por U1066, U1044, U1017 e U1072.

**Localizar itens tooa relacionados fornecido item**

Selecionando **itens relacionados** em **tipo de previsão do Recomendador**, você está solicitando a recomendação de saudação item tooa fornecido do sistema toofind itens relacionados. Relacionadas a itens são Olá itens provavelmente toobe gostou por Olá mesmo usuário. Olá último parâmetro toochoose neste cenário é *relacionados a seleção de item*. Olá opção **de itens classificados (para avaliação de modelo)** é usada principalmente para avaliação durante o processo de treinamento de saudação do modelo. Escolhemos **De todos os itens** para este estágio da previsão. Olá visualização de saudação [classificar Recomendador Matchbox] [ score-matchbox-recommender] saída é semelhante a Figura 24.

![Resultado da pontuação do sistema de recomendação - itens relacionados](./media/machine-learning-interpret-model-results/24.png)

Figura 24. Visualizar os resultados de pontuação do sistema de recomendação hello – itens relacionados

Olá primeiro de saudação de representa colunas Olá seis necessário de IDs de item de dado toofind itens relacionados ao, conforme fornecido por dados de entrada hello. Olá, outro repositório de cinco colunas Olá itens relacionados previstos do item de saudação em ordem decrescente em termos de relevância. Por exemplo, na primeira linha de saudação, item de hello mais relevante para o item 135026 é 135074, seguido por 135035, 132875, 135055 e 134992.

**Publicação de serviço Web**

processo de saudação de publicação essas experiências de previsões de tooget de serviços da web é semelhante para cada um dos quatro cenários de saudação. Aqui, faremos segundo cenário de saudação (recomendável itens tooa fornecido do usuário) como um exemplo. Você pode seguir Olá mesmo procedimento com hello três outros.

Salvando Olá treinado sistema de recomendação como um modelo treinado e filtragem tooa de dados de entrada hello coluna de ID de usuário único como solicitado, você pode ligar experimento hello como na Figura 25 e publicá-lo como um serviço web.

![Experiência de problema de recomendação do restaurante Olá de pontuação](./media/machine-learning-interpret-model-results/25.png)

Figura 25. Experiência de problema de recomendação do restaurante Olá de pontuação

Executar o serviço de web hello, hello retornou resultado parece Figura 26. cinco restaurantes recomendado de saudação do usuário U1048 são 134986, 135018, 134975, 135021 e 132862.

![Exemplo de serviço de sistema de recomendação](./media/machine-learning-interpret-model-results/25_1.png)

![Resultados do teste de exemplo](./media/machine-learning-interpret-model-results/26.png)

Figura 26. Resultado do serviço Web do problema de recomendação de restaurante

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
