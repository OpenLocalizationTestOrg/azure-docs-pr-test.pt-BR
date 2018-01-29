---
title: "Gerenciar clusters Hadoop no HDInsight com o SDK do .NET – Azure | Microsoft Docs"
description: Saiba como realizar tarefas administrativas para os clusters Hadoop no HDInsight usando o SDK do .NET do HDInsight.
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: jgao
ms.openlocfilehash: d881d47e26460d3fff89c01245bba4c608dc8b08
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Gerenciar clusters Hadoop no HDInsight usando o SDK do .NET
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Saiba como gerenciar clusters HDInsight usando o [SDK do .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).

**Pré-requisitos**

Antes de começar este artigo, você deve ter o seguinte:

* **Uma assinatura do Azure**. Consulte [Obter a avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-to-azure-hdinsight"></a>Conectar-se ao Azure HDInsight

Você precisa dos seguintes pacotes NuGet:

```
Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
Install-Package Microsoft.Azure.Management.ResourceManager -Pre
Install-Package Microsoft.Azure.Management.HDInsight
```

O exemplo de código a seguir mostra como se conectar ao Azure antes que você possa administrar clusters do HDInsight em sua assinatura do Azure.

```csharp
using System;
using Microsoft.Azure;
using Microsoft.Azure.Management.HDInsight;
using Microsoft.Azure.Management.HDInsight.Models;
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;

namespace HDInsightManagement
{
    class Program
    {
        private static HDInsightManagementClient _hdiManagementClient;
        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId; 
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

        static void Main(string[] args)
        {
            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            // insert code here

            System.Console.WriteLine("Press ENTER to continue");
            System.Console.ReadLine();
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
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
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
    }
}
```

Você deverá ver um aviso ao executar este programa.  Se não desejar ver o aviso, confira [Criar aplicativos .NET do HDInsight com autenticação não interativa](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Criar clusters
Veja [Criar clusters baseados em Linux no HDInsight usando o SDK do .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Listar clusters
O trecho de código a seguir lista os clusters e algumas propriedades:

```csharp
var results = _hdiManagementClient.Clusters.List();
foreach (var name in results.Clusters) {
    Console.WriteLine("Cluster Name: " + name.Name);
    Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
    Console.WriteLine("\t Cluster location: " + name.Location);
    Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
}
```

## <a name="delete-clusters"></a>Excluir clusters
Use o seguinte trecho de código para excluir um cluster de forma síncrona ou assíncrona: 

```csharp
_hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
_hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");
```

## <a name="scale-clusters"></a>Dimensionar clusters
O recurso de dimensionamento de clusters permite que você altere o número de nós de trabalhador usados por um cluster em execução no Azure HDInsight sem precisar recriar o cluster.

> [!NOTE]
> Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis. Se não tiver certeza quanto à versão de seu cluster, você poderá verificar a página Propriedades.  Consulte [Listar e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

O impacto da alteração do número de nós de dados em cada tipo de cluster com suporte do HDInsight:

* O Hadoop
  
    Você pode aumentar continuamente o número de nós de trabalhador em um cluster Hadoop em execução sem afetar os trabalhos pendentes ou em execução. Novos trabalhos também podem ser enviados enquanto a operação está em andamento. Falhas em uma operação de dimensionamento são normalmente manipuladas para que o cluster sempre seja deixado em um estado funcional.
  
    Quando um cluster Hadoop é reduzido verticalmente pela diminuição do número de nós de dados, alguns dos serviços no cluster são reiniciados. Isso faz com que todos os trabalhos em execução e pendentes falhem após a conclusão da operação de dimensionamento. Você pode, no entanto, reenviar os trabalhos quando a operação for concluída.
* HBase
  
    Você pode adicionar ou remover diretamente nós do cluster HBase enquanto ele é executado. Servidores Regionais são equilibrados automaticamente em alguns minutos após o término da operação de dimensionamento. No entanto, você pode equilibrar manualmente os servidores regionais fazendo logon no nó de cabeçalho do cluster e executando os seguintes comandos em uma janela de prompt de comando:
  
    ```bash
    >pushd %HBASE_HOME%\bin
    >hbase shell
    >balancer
    ```
* Storm
  
    Você pode adicionar ou remover nós de dados continuamente para seu cluster Strom enquanto ele é executado. Mas, após a conclusão bem-sucedida da operação de dimensionamento, você precisará redistribuir a topologia.
  
    A redistribuição pode ser feita de duas maneiras:
  
  * Interface da Web Storm
  * Ferramenta CLI (interface de linha de comando)
    
    Consulte a [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.
    
    A IU da Web do Storm está disponível no cluster HDInsight:
    
    ![Redistribuir escala do Storm do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Aqui está um exemplo de como usar o comando CLI para reequilibrar a topologia do Storm:
    
    ```cli
    ## Reconfigure the topology "mytopology" to use 5 worker processes,
    ## the spout "blue-spout" to use 3 executors, and
    ## the bolt "yellow-bolt" to use 10 executors
    $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10
    ```

O trecho de código a seguir mostra como redimensionar um cluster de forma síncrona ou assíncrona:

```csharp
_hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
_hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   
```

## <a name="grantrevoke-access"></a>Conceder/revogar acesso
Os clusters HDInsight têm os seguintes serviços Web HTTP (todos esses serviços têm pontos de extremidade RESTful):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Por padrão, esses serviços são concedidos para acesso. Você pode revogar/conceder o acesso. Para revogar:

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = false,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

Para conceder:

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = enable,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

> [!NOTE]
> Ao conceder/revogar o acesso, você redefinirá o nome de usuário de cluster e a senha.
> 
> 

Isso também pode ser feito por meio do Portal. Consulte [Administrar o HDInsight usando o Portal do Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Atualizar credenciais de usuário HTTP
É o mesmo procedimento para [acessar Conceder/Revogar HTTP](#grant/revoke-access). Se o cluster recebeu o acesso HTTP, você deverá revogá-lo.  E, em seguida, conceder acesso com novas credenciais de usuário HTTP.

## <a name="find-the-default-storage-account"></a>Encontrar a conta de armazenamento padrão
O trecho de código a seguir demonstra como obter o nome da conta de armazenamento padrão e a chave da conta de armazenamento padrão de um cluster.

```csharp
var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
foreach (var key in results.Configuration.Keys)
{
    Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
}
```

## <a name="submit-jobs"></a>Enviar trabalhos
**Enviar trabalhos MapReduce**

Veja [Executar amostras de MapReduce do Hadoop no HDInsight](hadoop/apache-hadoop-run-samples-linux.md).

**Enviar trabalhos Hive** 

Veja [Executar consultas do Hive usando o SDK do .NET](hadoop/apache-hadoop-use-hive-dotnet-sdk.md).

**Enviar trabalhos Pig**

Veja [Executar trabalhos do Pig usando o SDK do .NET](hadoop/apache-hadoop-use-pig-dotnet-sdk.md).

**Para enviar trabalhos de Sqoop**

Consulte [Usar o Sqoop com o HDInsight](hadoop/apache-hadoop-use-sqoop-dotnet-sdk.md).

**Para enviar trabalhos de Oozie**

Consulte [Usar o Oozie com Hadoop para definir e executar um fluxo de trabalho no HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-to-azure-blob-storage"></a>Carregar dados no armazenamento de Blob do Azure
Veja [Carregar dados no HDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Veja também
* [Documentação de referência do SDK do .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Administrar o HDInsight usando o Portal do Azure][hdinsight-admin-portal]
* [Administrar o HDInsight usando uma interface de linha de comando][hdinsight-admin-cli]
* [Criar clusters HDInsight][hdinsight-provision]
* [Carregar dados no HDInsight][hdinsight-upload-data]
* [Introdução ao Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]:hadoop/submit-apache-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]:hadoop/hdinsight-use-hive.md
[hdinsight-use-mapreduce]:hadoop/hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


