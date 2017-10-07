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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Coletar despejos de pilha em toodebug de armazenamento de Blob e analisar os serviços Hadoop
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Despejos de pilha contém um instantâneo de memória do aplicativo hello, incluindo valores hello das variáveis no tempo Olá Olá despejo foi criado. Portanto, eles são úteis para diagnosticar problemas que ocorrem no tempo de execução. Despejos de memória de heap podem ser coletados para os serviços Hadoop e colocados dentro de saudação conta de armazenamento de BLOBs do Azure de um usuário em HDInsightHeapDumps automaticamente /.

coleção de saudação de despejos de pilha para vários serviços deve ser habilitada para serviços em clusters individuais. padrão de saudação para esse recurso é toobe off para um cluster. Esses despejos de memória de heap podem ser grandes, portanto, é aconselhável toomonitor conta de armazenamento de Blob de saudação onde eles estão sendo salvas depois que habilitar a coleção de saudação.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). informações Olá neste artigo se aplica somente com base em tooWindows HDInsight. Para obter informações sobre o HDInsight baseado em Linux, consulte [Habilitar despejos de heap para serviços do Hadoop no HDInsight baseado em Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>Serviços qualificados para despejos de heap
Você pode habilitar os despejos de pilha para Olá serviços a seguir:

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>Elementos de configuração que habilitam despejos de heap
tooturn em despejos de pilha para um serviço, você precisa tooset elementos de configuração apropriado Olá na seção Olá para esse serviço, que é especificado pelo **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

Olá valor **service_name** pode ser qualquer um dos serviços de saudação listados aqui: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, ou namenode.

## <a name="enable-using-azure-powershell"></a>Habilitar usando o Azure PowerShell
Por exemplo, tooturn em despejos de pilha usando o Azure PowerShell para jobhistoryserver, você pode usar Olá script a seguir:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Habilitar o uso do SDK do .NET
Por exemplo, tooturn em despejos de pilha usando hello Azure HDInsight .NET SDK para jobhistoryserver, você pode usar Olá código a seguir:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
