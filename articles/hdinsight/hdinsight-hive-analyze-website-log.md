---
title: "Usar Hive com Hadoop para análise de log do site – HDInsight do Azure | Microsoft Docs"
description: "Saiba como usar o Hive com o HDInsight para analisar os logs do Website. Você usará um arquivo de log como entrada em uma tabela do HDInsight e usará o HiveQL para consultar os dados."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="3909f-104">Usar o Hive com o HDInsight baseado no Windows para analisar logs de sites</span><span class="sxs-lookup"><span data-stu-id="3909f-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="3909f-105">Saiba como usar o HiveQL com HDInsight para analisar os logs de um Website.</span><span class="sxs-lookup"><span data-stu-id="3909f-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="3909f-106">A análise de log do Website pode ser usada para segmentar seu público com base em atividades semelhantes, categorizar os visitantes do site por demografia e descobrir o conteúdo que eles veem, seus Websites de origem e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="3909f-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3909f-107">As etapas neste documento só funcionam com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="3909f-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="3909f-108">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="3909f-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="3909f-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="3909f-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3909f-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3909f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="3909f-111">Neste exemplo, você utilizará um cluster do HDInsight para analisar arquivos de log do Website para obter informações sobre a frequência de visitas ao Website por meio de Websites externos em um dia.</span><span class="sxs-lookup"><span data-stu-id="3909f-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="3909f-112">Você também vai gerar um resumo dos erros de site que os usuários enfrentam.</span><span class="sxs-lookup"><span data-stu-id="3909f-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="3909f-113">Você saberá como:</span><span class="sxs-lookup"><span data-stu-id="3909f-113">You will learn how to:</span></span>

* <span data-ttu-id="3909f-114">Conectar-se a um armazenamento de Blob do Azure, que contém os arquivos de log do site.</span><span class="sxs-lookup"><span data-stu-id="3909f-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="3909f-115">Criar tabelas do HIVE para consultar esses logs.</span><span class="sxs-lookup"><span data-stu-id="3909f-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="3909f-116">Criar consultas do HIVE para analisar os dados.</span><span class="sxs-lookup"><span data-stu-id="3909f-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="3909f-117">Usar o Microsoft Excel para conectar-se ao HDInsight (usando ODBC, conectividade de banco de dados aberta) para recuperar os dados analisados.</span><span class="sxs-lookup"><span data-stu-id="3909f-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="3909f-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3909f-119">Prerequisites</span></span>
* <span data-ttu-id="3909f-120">Você deve ter provisionado um cluster Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3909f-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="3909f-121">Para obter instruções, confira [Provisionar clusters do HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="3909f-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="3909f-122">Você deve ter o Microsoft Excel 2013 ou Microsoft Excel 2010 instalado.</span><span class="sxs-lookup"><span data-stu-id="3909f-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="3909f-123">Você deve ter o [Driver ODBC do Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886) para importar dados do Hive no Excel.</span><span class="sxs-lookup"><span data-stu-id="3909f-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="3909f-124">Para executar a amostra</span><span class="sxs-lookup"><span data-stu-id="3909f-124">To run the sample</span></span>
1. <span data-ttu-id="3909f-125">No [Portal do Azure](https://portal.azure.com/), no quadro inicial (caso você tenha fixado o cluster ali), clique no bloco do cluster no qual você deseja executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="3909f-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="3909f-126">Na folha do cluster, em **Links Rápidos**, clique em **Painel do Cluster** e, na folha **Painel do Cluster**, clique em **Painel do Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3909f-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="3909f-127">Como alternativa, você pode abrir diretamente o painel usando a seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="3909f-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="3909f-128">Quando solicitado, faça a autenticação usando o nome de usuário e senha do administrador usados ao provisionar o cluster.</span><span class="sxs-lookup"><span data-stu-id="3909f-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="3909f-129">Na página da Web que é aberta, clique na guia **Galeria de Introdução** e, sob a categoria **Soluções com Dados de Exemplo**, clique no exemplo **Análise de Log do Site**.</span><span class="sxs-lookup"><span data-stu-id="3909f-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="3909f-130">Siga as instruções fornecidas na página da Web para concluir a amostra.</span><span class="sxs-lookup"><span data-stu-id="3909f-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3909f-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3909f-131">Next steps</span></span>
<span data-ttu-id="3909f-132">Experimente o exemplo a seguir: [Analisando dados do sensor usando o Hive com HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="3909f-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
