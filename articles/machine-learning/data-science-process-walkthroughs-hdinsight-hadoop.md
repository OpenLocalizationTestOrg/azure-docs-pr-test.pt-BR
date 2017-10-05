---
title: "Passo a passos da ciência de dados do HDInsight Hadoop usando o Hive no Azure | Microsoft Docs"
description: "Os exemplos do Processo de Ciência de Dados de Equipe que mostram o passo a passo do uso do Hive no Azure HDInsight Hadoop para executar análises preditivas."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="85827-103">Passo a passos da ciência de dados do HDInsight Hadoop usando o Hive no Azure</span><span class="sxs-lookup"><span data-stu-id="85827-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="85827-104">Essas orientações usam o Hive com um cluster do HDInsight Hadoop para executar a análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="85827-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="85827-105">Eles seguem as etapas descritas no Processo de Ciência de Dados de Equipe.</span><span class="sxs-lookup"><span data-stu-id="85827-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="85827-106">Para obter uma visão geral do Processo de Ciência de Dados de Equipe, veja [Processo de Ciência de Dados](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85827-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="85827-107">Para obter uma introdução ao Azure HDInsight, veja [Introdução ao Azure HDInsight, a pilha de tecnologia do Hadoop e clusters do Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85827-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="85827-108">Os passo a passos adicionais de ciência de dados que executam o Processo de Ciência de Dados de Equipe são agrupados pela **plataforma** que eles usam:</span><span class="sxs-lookup"><span data-stu-id="85827-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="85827-109">Prever gorjetas de táxi usando Hive com HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="85827-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="85827-110">O passo a passo [Usar clusters do HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) usa dados dos táxis de Nova York para prever:</span><span class="sxs-lookup"><span data-stu-id="85827-110">The [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="85827-111">Se uma gorjeta é paga</span><span class="sxs-lookup"><span data-stu-id="85827-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="85827-112">A distribuição de valores de dica</span><span class="sxs-lookup"><span data-stu-id="85827-112">The distribution of tip amounts</span></span>

<span data-ttu-id="85827-113">O cenário é implementado usando o Hive com um [cluster do Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="85827-113">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="85827-114">Saiba como armazenar, explorar e destacar os dados de engenharia de uma corrida de táxi de NYC disponível publicamente e um conjunto de dados de tarifas.</span><span class="sxs-lookup"><span data-stu-id="85827-114">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="85827-115">Você também pode usar o Azure Machine Learning para criar e implantar os modelos.</span><span class="sxs-lookup"><span data-stu-id="85827-115">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="85827-116">Prever cliques de anúncio usando Hive com HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="85827-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="85827-117">O passo a passo [Usar clusters HDInsight Hadoop do Azure em um conjunto de dados de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) usa um conjunto de dados de clique [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) publicamente disponível para prever se uma gorjeta é paga e se está no intervalo de valores esperados.</span><span class="sxs-lookup"><span data-stu-id="85827-117">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="85827-118">O cenário é implementado usando o Hive com um [cluster HDInsight Hadoop do Azure](https://azure.microsoft.com/services/hdinsight/) para armazenamento, exploração, engenharia de recursos e amostragem de dados.</span><span class="sxs-lookup"><span data-stu-id="85827-118">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="85827-119">Ele usa o Azure Machine Learning para criar, treinar e classificar um modelo de classificação binária prevendo se um usuário clica em um anúncio.</span><span class="sxs-lookup"><span data-stu-id="85827-119">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="85827-120">O passo a passo termina mostrando como publicar um destes modelos como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="85827-120">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="85827-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85827-121">Next steps</span></span>

<span data-ttu-id="85827-122">Para uma discussão sobre os principais componentes do Processo de Ciência de Dados de Equipe, veja [Visão geral do Processo de Ciência de Dados de Equipe](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85827-122">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="85827-123">Para uma discussão sobre o ciclo de vida do Processo de Ciência de Dados de Equipe que você pode usar para estruturar seus projetos de ciência de dados, veja [Ciclo de vida do Processo de Ciência de Dados de Equipe](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="85827-123">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="85827-124">O ciclo de vida descreve as etapas, do início ao fim, que os projetos normalmente seguem quando são executados.</span><span class="sxs-lookup"><span data-stu-id="85827-124">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

