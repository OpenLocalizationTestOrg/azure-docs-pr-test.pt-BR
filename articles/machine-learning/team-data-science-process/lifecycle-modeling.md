---
title: "Estágio de modelagem do ciclo de vida do Processo de Ciência de Dados da Equipe – Azure | Microsoft Docs"
description: "As metas, as tarefas e os resultados para o estágio de modelagem dos seus projetos de ciência de dados"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: bradsev;
ms.openlocfilehash: a7fc5f2128e9c13182ca5bd7a6bd61ae41ef775c
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="modeling"></a>Modelagem

Este artigo descreve as metas, as tarefas e os resultados associados ao estágio de modelagem do TDSP (Processo de Ciência de Dados da Equipe). Esse processo fornece um ciclo de vida recomendado que você pode usar para estruturar seus projetos de ciência de dados. O ciclo de vida descreve os estágios principais que os projetos normalmente executam, com frequência de modo iterativo:

   1. **Noções básicas sobre negócios**
   2. **Aquisição de dados e entendimento**
   3. **Modelagem**
   4. **Implantação**
   5. **Aceitação do cliente**

Aqui está uma representação visual do ciclo de vida do TDSP:

![Ciclo de vida do TDSP](./media/lifecycle/tdsp-lifecycle2.png) 


## <a name="goals"></a>Metas
* Determine os recursos de dados ideais para o modelo de aprendizado de máquina.
* Crie um modelo de aprendizado de máquina informativo que preveja o destino da maneira mais precisa.
* Crie um modelo de aprendizado de máquina adequado para a produção.

## <a name="how-to-do-it"></a>Como fazer isso
Há três tarefas principais abordadas neste estágio:

  * **Engenharia de recursos**: crie recursos de dados dos dados brutos para facilitar o treinamento do modelo.
  * **Treinamento do modelo**: encontre o modelo que responde à pergunta com mais precisão, comparando suas métricas de sucesso.
  * Determine se seu modelo é **adequado para produção.**

### <a name="feature-engineering"></a>Engenharia de recursos
A engenharia de recursos envolve a inclusão, agregação e transformação de variáveis brutas para criar os recursos usados na análise. Se você desejar obter informações sobre o que está guiando um modelo, então será necessário entender como os recursos estão relacionados entre si e como os algoritmos de aprendizado de máquina devem usar esses recursos. 

Esta etapa requer uma combinação criativa de experiência de domínio e das ideias obtidas na etapa de exploração de dados. A engenharia de recursos é um equilíbrio entre encontrar e incluir variáveis informativas, mas, ao mesmo tempo, tentar evitar muitas variáveis não relacionadas. Variáveis informativas melhoram seus resultados; variáveis não relacionadas introduzem ruído desnecessário no modelo. Você também precisa gerar esses recursos para os novos dados obtidos durante a pontuação. Como resultado, a geração desses recursos só pode depender dos dados disponíveis no momento da pontuação. 

Para obter diretrizes técnicas sobre a engenharia de recursos ao fazer uso de várias tecnologias de dados do Azure, consulte [Feature engineering in the data science process](create-features.md) (Engenharia de recursos no processo de ciência de dados). 

### <a name="model-training"></a>Treinamento do modelo
Dependendo do tipo da pergunta que você estiver tentando responder, haverá vários algoritmos de modelagem disponíveis. Para obter diretrizes sobre como escolher algoritmos, consulte [Como escolher algoritmos para o Microsoft Azure Machine Learning](../studio/algorithm-choice.md). Embora este artigo use o Azure Machine Learning, as diretrizes fornecidas aqui são úteis para quaisquer projetos de aprendizado de máquina. 

O processo de treinamento do modelo inclui as seguintes etapas: 

   * **Dividir os dados de entrada** aleatoriamente para modelagem em um conjunto de dados de treinamento e um conjunto de dados de teste.
   * **Crie os modelos** usando o conjunto de dados de treinamento.
   * **Avalie** o conjunto de dados de treinamento e de teste. Use uma série de algoritmos de aprendizado de máquina concorrentes, juntamente com os vários parâmetros de ajustes associados (conhecidos como *limpeza de parâmetros*), voltados para responder à pergunta de interesse com os dados atuais.
   * **Determine a "melhor" solução** para responder à pergunta, comparando a métrica de sucesso entre os métodos alternativos.

> [!NOTE]
> **Evite o vazamento**: será possível causar o vazamento de dados se você incluir dados de fora do conjunto de dados de treinamento que permite a um modelo ou ao algoritmo de aprendizado de máquina fazer previsões boas de forma irrealista. A perda é um motivo comum pelo qual os cientistas de dados ficam preocupados quando obtêm resultados preditivos que parecem bons demais para serem verdadeiros. Essas dependências podem ser difíceis de serem detectadas. Para evitar vazamentos, geralmente é necessária a iteração entre a criação de um conjunto de dados de análise, a criação de um modelo e a avaliação da precisão dos resultados. 
> 
> 

Fornecemos uma [ferramenta automatizada de modelagem e relatório](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) com o TDSP que pode ser executada por meio de vários algoritmos e limpezas de parâmetros para produzir um modelo de linha de base. Ela também produz um relatório de modelagem de linha de base que fornece um resumo do desempenho de cada combinação de modelo e de parâmetro, incluindo a importância da variável. Esse processo também é iterativo, pois pode gerar mais engenharia de recursos. 

## <a name="artifacts"></a>Artefatos
Os artefatos produzidos neste estágio incluem:

   * [Conjuntos de recursos](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): os recursos desenvolvidos para a modelagem estão descritos na seção **Conjuntos de recursos** do relatório **Definição de dados**. Ele contém ponteiros para o código para gerar os recursos e uma descrição de como o recurso foi gerado.
   * [Relatório de modelo](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): para cada modelo testado, é produzido um relatório padrão baseado em modelo que fornece detalhes sobre cada experimento.
   * **Decisão de ponto de verificação**: avalie se o modelo tem um bom desempenho, suficiente para implantá-lo em um sistema de produção. Algumas perguntas importantes a serem feitas são:
     * O modelo responde à pergunta com confiança suficiente, considerando os dados de teste? 
     * Você deve experimentar abordagens alternativas? Você deve coletar dados adicionais, realizar mais engenharia de recursos ou fazer experimentos com outros algoritmos?

## <a name="next-steps"></a>Próximas etapas

Aqui estão os links para cada etapa do ciclo de vida do TDSP:

   1. [Noções básicas sobre negócios](lifecycle-business-understanding.md)
   2. [Aquisição de dados e entendimento](lifecycle-data.md)
   3. [Modelagem](lifecycle-modeling.md)
   4. [Implantação](lifecycle-deployment.md)
   5. [Aceitação do cliente](lifecycle-acceptance.md)

Fornecemos passo a passo completos que demonstram todas as etapas do processo para cenários específicos. O artigo [Passo a passos de exemplo](walkthroughs.md) fornece uma lista dos cenários com descrições de links e miniaturas. Os passo a passo ilustram como combinar ferramentas e serviços de nuvem e locais em um fluxo de trabalho ou pipeline para criar um aplicativo inteligente. 

Para obter exemplos de como executar etapas nos TDSPs que usam o Azure Microsoft Azure Machine Learning Studio, consulte [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess) (Usar o TDSP com o Azure Machine Learning). 
