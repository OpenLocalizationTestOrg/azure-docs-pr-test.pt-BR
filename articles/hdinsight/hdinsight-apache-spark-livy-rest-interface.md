---
title: aaaUse Livy Spark toosubmit trabalhos tooSpark cluster HDInsight do Azure | Microsoft Docs
description: Saiba como toouse Apache Spark REST API toosubmit Spark trabalhos de cluster do Azure HDInsight tooan remotamente.
keywords: api rest do apache spark, spark livy
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Use a API de REST do Apache Spark toosubmit trabalhos remotos tooan cluster HDInsight Spark

Saiba como toouse Livy, Olá Apache Spark REST API, que é usado toosubmit remoto trabalhos de cluster do Azure HDInsight Spark tooan. Para obter a documentação detalhada, confira [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

Você pode usar os shells de Spark Livy toorun interativos ou enviar lote toobe de trabalhos executado em Spark. Este artigo aborda usando trabalhos de lote Livy toosubmit. trechos de código Olá neste artigo usam toomake ondulação de ponto de extremidade Livy Spark toohello de chamadas de API REST.

**Pré-requisitos:**

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). Este artigo usa ondulação toodemonstrate como toomake API REST chama em relação a um cluster HDInsight Spark.

## <a name="submit-a-livy-spark-batch-job"></a>Enviar um trabalho em lotes do Livy Spark
Antes de enviar um trabalho em lotes, você deve carregar Olá aplicativo jar no armazenamento de cluster Olá associado Olá cluster. Você pode usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), um utilitário de linha de comando, toodo para. Há vários outros clientes que você pode usar dados tooupload. É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Exemplos**:

* Se o arquivo jar do hello está no armazenamento de cluster da saudação (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Se você quiser toopass Olá o nome do arquivo jar e Olá classname como parte de um arquivo de entrada (neste exemplo, txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Obter informações sobre lotes Livy Spark em execução no cluster Olá
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Exemplos**:

* Se você quiser que todos os lotes de Livy Spark Olá em execução no cluster Olá tooretrieve:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Se você quiser tooretrieve um lote específico com um determinado batchId
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Excluir um trabalho em lotes do Livy Spark
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Exemplo**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark e alta disponibilidade
Livy fornece alta disponibilidade para trabalhos Spark em execução no cluster de saudação. Aqui estão alguns exemplos.

* Se Olá serviço Livy falhar depois de ter enviado um trabalho remotamente tooa Spark cluster, hello trabalho continua toorun no plano de fundo de saudação. Quando Livy é fazer backup, restaura os status de saudação do trabalho hello e relatórios-o novamente.
* Blocos de anotações do Jupyter para HDInsight são ativados pelas Livy em Olá back-end. Se um bloco de anotações estiver executando um trabalho Spark e Olá serviço Livy é reiniciado, notebook Olá continua células de código Olá toorun. 

## <a name="show-me-an-example"></a>Mostrar um exemplo
Nesta seção, podemos examinar o trabalho do exemplos toouse Livy Spark toosubmit em lotes, monitorar o progresso de saudação do trabalho hello e, em seguida, excluí-lo. Olá, usamos neste exemplo de aplicativo é hello um desenvolvidos no artigo Olá [criar um aplicativo de Scala autônomo e toorun no cluster HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md). etapas de saudação aqui supõem que:

* Você já copiou Olá aplicativo jar toohello armazenamento conta associada Olá cluster.
* Você tem ondulação instalada no computador de saudação em que você estiver experimentando essas etapas.

Execute Olá etapas a seguir:

1. Vamos primeiro verificar se Livy Spark está em execução no cluster de saudação. Podemos fazer isso obtendo uma lista de lotes em execução. Se você estiver executando um trabalho usando Livy para Olá primeira vez, a saída de hello deve retornar zero.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Você deve obter um toohello semelhante saída trecho de código a seguir:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Observe como a última linha hello na saída de hello informa **total: 0**, que sugere sem lotes em execução.

2. Agora vamos enviar um trabalho em lotes. saudação de trecho de código a seguir usa um nome do arquivo de entrada (txt) toopass Olá jar e o nome da classe hello como parâmetros. Se você estiver executando essas etapas em um computador Windows, usar um arquivo de entrada é hello abordagem recomendada.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Olá parâmetros no arquivo hello **txt** são definidas da seguinte maneira:
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Você verá um toohello semelhante saída trecho de código a seguir:
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Observe como a última linha hello de saída de hello informa **estado: iniciando**. Assim como, **id:0**. Aqui, **0** é a ID do lote hello.

3. Agora você pode recuperar o status Olá deste lote específico usando a ID do lote hello.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Você verá um toohello semelhante saída trecho de código a seguir:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Olá saída agora mostra **estado: êxito**, que sugere que o trabalho Olá foi concluída com êxito.

4. Se você quiser, agora você pode excluir lote hello.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Você verá um toohello semelhante saída trecho de código a seguir:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Olá última linha da saída de hello mostra que esse lote Olá foi excluído com êxito. Excluir um trabalho, enquanto ele está em execução, também elimina trabalho hello. Se você excluir um trabalho que foi concluída com êxito ou caso contrário, ele exclui informações de trabalho Olá completamente.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Uso do Livy Spark em clusters do HDInsight 3.5

Cluster HDInsight 3.5, por padrão, desabilita o uso de arquivos de dados de exemplo do arquivo local caminhos tooaccess ou jars. Recomendamos que você Olá toouse `wasb://` caminho em vez disso, tooaccess jars ou dados de exemplo dos arquivos do cluster de saudação. Se você quiser caminho local toouse, você deve atualizar a configuração do Ambari Olá adequadamente. toodo para:

1. Vá toohello Ambari portal para cluster hello. Saudação da interface do usuário do Ambari Web está disponível no seu cluster HDInsight no https://**CLUSTERNAME**. azurehdidnsight.net, onde CLUSTERNAME é o nome de saudação do cluster.

2. De Olá barra de navegação esquerda, clique em **Livy**e, em seguida, clique em **configurações**.

3. Em **livy padrão** adicionar o nome da propriedade Olá `livy.file.local-dir-whitelist` e defina seu valor muito**"/"** se desejar que o sistema de toofile tooallow acesso completo. Se você quiser acessar o tooallow tooa somente diretório específico, forneça Olá caminho toothat diretório como valor de saudação.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Enviar trabalhos da Livy para um cluster em uma rede virtual do Azure

Se você conectar tooan cluster HDInsight Spark de dentro de uma rede Virtual do Azure, você pode conectar-se diretamente tooLivy no cluster de saudação. Nesse caso, Olá URL de ponto de extremidade Livy é `http://<IP address of hello headnode>:8998/batches`. Aqui, **8998** Olá porta na qual Livy é executado no nó principal do cluster hello. Para obter mais informações sobre como acessar serviços em portas não públicas, consulte [Portas usadas pelos serviços de Hadoop no HDInsight](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Solucionar problemas

Aqui estão alguns problemas que você possa encontrar ao usar Livy para clusters de tooSpark de envio de trabalho remota.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>Não há suporte para o usar um jar externa de armazenamento adicional da saudação

**Problema:** se seu trabalho Livy Spark referencia um jar externa Olá adicionais da conta de armazenamento associada Olá cluster, o trabalho de saudação falhar.

**Resolução:** Certifique-se de que jar Olá deseja toouse está disponível no armazenamento padrão da saudação associado Olá cluster do HDInsight.





## <a name="next-step"></a>Próxima etapa

* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

