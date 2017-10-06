---
title: "aaaUse Hive com Hadoop para análise de log do site - HDInsight do Azure | Microsoft Docs"
description: "Saiba como toouse Hive com HDInsight tooanalyze site registra. Você usa um arquivo de log como entrada para uma tabela de HDInsight e usar dados de saudação do HiveQL tooquery."
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
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="55cb7-104">Use o Hive com logs de tooanalyze HDInsight baseados em Windows de sites</span><span class="sxs-lookup"><span data-stu-id="55cb7-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="55cb7-105">Saiba como toouse HiveQL com HDInsight tooanalyze logs de um site.</span><span class="sxs-lookup"><span data-stu-id="55cb7-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="55cb7-106">Análise de log do site pode ser usado toosegment seu público-alvo com base nas atividades semelhantes, categorizar os visitantes do site por dados demográficos e toofind conteúdo Olá exibirem, Olá sites que eles vêm e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="55cb7-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55cb7-107">Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="55cb7-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="55cb7-108">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="55cb7-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="55cb7-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="55cb7-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="55cb7-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="55cb7-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="55cb7-111">Neste exemplo, você usará uma HDInsight cluster tooanalyze site log arquivos tooget percepção frequência de saudação do site toohello visitas a sites externos em um dia.</span><span class="sxs-lookup"><span data-stu-id="55cb7-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="55cb7-112">Você também irá gerar um resumo de erros de site que os usuários de saudação enfrentar.</span><span class="sxs-lookup"><span data-stu-id="55cb7-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="55cb7-113">Você saberá como:</span><span class="sxs-lookup"><span data-stu-id="55cb7-113">You will learn how to:</span></span>

* <span data-ttu-id="55cb7-114">Conecte-se tooa armazenamento de BLOBs do Azure, que contém arquivos de log do site.</span><span class="sxs-lookup"><span data-stu-id="55cb7-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="55cb7-115">Criar tabelas de HIVE tooquery esses logs.</span><span class="sxs-lookup"><span data-stu-id="55cb7-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="55cb7-116">Crie consultas de HIVE tooanalyze dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="55cb7-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="55cb7-117">Usar o Microsoft Excel tooconnect tooHDInsight (por meio de dados do banco de dados aberto connectivity (ODBC) tooretrieve Olá analisado.</span><span class="sxs-lookup"><span data-stu-id="55cb7-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="55cb7-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="55cb7-119">Prerequisites</span></span>
* <span data-ttu-id="55cb7-120">Você deve ter provisionado um cluster Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="55cb7-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="55cb7-121">Para obter instruções, confira [Provisionar clusters do HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="55cb7-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="55cb7-122">Você deve ter o Microsoft Excel 2013 ou Microsoft Excel 2010 instalado.</span><span class="sxs-lookup"><span data-stu-id="55cb7-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="55cb7-123">Você deve ter [Microsoft ODBC Driver Hive](http://www.microsoft.com/download/details.aspx?id=40886) tooimport dados de Hive no Excel.</span><span class="sxs-lookup"><span data-stu-id="55cb7-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="55cb7-124">exemplo de hello toorun</span><span class="sxs-lookup"><span data-stu-id="55cb7-124">toorun hello sample</span></span>
1. <span data-ttu-id="55cb7-125">De saudação [Portal do Azure](https://portal.azure.com/), da saudação quadro inicial (se você fixou o cluster de saudação existe), clique em bloco de cluster Olá no qual você deseja que o exemplo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="55cb7-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="55cb7-126">De saudação do cluster folha, em **Links rápidos**, clique em **painel Cluster**e, em seguida, Olá **painel Cluster** folha, clique em **HDInsight Cluster Painel**.</span><span class="sxs-lookup"><span data-stu-id="55cb7-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="55cb7-127">Como alternativa, você pode abrir diretamente painel hello usando Olá URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="55cb7-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="55cb7-128">Quando solicitado, autentica usando o nome de usuário de administrador hello e senha que você usou ao provisionar o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="55cb7-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="55cb7-129">Na página de web de saudação que é aberta, clique em Olá **Galeria de Introdução** guia e, em seguida, em Olá **soluções com dados de exemplo** categoria, clique Olá **análise de Log do site** exemplo.</span><span class="sxs-lookup"><span data-stu-id="55cb7-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="55cb7-130">Siga as instruções de saudação fornecidas no exemplo de saudação de toofinish hello página da web.</span><span class="sxs-lookup"><span data-stu-id="55cb7-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55cb7-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55cb7-131">Next steps</span></span>
<span data-ttu-id="55cb7-132">Tente Olá exemplo a seguir: [analisando dados de sensor com Hive HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="55cb7-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
