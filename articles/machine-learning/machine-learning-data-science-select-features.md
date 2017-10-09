---
title: "seleção de aaaFeature em Olá processo de ciência de dados do Team | Microsoft Docs"
description: "Explica a finalidade de saudação da seleção de recursos e fornece exemplos de sua função no processo de aprimoramento de dados de saudação do aprendizado de máquina."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Seleção de recursos em Olá processo de ciência de dados da equipe (TDSP)
Este artigo explica as finalidades de saudação da seleção de recursos e fornece exemplos de sua função no processo de aprimoramento de dados de saudação do aprendizado de máquina. Esses exemplos foram extraídos do Azure Machine Learning Studio. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Olá engenharia e seleção de recursos é uma parte da saudação processo de ciência da dados (TDSP) da equipe descritas em [novidades Olá processo de ciência de dados de equipe?](data-science-process-overview.md). Engenharia de recurso e seleção são partes Olá **desenvolver recursos** etapa Olá TDSP.

* **recurso engenharia**: este processo tenta toocreate os recursos relevantes adicionais de saudação bruto os recursos existentes nos dados hello e algoritmo de aprendizado de toohello tooincrease capacidade de previsão.
* **seleção de recursos**: esse processo seleciona o subconjunto de chave Olá original de recursos de dados em uma dimensionalidade de saudação tooreduce tentativa de problema de treinamento hello.

Normalmente **recurso engenharia** é aplicada primeiro toogenerate adicionais aos recursos e, em seguida, Olá **seleção de recursos** etapa é executada tooeliminate altamente correlacionado, redundante ou irrelevante recursos.

## <a name="filtering-features-from-your-data---feature-selection"></a>Filtrando recursos de seus dados - Seleção de recursos
Seleção de recursos é um processo que normalmente é aplicado para a construção de saudação de conjuntos de dados de treinamento para tarefas de modelagem de previsão, como tarefas de classificação ou regressão. meta de saudação é tooselect um subconjunto de recursos de saudação do conjunto de dados original Olá que reduza suas dimensões usando um conjunto mínimo de recursos toorepresent Olá máximo de variação nos dados de saudação. Esse subconjunto de recursos são, em seguida, Olá apenas recursos toobe incluídos tootrain modelo de saudação. A seleção de recursos atende a duas finalidades principais.

* Primeiro, a seleção de recursos frequentemente aumenta a precisão de classificação, eliminando recursos irrelevantes, redundantes ou altamente correlacionados.
* Em segundo lugar, ele diminui Olá vários recursos que torna mais eficiente o processo de treinamento do modelo. Isso é particularmente importante para alunos que são caro tootrain como máquinas de vetor de suporte.

Embora a seleção de recurso de busca tooreduce vários Olá recursos no modelo de Olá Olá conjunto de dados usado tootrain, não é geralmente chamado tooby Olá termo "redução de dimensionalidade". Métodos de seleção de recurso extrair um subconjunto de recursos originais em dados saudação sem alterá-los.  Métodos de redução de dimensionalidade empregam recursos de engenharia que podem transformar recursos original hello e, portanto, modificá-las. Exemplos de métodos de redução de dimensionalidade incluem a Análise de Componente Principal, a análise de correlação canônica e a Decomposição de Valor Singular.

Entre outros, uma categoria amplamente aplicada de métodos de seleção de recursos em um contexto supervisionado é a "seleção de recursos baseada em filtros". Avaliando a correlação de saudação entre cada atributo de destino do recurso e hello, esses métodos se aplicam a tooassign uma medida estatística um recurso de tooeach de pontuação. recursos de saudação são então classificados pela pontuação hello, que pode ser usado toohelp conjunto Olá limite para manter ou eliminar um recurso específico. Correlação pessoa, informações mútuas e teste de quadrados do hello Chi são exemplos de medidas estatísticas de saudação usadas nesses métodos.

No Estúdio do Azure Machine Learning, há módulos fornecidos para seleção de recursos. Conforme mostrado na figura a seguir de saudação, esses módulos abrangem [seleção de recursos baseada em filtro] [ filter-based-feature-selection] e [análise Discriminante Linear Fisher] [ fisher-linear-discriminant-analysis].

![Exemplo de seleção de recursos](./media/machine-learning-data-science-select-features/feature-Selection.png)

Considere, por exemplo, uso de saudação do hello [seleção de recursos baseada em filtro] [ filter-based-feature-selection] módulo. Para fins de saudação de conveniência, continuamos exemplo toouse hello texto mineração descrito acima. Suponha que desejamos toobuild um modelo de regressão depois de um conjunto de 256 recursos são criados por meio de saudação [hash de recurso] [ feature-hashing] módulo, essa variável de resposta de saudação é hello "Col1" e representa um catálogo Revise as classificações que variam de 1 too5. Definindo "Método de pontuação do recurso" toobe "Correlação de Pearson", Olá "Coluna de destino" toobe "Col1" e too50 de "Número de recursos desejados" hello. Em seguida, o módulo de saudação [seleção de recursos baseada em filtro] [ filter-based-feature-selection] produzirá um conjunto de dados que contém 50 recursos junto com o atributo de destino hello "Col1". a seguir Olá figura mostra o fluxo de saudação desse teste e Olá parâmetros de entrada que acabamos de descrever.

![Exemplo de seleção de recursos](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Olá seguinte figura mostra Olá conjuntos de dados resultante. Cada recurso é classificado com base em Olá correlação de Pearson entre si mesmo e hello "Col1" do atributo de destino. recursos de saudação com pontos mais altos são mantidos.

![Exemplo de seleção de recursos](./media/machine-learning-data-science-select-features/feature-Selection2.png)

pontuações de saudação correspondente de recursos de saudação selecionado são mostradas no hello figura a seguir.

![Exemplo de seleção de recursos](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Aplicando isso [seleção de recursos baseada em filtro] [ filter-based-feature-selection] módulo, 50 de 256 recursos são selecionados porque eles têm hello mais recursos correlacionados com variável de destino hello "Col1", com base em Olá de pontuação método "Correlação de Pearson".

## <a name="conclusion"></a>Conclusão
Seleção de recursos e de engenharia de recurso são dois normalmente de engenharia e recursos selecionados aumentam a eficiência de saudação do hello treinamento processo que tentativas de informações de chave de saudação do tooextract contidas nos dados de saudação. Eles também melhoram power Olá esses modelos tooclassify Olá de dados de entrada com precisão e toopredict resultados de seu interesse mais robustez. Engenharia de recurso e seleção também podem combinar o aprendizado de saudação toomake computacionalmente mais manejável. Isso é feito, aprimorando e, em seguida, reduzindo o número de saudação de recursos necessários toocalibrate ou treinar um modelo. Matematicamente falando, o modelo de Olá Olá recursos tootrain selecionado são um conjunto mínimo de variáveis independentes que explicam Olá padrões nos dados hello e, em seguida, prever os resultados com êxito.

Observe que nem sempre é necessariamente tooperform seleção de engenharia ou recurso do recurso. Se for necessário ou não depende de dados Olá temos ou coletar, algoritmo Olá que podemos escolher, e Olá objetivo do experimento hello.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

