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
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Use o Hive com logs de tooanalyze HDInsight baseados em Windows de sites
Saiba como toouse HiveQL com HDInsight tooanalyze logs de um site. Análise de log do site pode ser usado toosegment seu público-alvo com base nas atividades semelhantes, categorizar os visitantes do site por dados demográficos e toofind conteúdo Olá exibirem, Olá sites que eles vêm e assim por diante.

> [!IMPORTANT]
> Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows. O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Neste exemplo, você usará uma HDInsight cluster tooanalyze site log arquivos tooget percepção frequência de saudação do site toohello visitas a sites externos em um dia. Você também irá gerar um resumo de erros de site que os usuários de saudação enfrentar. Você saberá como:

* Conecte-se tooa armazenamento de BLOBs do Azure, que contém arquivos de log do site.
* Criar tabelas de HIVE tooquery esses logs.
* Crie consultas de HIVE tooanalyze dados de saudação.
* Usar o Microsoft Excel tooconnect tooHDInsight (por meio de dados do banco de dados aberto connectivity (ODBC) tooretrieve Olá analisado.

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Pré-requisitos
* Você deve ter provisionado um cluster Hadoop no Azure HDInsight. Para obter instruções, confira [Provisionar clusters do HDInsight][hdinsight-provision].
* Você deve ter o Microsoft Excel 2013 ou Microsoft Excel 2010 instalado.
* Você deve ter [Microsoft ODBC Driver Hive](http://www.microsoft.com/download/details.aspx?id=40886) tooimport dados de Hive no Excel.

## <a name="toorun-hello-sample"></a>exemplo de hello toorun
1. De saudação [Portal do Azure](https://portal.azure.com/), da saudação quadro inicial (se você fixou o cluster de saudação existe), clique em bloco de cluster Olá no qual você deseja que o exemplo de hello toorun.
2. De saudação do cluster folha, em **Links rápidos**, clique em **painel Cluster**e, em seguida, Olá **painel Cluster** folha, clique em **HDInsight Cluster Painel**. Como alternativa, você pode abrir diretamente painel hello usando Olá URL a seguir:

         https://<clustername>.azurehdinsight.net

    Quando solicitado, autentica usando o nome de usuário de administrador hello e senha que você usou ao provisionar o cluster hello.
3. Na página de web de saudação que é aberta, clique em Olá **Galeria de Introdução** guia e, em seguida, em Olá **soluções com dados de exemplo** categoria, clique Olá **análise de Log do site** exemplo.
4. Siga as instruções de saudação fornecidas no exemplo de saudação de toofinish hello página da web.

## <a name="next-steps"></a>Próximas etapas
Tente Olá exemplo a seguir: [analisando dados de sensor com Hive HDInsight](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
