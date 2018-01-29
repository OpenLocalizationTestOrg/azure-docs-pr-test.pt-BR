---
title: "Estágio de implantação do ciclo de vida do Processo de Ciência de Dados da Equipe – Azure | Microsoft Docs"
description: "As metas, as tarefas e as entregas para o estágio de implantação dos seus projetos de ciência de dados"
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
ms.openlocfilehash: 45d801bf0096879143f91feb230445625559379f
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="deployment"></a>Implantação

Este artigo descreve as metas, as tarefas e as entregas associadas à implantação do TDSP (Processo de Ciência de Dados da Equipe). Esse processo fornece um ciclo de vida recomendado que você pode usar para estruturar seus projetos de ciência de dados. O ciclo de vida descreve os estágios principais que os projetos normalmente executam, com frequência de modo iterativo:

   1. **Noções básicas sobre negócios**
   2. **Aquisição de dados e entendimento**
   3. **Modelagem**
   4. **Implantação**
   5. **Aceitação do cliente**

Aqui está uma representação visual do ciclo de vida do TDSP: 

![Ciclo de vida do TDSP](./media/lifecycle/tdsp-lifecycle2.png) 


## <a name="goal"></a>Objetivo
Implante modelos com um pipeline de dados em um ambiente de produção ou semelhante à produção para aceitação do usuário final. 

## <a name="how-to-do-it"></a>Como fazer isso
A principal tarefa abordada neste estágio:

**Operacionalizar o modelo**: implante o modelo e o pipeline em um ambiente de produção ou semelhante à produção para consumo do aplicativo.

### <a name="operationalize-a-model"></a>Operacionalizar um modelo
Depois que você tiver um conjunto de modelos com um bom desempenho, eles poderão ser operacionalizados para o consumo de outros aplicativos. Dependendo dos requisitos de negócios, as previsões são feitas em tempo real ou em lotes. Para implantar modelos, exponha-os com uma interface de API livre. A interface permite que o modelo seja consumido facilmente de vários aplicativos, tais como:

   * Sites online
   * Planilhas 
   * Painéis
   * Aplicativos de linha de negócios 
   * Aplicativos de back-end 

Para obter exemplos de operacionalização de modelos com um serviço Web do Azure Machine Learning, consulte [Implantar um serviço Web do Azure Machine Learning](../studio/publish-a-machine-learning-web-service.md). É uma prática recomendada integrar a telemetria e o monitoramento no modelo de produção e no pipeline de dados implantados. Essa prática ajuda com o relatório de status do sistema e a solução de problemas subsequentes.  

## <a name="artifacts"></a>Artefatos

* Um painel de status que exibe informações sobre a integridade do sistema e as principais métricas
* Um relatório de modelagem final com detalhes da implantação
* Um documento de arquitetura da solução final


## <a name="next-steps"></a>Próximas etapas

Aqui estão os links para cada etapa do ciclo de vida do TDSP:

   1. [Noções básicas sobre negócios](lifecycle-business-understanding.md)
   2. [Aquisição de dados e entendimento](lifecycle-data.md)
   3. [Modelagem](lifecycle-modeling.md)
   4. [Implantação](lifecycle-deployment.md)
   5. [Aceitação do cliente](lifecycle-acceptance.md)

Fornecemos passo a passo completos que demonstram todas as etapas do processo para cenários específicos. O artigo [Passo a passos de exemplo](walkthroughs.md) fornece uma lista dos cenários com descrições de links e miniaturas. Os passo a passo ilustram como combinar ferramentas e serviços de nuvem e locais em um fluxo de trabalho ou pipeline para criar um aplicativo inteligente. 

Para obter exemplos de como executar etapas nos TDSPs que usam o Azure Microsoft Azure Machine Learning Studio, consulte [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess) (Usar o TDSP com o Azure Machine Learning).
