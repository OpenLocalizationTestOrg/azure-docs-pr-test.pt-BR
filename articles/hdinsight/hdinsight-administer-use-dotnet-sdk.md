---
title: clusters de aaaManage Hadoop no HDInsight .NET SDK - Azure | Microsoft Docs
description: "Saiba como tarefas tooperform administrativa para Olá clusters Hadoop em HDInsight usando o HDInsight .NET SDK."
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
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Gerenciar clusters Hadoop no HDInsight usando o SDK do .NET
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Saiba como toomanage HDInsight clusters usando [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Pré-requisitos**

Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>Conecte-se tooAzure HDInsight

Você precisa Olá pacotes do Nuget a seguir:

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Olá exemplo de código a seguir mostra como clusters de tooconnect tooAzure para que você possa administrar HDInsight em sua assinatura do Azure.

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
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
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
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

Você deverá ver um aviso ao executar este programa.  Se você não quiser prompt de saudação toosee, consulte [criar aplicativos .NET HDInsight de autenticação não interativo](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Criar clusters
Consulte [baseados em Linux criar clusters HDInsight usando Olá SDK .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Listar clusters
Olá trecho de código a seguir mostra os clusters e algumas propriedades:

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Excluir clusters
Use Olá seguindo o trecho de código toodelete um cluster de forma síncrona ou assíncrona: 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>Dimensionar clusters
dimensionando o recurso de cluster de saudação permite toochange número de saudação de nós de trabalho usado por um cluster que está em execução no Azure HDInsight sem ter que toore-criar o cluster de saudação.

> [!NOTE]
> Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis. Se você não tiver certeza da versão de saudação do cluster, você pode verificar a página de propriedades de saudação.  Confira [Listar e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

impacto de saudação do alterando o número de saudação de nós de dados para cada tipo de cluster HDInsight com suporte:

* O Hadoop
  
    Você perfeitamente pode aumentar o número de saudação de nós de trabalho em um cluster de Hadoop que está sendo executado sem afetar todos os trabalhos pendentes ou em execução. Novos trabalhos também podem ser enviados enquanto Olá operação está em andamento. Falhas em uma operação de dimensionamento são controladas normalmente para que hello cluster seja sempre deixado em um estado funcional.
  
    Quando um cluster Hadoop é reduzido, reduzindo o número de saudação de nós de dados, alguns dos serviços de saudação em cluster Olá são reiniciados. Isso faz com que todas as e pendentes toofail trabalhos na conclusão de saudação do hello a operação de dimensionamento. No entanto, você pode, reenviar trabalhos Olá após a conclusão da operação de saudação.
* HBase
  
    Sem problemas, você pode adicionar ou remover o cluster de HBase tooyour nós enquanto ele está em execução. Servidores regionais são balanceados automaticamente dentro de alguns minutos após o término da operação de dimensionamento de saudação. No entanto, você pode equilibrar manualmente servidores regionais Olá fazendo logon no nó principal de saudação do cluster e em execução hello comandos a seguir em uma janela de prompt de comando:
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    Sem problemas, você pode adicionar ou remover o cluster de profusão de tooyour de nós de dados enquanto ele está em execução. Mas, após a conclusão bem-sucedida da operação de dimensionamento de saudação, você precisará de topologia de saudação toorebalance.
  
    A redistribuição pode ser feita de duas maneiras:
  
  * Interface da Web Storm
  * Ferramenta CLI (interface de linha de comando)
    
    Consulte toohello [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.
    
    Interface da web Hello Storm está disponível no cluster do HDInsight hello:
    
    ![Redistribuir escala do Storm do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Aqui está um exemplo como toouse Olá CLI comando topologia de profusão de saudação toorebalance:
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Olá seguindo o trecho de código mostra como tooresize um cluster de forma síncrona ou assíncrona:

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>Conceder/revogar acesso
Clusters HDInsight tem Olá serviços da web HTTP (todos esses serviços têm pontos de extremidade RESTful) a seguir:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Por padrão, esses serviços são concedidos para acesso. Você pode revogar/conceder acesso de saudação. toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Revogando concedendo/acesso hello, redefinirá senha e nome de usuário de cluster hello.
> 
> 

Isso também pode ser feito por meio do Portal de saudação. Consulte [HDInsight administrar usando Olá portal do Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Atualizar credenciais de usuário HTTP
É Olá mesmo procedimento como [acesso Grant/revoke HTTP](#grant/revoke-access). Se foi concedida cluster Olá Olá acesso HTTP, você deve primeiro revogá-lo.  E, em seguida, conceder acesso de saudação com novas credenciais de usuário HTTP.

## <a name="find-hello-default-storage-account"></a>Localizar a conta de armazenamento saudação padrão
saudação de trecho de código a seguir demonstra como tooget Olá nome de conta de armazenamento padrão e Olá chave de conta de armazenamento padrão para um cluster.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>Enviar trabalhos
**trabalhos de MapReduce toosubmit**

Veja [Executar amostras de MapReduce do Hadoop no HDInsight](hdinsight-hadoop-run-samples-linux.md).

**trabalhos de Hive toosubmit** 

Veja [Executar consultas do Hive usando o SDK do .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).

**trabalhos de Pig toosubmit**

Veja [Executar trabalhos do Pig usando o SDK do .NET](hdinsight-hadoop-use-pig-dotnet-sdk.md).

**trabalhos de Sqoop toosubmit**

Consulte [Usar o Sqoop com o HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**toosubmit Oozie trabalhos**

Consulte [Oozie de uso com toodefine Hadoop e executar um fluxo de trabalho no HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Carregue o armazenamento de Blob de tooAzure de dados
Consulte [carregar dados tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Consulte também
* [Documentação de referência do SDK do .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Administrar HDInsight usando Olá portal do Azure][hdinsight-admin-portal]
* [Administrar o HDInsight usando uma interface de linha de comando][hdinsight-admin-cli]
* [Criar clusters HDInsight][hdinsight-provision]
* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Introdução ao Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


