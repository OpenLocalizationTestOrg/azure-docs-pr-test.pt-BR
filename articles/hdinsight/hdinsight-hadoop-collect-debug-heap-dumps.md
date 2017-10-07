---
title: "aaaDebug e analisar os serviços Hadoop com despejos de pilha - Azure | Microsoft Docs"
description: "Coletar despejos de pilha para os serviços Hadoop e coloque dentro Olá conta de armazenamento de BLOBs do Azure para análise e depuração automaticamente."
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
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="e4eb8-103">Coletar despejos de pilha em toodebug de armazenamento de Blob e analisar os serviços Hadoop</span><span class="sxs-lookup"><span data-stu-id="e4eb8-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="e4eb8-104">Despejos de pilha contém um instantâneo de memória do aplicativo hello, incluindo valores hello das variáveis no tempo Olá Olá despejo foi criado.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="e4eb8-105">Portanto, eles são úteis para diagnosticar problemas que ocorrem no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="e4eb8-106">Despejos de memória de heap podem ser coletados para os serviços Hadoop e colocados dentro de saudação conta de armazenamento de BLOBs do Azure de um usuário em HDInsightHeapDumps automaticamente /.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="e4eb8-107">coleção de saudação de despejos de pilha para vários serviços deve ser habilitada para serviços em clusters individuais.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="e4eb8-108">padrão de saudação para esse recurso é toobe off para um cluster.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="e4eb8-109">Esses despejos de memória de heap podem ser grandes, portanto, é aconselhável toomonitor conta de armazenamento de Blob de saudação onde eles estão sendo salvas depois que habilitar a coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4eb8-110">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e4eb8-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e4eb8-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="e4eb8-112">informações Olá neste artigo se aplica somente com base em tooWindows HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="e4eb8-113">Para obter informações sobre o HDInsight baseado em Linux, consulte [Habilitar despejos de heap para serviços do Hadoop no HDInsight baseado em Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e4eb8-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="e4eb8-114">Serviços qualificados para despejos de heap</span><span class="sxs-lookup"><span data-stu-id="e4eb8-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="e4eb8-115">Você pode habilitar os despejos de pilha para Olá serviços a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4eb8-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="e4eb8-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="e4eb8-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="e4eb8-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="e4eb8-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="e4eb8-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="e4eb8-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="e4eb8-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="e4eb8-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="e4eb8-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="e4eb8-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="e4eb8-121">Elementos de configuração que habilitam despejos de heap</span><span class="sxs-lookup"><span data-stu-id="e4eb8-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="e4eb8-122">tooturn em despejos de pilha para um serviço, você precisa tooset elementos de configuração apropriado Olá na seção Olá para esse serviço, que é especificado pelo **service_name**.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="e4eb8-123">Olá valor **service_name** pode ser qualquer um dos serviços de saudação listados aqui: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, ou namenode.</span><span class="sxs-lookup"><span data-stu-id="e4eb8-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="e4eb8-124">Habilitar usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4eb8-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="e4eb8-125">Por exemplo, tooturn em despejos de pilha usando o Azure PowerShell para jobhistoryserver, você pode usar Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4eb8-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="e4eb8-126">Habilitar o uso do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="e4eb8-126">Enable using .NET SDK</span></span>
<span data-ttu-id="e4eb8-127">Por exemplo, tooturn em despejos de pilha usando hello Azure HDInsight .NET SDK para jobhistoryserver, você pode usar Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4eb8-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
