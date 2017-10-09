---
title: aaaUse Pig do Hadoop com o PowerShell no HDInsight - Azure | Microsoft Docs
description: Saiba como cluster de toosubmit Pig trabalhos tooa Hadoop no HDInsight usando o PowerShell do Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Use trabalhos de Pig do Azure PowerShell toorun com HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Este documento fornece um exemplo de uso do Azure PowerShell toosubmit Pig trabalhos tooa Hadoop no cluster HDInsight. Pig permite que os trabalhos de MapReduce toowrite usando uma linguagem (Pig latino) que modela transformações de dados, em vez de mapear e reduzir as funções.

> [!NOTE]
> Este documento não fornece uma descrição detalhada do que fazem instruções de Pig latino Olá usadas nos exemplos de saudação. Para obter informações sobre Olá Pig latino usado neste exemplo, consulte [usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md).

## <a id="prereq"></a>Pré-requisitos

* **Um cluster Azure HDInsight**

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Uma estação de trabalho com o PowerShell do Azure**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>Executar trabalhos do Pig usando o PowerShell

PowerShell do Azure fornece *cmdlets* que permitem que você tooremotely executar trabalhos de Pig no HDInsight. Internamente, o PowerShell usa chamadas REST muito[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) em execução no cluster do HDInsight hello.

cmdlets a seguir Hello são usados durante a execução de trabalhos de Pig em um cluster HDInsight remoto:

* **Logon AzureRmAccount**: autentica o Azure PowerShell tooyour assinatura do Azure
* **Novo AzureRmHDInsightPigJobDefinition**: cria um *definição de trabalho* usando Olá especificado Pig latino instruções
* **Iniciar AzureRmHDInsightJob**: envia Olá tooHDInsight de definição de trabalho, inicia o trabalho de saudação e retorna um *trabalho* objeto que pode ser toocheck usado Olá status do trabalho de saudação
* **Espera-AzureRmHDInsightJob**: usa Olá objeto toocheck Olá status do trabalho do trabalho de saudação. Ele aguarda até que o trabalho Olá foi concluído ou tempo de espera de saudação foi excedido.
* **Get-AzureRmHDInsightJobOutput**: usado tooretrieve saída de saudação do trabalho Olá

Olá etapas a seguir demonstram como toouse toorun esses cmdlets um trabalho em seu cluster HDInsight.

1. Usando um editor, salvar Olá código como a seguir **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Abra um novo prompt de comando do Windows PowerShell. Alterar diretórios toohello local de saudação **pigjob.ps1** de arquivo e use Olá script do comando toorun Olá a seguir:

        .\pigjob.ps1

    Você está toolog solicitada no tooyour assinatura do Azure. Em seguida, você será solicitado para Olá HTTPs/Admin nome e a senha para o cluster do HDInsight hello.

2. Quando o trabalho de saudação for concluído, ele deverá retornar informações toohello semelhante texto a seguir:

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Solucionar problemas

Se nenhuma informação é retornada quando Olá trabalho for concluído, um erro pode ter ocorrido durante o processamento. informações de erro tooview para este trabalho, adicionar Olá após o término do comando toohello de saudação **pigjob.ps1** arquivo, salve-o e, em seguida, execute-o novamente.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Isso retorna informações de saudação escrito tooSTDERR no servidor de saudação quando você executou o trabalho de saudação e pode ajudar a determinar por que o trabalho de saudação está falhando.

## <a id="summary"></a>Resumo
Como você pode ver, o Azure PowerShell fornece uma maneira fácil de toorun trabalhos de Pig em um cluster HDInsight, monitora o status de trabalho hello e recuperar Olá saída.

## <a id="nextsteps"></a>Próximas etapas
Para obter informações gerais sobre o Pig no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)
