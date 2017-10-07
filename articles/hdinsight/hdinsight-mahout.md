---
title: "recomendações de aaaGenerate usando Mahout HDInsight do PowerShell - Azure | Microsoft Docs"
description: "Saiba como toouse Olá Apache Mahout máquina aprendizado recomendações de filme toogenerate biblioteca com HDInsight (Hadoop) de um script do PowerShell em execução no seu cliente."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>Gerar recomendações de vídeo usando o Apache Mahout com o Hadoop no HDInsight (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Saiba como Olá toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizado de máquina com recomendações de filme toogenerate HDInsight do Azure. exemplo Hello neste documento usa o Azure PowerShell toorun Mahout trabalhos.

## <a name="prerequisites"></a>Pré-requisitos

* Criar um cluster HDInsight baseado em Linux. Para saber mais sobre como criar um, confira [Introdução ao uso do Hadoop baseado em Linux no HDInsight][getstarted].

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [PowerShell do Azure](/powershell/azure/overview)

## <a name="recommendations"></a>Gerar recomendações usando o Azure PowerShell

> [!WARNING]
> trabalho Olá nesta seção funciona usando o PowerShell do Azure. Muitas das classes de saudação fornecidos com Mahout atualmente não funcionam com o Azure PowerShell. Para obter uma lista de classes que não funcionam com o Azure PowerShell, consulte Olá [solução de problemas](#troubleshooting) seção.
>
> Para obter um exemplo do uso de SSH tooconnect tooHDInsight e exemplos de Mahout execução diretamente no cluster hello, consulte [gerar recomendações de filme usando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

Uma das funções de saudação que é fornecido por Mahout é um mecanismo de recomendação. Esse mecanismo aceita dados em formato de saudação do `userID`, `itemId`, e `prefValue` (Olá a preferência de usuários para o item de saudação). Mahout usa usuários de toodetermine Olá dados com as preferências de tipo de item, que podem ser usado toomake recomendações.

Hello exemplo a seguir é uma apresentação simplificada de como funciona o processo de recomendação de saudação:

* **ocorrência colegas**: Joe, Alice e Bob vinculadas todos os *estrela guerras*, *Olá Empire greves volta*, e *retorno de saudação Jedi*. Mahout determina que os usuários que também como qualquer um desses filmes Olá outras duas.

* **ocorrência colegas**: Bob e Alice também gostaram *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*. Mahout determina que os usuários que gostaram filmes de três anterior Olá também como esses filmes.

* **Recomendação de similaridade**: Joe porque gostou Olá três primeiros filmes, Mahout examina filmes que outras pessoas com as preferências semelhantes gostou, mas Joe não tem observados (gostou/classificado). Nesse caso, recomenda Mahout *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*.

### <a name="understanding-hello-data"></a>Noções básicas sobre dados saudação

A [GroupLens Research][movielens] oferece dados de classificação para filmes em um formato compatível com o Mahout. Esses dados estão disponíveis no armazenamento de padrão de saudação para seu cluster em `/HdiSamples//HdiSamples/MahoutMovieData`.

Há dois arquivos, `moviedb.txt` (informações sobre filmes Olá) e `user-ratings.txt`. Olá `user-ratings.txt` arquivo é usado durante a análise. Olá `moviedb.txt` arquivo é texto amigável tooprovide usado ao exibir os resultados de saudação da análise de saudação.

dados contidos no usuário ratings.txt Hello tem uma estrutura de `userID`, `movieID`, `userRating`, e `timestamp`, que informa como altamente cada usuário classificado como um filme. Aqui está um exemplo de dados de saudação:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Executar trabalho Olá

Use Olá toorun de script do Windows PowerShell um trabalho que usa o mecanismo de recomendação Olá Mahout com dados do filme Olá a seguir:

> [!NOTE]
> Esse arquivo solicita informações de cluster do HDInsight tooyour tooconnect usado e execução de trabalhos. Pode levar vários minutos para Olá trabalhos toocomplete e baixar o arquivo do hello txt.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> Trabalhos mahout não remova os dados temporários que são criados durante o processamento de trabalho hello. Olá `--tempDir` parâmetro é especificado em Olá exemplo trabalho tooisolate Olá os arquivos temporários em um diretório específico.

trabalho de Mahout Olá não retorna Olá tooSTDOUT de saída. Em vez disso, ele os armazena no diretório de saída especificado hello como **parte-r-00000**. script Hello baixa esse arquivo muito**txt** no diretório atual de saudação na estação de trabalho.

Olá, texto a seguir é um exemplo de conteúdo desse arquivo hello:

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

Olá primeira coluna é Olá `userID`. Olá valores contidos em ' [' e ']' são `movieId`:`recommendationScore`.

script Hello também baixa Olá `moviedb.txt` e `user-ratings.txt` arquivos, que são necessários tooformat Olá saída toobe mais legível.

### <a name="view-hello-output"></a>Exibir saída de hello

Embora hello saída gerada possa ser Okey para uso em um aplicativo, não é fácil de usar. Olá `moviedb.txt` de saudação servidor pode ser usado tooresolve Olá `movieId` tooa nome do filme. Use Olá seguindo as recomendações de toodisplay de script do PowerShell com nomes de filme:

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Use Olá comando toodisplay Olá recomendações em um formato amigável a seguir: 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

saudação de saída é similar toohello texto a seguir:

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="cannot-overwrite-files"></a>Não foi possível substituir os arquivos

Os trabalhos do Mahout não limpam arquivos temporários criados durante o processamento. Além disso, os trabalhos de saudação não substituir o arquivo de saída existente.

tooavoid erros ao executar trabalhos de Mahout, excluir arquivos temporários e de saída entre as execuções. arquivos de saudação tooremove criados pelo Olá scripts anteriores neste documento, use Olá script do PowerShell a seguir:

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <a name="nopowershell"></a>Classes que não funcionam com o Azure PowerShell

Trabalhos de mahout que usam Olá classes a seguir retornam várias mensagens de erro quando usados no Windows PowerShell:

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

trabalhos de toorun que usam essas classes, conecte-se o cluster do HDInsight toohello usando SSH e executar trabalhos de saudação da linha de comando de saudação. Para obter um exemplo de como usar SSH toorun Mahout trabalhos, consulte [gerar recomendações de filme usando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toouse Mahout, descubra outras maneiras de trabalhar com dados no HDInsight:

* [Hive com o HDInsight](hdinsight-use-hive.md)
* [Pig com o HDInsight](hdinsight-use-pig.md)
* [MapReduce com o HDInsight](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
