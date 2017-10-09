---
title: dados de sensor aaaAnalyze com Apache Storm e HBase | Microsoft Docs
description: "Saiba como tooconnect tooApache Storm com uma rede virtual. Use Storm com dados de sensor do HBase tooprocess de um hub de eventos e visualizá-la com D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Analisar dados de sensor com o Apache Storm e com o HBase no HDInsight (Hadoop)

Saiba como toouse Apache Storm no HDInsight tooprocess os dados do sensor de Hub de eventos do Azure. Olá dados são armazenados no Apache HBase em HDInsight e visualizado usando D3.js.

saudação do Azure Resource Manager modelo usada neste documento demonstra como toocreate vários recursos do Azure em um grupo de recursos. modelo de saudação cria uma rede Virtual do Azure, dois clusters de HDInsight (Storm e HBase) e um aplicativo Web do Azure. Uma implementação de Node. js de um painel da web em tempo real é implantado automaticamente toohello web app.

> [!NOTE]
> informações de saudação neste documento e o exemplo neste documento exigem HDInsight versão 3.6.
>
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Pré-requisitos

* Uma assinatura do Azure.
* [Node. js](http://nodejs.org/): painel de web hello toopreview usados localmente no seu ambiente de desenvolvimento.
* [Java e hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): usado toodevelop topologia de profusão de saudação.
* [Maven](http://maven.apache.org/what-is-maven.html): projeto de saudação toobuild e compilação usado.
* [Git](http://git-scm.com/): projeto de saudação toodownload usado do GitHub.
* Um **SSH** cliente: clusters de HDInsight baseados em Linux toohello tooconnect usados. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> Não é necessário um cluster HDInsight existente. Olá etapas neste documento para criar hello recursos a seguir:
> 
> * Uma Rede virtual do Azure
> * Um cluster Storm no HDInsight (baseado em Linux, dois nós de trabalho)
> * Um cluster HBase no HDInsight (baseado em Linux, dois nós de trabalho)
> * Um aplicativo Web do Azure que hospeda o painel da web de saudação

## <a name="architecture"></a>Arquitetura

![diagrama da arquitetura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

Este exemplo consiste em Olá componentes a seguir:

* **Hub de Eventos do Azure**: contém os dados coletados dos sensores.
* **Storm no HDInsight**: fornece processamento em tempo real dos dados do Hub de Eventos.
* **HBase no HDInsight**: fornece um armazenamento de dados NoSQL persistente para dados depois que eles são processados pelo Storm.
* **Serviço de rede Virtual do Azure**: permite a comunicação segura entre hello Storm no HDInsight e HBase em clusters de HDInsight.
  
  > [!NOTE]
  > Uma rede virtual é necessária ao usar a API de cliente de Java HBase hello. Ela não fica exposta por gateway de público Olá para clusters do HBase. Clusters HBase instalar e Storm em Olá mesma rede virtual permite Olá cluster Storm (ou qualquer outro sistema na rede virtual Olá) toodirectly acessar HBase usando a API do cliente.

* **Site do painel**: um painel de exemplo que traça gráficos de dados em tempo real.
  
  * site de saudação é implementado em Node. js.
  * [Socket.IO](http://socket.io/) é usado para comunicação em tempo real entre Olá site da Web e de topologia de profusão de saudação.
    
    > [!NOTE]
    > O uso do Socket.io para a comunicação é um detalhe de implementação. Você pode usar qualquer estrutura de comunicação, como SignalR ou WebSockets brutos.

  * [D3.js](http://d3js.org/) toograph usado Olá dados enviados toohello site.

> [!IMPORTANT]
> Dois clusters são necessários, pois não há nenhum método com suporte toocreate um HDInsight cluster Storm e HBase.

Olá topologia lê dados de Hub de eventos usando Olá [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe e grava dados em HBase usando Olá [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe. Comunicação com o site de saudação é realizada usando [client.java socket.io](https://github.com/nkzawa/socket.io-client.java).

Olá diagrama a seguir explica o layout de saudação da topologia de saudação:

![diagrama de topologia](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Este diagrama é uma exibição simplificada de topologia de saudação. Uma instância de cada componente é criada para cada partição no Hub de Eventos. Essas instâncias são distribuídas entre os nós de saudação em cluster hello e dados são roteados entre eles, da seguinte maneira:
> 
> * Dados do analisador de toohello spout Olá são com balanceamento de carga.
> * Dados de saudação analisador toohello painel e HBase são agrupados por ID do dispositivo, para que as mensagens de Olá mesmo dispositivo sempre fluxo toohello mesmo componente.

### <a name="topology-components"></a>Componentes da topologia

* **Evento Hub Spout**: spout Olá é fornecido como parte da versão do Apache Storm 0.10.0 e superior.
  
  > [!NOTE]
  > spout do Hub de eventos Olá usado neste exemplo requer uma profusão de versão do cluster HDInsight 3.5 ou 3.6.

* **ParserBolt.java**: Olá dados emitida pelo spout Olá JSON bruto e, ocasionalmente, mais de um evento é emitido por vez. Este raio lê dados de saudação emitidos pelo Olá spout e analisa a mensagem de saudação do JSON. raio Hello, em seguida, emite os dados de saudação como uma tupla que contém vários campos.
* **DashboardBolt.java**: esse componente demonstra como toouse Olá Socket.io biblioteca de cliente para dados do Java toosend no painel da web toohello em tempo real.
* **não hbase.yaml**: Olá definição de topologia usada durante a execução no modo local. Não usa componentes HBase.
* **com hbase.yaml**: Olá definição de topologia usada ao executar topologia Olá no cluster hello. Usa componentes HBase.
* **dev.properties**: Olá informações de configuração para spout do Hub de eventos de saudação, HBase raio e os componentes do painel.

## <a name="prepare-your-environment"></a>Prepare o seu ambiente

Antes de usar este exemplo, você deve criar um Hub de eventos do Azure, a topologia que Storm Olá lê do.

### <a name="configure-event-hub"></a>Configurar o Hub de Eventos

Hub de eventos é a fonte de dados de saudação para este exemplo. Use Olá etapas toocreate um Hub de eventos a seguir.

1. De saudação [portal do Azure](https://portal.azure.com), selecione **+ novo** -> **Internet das coisas** -> **Hubs de eventos**.
2. Em Olá **criar Namespace** , execute as seguintes tarefas de saudação:
   
   1. Insira um **nome** Olá namespace.
   2. Selecione um tipo de preço. **Básico** é suficiente para este exemplo.
   3. Selecione hello Azure **assinatura** toouse.
   4. Selecione um grupo de recursos existente ou crie um novo.
   5. Selecione Olá **local** para Olá Hub de eventos.
   6. Selecione **Pin toodashboard**e, em seguida, clique em **criar**.

3. Quando o processo de criação de saudação for concluído, Olá informações de Hubs de eventos para o namespace é exibida. Desse local, selecione **+ Adicionar Hub de Eventos**. Em Olá **criar Hub de eventos** seção, insira um nome de **sensordata**e, em seguida, selecione **criar**. Deixe Olá outros campos com valores padrão de saudação.
4. Olá dos Hubs de eventos Exibir para seu namespace, selecione **Hubs de eventos**. Selecione Olá **sensordata** entrada.
5. Olá sensordata Hub de eventos, selecione **políticas de acesso compartilhado**. Saudação de uso **+ adicionar** saudação do link tooadd políticas a seguir:

    | Nome da política | Declarações |
    | ----- | ----- |
    | dispositivos | Enviar |
    | storm | Escutar |

1. Selecione ambas as políticas e anote Olá **chave primária** valor. Você precisa valor Olá para ambas as políticas em etapas futuras.

## <a name="download-and-configure-hello-project"></a>Baixar e configurar o projeto de saudação

Use Olá seguindo o projeto de saudação toodownload do GitHub.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Após a conclusão do comando hello, você tem Olá estrutura de diretórios a seguir:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Este documento não entra nos detalhes de toofull de código Olá incluídos neste exemplo. No entanto, o código de saudação totalmente é comentado.

tooconfigure tooread de projeto de saudação do Hub de eventos, abra Olá `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` e adicione seu toohello de informações de Hub de eventos linhas seguintes:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Compile e teste localmente

> [!IMPORTANT]
> Usando a topologia de saudação localmente requer um ambiente de desenvolvimento profusão de trabalho. Para saber mais, confira [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Configurando um ambiente de desenvolvimento Storm) em Apache.org.

> [!WARNING]
> Se você estiver usando um ambiente de desenvolvimento do Windows, você pode receber um `java.io.IOException` ao executar a topologia de saudação localmente. Nesse caso, mova na topologia de saudação toorunning no HDInsight.

Antes de testar, você deve iniciar Olá painel tooview Olá saída de topologia hello e gerar dados toostore no Hub de eventos.

> [!IMPORTANT]
> componente do HBase Olá dessa topologia não está ativo quando testar localmente. Olá API Java para o cluster do HBase Olá não pode ser acessado de fora Olá rede Virtual do Azure que contém Olá clusters.

### <a name="start-hello-web-application"></a>Iniciar o aplicativo da web hello

1. Abra um prompt de comando e altere os diretórios muito`hdinsight-eventhub-example/dashboard`. Use Olá dependências de saudação do comando tooinstall exigidas pelo aplicativo de web Olá a seguir:
   
    ```bash
    npm install
    ```

2. Use Olá aplicativo web do comando toostart hello a seguir:
   
    ```bash
    node server.js
    ```
   
    Você verá um toohello semelhante mensagem texto a seguir:
   
        Server listening at port 3000

3. Abra um navegador da web e digite `http://localhost:3000/` como endereço de saudação. Um toohello semelhante página imagem a seguir é exibida:
   
    ![Painel da Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Deixe esse prompt de comando aberto. Depois de testes, use servidor de web de saudação de toostop Ctrl-C.

### <a name="generate-data"></a>Gerar dados

> [!NOTE]
> Hello etapas desta seção usam Node. js para que eles podem ser usados em qualquer plataforma. Para obter outros exemplos de idioma, consulte Olá `SendEvents` directory.

1. Abra um novo prompt, shell ou terminal e altere os diretórios muito`hdinsight-eventhub-example/SendEvents/nodejs`. dependências de saudação tooinstall exigidas pelo aplicativo hello, use Olá comando a seguir:

    ```bash
    npm install
    ```

2. Olá abrir `app.js` do arquivo em um editor de texto e adicione Olá informações de Hub de eventos obtidos anteriormente:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > Este exemplo supõe que você usou o `sensordata` como nome de saudação do seu Hub de eventos. E se `devices` como nome de saudação da política de saudação que tem um `Send` de declaração.

3. Use Olá comando tooinsert novas entradas no Hub de eventos a seguir:
   
    ```bash
    node app.js
    ```
   
    Você verá várias linhas de saída que contêm dados de saudação enviada tooEvent Hub:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Criar e iniciar a topologia de saudação

1. Abra um novo prompt de comando e altere os diretórios muito`hdinsight-eventhub-example/TemperatureMonitor`. toobuild e pacote hello topologia, use Olá comando a seguir: 

    ```bash
    mvn clean package
    ```

2. toostart Olá topologia em modo local, use Olá comando a seguir:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`topologia de saudação inicia no modo local.
    * `--filter`Olá usa `dev.properties` toopopulate parâmetros na definição de topologia de saudação do arquivo.
    * `resources/no-hbase.yaml`Olá usa `no-hbase.yaml` definição de topologia.
 
   Depois de iniciado, topologia Olá lê as entradas do Hub de eventos e as envia toohello painel em execução no seu computador local. Você deverá ver linhas no painel da web hello, semelhante toohello imagem a seguir:
   
    ![Painel com dados](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Enquanto estiver executando o painel hello, use Olá `node app.js` tooEvent de dados novo toosend Hubs as etapas de comando de saudação anterior. Porque os valores de temperatura Olá gerados aleatoriamente, gráfico de saudação deve atualizar tooshow grandes alterações de temperatura.
   
   > [!NOTE]
   > Você deve estar no hello **hdinsight-eventhub-exemplo/SendEvents/Nodejs** diretório ao usar Olá `node app.js` comando.

3. Depois de verificar atualizações de painel hello, parada Olá topologia usando Ctrl + C. Você também pode usar servidor web local do Ctrl + C toostop hello.

## <a name="create-a-storm-and-hbase-cluster"></a>Criar um cluster Storm e HBase

Olá as etapas desta seção usam um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate um cluster de rede Virtual do Azure e uma tempestade e HBase na rede virtual hello. modelo de saudação também cria um aplicativo Web do Azure e implanta uma cópia do painel Olá nele.

> [!NOTE]
> Uma rede virtual é usada para que a topologia de saudação em execução no cluster de profusão de saudação pode se comunicar diretamente com cluster do HBase hello usando Olá HBase Java API.

modelo do Gerenciador de recursos de saudação usado neste documento está localizado em um contêiner de blob público em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Clique em Olá botão toosign em tooAzure e modelo do Gerenciador de recursos de saudação abrir no portal do Azure de saudação a seguir.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. De saudação **implantação personalizada** seção, digite Olá valores a seguir:
   
    ![Parâmetros do HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Nome do Cluster base**: esse valor é usado como nome de base Olá para clusters de saudação Storm e HBase. Por exemplo, a inserção de **abc** cria um cluster Storm chamado **storm-abc** e um cluster HBase chamado **hbase-abc**.
   * **Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para clusters de saudação Storm e HBase.
   * **Senha de logon de cluster**: senha do usuário administrador Olá para clusters de saudação Storm e HBase.
   * **Nome de usuário SSH**: Olá toocreate de usuário SSH para clusters de saudação Storm e HBase.
   * **Senha SSH**: senha Olá para usuário SSH Olá Olá Storm e HBase clusters.
   * **Local**: região Olá Olá clusters são criados no.
     
     Clique em **Okey** toosave parâmetros de saudação.

3. Saudação de uso **Noções básicas de** seção toocreate um grupo de recursos ou selecione um existente.
4. Em Olá **local do grupo de recursos** menu suspenso, selecione Olá mesmo local que você selecionou para Olá **local** parâmetro hello **configurações** seção.
5. Ler Olá termos e condições e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.
6. Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**. Demora cerca de 20 minutos toocreate clusters hello.

Após a criação dos recursos de hello, informações sobre o grupo de recursos de saudação são exibidas.

![Grupo de recursos para redes hello e clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Observe que os nomes de saudação de clusters de HDInsight Olá ficam **profusão de nome de base** e **nome base do hbase**, onde nome base é o nome da saudação fornecido toohello modelo. Você pode usar esses nomes em uma etapa posterior ao conectar-se toohello clusters. Também Observe que Olá nome do site de painel Olá é **nome base painel**. Esse valor é usado posteriormente neste documento.

## <a name="configure-hello-dashboard-bolt"></a>Configurar o raio do painel Olá

Painel de toohello de dados toosend implantado como um aplicativo web, você deve modificar Olá a seguinte linha no hello `dev.properties`arquivo:

```yaml
dashboard.uri: http://localhost:3000
```

Alterar `http://localhost:3000` muito`http://BASENAME-dashboard.azurewebsites.net` e salve o arquivo hello. Substituir **nome base** com o nome de base Olá fornecido na etapa anterior hello. Você também pode usar o grupo de recursos de saudação criado anteriormente tooselect Olá painel e exibição Olá URL.

## <a name="create-hello-hbase-table"></a>Criar a tabela do HBase Olá

toostore dados em HBase, podemos deve primeiro criar uma tabela. Pré-criar recursos Storm precisa toowrite para, como tentar recursos toocreate, de dentro de uma topologia Storm podem resultar em várias instâncias tentar toocreate Olá mesmo recurso. Criar recursos de Olá fora Olá topologia e usar profusão de leitura/gravação e análise.

1. Use o cluster do SSH tooconnect toohello HBase usando o usuário SSH hello e a senha fornecidos toohello modelo durante a criação do cluster. Por exemplo, se estiver conectando usando Olá `ssh` de comando, você usaria Olá sintaxe a seguir:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Substituir `sshuser` com nome de usuário SSH Olá fornecida ao criar o cluster de saudação. Substituir `clustername` com o nome do cluster HBase hello.

2. Da sessão SSH hello, inicie o shell do HBase hello.
   
    ```bash
    hbase shell
    ```
   
    Quando o shell Olá tiver sido carregado, você ver um `hbase(main):001:0>` prompt.

3. Em Olá shell do HBase, digite Olá comando toocreate dados do sensor de saudação de toostore uma tabela a seguir:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Verifique se que essa tabela Olá foi criada usando o comando a seguir de saudação:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Isso retorna informações o toohello semelhante exemplo a seguir, indicando que há 0 linhas na tabela de saudação.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Digite `exit` tooexit Olá shell do HBase:

## <a name="configure-hello-hbase-bolt"></a>Configurar o raio do HBase Olá

toowrite tooHBase do cluster de Storm hello, você deve fornecer raio do HBase Olá com detalhes de configuração de saudação do cluster HBase.

1. Use uma saudação quorum do exemplos tooretrieve Olá Zookeeper para seu cluster HBase a seguir:

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Substituir `your_HDInsight_cluster_name` com nome de saudação do cluster HDInsight. Para obter mais informações sobre como instalar Olá `jq` utilitário, consulte [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > Quando solicitado, insira a senha de saudação para logon de admin do HDInsight hello.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Substitua ' your_HDInsight_cluster_name com nome de saudação do cluster HDInsight. Quando solicitado, insira a senha de saudação para logon de admin do HDInsight hello.
    >
    > Este exemplo exige o Azure PowerShell. Para saber mais sobre como usar o Azure PowerShell, confira [Introdução ao Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)

    informações de Hello retornadas por esses exemplos são semelhante toohello texto a seguir:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Essas informações são usadas pelo toocommunicate Storm com cluster HBase de saudação.

2. Modificar Olá `dev.properties` e adicione Olá Zookeeper quorum informações toohello linha a seguir:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Criar o pacote e implantar Olá solução tooHDInsight

Em seu ambiente de desenvolvimento, use Olá cluster de storm etapas toodeploy Olá Storm topologia toohello a seguir.

1. De saudação `TemperatureMonitor` diretório, use a seguir Olá comando tooperform uma nova compilação e crie um pacote JAR do seu projeto:
   
        mvn clean package
   
    Este comando cria um arquivo chamado `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `diretório de destino do projeto.

2. Saudação do uso scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` e `dev.properties` cluster de Storm tooyour arquivos. Olá seguinte exemplo, substitua `sshuser` com você forneceu ao criar cluster hello, de usuário SSH hello e `clustername` com nome de saudação do cluster Storm. Quando solicitado, insira a senha Olá para o usuário SSH hello.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Pode levar vários minutos arquivos de saudação tooupload.

    Para obter mais informações sobre como usar o hello `scp` e `ssh` comandos com o HDInsight, consulte [usar SSH com HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Depois que o arquivo hello foi carregado, conecte o cluster de profusão de toohello usando o SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Substituir `sshuser` com nome de usuário SSH hello. Substituir `clustername` com o nome do cluster Storm hello.

4. toostart Olá topologia, use Olá comandos da sessão SSH Olá a seguir:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`envia Olá topologia toohello serviço Nimbus, que distribui a ele toohello nós de supervisor em cluster hello.
    * `--filter`Olá usa `dev.properties` toopopulate parâmetros na definição de topologia de saudação do arquivo.
    * `-R /with-hbase.yaml`Olá usa `with-hbase.yaml` incluída no pacote de saudação de topologia.

5. Depois de topologia Olá foi iniciado, abrir um site de toohello do navegador publicado no Azure, em seguida, use Olá `node app.js` comando toosend dados tooEvent Hub. Você deve ver informações de Olá Olá web painel atualização toodisplay.
   
    ![painel Transações da Web](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>Exibir dados do HBase

Use Olá tooHBase de tooconnect as etapas a seguir e verifique se que dados saudação foi gravados toohello tabela:

1. Use SSH tooconnect toohello HBase cluster.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Substituir `sshuser` com nome de usuário SSH hello. Substituir `clustername` com o nome do cluster HBase hello.

2. Da sessão SSH hello, inicie o shell do HBase hello.
   
    ```bash
    hbase shell
    ```
   
    Quando o shell Olá tiver sido carregado, você ver um `hbase(main):001:0>` prompt.

3. Exibir as linhas da tabela de saudação:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Esse comando retorna informações o toohello semelhante texto a seguir, indicando que há dados na tabela de saudação.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Operação de varredura retorna um máximo de 10 linhas da tabela de saudação.

## <a name="delete-your-clusters"></a>Excluir os clusters

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

clusters de saudação toodelete, armazenamento e aplicativo web ao mesmo tempo, exclua o grupo de recursos de saudação que os contém.

## <a name="next-steps"></a>Próximas etapas

Para obter mais exemplos de topologias Storm com o HDInsight, consulte [Topologias de exemplo para o Storm no HDInsight](hdinsight-storm-example-topology.md)

Para obter mais informações sobre o Apache Storm, consulte Olá [Apache Storm](https://storm.incubator.apache.org/) site.

Para obter mais informações sobre HBase em HDInsight, consulte Olá [HBase visão geral de HDInsight](hdinsight-hbase-overview.md).

Para obter mais informações sobre Socket.io, consulte Olá [socket.io](http://socket.io/) site.

Para saber mais sobre D3.js, confira [D3.js - Documentos controlados por dados](http://d3js.org/)

Para saber mais sobre como criar topologias em Java, confira [Desenvolver topologias Java para Apache Storm no HDInsight](hdinsight-storm-develop-java-topology.md).

Para saber mais sobre como se conectar ao cluster Storm, confira [Desenvolver topologias C# para Apache Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
