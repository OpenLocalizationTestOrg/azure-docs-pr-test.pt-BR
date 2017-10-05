---
title: "Depurar e analisar serviços do Hadoop com despejos de heap – Azure | Microsoft Docs"
description: "Colete despejos de heap automaticamente para serviços do Hadoop e coloque dentro a conta de armazenamento de Blobs do Azure para depuração e análise."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="3f5bb-103">Coletar despejos de heap no armazenamento de Blob para depurar e analisar serviços do Hadoop</span><span class="sxs-lookup"><span data-stu-id="3f5bb-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="3f5bb-104">Despejos de heap contêm um instantâneo da memória do aplicativo, incluindo os valores das variáveis no momento em que o despejo foi criado.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="3f5bb-105">Portanto, eles são úteis para diagnosticar problemas que ocorrem no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="3f5bb-106">Despejos de heap dos serviços Hadoop podem ser coletados automaticamente e colocados na conta de armazenamento de Blob do Azure de um usuário em HDInsightHeapDumps/.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="3f5bb-107">A coleção de despejos de heap para vários serviços deve ser habilitada para serviços em clusters individuais.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="3f5bb-108">O padrão para esse recurso deve ser desativado para um cluster.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="3f5bb-109">Esses despejos de heap podem ser grandes; portanto, é aconselhável monitorar a conta de armazenamento de Blob na qual eles são salvos após habilitar a coleta.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f5bb-110">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3f5bb-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3f5bb-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="3f5bb-112">As informações neste artigo aplicam-se apenas ao HDInsight baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="3f5bb-113">Para obter informações sobre o HDInsight baseado em Linux, consulte [Habilitar despejos de heap para serviços do Hadoop no HDInsight baseado em Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="3f5bb-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="3f5bb-114">Serviços qualificados para despejos de heap</span><span class="sxs-lookup"><span data-stu-id="3f5bb-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="3f5bb-115">Você pode habilitar o despejo de heap para os seguintes serviços:</span><span class="sxs-lookup"><span data-stu-id="3f5bb-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="3f5bb-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="3f5bb-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="3f5bb-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="3f5bb-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="3f5bb-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="3f5bb-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="3f5bb-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="3f5bb-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="3f5bb-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="3f5bb-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="3f5bb-121">Elementos de configuração que habilitam despejos de heap</span><span class="sxs-lookup"><span data-stu-id="3f5bb-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="3f5bb-122">Para habilitar despejos de heap para um serviço, você precisa definir os elementos de configuração apropriados na seção desse serviço, especificado por **service_name**.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="3f5bb-123">O valor de **service_name** pode ser qualquer um dos serviços listados aqui: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode ou namenode.</span><span class="sxs-lookup"><span data-stu-id="3f5bb-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="3f5bb-124">Habilitar usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f5bb-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="3f5bb-125">Por exemplo, para ativar despejos de heap para jobhistoryserver usando o Azure PowerShell, você pode usar o seguinte script:</span><span class="sxs-lookup"><span data-stu-id="3f5bb-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="3f5bb-126">Habilitar o uso do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="3f5bb-126">Enable using .NET SDK</span></span>
<span data-ttu-id="3f5bb-127">Por exemplo, para ativar despejos de heap para jobhistoryserver usando o SDK .NET do Azure HDInsight, você pode usar o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="3f5bb-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
