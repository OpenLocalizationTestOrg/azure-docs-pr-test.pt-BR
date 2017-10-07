---
title: aaaUse MapReduce e PowerShell com o Hadoop - HDInsight do Azure | Microsoft Docs
description: Saiba como toouse PowerShell tooremotely executar trabalhos de MapReduce com Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>Executar trabalhos MapReduce com Hadoop no HDInsight usando o PowerShell

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Este documento fornece um exemplo de uso do Azure PowerShell toorun um trabalho de MapReduce em um Hadoop no cluster HDInsight.

## <a id="prereq"></a>Pré-requisitos

* **Um cluster Azure HDInsight (Hadoop no HDInsight)**

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Uma estação de trabalho com o PowerShell do Azure**.

## <a id="powershell"></a>Executar um trabalho MapReduce usando o PowerShell do Azure

PowerShell do Azure fornece *cmdlets* que permitem que você tooremotely executar trabalhos de MapReduce no HDInsight. Internamente, isso é feito por meio de chamadas REST muito[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anteriormente chamado de Templeton) em execução no hello cluster HDInsight.

cmdlets a seguir Hello são usados durante a execução de trabalhos de MapReduce em um cluster HDInsight remoto.

* **Logon AzureRmAccount**: autentica o Azure PowerShell tooyour assinatura do Azure.

* **Novo AzureRmHDInsightMapReduceJobDefinition**: cria um novo *definição de trabalho* usando Olá especificar informações de MapReduce.

* **Iniciar AzureRmHDInsightJob**: envia Olá tooHDInsight de definição de trabalho, inicia o trabalho de saudação e retorna um *trabalho* objeto que pode ser toocheck usado Olá status do trabalho de saudação.

* **Espera-AzureRmHDInsightJob**: usa Olá objeto toocheck Olá status do trabalho do trabalho de saudação. Ele aguardará até Olá trabalho for concluído ou tempo de espera de saudação for excedido.

* **Get-AzureRmHDInsightJobOutput**: usado tooretrieve saída de saudação do trabalho de saudação.

Olá etapas a seguir demonstram como toouse toorun esses cmdlets um trabalho em seu cluster HDInsight.

1. Usando um editor, salvar Olá código como a seguir **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Abra um novo prompt de comando do **PowerShell do Azure** . Alterar diretórios toohello local de saudação **mapreducejob.ps1** de arquivo e use Olá script do comando toorun Olá a seguir:

        .\mapreducejob.ps1

    Quando você executa o script hello, você será solicitado a nome de saudação do cluster do HDInsight hello e nome de conta do hello HTTPS/administrador e senha para cluster Olá. Você também pode ser solicitados tooauthenticate tooyour assinatura do Azure.

3. Ao Olá trabalho for concluído, você recebe saída toohello semelhante texto a seguir:

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Essa saída indica que o trabalho Olá foi concluída com êxito.

    > [!NOTE]
    > Se hello **ExitCode** é um valor diferente de 0, consulte [solução de problemas](#troubleshooting).

    Este exemplo também armazena Olá baixado arquivos tooan **txt** arquivo hello no diretório em que você executar o script hello.

### <a name="view-output"></a>Exibir saída

Olá abrir **txt** palavras de arquivo em uma saudação de toosee do editor de texto e contagens produzido pelo trabalho de saudação.

> [!NOTE]
> saudação de arquivos de saída de um trabalho de MapReduce são imutáveis. Então se você executar novamente este exemplo, você precisa de nome de saudação do toochange saudação do arquivo de saída.

## <a id="troubleshooting"></a>Solucionar problemas

Se nenhuma informação é retornada quando Olá trabalho for concluído, um erro pode ter ocorrido durante o processamento. informações de erro tooview para este trabalho, adicionar Olá após o término do comando toohello de saudação **mapreducejob.ps1** arquivo, salve-o e, em seguida, execute-o novamente.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Esse cmdlet retorna informações de saudação escrito tooSTDERR no servidor de saudação quando você executou o trabalho de saudação e pode ajudar a determinar por que o trabalho de saudação está falhando.

## <a id="summary"></a>Resumo

Como você pode ver, o Azure PowerShell fornece uma maneira fácil de toorun trabalhos MapReduce em um cluster HDInsight, monitora o status de trabalho hello e recuperar Olá saída.

## <a id="nextsteps"></a>Próximas etapas

Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:

* [Usar o MapReduce no Hadoop do HDInsight](hdinsight-use-mapreduce.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
