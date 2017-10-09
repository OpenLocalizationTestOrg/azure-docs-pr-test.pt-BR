---
title: dados de sensor aaaAnalyze usando Hive e Hadoop - HDInsight do Azure | Microsoft Docs
description: "Saiba como dados de sensor tooanalyze usando Olá Console de consulta de Hive com HDInsight (Hadoop), e visualizar dados Olá no Microsoft Excel com PowerView."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="6674a-103">Analisar dados de sensor usando Olá Console de consulta de Hive no Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6674a-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="6674a-104">Saiba como os dados do sensor tooanalyze usando Olá Console de consulta de Hive com HDInsight (Hadoop), em seguida, visualize os dados de saudação no Microsoft Excel usando o Power View.</span><span class="sxs-lookup"><span data-stu-id="6674a-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6674a-105">Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="6674a-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="6674a-106">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="6674a-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="6674a-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6674a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6674a-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6674a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="6674a-109">Neste exemplo, você usa dados históricos do Hive tooprocess e identificar problemas com sistemas de aquecimento e ar-condicionado.</span><span class="sxs-lookup"><span data-stu-id="6674a-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="6674a-110">Especificamente, você pode identificar sistemas são tooreliably não é possível manter um conjunto de temperatura executando Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6674a-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="6674a-111">Criar tabelas de HIVE tooquery dados armazenados em arquivos de valores separados por vírgulas (CSV).</span><span class="sxs-lookup"><span data-stu-id="6674a-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="6674a-112">Crie consultas de HIVE tooanalyze dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6674a-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="6674a-113">Olá analisado de tooretrieve dados, usar o Microsoft Excel tooconnect tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="6674a-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="6674a-114">dados de saudação toovisualize, use o Power View.</span><span class="sxs-lookup"><span data-stu-id="6674a-114">toovisualize hello data, use Power View.</span></span>

![Um diagrama de arquitetura da solução Olá](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="6674a-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6674a-116">Prerequisites</span></span>

* <span data-ttu-id="6674a-117">Um cluster do HDInsight (Hadoop): veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obter informações sobre como criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="6674a-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="6674a-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="6674a-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="6674a-119">O Microsoft Excel é usado para visualização de dados no [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="6674a-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="6674a-120">Driver ODBC do Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="6674a-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="6674a-121">exemplo de hello toorun</span><span class="sxs-lookup"><span data-stu-id="6674a-121">toorun hello sample</span></span>

1. <span data-ttu-id="6674a-122">A partir do navegador da web, navegar toohello URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="6674a-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="6674a-123">Substituir `<clustername>` com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6674a-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="6674a-124">Quando solicitado, autentica usando o nome de usuário de administrador hello e a senha que você usou ao provisionar este cluster.</span><span class="sxs-lookup"><span data-stu-id="6674a-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="6674a-125">De saudação página da web que é aberta, clique em hello **Galeria de Introdução** guia e, em seguida, em hello **soluções com dados de exemplo** categoria, clique em hello **análise de dados do Sensor** exemplo.</span><span class="sxs-lookup"><span data-stu-id="6674a-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Imagem da galeria de Introdução](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="6674a-127">Siga as instruções de saudação fornecidas no exemplo de saudação de toofinish hello página da web.</span><span class="sxs-lookup"><span data-stu-id="6674a-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
