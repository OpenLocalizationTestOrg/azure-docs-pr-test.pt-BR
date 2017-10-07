---
title: aaaUse Apache Spark streaming com Hubs de eventos de HDInsight do Azure | Microsoft Docs
description: Crie uma amostra de streaming do Apache Spark como toosend um dados tooAzure Hub de eventos de fluxo e receber os eventos em cluster HDInsight Spark usando um aplicativo scala.
keywords: streaming do apache spark, streaming do spark, exemplo de spark, exemplo de streaming do apache spark, exemplo do hub de evento do azure, exemplo de spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Streaming do Apache Spark: processe dados de Hubs de Eventos do Azure com o cluster Spark no HDInsight

Neste artigo, você deve criar um Apache Spark streaming de exemplo que envolve Olá etapas a seguir:

1. Você pode usar mensagens tooingest aplicativo autônomo em um Hub de eventos do Azure.

2. Para recuperar mensagens de saudação do Hub de eventos com duas abordagens diferentes, em tempo real usando um aplicativo em execução no cluster Spark no HDInsight do Azure.

3. Criar pipelines analíticos streaming toopersist sistemas de armazenamento de toodifferent de dados ou obter ideias de dados em funcionamento hello.

## <a name="prerequisites"></a>Pré-requisitos

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Conceitos de Streaming do Spark

Para obter uma explicação detalhada do streaming Spark, veja [Visão geral do streaming do Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview). HDInsight traz Olá cluster tooa de recursos de streaming mesmo Spark no Azure.  

## <a name="what-does-this-solution-do"></a>O que essa solução faz?

Neste artigo, toocreate um exemplo de streaming Spark, execute Olá etapas a seguir:

1. Crie um Hub de Eventos do Azure que vá receber uma transmissão de eventos.

2. Executar um aplicativo autônomo local que gera eventos e envia-toohello Hub de eventos do Azure. aplicativo de exemplo Hello que faz isso é publicado na [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Execute um aplicativo de streaming remotamente em um cluster Spark que lê o eventos de streaming do Hub de Eventos do Azure e execute procedimentos diversos de análise/processamento de dados.

## <a name="create-an-azure-event-hub"></a>Criar um Hub de Eventos do Azure

1. Faça logon no toohello [Portal do Azure](https://ms.portal.azure.com)e clique em **novo** em Olá superior esquerda da tela hello.

2. Clique em **Internet das Coisas** e, em seguida, clique em **Hubs de Eventos**.

    ![Criar hub de eventos para exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Criar hub de eventos para exemplo de streaming do Spark")

3. Em Olá **criar namespace** folha, insira um nome de namespace. Escolha Olá preço (básico ou padrão). Além disso, escolha uma assinatura do Azure, o grupo de recursos e o local no qual recurso de saudação toocreate. Clique em **criar** toocreate Olá namespace.

      ![Fornecer um nome ao hub de eventos para o exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fornecer um nome ao hub de eventos para o exemplo de streaming do Spark")

    > [!NOTE]
    > Você deve selecionar Olá mesmo **local** como seu cluster Apache Spark no HDInsight tooreduce latência e custos.
    >
    >

4. Na lista de namespace de Hubs de eventos hello, clique em Olá recém-criado namespace.      


5. Na folha de namespace hello, clique em **Hubs de eventos**e, em seguida, clique em **+ Hub de eventos** toocreate um novo Hub de eventos.
   
    ![Criar hub de eventos para exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Criar hub de eventos para exemplo de streaming do Spark")

6. Digite um nome para o Hub de eventos, too10 de contagem de partição do conjunto hello e too1 de retenção de mensagem. Nós não são arquivar mensagens de saudação nesta solução para deixar Olá restante como padrão e, em seguida, clique em **criar**.
   
    ![Fornecer detalhes do hub de eventos para o exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fornecer detalhes do hub de eventos para o exemplo de streaming do Spark")

7. Olá recém-criado Hub de eventos é listado na folha de Hub de eventos de saudação.
    
     ![Exibir Hub de eventos de exemplo de fluxo contínuo do hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Hub de eventos de exibição para Olá despertar streaming de exemplo")

8. Na folha de namespace hello (não Olá específico Hub de eventos folha), clique em **políticas de acesso compartilhado**e, em seguida, clique em **RootManageSharedAccessKey**.
    
     ![Definir políticas de Hub de eventos para o exemplo de fluxo contínuo do hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "políticas de Hub de eventos definida para Olá despertar streaming de exemplo")

9. Clique em Olá Olá de toocopy do botão de cópia **RootManageSharedAccessKey** primária conexão e chave de cadeia de caracteres toohello área de transferência. Salve essas toouse posteriormente no tutorial de saudação.
    
     ![Exibir chaves de política do Hub de eventos para exemplo de fluxo contínuo do hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "chaves de política do Hub de eventos de exibição para Olá despertar streaming de exemplo")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>Enviar mensagens tooAzure Hub de eventos usando um aplicativo de exemplo Scala

Nesta seção você usar um aplicativo Scala autônomo local que gera um fluxo de eventos e o envia tooAzure Hub de eventos que você criou anteriormente. Este aplicativo está disponível no GitHub em [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). etapas de saudação aqui supõem que você já tiver bifurcada este repositório GitHub.

1. Verifique se que você tem o seguinte Olá instalado no computador de saudação em que você executa este aplicativo.

    * Kit de desenvolvimento Oracle Java. Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. Você pode baixá-lo [aqui](https://maven.apache.org/download.cgi). Instruções tooinstall Maven estão disponíveis [aqui](https://maven.apache.org/install.html).

2. Abra um prompt de comando e navegue local toohello clonar o repositório do GitHub Olá Olá aplicativo de exemplo Scala e execute Olá aplicativo de hello toobuild comando a seguir.

        mvn package

3. Olá jar de saída para o aplicativo hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, é criado sob **/destino** directory. Você usa este JAR posteriormente na solução completa do tootest Olá neste artigo.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Criar as mensagens de tooreceive do aplicativo de Hub de eventos em um cluster do Spark 

Temos duas tooconnect abordagens Spark Streaming e Hubs de eventos do Azure, com base no receptor de conexão e conexão direta com base DStream. Com base em DStream direta é apresentado em janeiro de 2017, versão Olá 2.0.3. Ele deve conexão tooreplace Olá original com base no destinatário conforme ele é mais eficaz e eficiente de recursos. Mais detalhes podem ser encontrados em [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). O Direct DStream dá suporte apenas ao Spark 2.0+.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Criar aplicativos com o conector do hello dependência toospark eventhubs

Podemos também publica Olá versão do Spark-EventHubs no GitHub de preparo. toouse Olá preparo versão Spark EventHubs, primeira etapa de saudação é tooindicate GitHub como Olá repositório de origem adicionando Olá toopom.xml de entrada a seguir:

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

Em seguida, você pode adicionar Olá dependência tooyour projeto tootake Olá versão de pré-lançamento a seguir.

Dependência do Maven

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

Dependência SBT

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Conexão por Direct DStream

Um arquivo jar pré-criado que contém exemplos que usam Direct DStream pode ser baixado em [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).

arquivo jar de saudação contém três exemplos, cujo código-fonte estão disponíveis em [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Usando [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) como um exemplo:

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

Em hello, o exemplo acima `eventhubParameters` Olá parâmetros específicos tooa EventHubs de única instância e você tem toopass-toohello `createDirectStreams` API que constrói um namespace de Hubs de eventos DStream direto objeto mapeamento tooa. Sobre Olá DStream direto, você pode chamar qualquer API DStream fornecido pela estrutura Spark API de Streaming. Neste exemplo, calculamos frequência saudação de cada palavra em intervalos de lote micro 3 última hello.

### <a name="receiver-based-connection"></a>Conexão com base em receptor

Um Spark streaming escrito em Scala, que recebe eventos e destinos de toodifferent de saudação de rota, o aplicativo de exemplo está disponível em [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Siga as etapas de saudação abaixo do aplicativo de saudação tooupdate para sua configuração de Hub de eventos e criar hello jar de saída.

1. Inicie a IDEIA de IntelliJ e de saudação iniciar tela, selecione **Check-out do controle de versão** e, em seguida, clique em **Git**.
   
    ![Exemplo de streaming do Apache Spark – obter fontes do Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Exemplo de streaming do Apache Spark – obter fontes do Git")

2. Em Olá **Clone repositório** caixa de diálogo, forneça a URL Olá toohello tooclone de repositório Git do, especifique Olá tooclone de diretório para e, em seguida, clique em **Clone**.
   
    ![Exemplo de streaming do Apache Spark – clonar do Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Exemplo de streaming do Apache Spark – clonar do Git")
3. Siga os prompts de saudação até que o projeto Olá completamente é clonado. Pressione **Alt + 1** tooopen Olá **exibição projeto**. Ele deve ser semelhante a seguinte hello.
   
    ![Exemplo de streaming do Apache Spark – Exibição do Projeto](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Exemplo de streaming do Apache Spark – Exibição do Projeto")
4. Verifique se o código do aplicativo hello é compilado com Java8. tooensure, clique **arquivo**, clique em **estrutura do projeto**e em Olá **projeto** guia, verifique se o nível de linguagem do projeto está definido muito**8 - Lambdas, tipo anotações, etc.**.
   
    ![Exemplo de streaming do Apache Spark – Definir compilador](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Exemplo de streaming do Apache Spark – Definir compilador")
5. Olá abrir **pom.xml** e verifique se a versão do Spark hello está correta. Em `<properties>` nó, procure Olá trecho de código a seguir e verificar a versão do Spark hello.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. aplicativo Hello requer um jar dependência chamado **jar do driver JDBC**. Isso é necessário toowrite mensagens de saudação recebidas do Hub de eventos em um banco de dados do SQL Azure. Você pode baixar esse jar (v 4.1 ou posterior) [aqui](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Adicione referência toothis jar na biblioteca de saudação do projeto. Execute Olá etapas a seguir:
     
     1. Na janela de IDEIA IntelliJ onde você tem aplicativo hello abrir, clique em **arquivo**, clique em **estrutura do projeto**e, em seguida, clique em **bibliotecas**. 
     2. Clique em Olá Adicionar ícone (![Adicionar ícone](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), clique em **Java**e, em seguida, navegue toohello local onde você baixou o jar do driver JDBC hello. Siga Olá prompts tooadd Olá arquivo toohello projeto biblioteca jar.

         ![adicionar dependências ausentes](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Adicionar jars de dependência ausente")
     3. Clique em **Aplicar**.

7. Crie arquivo de jar de saída de hello. Execute Olá etapas a seguir.

   1. Em Olá **estrutura do projeto** caixa de diálogo, clique em **artefatos** e, em seguida, clique em hello mais símbolo. Na caixa de diálogo pop-up de saudação, clique em **JAR**e, em seguida, clique em **de módulos com dependências**.      
       
       ![Exemplo de streaming do Apache Spark – Criar JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Exemplo de streaming do Apache Spark – Criar JAR")
   2. Em Olá **criar JAR de módulos** caixa de diálogo, clique nas reticências da saudação (![reticências](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) em relação a saudação **classe principal**.
   3. Em Olá **selecionar principal classe** caixa de diálogo caixa, selecione qualquer uma das classes disponíveis hello e, em seguida, clique em **Okey**.
      
       ![Exemplo de streaming do Apache Spark – selecionar classe para jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Exemplo de streaming do Apache Spark – selecionar classe para jar")
   4. Em Olá **criar JAR de módulos** caixa de diálogo caixa, certifique-se de que a opção Olá muito**extrair toohello destino JAR** está selecionado e, em seguida, clique em **Okey**. Isso cria um JAR único com todas as dependências.
      
       ![Exemplo de streaming do Apache Spark – criar jar a partir de módulos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Exemplo de streaming do Apache Spark – criar jar a partir de módulos")
   5. Olá **Layout de saída** guia lista todos os jars Olá que estão incluídos como parte do projeto de Maven hello. Você pode selecionar e excluir Olá aqueles nos quais Olá Scala aplicativo não tem nenhuma dependência direta. Para o aplicativo hello, estamos criando aqui, você pode remover Olá tudo, exceto o último (**spark-streaming--persistência-exemplos de dados de saída de compilação**). Selecione Olá jars toodelete e clique em Olá **excluir** ícone (![excluir ícone](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Exemplo de streaming do Apache Spark – excluir jars extraídos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Exemplo de streaming do Apache Spark – excluir jars extraídos")
      
       Certifique-se de **compilar no Verifique** caixa é selecionada, o que garante que jar Olá é criado sempre que o projeto Olá for criado ou atualizado. Clique em **Aplicar**.
   6. Em Olá **Layout de saída** guia à direita na parte inferior de saudação do hello **elementos disponíveis** caixa, você tem jar do hello SQL JDBC que você adicionou a biblioteca de projeto toohello anterior. Você deve adicionar esse toohello **Layout de saída** guia. Clique no arquivo jar do hello e clique **extrair em saída raiz**.
      
       ![Exemplo de streaming do Apache Spark – extrair jar de dependência](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Exemplo de streaming do Apache Spark – extrair jar de dependência")  
      
       Olá **Layout de saída** guia agora deve se parecer com isso.
      
       ![Exemplo de streaming do Apache Spark – guia de saída final](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Exemplo de streaming do Apache Spark – guia de saída final")        
      
       Em Olá **estrutura do projeto** caixa de diálogo, clique em **aplicar** e, em seguida, clique em **Okey**.    
   7. Olá barra de menus, clique em **criar**e, em seguida, clique em **projeto Make**. Você também pode clicar em **criar artefatos** toocreate jar de saudação. Olá jar de saída é criado sob **\classes\artifacts**.
      
       ![Exemplo de streaming do Apache Spark – JAR de saída](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Exemplo de streaming do Apache Spark – JAR de saída")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Executar o aplicativo hello remotamente em um cluster do Spark usando Livy

Neste artigo use Livy toorun Olá Apache Spark streaming aplicativo remotamente em um cluster Spark. Para obter uma discussão detalhada sobre como toouse Livy com HDInsight Spark do cluster, consulte [enviar trabalhos remotamente tooan Apache Spark cluster no Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md). Antes de começar executando o aplicativo de streaming de Spark hello, há algumas coisas que você deve fazer:

1. Iniciar Olá autônomo local aplicativo toogenerate eventos e enviados tooEvent Hub. Use Olá toodo de comando a seguir para:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Saudação de cópia streaming jar (**spark-streaming-data-persistência-examples.jar**) toohello associado Olá cluster de armazenamento de Blob do Azure. Isso torna Olá jar acessível tooLivy. Você pode usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), um comando de linha utilitário, toodo assim. Há muito de outros clientes, você pode usar dados de tooupload. É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).
3. Instale ONDULAÇÃO no computador de saudação onde você está executando esses aplicativos. Usamos ONDULAÇÃO tooinvoke Olá Olá de toorun de pontos de extremidade Livy trabalhos remotamente.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Executar Olá Spark streaming tooreceive Olá eventos do aplicativo em um Blob de armazenamento do Azure como texto

Abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar hello (nome de usuário/senha e cluster substituir) de comando a seguir:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Olá parâmetros no arquivo hello **inputBlob.txt** são definidos da seguinte maneira:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Vamos Entenda quais são os parâmetros de saudação no arquivo de entrada hello:

* **arquivo** Olá caminho toohello aplicativo jar em arquivo hello conta de armazenamento do Azure associada Olá cluster.
* **nome da classe** é Olá nome da classe Olá JAR hello.
* **argumentos** Olá lista de argumentos necessários pela classe Olá
* **numExecutors** é Olá número de núcleos usados pelo saudação do Spark toorun streaming de aplicativos. Sempre deve ser pelo menos duas vezes o número de saudação de partições de Hub de eventos.
* **executorMemory**, **executorCores**, **driverMemory** são parâmetros usados tooassign necessários recursos toohello aplicativo de transmissão.

> [!NOTE]
> Não é necessário toocreate Olá pastas de saída (EventCheckpoint, EventCount/EventCount10) que são usadas como parâmetros. Olá streaming aplicativo criará para você.
>
>

Quando você executa o comando hello, você verá uma saída semelhante Olá seguinte:

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Anote o ID de lote Olá na última linha hello da saída da saudação (no exemplo é '1'). tooverify que Olá aplicativo seja executado com êxito, você pode examinar sua conta de armazenamento do Azure associada Olá cluster e você deverá ver Olá **/EventCount/EventCount10** pasta criada ali. Essa pasta deve conter blobs que captura Olá número de eventos processados em Olá período de tempo especificado para o parâmetro hello **lote intervalo em segundos**.

aplicativo de transmissão Olá Spark continuará toorun até você eliminá-lo. Assim, o toodo use Olá comando a seguir:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Executar aplicativos de saudação tooreceive eventos de saudação em um Blob de armazenamento do Azure como JSON
Abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar hello (nome de usuário/senha e cluster substituir) de comando a seguir:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Olá parâmetros no arquivo hello **inputJSON.txt** são definidos da seguinte maneira:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

parâmetros de saudação são semelhante toowhat especificada para saída de texto de saudação na etapa anterior hello. Novamente, não é necessário toocreate Olá pastas de saída (EventCheckpoint, EventCount/EventCount10) que são usadas como parâmetros. Olá streaming aplicativo criará para você.

 Depois de executar o comando hello, você pode examinar sua conta de armazenamento do Azure associada Olá cluster e você deverá ver Olá **/EventStore10** pasta criada ali. Abrir qualquer arquivo prefixado com **parte -** e você deve consultar eventos Olá processados em um formato JSON.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Executar aplicativos de saudação tooreceive eventos de saudação em uma tabela de Hive
Olá toorun aplicativo de transmissão Spark que eventos de fluxos em uma seção de tabela que você precisa de alguns componentes adicionais. Estes são:

* datanucleus-api-jdo-3.2.6.jar
* datanucleus-rdbms-3.2.9.jar
* datanucleus-core-3.2.10.jar
* hive-site.xml

Olá **. jar** arquivos estão disponíveis no seu cluster HDInsight Spark no `/usr/hdp/current/spark-client/lib`. Olá **hive-site.XML** está disponível em `/usr/hdp/current/spark-client/conf`.

Você pode usar [WinScp](http://winscp.net/eng/download.php) toocopy esses arquivos do computador local do hello cluster tooyour. Você pode usar ferramentas toocopy esses arquivos por conta de armazenamento tooyour associados cluster hello. Para obter mais informações sobre como os arquivos de tooupload toohello conta de armazenamento, consulte [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md).

Depois que você copiou em Olá arquivos tooyour conta de armazenamento do Azure, abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar hello (nome de usuário/senha e cluster substituir) de comando a seguir:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Olá parâmetros no arquivo hello **inputHive.txt** são definidos da seguinte maneira:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

parâmetros de saudação são semelhante toowhat especificada para saída de texto de saudação, nas etapas anteriores hello. Novamente, você não precisa saída de hello toocreate pastas (EventCheckpoint, EventCount/EventCount10) ou hello tabela Hive (EventHiveTable10) que são usados como parâmetros de saída. Olá streaming aplicativo criará para você. Observe que Olá **jars** e **arquivos** opção inclui arquivos do caminhos toohello. jar e hive-site.XML Olá que você copiou toohello conta de armazenamento.

tooverify que Olá tabela hive foi criado com êxito, você pode SSH em cluster hello e executadas consultas de Hive. Para obter instruções, consulte [usar o Hive com Hadoop no HDInsight com SSH](hdinsight-hadoop-use-hive-ssh.md). Quando você estiver conectado usando SSH, você pode executar Olá tooverify de comando a seguir essa tabela de Hive hello, **EventHiveTable10**, é criado.

    show tables;

Você verá uma saída semelhante toohello a seguir:

    OK
    eventhivetable10
    hivesampletable

Você também pode executar uma consulta SELECT tooview conteúdo de saudação da tabela de saudação.

    SELECT * FROM eventhivetable10 LIMIT 10;

Você verá uma saída semelhante Olá seguinte:

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Executar aplicativos de saudação tooreceive eventos de saudação em uma tabela de banco de dados do SQL Azure
Antes de executar essa etapa, verifique se que você tem um banco de dados SQL Azure criado. Para obter instruções, consulte [Criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md). toocomplete seção, você precisa valores para o nome do banco de dados, nome do servidor de banco de dados e credenciais de administrador de banco de dados hello como parâmetros. Tabela de banco de dados de saudação toocreate não é necessário embora. Olá aplicativo streaming Spark que cria para você.

Abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar Olá comando a seguir:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Olá parâmetros no arquivo hello **inputSQL.txt** são definidos da seguinte maneira:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

tooverify que Olá aplicativo é executado com êxito, você pode se conectar a banco de dados do SQL Azure toohello usando o SQL Server Management Studio. Para obter instruções sobre como toodo que, consulte [conectar tooSQL banco de dados com o SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md). Quando você estiver conectado toohello banco de dados, você poderá navegar toohello **EventContent** tabela que foi criada pelo Olá streaming de aplicativos. Você pode executar uma consulta rápida tooget Olá de dados da tabela de saudação. Execute Olá consulta a seguir:

    SELECT * FROM EventCount

Você deve ver o seguinte de toohello semelhante de saída:

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)
* [Design de Conexão com Base no Receptor e Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar maiores Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
