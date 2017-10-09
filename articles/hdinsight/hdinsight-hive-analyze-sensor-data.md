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
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Analisar dados de sensor usando Olá Console de consulta de Hive no Hadoop no HDInsight

Saiba como os dados do sensor tooanalyze usando Olá Console de consulta de Hive com HDInsight (Hadoop), em seguida, visualize os dados de saudação no Microsoft Excel usando o Power View.

> [!IMPORTANT]
> Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows. O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


Neste exemplo, você usa dados históricos do Hive tooprocess e identificar problemas com sistemas de aquecimento e ar-condicionado. Especificamente, você pode identificar sistemas são tooreliably não é possível manter um conjunto de temperatura executando Olá tarefas a seguir:

* Criar tabelas de HIVE tooquery dados armazenados em arquivos de valores separados por vírgulas (CSV).
* Crie consultas de HIVE tooanalyze dados de saudação.
* Olá analisado de tooretrieve dados, usar o Microsoft Excel tooconnect tooHDInsight.
* dados de saudação toovisualize, use o Power View.

![Um diagrama de arquitetura da solução Olá](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster do HDInsight (Hadoop): veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obter informações sobre como criar um cluster.
* Microsoft Excel 2013

  > [!NOTE]
  > O Microsoft Excel é usado para visualização de dados no [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Driver ODBC do Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>exemplo de hello toorun

1. A partir do navegador da web, navegar toohello URL a seguir: 

         https://<clustername>.azurehdinsight.net

    Substituir `<clustername>` com nome de saudação do cluster HDInsight.

    Quando solicitado, autentica usando o nome de usuário de administrador hello e a senha que você usou ao provisionar este cluster.

2. De saudação página da web que é aberta, clique em hello **Galeria de Introdução** guia e, em seguida, em hello **soluções com dados de exemplo** categoria, clique em hello **análise de dados do Sensor** exemplo.

    ![Imagem da galeria de Introdução](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Siga as instruções de saudação fornecidas no exemplo de saudação de toofinish hello página da web.
