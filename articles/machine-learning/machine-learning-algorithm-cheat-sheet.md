---
title: roteiro do algoritmo de aprendizado de aaaMachine | Microsoft Docs
description: "Um roteiro de algoritmo de aprendizado de máquina para impressão o ajuda a escolher o algoritmo de direito de saudação para seu modelo de previsão no estúdio de aprendizado de máquina do Azure."
keywords: "folha de consulta de algoritmo, folha de consulta, algoritmo de aprendizado de máquina"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Página de dicas úteis do algoritmo para Machine Learning para o Microsoft Azure Machine Learning Studio
Olá **Microsoft Azure Machine Learning algoritmo Cheat Sheet** ajuda você a escolher o algoritmo certo de saudação para um modelo de análise de previsão.

[O estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/) tem uma grande biblioteca de algoritmos de saudação ***regressão***, ***classificação***, ***clustering***e ***detecção de anomalias*** famílias. Cada um é projetado tooaddress um tipo de problema de aprendizado de máquina diferente.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>Baixe: Folha de Consulta do algoritmo de Aprendizado de Máquina
**Baixar Olá roteiro aqui: [Machine Learning algoritmo Cheat Sheet (11 x 17 em.)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![Roteiro do algoritmo de aprendizado de máquina: Saiba como toochoose um algoritmo de aprendizado de máquina.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

Baixar e imprimir Olá Cheat Sheet de algoritmo de aprendizado de máquina em Tabloide Tamanho tookeep-lo à mão e obter ajuda, escolhendo um algoritmo.

> [!NOTE]
> Consulte o artigo Olá [como toochoose algoritmos de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-choice.md) para um guia detalhado toousing este roteiro.
> 
> 

## <a name="more-help-with-algorithms"></a>Obter ajuda com algoritmos
* Para obter ajuda usando este roteiro para escolher o algoritmo certo hello, além de uma discussão mais profunda de tipos diferentes de saudação de algoritmos de aprendizado de máquina e como elas são usadas, consulte [como algoritmos de toochoose para Microsoft Azure aprendizado de máquina](machine-learning-algorithm-choice.md).
* Para obter um infográfico para baixar que descreve algoritmos e fornece exemplos, consulte [Infográfico para baixar: conceitos básicos do aprendizado de máquina com exemplos de algoritmo](machine-learning-basics-infographic-with-algorithm-examples.md).
* Para obter uma lista por categoria de todos os Olá máquina algoritmos de aprendizado disponíveis no estúdio de aprendizado de máquina, consulte [inicializar modelo] [ initialize-model] em hello algoritmo Studio de aprendizado de máquina e a Ajuda do módulo.
* Para obter uma lista completa em ordem alfabética dos algoritmos e módulos no Machine Learning Studio, consulte a [Lista de A-Z de módulos do Machine Learning Studio][a-z-list] na Ajuda de módulo e algoritmo do Machine Learning Studio.
* toodownload e imprimir um diagrama que fornece uma visão geral dos recursos de saudação do estúdio de aprendizado de máquina, consulte [diagrama de visão geral dos recursos do estúdio de aprendizado de máquina do Azure](machine-learning-studio-overview-diagram.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>Observações e definições de terminologia para o algoritmo de aprendizado de máquina Olá roteiro

* as sugestões de Olá oferecidas no roteiro algoritmo são aproximadas regras de práticas. Algumas podem ser ajustadas e algumas podem ser flagrantemente violadas. Isso é pretendido toosuggest um ponto de partida. Não tenha medo toorun uma competição cabeça a cabeça entre vários algoritmos em seus dados. Não há simplesmente nenhum substituto para entender os princípios de saudação de cada algoritmo e Noções básicas sobre o sistema de saudação que gerou a seus dados.

* Cada algoritmo de aprendizado de máquina tem seu próprio estilo ou *tendência indutiva*. Para um problema específico, vários algoritmos podem ser apropriados e um algoritmo pode ser mais adequado do que outros. Mas nem sempre é possível tooknow com antecedência qual é hello mais adequado. Em casos assim, vários algoritmos são listados juntos no roteiro hello. Uma estratégia apropriada seria tootry um algoritmo e se os resultados de saudação ainda não estiver satisfatórios, tente Olá outras pessoas. Aqui está um exemplo de hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com/) de um experimento que tenta vários algoritmos em relação a saudação mesmos dados e compara Olá resultados: [classificadores de comparação de classe vários: reconhecimento de letra ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* Há três categorias principais de aprendizado de máquina: **aprendizado supervisionado**, **aprendizado sem supervisão** e **aprendizado de reforço**.

  * Em **aprendizado supervisionado**, cada ponto de dados é rotulado ou associado a uma categoria ou um valor de interesse.  Um exemplo de um rótulo categórico é atribuir uma imagem como, por exemplo, um gato ou um cão.  Um exemplo de um rótulo de valor é o preço de venda Olá associado com um carro usado. meta de aprendizado supervisionado Hello é toostudy muitos rotulado como exemplos de como essas e, em seguida, toobe toomake capaz de previsões sobre pontos de dados futuros. Por exemplo, identificar novas fotos com hello correta animal ou atribuir tooother de preços de venda precisas usadas carros. Este é um tipo popular e útil de aprendizado de máquina. Todos os módulos de saudação no aprendizado de máquina do Azure são de aprendizado supervisionados algoritmos exceto [Clustering K-Means][k-means-clustering].

  * No **aprendizado não supervisionado**, os pontos de dados não têm rótulos associados a eles. Olá em vez disso, o objetivo de um algoritmo de aprendizado sem supervisão são tooorganize dados de saudação de alguma forma ou toodescribe sua estrutura. Isso pode significar agrupá-los em clusters, como faz o K-means, ou encontrar diferentes maneiras de consultar dados complexos para que eles pareçam mais simples.

  * Em **aprendizado Reforce seu**, algoritmo Olá obtém toochoose uma ação no ponto de dados de tooeach de resposta. É uma abordagem comum robótica, onde hello, conjunto de leituras de sensor em um ponto no tempo é um ponto de dados e o algoritmo Olá deve escolher ação próxima do robô Olá. Também é um ajuste natural para aplicativos da Internet das Coisas. algoritmo de aprendizado Olá também recebe um sinal de recompensa foi um curto período de tempo mais tarde, que indica o quão boa decisão de saudação. Com base nisso, o algoritmo Olá modifica sua estratégia de recompensa mais alta da ordem tooachieve hello. Atualmente, não há nenhum módulo de algoritmo de reforço de aprendizado no Aprendizado de Máquina do Azure.

* **Métodos Bayesianos** supõem Olá de pontos de dados estatisticamente. Isso significa que Olá variabilidade unmodeled em um ponto de dados é uncorrelated com outras pessoas, ou seja, ele não pode ser previsto. Por exemplo, se dados Olá que está sendo registrados são o número de saudação de minutos até que o treinamento de metrô Avançar Olá chega, duas medidas tomadas dia entre são estatisticamente independentes. No entanto, duas medidas tomadas um minuto entre eles não são estatisticamente independentes - valor Olá um é altamente previsão do valor de saudação do hello outros.

* **Regressão de árvore de decisão aumentada** aproveita a sobreposição de recurso ou interação entre os recursos. Significa que, em quaisquer dados determinados ponto, Olá valor de um recurso é um pouco previsão do valor de saudação do outro. Por exemplo, em dados de baixa/alta temperatura diária, saber temperatura baixa Olá dia Olá permite toomake uma estimativa razoável em Olá alta. informações de saudação contidas em dois recursos de saudação são um pouco redundantes.

* A classificação de dados em mais de duas categorias pode ser feita usando-se um classificador inerentemente multiclasse ou pela combinação de um conjunto de classificadores de duas classes em um **conjunto**. Abordagem de ensemble hello, há uma classificação de duas classes separada para cada classe - cada um deles separa os dados de saudação em duas categorias: "Esta classe" e "não essa classe." Em seguida, esses classificadores votam na atribuição correto de Olá Olá do ponto de dados. Isso é Olá operacional princípio [Multiclasse uma-vs-todas][one-vs-all-multiclass].

* Vários métodos, incluindo Regressão logística e máquina do ponto Bayesiana hello, suponha que **limites de classe linear**. Ou seja, ele assume que Olá limites entre classes são aproximadamente linhas retas (ou hyperplanes em Olá caso mais geral). Geralmente, isso é uma característica de dados de saudação que você não sabe até depois que você tentou tooseparate, mas ele é algo que normalmente podem ser aprendidos visualizando com antecedência. Se os limites de classe Olá parecer muito irregulares, fique com árvores de decisão, selvas de decisão, redes neurais ou máquinas de vetor de suporte.

* Redes neurais podem ser usadas com variáveis categóricas criando um **variável fictício** para cada categoria, configurá-la too1 em casos onde Olá categoria se aplica, 0, onde ele não.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
