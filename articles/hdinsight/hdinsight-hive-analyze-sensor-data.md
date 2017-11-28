---
title: "Analisar dados de sensor usando Hive e Hadoop – HDInsight do Azure | Microsoft Docs"
description: Saiba como analisar dados do sensor usando o Console de consulta Hive com HDInsight (Hadoop) e depois visualizar os dados no Microsoft Excel usando o PowerView.
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
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="57fa9-103">Analisar dados de sensor usando o Console de consulta Hive no Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="57fa9-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="57fa9-104">Saiba como analisar dados do sensor usando o Console de consulta Hive com HDInsight (Hadoop) e depois visualizar os dados no Microsoft Excel usando o Power View.</span><span class="sxs-lookup"><span data-stu-id="57fa9-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57fa9-105">As etapas neste documento só funcionam com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="57fa9-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="57fa9-106">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="57fa9-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="57fa9-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="57fa9-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="57fa9-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="57fa9-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="57fa9-109">Neste exemplo, usamos o Hive para processar dados históricos e identificar problemas com sistemas de aquecimento e refrigeração.</span><span class="sxs-lookup"><span data-stu-id="57fa9-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="57fa9-110">Especificamente, você pode identificar sistemas não conseguem manter uma temperatura definida de maneira confiável executando as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="57fa9-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="57fa9-111">Crie tabelas do HIVE para consultar dados armazenados em arquivos com valores separados por vírgulas (CSV).</span><span class="sxs-lookup"><span data-stu-id="57fa9-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="57fa9-112">Criar consultas do HIVE para analisar os dados.</span><span class="sxs-lookup"><span data-stu-id="57fa9-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="57fa9-113">Para recuperar os dados analisados, use o Microsoft Excel para conectar-se ao HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57fa9-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="57fa9-114">Use o Power View para visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="57fa9-114">To visualize the data, use Power View.</span></span>

![Um diagrama da arquitetura da solução](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="57fa9-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="57fa9-116">Prerequisites</span></span>

* <span data-ttu-id="57fa9-117">Um cluster do HDInsight (Hadoop): veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obter informações sobre como criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="57fa9-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="57fa9-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="57fa9-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="57fa9-119">O Microsoft Excel é usado para visualização de dados no [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="57fa9-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="57fa9-120">Driver ODBC do Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="57fa9-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="57fa9-121">Para executar a amostra</span><span class="sxs-lookup"><span data-stu-id="57fa9-121">To run the sample</span></span>

1. <span data-ttu-id="57fa9-122">No seu navegador da Web, navegue até a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="57fa9-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="57fa9-123">Substitua `<clustername>` pelo nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57fa9-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="57fa9-124">Quando solicitado, faça a autenticação usando o nome de usuário e senha do administrador usados ao provisionar esse cluster.</span><span class="sxs-lookup"><span data-stu-id="57fa9-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="57fa9-125">Na página da Web que é aberta, clique na guia **Galeria de introdução** e na categoria **Soluções com dados de amostra**, clique na amostra **Análise de dados do sensor**.</span><span class="sxs-lookup"><span data-stu-id="57fa9-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Imagem da galeria de Introdução](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="57fa9-127">Siga as instruções fornecidas na página da Web para concluir a amostra.</span><span class="sxs-lookup"><span data-stu-id="57fa9-127">Follow the instructions provided on the web page to finish the sample.</span></span>
