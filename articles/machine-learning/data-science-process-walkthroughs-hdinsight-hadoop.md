---
title: "aaaHDInsight Hadoop dados ciência explicações passo a passo usando o Hive no Azure | Microsoft Docs"
description: "Exemplos de saudação processo de ciência de dados de equipe que o guiam através do uso de saudação do Hive em análise preditiva do toodo Hadoop de HDInsight do Azure."
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
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="2ef6e-103">Passo a passos da ciência de dados do HDInsight Hadoop usando o Hive no Azure</span><span class="sxs-lookup"><span data-stu-id="2ef6e-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="2ef6e-104">Essas orientações usam Hive com um análise de previsão de toodo do cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="2ef6e-105">Eles sigam etapas de saudação descritas em Olá processo de ciência de dados de equipe.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="2ef6e-106">Para obter uma visão geral de saudação processo de ciência de dados de equipe, consulte [processo de ciência de dados](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ef6e-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="2ef6e-107">Para uma introdução tooAzure HDInsight, consulte [tooAzure Introdução HDInsight, Olá pilha de tecnologia de Hadoop e clusters de Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2ef6e-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="2ef6e-108">Orientações de ciência de dados adicionais que execute Olá processo de ciência de dados do Team são agrupadas por Olá **plataforma** que eles usam:</span><span class="sxs-lookup"><span data-stu-id="2ef6e-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="2ef6e-109">Prever gorjetas de táxi usando Hive com HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="2ef6e-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="2ef6e-110">Olá [Hadoop de HDInsight Use clusters](machine-learning-data-science-process-hive-walkthrough.md) passo a passo usa dados de Nova York táxis toopredict:</span><span class="sxs-lookup"><span data-stu-id="2ef6e-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="2ef6e-111">Se uma gorjeta é paga</span><span class="sxs-lookup"><span data-stu-id="2ef6e-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="2ef6e-112">distribuição de saudação de quantidades de dica</span><span class="sxs-lookup"><span data-stu-id="2ef6e-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="2ef6e-113">cenário de saudação é implementado usando o Hive com um [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2ef6e-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="2ef6e-114">Você aprenderá como toostore, explorar e recurso engenheiro de dados de uma viagem de táxi NYC disponível publicamente e passagens de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="2ef6e-115">Você também usa toobuild de aprendizado de máquina do Azure e implantar modelos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="2ef6e-116">Prever cliques de anúncio usando Hive com HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="2ef6e-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="2ef6e-117">Olá [Use Clusters de Hadoop de HDInsight do Azure em um conjunto de dados de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) passo a passo usa disponível publicamente [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) clique toopredict de conjunto de dados se uma dica é pago e Olá intervalo de valores esperados.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="2ef6e-118">cenário de saudação é implementado usando o Hive com um [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, explorar, engenheiro de recursos e para baixo de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="2ef6e-119">Ele usa toobuild de aprendizado de máquina do Azure, treinar e classificar um modelo de classificação binária prever se um usuário clica em um anúncio.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="2ef6e-120">instruções passo a passo de saudação conclui mostrando como toopublish um desses modelos como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2ef6e-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ef6e-121">Next steps</span></span>

<span data-ttu-id="2ef6e-122">Para obter uma discussão dos componentes-chave Olá que compõem a saudação processo de ciência de dados de equipe, consulte [visão geral do processo de ciência de dados de equipe](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ef6e-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="2ef6e-123">Para obter uma discussão do ciclo de vida do processo de ciência de dados de equipe Olá que você pode usar toostructure seus projetos de ciência de dados, consulte [ciclo de vida do processo de ciência de dados de equipe](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="2ef6e-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="2ef6e-124">ciclo de vida de saudação descreve as etapas de hello, do início toofinish, que projetos normalmente seguem quando eles são executados.</span><span class="sxs-lookup"><span data-stu-id="2ef6e-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

