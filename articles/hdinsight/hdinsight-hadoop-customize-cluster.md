---
title: "aaaCustomize Clusters HDInsight usando script de ações - Azure | Microsoft Docs"
description: "Saiba como toocustomize HDInsight clusters usando a ação de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>Personalizar clusters HDInsight baseados em Windows usando a Ação de Script
**Ação de script** pode ser usado tooinvoke [scripts personalizados](hdinsight-hadoop-script-actions.md) durante processo de criação de cluster Olá para instalar software adicional em um cluster.

informações Olá neste artigo são específico com base em tooWindows clusters de HDInsight. Para cluster baseados em Linux, confira [Personalizar clusters do HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Clusters HDInsight podem ser personalizados em uma variedade de outras maneiras, como incluir contas de armazenamento do Azure adicionais, alterar Olá Hadoop arquivos de configuração (Core-site.XML, hive-site.XML, etc.) ou adicionando compartilhado bibliotecas (por exemplo, Hive, Oozie) em locais comuns em cluster hello. Essas personalizações podem ser feitas por meio do PowerShell do Azure, hello Azure HDInsight .NET SDK, ou Olá portal do Azure. Para obter mais informações, veja [Criar clusters Hadoop no HDInsight][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Ação de script no processo de criação de cluster Olá
Ação de script é usada apenas enquanto um cluster está no processo de saudação do que está sendo criado. Olá seguinte diagrama ilustra quando a ação de Script é executada durante o processo de criação de saudação:

![Personalização do cluster HDInsight e estágios durante a criação de cluster][img-hdi-cluster-states]

Quando estiver executando o script hello, cluster Olá insere Olá **ClusterCustomization** estágio. Neste estágio, script hello é executado na conta de administrador de sistema hello, paralelamente em todas as Olá especificado nós no cluster hello e fornece privilégios totais de administrador em nós de saudação.

> [!NOTE]
> Porque você tem privilégios de administrador em nós de cluster Olá durante o **ClusterCustomization** estágio, você pode usar operações de tooperform script hello como parar e iniciar serviços, incluindo serviços relacionados ao Hadoop. Portanto, como parte do script hello, você deve garantir que os serviços do Ambari hello e outros serviços relacionados ao Hadoop estão funcionando antes que o script hello terminar a execução. Esses serviços são necessários toosuccessfully verificar integridade hello e estado do cluster Olá enquanto ele está sendo criado. Se você alterar qualquer configuração no cluster que afeta a esses serviços, você deve usar funções auxiliares Olá fornecidos. Para obter mais informações sobre funções auxiliares, confira [Desenvolver scripts de Ação de Script para o HDInsight][hdinsight-write-script].
>
>

saída de Hello e logs de erros de saudação para script hello são armazenados na conta de armazenamento padrão de saudação especificado para o cluster de saudação. Olá logs são armazenados em uma tabela com o nome da saudação **u < \cluster-name-fragment >< \time-stamp > setuplog**. Esses são os logs de agregação de script hello executado em todos os nós de saudação (nó principal e nós de trabalho) no cluster hello.

Cada cluster pode aceitar várias ações de script que são invocadas em ordem de saudação na qual elas são especificadas. Um script pode ser executado no nó principal hello, nós de trabalho hello ou ambos.

HDInsight fornece Olá de tooinstall scripts vários componentes a seguir em clusters de HDInsight:

| Nome | Script |
| --- | --- |
| **Instalar Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Consulte [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]. |
| **Instalar R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Consulte [Instalar e usar o R em clusters HDInsight][hdinsight-install-r]. |
| **Instalar Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Consulte [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Instalar o Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Consulte [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md). |
| **Pré-carregar bibliotecas Hive** |https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1. Consulte [Adicionar bibliotecas do Hive em clusters do HDInsight](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Scripts de chamada usando Olá portal do Azure
**De saudação portal do Azure**

1. Comece criando um cluster como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
2. Em configuração opcional, para Olá **ações de Script** folha, clique em **Adicionar ação de script** tooprovide detalhes sobre a ação de script hello, conforme mostrado abaixo:

    ![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize de ação de Script de Use um cluster")

    <table border='1'>
        <tr><th>Propriedade</th><th>Valor</th></tr>
        <tr><td>Nome</td>
            <td>Especifique um nome para a ação de script hello.</td></tr>
        <tr><td>URI do script</td>
            <td>Especifique Olá URI toohello script que é invocado toocustomize Olá cluster. s</td></tr>
        <tr><td>Cabeçalho/Trabalho</td>
            <td>Especificar nós de saudação (**Head** ou **trabalho**) no qual personalização Olá script é executado.</b>.
        <tr><td>parâmetros</td>
            <td>Especifica parâmetros de hello, se exigido pelo script hello.</td></tr>
    </table>

    Pressione ENTER tooadd mais de um script ação tooinstall vários componentes no cluster hello.
3. Clique em **selecione** toosave Olá configuração da ação de script e continuar com a criação do cluster.

## <a name="call-scripts-using-azure-powershell"></a>Chamar scripts usando o Azure PowerShell
Esse script de PowerShell a seguir demonstra como tooinstall Spark no Windows com base em cluster HDInsight.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall outros softwares, você precisará de arquivo de script hello tooreplace no script hello:

Quando solicitado, insira as credenciais de saudação para cluster hello. Pode levar vários minutos antes de saudação cluster é criado.

## <a name="call-scripts-using-net-sdk"></a>Scripts de chamada usando o SDK do .NET
Olá exemplo a seguir demonstra como tooinstall Spark no Windows com base em cluster HDInsight. tooinstall outros softwares, você precisará de arquivo de script hello tooreplace no código de saudação.

**toocreate um cluster HDInsight com Spark**

1. No Visual Studio, crie um aplicativo de console C#.
2. Olá Nuget Package Manager Console, execute Olá comando a seguir.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Saudação de uso usando as instruções no arquivo Program.cs de saudação a seguir:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Coloque o código de saudação na classe Olá com os seguintes hello:

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. Pressione **F5** aplicativo hello de toorun.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Suporte para software livre utilizado em clusters do HDInsight
saudação de serviço do Microsoft Azure HDInsight é uma plataforma flexível que permite que aplicativos de dados grandes de toobuild na nuvem hello usando um ecossistema de tecnologias de código-fonte aberto formado em torno do Hadoop. Microsoft Azure fornece um nível geral de suporte para tecnologias do código-fonte aberto, conforme discutido em Olá **escopo suporte** seção Olá <a href="http://azure.microsoft.com/support/faq/" target="_blank">site de perguntas Frequentes de suporte do Azure</a>. Olá serviço HDInsight fornece um nível adicional de suporte para alguns dos componentes do hello, conforme descrito abaixo.

Há dois tipos de componentes de código-fonte aberto que estão disponíveis no hello serviço HDInsight:

* **Componentes internos** -esses componentes são pré-instaladas em clusters de HDInsight e fornecem funcionalidade principal do cluster hello. Por exemplo, o ResourceManager YARN, linguagem de consulta de Hive hello (HiveQL) e biblioteca de Mahout Olá pertencem toothis categoria. Uma lista completa dos componentes do cluster está disponível em [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?](hdinsight-component-versioning.md) </a>.
* **Componentes personalizados** -você, como um usuário de cluster hello, instalar ou usar em sua carga de trabalho qualquer componente criado por você ou disponível na comunidade de saudação.

Componentes internos são totalmente suportados e ajudarão tooisolate e resolver problemas relacionados toothese componentes Microsoft Support.

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados e ajudarão tooisolate e resolver problemas relacionados toothese componentes Microsoft Support.
>
> Componentes personalizados recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação. Isso pode resultar em resolver o problema de saudação ou solicitando que tooengage de canais disponíveis para Olá abrir tecnologias de origem onde profundo conhecimento para que a tecnologia é encontrado. Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). E mais, os projetos Apache têm sites de projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).
>
>

Olá serviço HDInsight fornece várias maneiras de componentes personalizados toouse. Independentemente de como um componente for usado ou instalado no cluster hello, hello mesmo nível de suporte se aplica. Abaixo está uma lista das maneiras mais comuns de saudação que componentes personalizados podem ser usados em clusters de HDInsight:

1. Envio de trabalho - Hadoop ou outros tipos de trabalhos em execução ou usam componentes personalizados pode ser enviado toohello cluster.
2. Personalização de cluster - durante a criação do cluster, você pode especificar configurações adicionais e componentes personalizados que serão instalados em nós de cluster de saudação.
3. Exemplos - para os componentes personalizados, Microsoft e outros podem fornecer exemplos de como esses componentes podem ser usados em clusters de HDInsight hello. Esses exemplos são fornecidos sem suporte.

## <a name="develop-script-action-scripts"></a>Desenvolver scripts de Ação de script
Confira [Desenvolver scripts da Ação de Script para o HDInsight][hdinsight-write-script].

## <a name="see-also"></a>Consulte também
* [Criar clusters de Hadoop em HDInsight] [ hdinsight-provision-cluster] fornece instruções sobre como toocreate uma HDInsight cluster usando outras opções personalizadas.
* [Desenvolver scripts de Ação de Script para o HDInsight][hdinsight-write-script]
* [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]
* [Instalar e usar R em clusters do HDInsight][hdinsight-install-r]
* [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md).
* [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Estágios durante a criação de cluster"
