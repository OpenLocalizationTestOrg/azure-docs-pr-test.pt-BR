---
title: eventos de aaaProcess dos Hubs de eventos com Storm - HDInsight do Azure | Microsoft Docs
description: "Saiba como tooprocess dados de Hubs de eventos do Azure com uma topologia c# Storm criados no Visual Studio, usando Olá ferramentas HDInsight para Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (C#)

Saiba como toowork com Hubs de eventos do Azure do Apache Storm no HDInsight. Este documento usa um c# Storm topologia tooread e gravar dados de Hubs Evbent

> [!NOTE]
> Para uma versão Java desse projeto, veja [Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

Olá etapas deste documento usam SCP.NET, um pacote do NuGet que torna mais fácil toocreate c# topologias e componentes para usar com Storm no HDInsight.

> [!IMPORTANT]
> Enquanto Olá as etapas neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio, projeto compilado Olá pode ser enviado tooa Storm no cluster HDInsight que usa o Linux. Somente os clusters baseados em Linux criados depois de 28 de outubro de 2016 são compatíveis com as topologias do SCP.NET.

HDInsight 3.4 e topologias de toorun Mono c# uso maiores. exemplo Hello usado neste documento funciona com HDInsight 3.6. Se você planeja criar suas próprias soluções de .NET para HDInsight, verifique Olá [compatibilidade Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento para incompatibilidades.

### <a name="cluster-versioning"></a>Controle de versão do cluster

Olá pacote Microsoft.SCP.Net.SDK NuGet usado para o seu projeto deve corresponder a versão principal de saudação do Storm instalado no HDInsight. As versões 3.5 e 3.6 do HDInsight usam o Storm 1.x, assim, você deve usar a versão 1.0.x.x do SCP.NET com esses clusters.

> [!IMPORTANT]
> exemplo Hello neste documento espera um 3.5 HDInsight ou cluster 3.6.
>
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

As topologias C# também devem ser destinadas ao .NET 4.5.

## <a name="how-toowork-with-event-hubs"></a>Como toowork com Hubs de eventos

A Microsoft fornece um conjunto de componentes de Java que podem ser usado toocommunicate com Hubs de eventos de uma topologia de profusão. Você pode encontrar hello Java (arquivo JAR) que contém uma versão compatível do HDInsight 3.6 desses componentes em [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Enquanto os componentes de saudação são escritos em Java, você pode usá-los facilmente de uma topologia de c#.

Olá componentes a seguir é usado neste exemplo:

* __EventHubSpout__: lê dados nos Hubs de Eventos.
* __EventHubBolt__: grava dados tooEvent Hubs.
* __EventHubSpoutConfig__: usado tooconfigure EventHubSpout.
* __EventHubBoltConfig__: usado tooconfigure EventHubBolt.

### <a name="example-spout-usage"></a>Exemplo de uso do spout

SCP.NET fornece métodos para adicionar uma topologia de tooyour EventHubSpout. Esses métodos tornam mais fácil tooadd um spout que o uso de métodos genéricos Olá para adicionar um componente de Java. Olá exemplo a seguir demonstra como toocreate uma spout usando Olá __SetEventHubSpout__ e **EventHubSpoutConfig** métodos fornecidos pelo SCP.NET:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

exemplo anterior Hello cria um novo componente spout chamado __EventHubSpout__e configura toocommunicate com um hub de eventos. Dica de paralelismo Olá para o componente de saudação é definida toohello número de partições no hub de eventos de saudação. Essa configuração permite Storm toocreate uma instância do componente de saudação para cada partição.

### <a name="example-bolt-usage"></a>Exemplo de uso de bolt

Saudação de uso **JavaComponmentConstructor** método toocreate uma instância do raio da saudação. Olá exemplo a seguir demonstra como toocreate e configurar uma nova instância da saudação **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> Este exemplo usa uma expressão de Clojure passada como uma cadeia de caracteres, em vez de usar **JavaComponentConstructor** toocreate um **EventHubBoltConfig**, como exemplo de spout hello fez. Ambos os métodos funcionam. Use o método hello parece tooyou melhor.

## <a name="download-hello-completed-project"></a>Baixe o projeto de saudação concluída

Você pode baixar uma versão completa do projeto Olá criado neste tutorial de [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). No entanto, você ainda precisa tooprovide configurações seguindo as etapas de saudação neste tutorial.

### <a name="prerequisites"></a>Pré-requisitos

* Um [Apache Storm no cluster HDInsight versão 3.5 ou 3.6](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > exemplo Hello usado neste documento requer Storm no HDInsight versão 3.5 ou 3.6. Isso não funciona com versões anteriores do HDInsight, devido a alterações de nome de classe toobreaking. Para obter uma versão desse exemplo que funcione com clusters mais antigos, consulte [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* Um [Hub de eventos do Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Olá [SDK .NET do Azure](http://azure.microsoft.com/downloads/).

* Olá [ferramentas HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Java JDK 1.8 ou posterior em seu ambiente de desenvolvimento. Downloads de JDK estão disponíveis na [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Olá **JAVA_HOME** diretório de toohello de ponto de deve variável de ambiente que contém Java.
  * Olá **%JAVA_HOME%/bin** diretório deve estar no caminho de saudação.

## <a name="download-hello-event-hubs-components"></a>Baixar os componentes de Hubs de eventos Olá

Saudação de download dos Hubs de eventos spout e incluem o componente de [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Crie um diretório chamado `eventhubspout`e salve o arquivo de saudação no diretório de saudação.

## <a name="configure-event-hubs"></a>Configurar os Hubs de Eventos

Hubs de eventos é a fonte de dados de saudação para este exemplo. Use informações de saudação na seção "Criar um hub de eventos" de saudação do [Introdução aos Hubs de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. Depois que o hub de eventos Olá tiver sido criado, exibir hello **EventHub** folha em hello Azure portal e selecione **políticas de acesso compartilhado**. Selecione **+ adicionar** tooadd Olá políticas a seguir:

   | Nome | Permissões |
   | --- | --- |
   | gravador |Enviar |
   | leitor |Escutar |

    ![Captura de tela da janela Políticas de acesso compartilhadas](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Selecione Olá **leitor** e **gravador** políticas. Copie e salve o valor de chave primária Olá para ambas as políticas, pois esses valores são usados mais tarde.

## <a name="configure-hello-eventhubwriter"></a>Configurar Olá EventHubWriter

1. Se já não tiver instalado a versão mais recente Olá das ferramentas do HDInsight Olá para o Visual Studio, consulte [começar a usar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Baixar a solução de saudação do [eventhub de profusão de híbrida](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. Em Olá **EventHubWriter** projeto, abra Olá **App. config** arquivo. Use as informações de saudação do hub de eventos de saudação que você configurou anteriormente toofill no valor Olá Olá chaves a seguir:

   | Chave | Valor |
   | --- | --- |
   | EventHubPolicyName |gravador (se você usou um nome diferente para a política de saudação com *enviar* permissão, usá-lo em vez disso.) |
   | EventHubPolicyKey |chave de saudação para política de gravador hello. |
   | EventHubNamespace |Olá namespace que contém o hub de eventos. |
   | EventHubName |O nome do hub de eventos. |
   | EventHubPartitionCount |número de saudação de partições em seu hub de eventos. |

4. Salve e feche o hello **App. config** arquivo.

## <a name="configure-hello-eventhubreader"></a>Configurar Olá EventHubReader

1. Olá abrir **EventHubReader** projeto.

2. Olá abrir **App. config** arquivo hello **EventHubReader**. Use as informações de saudação do hub de eventos de saudação que você configurou anteriormente toofill no valor Olá Olá chaves a seguir:

   | Chave | Valor |
   | --- | --- |
   | EventHubPolicyName |leitor (se você usou um nome diferente para a política de saudação com *escutar* permissão, usá-lo em vez disso.) |
   | EventHubPolicyKey |chave de saudação para política de leitor de saudação. |
   | EventHubNamespace |Olá namespace que contém o hub de eventos. |
   | EventHubName |O nome do hub de eventos. |
   | EventHubPartitionCount |número de saudação de partições em seu hub de eventos. |

3. Salve e feche o hello **App. config** arquivo.

## <a name="deploy-hello-topologies"></a>Implantar topologias Olá

1. De **Gerenciador de soluções**, Olá atalho **EventHubReader** do projeto e selecione **enviar tooStorm no HDInsight**.

    ![Captura de tela do Gerenciador de soluções, com enviar tooStorm no HDInsight realçado](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. Em Olá **topologia enviar** caixa de diálogo, selecione seu **Cluster Storm**. Expanda **configurações adicionais**, selecione **caminhos de arquivo Java**, selecione **...** e selecione Olá diretório que contém o arquivo JAR Olá que você baixou anteriormente. Por fim, clique em **Enviar**.

    ![Captura de tela da caixa de diálogo Enviar Topologia](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Quando a topologia de saudação tiver sido enviada, Olá **Storm topologias visualizador** é exibida. tooview informações sobre topologia hello, selecione Olá **EventHubReader** topologia no painel esquerdo da saudação.

    ![Captura de tela do Visualizador de Topologias do Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. De **Gerenciador de soluções**, Olá atalho **EventHubWriter** do projeto e selecione **enviar tooStorm no HDInsight**.

5. Em Olá **topologia enviar** caixa de diálogo, selecione seu **Cluster Storm**. Expanda **configurações adicionais**, selecione **caminhos de arquivo Java**, selecione **...** , e o diretório de Olá select que contém o arquivo JAR de saudação você baixou anteriormente. Por fim, clique em **Enviar**.

6. Quando a topologia de saudação tiver sido enviada, atualizar a lista de topologia de saudação no hello **Storm topologias visualizador** tooverify ambas as topologias estão em execução no cluster de saudação.

7. Em **Storm topologias visualizador**, selecione Olá **EventHubReader** topologia.

8. componente de saudação tooopen resumo de raio hello, clique duas vezes em Olá **LogBolt** componente no diagrama de saudação.

9. Em Olá **executores** seção, selecione um dos links de saudação em Olá **porta** coluna. Isso exibe informações registradas pelo componente de saudação. informações de saudação registrada são semelhante toohello texto a seguir:

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Parar topologias Olá

topologias de saudação toostop, selecione cada topologia em Olá **profusão de Visualizador de topologia**, em seguida, clique em **Kill**.

![Captura de tela do Visualizador de Topologia do Storm, com o botão Encerrar realçado](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Excluir o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Próximas etapas

Neste documento, você aprendeu como a toouse Hubs de eventos do Java Olá spout e incluir a partir de um toowork de topologia c# com dados em Hubs de eventos do Azure. toolearn mais sobre a criação de topologias de c#, consulte o seguinte hello:

* [Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Guia de programação do SCP](hdinsight-storm-scp-programming-guide.md)
* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)
