---
title: aaaUse interativo Hive no HDInsight - Azure | Microsoft Docs
description: Saiba como toouse interativo (Hive no LLAP) de Hive no HDInsight.
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Usar o Hive Interativo no HDInsight (Visualização)
O Hive Interativo (também conhecido como [Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) é um novo [tipo de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) do HDInsight.  O Hive Interativo permite o armazenamento em cache na memória, o que torna as consultas do Hive muito mais interativas e rápidas. Este novo recurso torna HDInsight uma saudação mais funcionais, flexíveis e abrir soluções de Big Data do mundo na nuvem Olá com caches de memória (usando Hive e Spark) e advanced analytics por meio da profunda integração com serviços de R. 

cluster de Hive interativo Olá é diferente do cluster de Hadoop hello. Ele contém apenas serviço de Hive hello. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie e outros serviços, em breve, serão removidos desse tipo de cluster.
> Olá serviço Hive no cluster de Hive interativo Olá só está acessível por meio de Olá exibição Ambari Hive, Beeline e Hive ODBC. Ele não pode ser acessado por meio do console do Hive, do Templeton, da CLI do Azure e do Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Criar um cluster do Hive Interativo
O cluster do Hive Interativo é compatível apenas com clusters baseados em Linux. Para obter informações sobre a criação de clusters HDInsight, confira [Criar clusters Hadoop baseados em Linux em HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Executar o Hive do Hive Interativo
Há diferentes opções para executar consultas do Hive:

* Execute o Hive usando Olá Ambari Hive exibição
  
    Para obter informações de Olá sobre como usar o hello exibição Hive, consulte [Olá Use exibição de Hive com Hadoop no HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Executar o Hive usando o Beeline
  
    Para obter informações de saudação usando Beeline no HDInsight, consulte [uso de Hive do Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    Você pode usar Beeline de saudação um nó principal ou um nó de borda vazia.  É recomendável usar o Beeline em um nó de borda vazio.  Para saber mais sobre como criar um cluster HDInsight com um nó de borda vazio, confira [Usar nós de borda vazios no HDInsight](hdinsight-apps-use-edge-node.md).
* Executar o Hive usando o ODBC do Hive
  
    Para obter informações de hello usando ODBC Hive, consulte [tooHadoop Excel conectar-se com hello Hive do Microsoft ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).

**Olá toofind cadeia de caracteres de conexão JDBC:**

1. Logon tooAmbari usando Olá URL a seguir: https://<ClusterName>. N e t.
2. Clique em **Hive** no menu esquerdo hello.
3. Clique em Olá realçado ícone toocopy Olá URL:
   
   ![JDBC LLAP do Hive Interativo no Hadoop HDInsight](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Consulte também
* [Criar clusters baseados em Linux Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Saiba como clusters de toocreate interativo Hive no HDInsight.
* [Use o Hive com Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md): Saiba como consultas de Hive toouse Beeline toosubmit.
* [Conectar Excel tooHadoop com hello Hive do Microsoft ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): Saiba como tooconnect Excel tooHive.

