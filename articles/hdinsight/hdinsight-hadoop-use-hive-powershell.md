---
title: aaaUse Hive do Hadoop com o PowerShell no HDInsight - Azure | Microsoft Docs
description: Use consultas de Hive do PowerShell toorun no Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>Executar consultas Hive usando o PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Este documento fornece um exemplo de uso do Azure PowerShell Olá grupo de recursos do Azure toorun Hive em consultas em modo em uma Hadoop no cluster HDInsight.

> [!NOTE]
> Este documento não fornece uma descrição detalhada do que fazem declarações do HiveQL Olá que são usadas nos exemplos de saudação. Para obter informações sobre Olá HiveQL que é usado neste exemplo, consulte [uso de Hive do Hadoop no HDInsight](hdinsight-use-hive.md).

**Pré-requisitos**

* **Um cluster Azure HDInsight**: não importa se o cluster de saudação é Windows ou Linux.

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Uma estação de trabalho com o PowerShell do Azure**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Executar consultas do Hive usando o Azure PowerShell

PowerShell do Azure fornece *cmdlets* que permitem que você tooremotely executar consultas de Hive no HDInsight. Internamente, os cmdlets Olá fazer chamadas REST muito[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) no cluster do HDInsight hello.

cmdlets a seguir Hello são usados ao executar consultas de Hive em um cluster HDInsight remoto:

* **Adicionar AzureRmAccount**: autentica o Azure PowerShell tooyour assinatura do Azure
* **Novo AzureRmHDInsightHiveJobDefinition**: cria um *definição de trabalho* usando Olá especificado HiveQL instruções
* **Iniciar AzureRmHDInsightJob**: envia Olá tooHDInsight de definição de trabalho, inicia o trabalho de saudação e retorna um *trabalho* objeto que pode ser toocheck usado Olá status do trabalho de saudação
* **Espera-AzureRmHDInsightJob**: usa Olá objeto toocheck Olá status do trabalho do trabalho de saudação. Ele aguardará até Olá trabalho for concluído ou tempo de espera de saudação for excedido.
* **Get-AzureRmHDInsightJobOutput**: usado tooretrieve saída de saudação do trabalho Olá
* **Invocar AzureRmHDInsightHiveJob**: usado toorun HiveQL instruções. Esta consulta de saudação do cmdlet blocos for concluída, em seguida, retorna os resultados de saudação
* **Use AzureRmHDInsightCluster**: conjuntos Olá toouse de cluster atual para Olá **AzureRmHDInsightHiveJob Invoke** comando

Olá etapas a seguir demonstram como toouse toorun esses cmdlets um trabalho em seu cluster HDInsight:

1. Usando um editor, salvar Olá código como a seguir **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Abra um novo prompt de comando do **PowerShell do Azure** . Alterar diretórios toohello local de saudação **hivejob.ps1** de arquivo e use Olá script do comando toorun Olá a seguir:

        .\hivejob.ps1

    Quando a execução do script hello, você está tooenter solicitadas Olá cluster nome e hello HTTPS/Admin credenciais de conta para cluster hello. Você também pode ser solicitado toolog em tooyour assinatura do Azure.

3. Quando o trabalho de saudação for concluído, ele retorna informações toohello semelhante thext a seguir:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Como mencionado anteriormente, **Invoke-Hive** pode ser usado toorun uma consulta e aguardar resposta hello. Use Olá toosee script como funciona o Invoke-Hive a seguir:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    saída de Hello aparência Olá texto a seguir:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Para mais consultas de HiveQL, você pode usar o hello Azure PowerShell **cadeias de caracteres Here** cmdlet ou HiveQL arquivos de script. Olá trecho a seguir mostra como Olá toouse **Invoke-Hive** cmdlet toorun um arquivo de script HiveQL. Olá, HiveQL arquivo de script deve ser carregado toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Para obter mais informações sobre **Here-Strings**, consulte <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Como usar Here-Strings do Windows PowerShell</a>.

## <a name="troubleshooting"></a>Solucionar problemas

Se nenhuma informação é retornada quando Olá trabalho for concluído, um erro pode ter ocorrido durante o processamento. informações de erro tooview para este trabalho, adicionar Olá seguindo toohello final de saudação **hivejob.ps1** arquivo, salve-o e, em seguida, execute-o novamente.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Esse cmdlet retorna informações de saudação escrito tooSTDERR no servidor de saudação quando você executou o trabalho de saudação.

## <a name="summary"></a>Resumo

Como você pode ver, PowerShell do Azure fornece uma maneira fácil toorun consultas de Hive em um cluster HDInsight, o status do trabalho de saudação do monitor e recuperar a saída de hello.

## <a name="next-steps"></a>Próximas etapas

Para obter informações gerais sobre o Hive no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)
