---
title: "aaaWhat é o processo de ciência de dados de equipe?  | Microsoft Docs"
description: "Olá, equipe de processo de ciência de dados é um método sistemático para a criação de aplicativos inteligentes que aproveitam a análise avançada."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>O que é Olá processo de ciência de dados da equipe (TDSP)?
Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md) fornece uma abordagem sistemática toobuilding aplicativos inteligentes que permite que as equipes de dados cientistas toocollaborate efetivamente Olá o ciclo de vida completo de atividades necessárias tooturn esses aplicativos em produtos. Olá TDSP descreve uma sequência de etapas que fornecem **orientação** em como problema de saudação toodefine, configurar as ferramentas de saudação e ambiente necessário, analisar os dados relevantes, criar e avaliar modelos de previsão e, em seguida, implantar esses modelos em aplicativos da empresa. 

Aqui estão as etapas Olá **processo de ciência de dados de equipe**:  

![Fluxo de trabalho do CAP](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

é o processo de saudação **iterativo**: Olá compreender novos e existentes ou refinamentos no modelo de saudação evolui e requer retrabalhando etapas concluídas anteriormente na sequência de saudação. Processos de planejamento de projeto e desenvolvimento organizacional existente são **facilmente adaptado** toowork com hello definido TDSP sequência de etapas. 

Olá etapas no processo de saudação são diagramadas e vinculadas a saudação [aprendizado TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e descrito abaixo.  

## <a name="preparation-steps"></a>Etapas de preparação
## <a name="p1-plan-hello-analytics-project"></a>P1. Plano de projeto de análise de Olá
Iniciar um projeto de análise, definindo suas metas de negócios e os problemas. Eles são especificados em termos de **requisitos de negócios**. Um objetivo central desta etapa é tooidentify Olá negócios variáveis (vendas de previsão ou Olá a probabilidade de uma ordem fraudulenta, por exemplo) que Olá analysis necessidades toopredict toosatisfy esses requisitos. Informações adicionais sobre planejamento, em seguida, é geralmente essencial toodevelop uma compreensão de saudação **fontes de dados** necessário tooaddress Olá objetivos do projeto de saudação da perspectiva de dados analítico. Não é incomum, por exemplo, o toofind que sistemas existentes necessário toocollect e tipos adicionais de tooaddress de dados de log Olá problema e alcançar as metas do projeto hello. Para obter orientações, consulte [planejar seu ambiente para Olá processo de ciência de dados de equipe](machine-learning-data-science-plan-your-environment.md) e [cenários para análises avançadas no aprendizado de máquina do Azure](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Configurar o ambiente de análise
Um ambiente de análise para Olá, equipe de processo de ciência de dados envolve vários componentes: 

* **espaços de trabalho de dados** onde dados saudação estão preparados para análise e modelagem, 
* um **infraestrutura de processamento** para pré-processamento, explorar e modelar dados Olá
* um **infraestrutura de tempo de execução** toooperationalize Olá modelos analíticos e executar aplicativos de cliente inteligente Olá que consomem os modelos de saudação.  

infraestrutura de análise de saudação precisa toobe instalação geralmente é parte de um ambiente que está separado dos principais sistemas operacionais. Mas, normalmente ele utiliza um de vários sistemas de empresa hello, bem como da empresa toohello externas de fontes de dados. infraestrutura de análise de saudação pode ser puramente baseado em nuvem ou uma instalação local ou uma mistura de Olá dois. Para opções, consulte [configurar ambientes de ciência de dados para uso em Olá processo de ciência de dados de equipe](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Etapas da análise:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Ingestão de dados no ambiente analíticos Olá
Olá primeira etapa é dados relevantes do hello toobring de várias fontes, ou de dentro da empresa Olá externa, em um analíticos ambientes onde os dados de saudação podem ser processados. Olá **formato** de saudação dados na fonte podem ser diferente da saudação formato exigido pelo destino hello. Portanto alguma transformação de dados também pode ter toobe feita por ferramentas de inclusão de saudação. Para obter opções, consulte [Carregar dados em ambientes de armazenamento para análise](machine-learning-data-science-ingest-data.md)

No recebimento inicial de toohello de adição de dados, muitos aplicativos inteligentes são necessárias toorefresh Olá dados regularmente como parte de um processo de aprendizado contínuo. Isso pode ser feito configurando um **pipeline de dados** ou um fluxo de trabalho. Isso faz parte da parte iterativo Olá processo Olá que inclui a recompilação e reavaliadas modelos analíticos hello, usados pelo aplicativo inteligente hello, implantação de solução de saudação. Veja, por exemplo, [mover dados de um tooSQL de servidor local no SQL Azure com o Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Explorar e pré-processar os dados
Olá próxima etapa é tooobtain uma compreensão mais profunda dos dados Olá investigando seu **estatísticas de resumo** , relações e usando técnicas de tais **visualização**. O tratamento de problemas de **qualidade de dados** e de integridade, como valores ausentes, incompatibilidades de tipos de dados e relacionamentos de dados inconsistentes também é feito aqui. Pré-processando as transformações são usada tooclean backup dos dados brutos de saudação antes análise adicional e modelagem podem ocorrer. Para obter uma descrição, consulte [tarefas tooprepare dados para o aprendizado de máquina avançada](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Desenvolver recursos
Os cientistas de dados, em colaboração com especialistas de domínio, devem identificar recursos Olá que captura Olá principais propriedades de conjunto de dados hello e que podem ser melhor variáveis de negócios essenciais Olá toopredict usado identificados durante o planejamento. Esses novos recursos podem ser derivados de dados existentes ou podem exigir toobe adicionais de dados coletado. Esse processo é conhecido como **recurso engenharia** e é uma saudação principais etapas da criação de um sistema eficiente análise preditiva. Esta etapa requer uma combinação creative Insights experiência e hello domínio obtida na etapa de exploração de dados hello. Para obter orientações, consulte [engenharia no Olá, equipe de processo de ciência de dados de recurso](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Criar modelos de previsão
Os cientistas de dados criar modelos analíticos toopredict Olá chave variáveis identificados por requisitos de negócios Olá definidos no hello planejamento etapa usando dados que foi limpo e featurized. Suportam a sistemas de aprendizado de máquina várias **modelagem algoritmos** que são aplicáveis tooa ampla variedade de casos. Para obter orientações, consulte [como toochoose algoritmos de aprendizado de máquina do Azure Team](machine-learning-algorithm-choice.md).

Os cientistas de dados devem escolher o modelo de hello mais apropriado para sua tarefa de previsão e não é incomum que resultados de vários modelos necessário toobe combinado tooobtain Olá melhores resultados. Olá para modelagem de dados de entrada é geralmente divididos aleatoriamente em três partes:

* um conjunto de dados de treinamento, 
* um conjunto de dados de validação, 
* um conjunto de dados de testes 

modelos de saudação são criados usando Olá **conjunto de dados de treinamento**. Olá combinação ideal de modelos (com parâmetros ajustados) está selecionada executando modelos hello e medir erros previsão Olá Olá **conjunto de dados de validação**. Olá finalmente **conjunto de dados de teste** tooevaluate usado Olá desempenho do modelo de saudação escolhido no dados independentes que não foi usado tootrain ou validar Olá modelo.  Para procedimentos, consulte [como tooevaluate modelo desempenho no aprendizado de máquina do Azure](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Implantar e consumir modelos
Assim que tivermos um conjunto de modelos que funcionam bem, eles podem ser **operacionalizada** para tooconsume outros aplicativos. Dependendo dos requisitos de negócios hello, as previsões são feitas em **em tempo real** ou em um **lote** base. toobe operacionalizada, modelos de saudação têm toobe exposta com um **abrir a interface da API** que seja consumida facilmente de vários aplicativos tais site on-line, planilhas, painéis ou linha de aplicativos de negócios e de back-end. Consulte [Implantar um serviço Web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Resumo e próximas etapas
Olá [processo de ciência de dados de equipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) é modelada como uma sequência de etapas repetidas que **fornecem orientação** tarefas Olá toouse necessário análise toobuild um inteligente aplicativos avançados. Cada etapa também fornece detalhes sobre como toouse várias tarefas de saudação Microsoft tecnologias toocomplete descrito. 

Enquanto TDSP não estabelece a tipos específicos de **documentação** artefatos, é uma melhor prática toodocument Olá resultados exploração de dados de saudação, modelagem e avaliação e toosave Olá código pertinente para que Olá análise pode iterada quando necessário. Isso também permite a reutilização de saudação ao trabalhar em outros aplicativos que envolvem dados semelhantes e tarefas de previsão de trabalho de análise.

Completo orientações de ponta a ponta que demonstram todas as etapas de saudação no processo de saudação para **cenários específicos** também são fornecidos. Consulte, por exemplo:

* [Olá processo de ciência de dados de equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Olá processo de ciência de dados de equipe em ação: usar clusters de HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).
* [Ciência de Dados usando Spark no Azure HD.mdnsight](machine-learning-data-science-spark-overview.md)
* [Ciência de dados escalonáveis no Azure Data Lake: um passo a passo de ponta a ponta](machine-learning-data-science-process-data-lake-walkthrough.md)

