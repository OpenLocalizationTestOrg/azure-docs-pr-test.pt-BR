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
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="a4da7-103">Gerenciar clusters Hadoop no HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="a4da7-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="a4da7-104">Saiba como gerenciar clusters HDInsight usando o [SDK do .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4da7-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="a4da7-105">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="a4da7-105">**Prerequisites**</span></span>

<span data-ttu-id="a4da7-106">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a4da7-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="a4da7-107">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a4da7-107">**An Azure subscription**.</span></span> <span data-ttu-id="a4da7-108">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a4da7-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="a4da7-109">Conectar-se ao Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4da7-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="a4da7-110">Você precisa dos seguintes pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="a4da7-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="a4da7-111">O exemplo de código a seguir mostra como se conectar ao Azure antes que você possa administrar clusters do HDInsight em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4da7-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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

<span data-ttu-id="a4da7-112">Você deverá ver um aviso ao executar este programa.</span><span class="sxs-lookup"><span data-stu-id="a4da7-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="a4da7-113">Se não desejar ver o aviso, confira [Criar aplicativos .NET do HDInsight com autenticação não interativa](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="a4da7-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="a4da7-114">Criar clusters</span><span class="sxs-lookup"><span data-stu-id="a4da7-114">Create clusters</span></span>
<span data-ttu-id="a4da7-115">Veja [Criar clusters baseados em Linux no HDInsight usando o SDK do .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="a4da7-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="a4da7-116">Listar clusters</span><span class="sxs-lookup"><span data-stu-id="a4da7-116">List clusters</span></span>
<span data-ttu-id="a4da7-117">O trecho de código a seguir lista os clusters e algumas propriedades:</span><span class="sxs-lookup"><span data-stu-id="a4da7-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="a4da7-118">Excluir clusters</span><span class="sxs-lookup"><span data-stu-id="a4da7-118">Delete clusters</span></span>
<span data-ttu-id="a4da7-119">Use o seguinte trecho de código para excluir um cluster de forma síncrona ou assíncrona:</span><span class="sxs-lookup"><span data-stu-id="a4da7-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="a4da7-120">Dimensionar clusters</span><span class="sxs-lookup"><span data-stu-id="a4da7-120">Scale clusters</span></span>
<span data-ttu-id="a4da7-121">O recurso de dimensionamento de clusters permite que você altere o número de nós de trabalhador usados por um cluster em execução no Azure HDInsight sem precisar recriar o cluster.</span><span class="sxs-lookup"><span data-stu-id="a4da7-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a4da7-122">Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="a4da7-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="a4da7-123">Se não tiver certeza quanto à versão de seu cluster, você poderá verificar a página Propriedades.</span><span class="sxs-lookup"><span data-stu-id="a4da7-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="a4da7-124">Confira [Listar e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="a4da7-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="a4da7-125">O impacto da alteração do número de nós de dados em cada tipo de cluster com suporte do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4da7-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="a4da7-126">O Hadoop</span><span class="sxs-lookup"><span data-stu-id="a4da7-126">Hadoop</span></span>
  
    <span data-ttu-id="a4da7-127">Você pode aumentar continuamente o número de nós de trabalhador em um cluster Hadoop em execução sem afetar os trabalhos pendentes ou em execução.</span><span class="sxs-lookup"><span data-stu-id="a4da7-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="a4da7-128">Novos trabalhos também podem ser enviados enquanto a operação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="a4da7-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="a4da7-129">Falhas em uma operação de dimensionamento são normalmente manipuladas para que o cluster sempre seja deixado em um estado funcional.</span><span class="sxs-lookup"><span data-stu-id="a4da7-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="a4da7-130">Quando um cluster Hadoop é reduzido verticalmente pela diminuição do número de nós de dados, alguns dos serviços no cluster são reiniciados.</span><span class="sxs-lookup"><span data-stu-id="a4da7-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="a4da7-131">Isso faz com que todos os trabalhos em execução e pendentes falhem após a conclusão da operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a4da7-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="a4da7-132">Você pode, no entanto, reenviar os trabalhos quando a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="a4da7-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="a4da7-133">HBase</span><span class="sxs-lookup"><span data-stu-id="a4da7-133">HBase</span></span>
  
    <span data-ttu-id="a4da7-134">Você pode adicionar ou remover diretamente nós do cluster HBase enquanto ele é executado.</span><span class="sxs-lookup"><span data-stu-id="a4da7-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="a4da7-135">Servidores Regionais são equilibrados automaticamente em alguns minutos após o término da operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a4da7-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="a4da7-136">No entanto, você pode equilibrar manualmente os servidores regionais fazendo logon no nó de cabeçalho do cluster e executando os seguintes comandos em uma janela de prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="a4da7-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="a4da7-137">Storm</span><span class="sxs-lookup"><span data-stu-id="a4da7-137">Storm</span></span>
  
    <span data-ttu-id="a4da7-138">Você pode adicionar ou remover nós de dados continuamente para seu cluster Strom enquanto ele é executado.</span><span class="sxs-lookup"><span data-stu-id="a4da7-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="a4da7-139">Mas, após a conclusão bem-sucedida da operação de dimensionamento, você precisará redistribuir a topologia.</span><span class="sxs-lookup"><span data-stu-id="a4da7-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="a4da7-140">A redistribuição pode ser feita de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="a4da7-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="a4da7-141">Interface da Web Storm</span><span class="sxs-lookup"><span data-stu-id="a4da7-141">Storm web UI</span></span>
  * <span data-ttu-id="a4da7-142">Ferramenta CLI (interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="a4da7-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="a4da7-143">Consulte a [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a4da7-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="a4da7-144">A IU da Web do Storm está disponível no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4da7-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![Redistribuir escala do Storm do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="a4da7-146">Aqui está um exemplo de como usar o comando CLI para reequilibrar a topologia do Storm:</span><span class="sxs-lookup"><span data-stu-id="a4da7-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="a4da7-147">O trecho de código a seguir mostra como redimensionar um cluster de forma síncrona ou assíncrona:</span><span class="sxs-lookup"><span data-stu-id="a4da7-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="a4da7-148">Conceder/revogar acesso</span><span class="sxs-lookup"><span data-stu-id="a4da7-148">Grant/revoke access</span></span>
<span data-ttu-id="a4da7-149">Os clusters HDInsight têm os seguintes serviços Web HTTP (todos esses serviços têm pontos de extremidade RESTful):</span><span class="sxs-lookup"><span data-stu-id="a4da7-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="a4da7-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="a4da7-150">ODBC</span></span>
* <span data-ttu-id="a4da7-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="a4da7-151">JDBC</span></span>
* <span data-ttu-id="a4da7-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="a4da7-152">Ambari</span></span>
* <span data-ttu-id="a4da7-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="a4da7-153">Oozie</span></span>
* <span data-ttu-id="a4da7-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="a4da7-154">Templeton</span></span>

<span data-ttu-id="a4da7-155">Por padrão, esses serviços são concedidos para acesso.</span><span class="sxs-lookup"><span data-stu-id="a4da7-155">By default, these services are granted for access.</span></span> <span data-ttu-id="a4da7-156">Você pode revogar/conceder o acesso.</span><span class="sxs-lookup"><span data-stu-id="a4da7-156">You can revoke/grant the access.</span></span> <span data-ttu-id="a4da7-157">Para revogar:</span><span class="sxs-lookup"><span data-stu-id="a4da7-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="a4da7-158">Para conceder:</span><span class="sxs-lookup"><span data-stu-id="a4da7-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="a4da7-159">Ao conceder/revogar o acesso, você redefinirá o nome de usuário de cluster e a senha.</span><span class="sxs-lookup"><span data-stu-id="a4da7-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="a4da7-160">Isso também pode ser feito por meio do Portal.</span><span class="sxs-lookup"><span data-stu-id="a4da7-160">This can also be done via the Portal.</span></span> <span data-ttu-id="a4da7-161">Consulte [Administrar o HDInsight usando o Portal do Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="a4da7-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="a4da7-162">Atualizar credenciais de usuário HTTP</span><span class="sxs-lookup"><span data-stu-id="a4da7-162">Update HTTP user credentials</span></span>
<span data-ttu-id="a4da7-163">É o mesmo procedimento para [acessar Conceder/Revogar HTTP](#grant/revoke-access). Se o cluster recebeu o acesso HTTP, você deverá revogá-lo.</span><span class="sxs-lookup"><span data-stu-id="a4da7-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="a4da7-164">E, em seguida, conceder acesso com novas credenciais de usuário HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4da7-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="a4da7-165">Encontrar a conta de armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="a4da7-165">Find the default storage account</span></span>
<span data-ttu-id="a4da7-166">O trecho de código a seguir demonstra como obter o nome da conta de armazenamento padrão e a chave da conta de armazenamento padrão de um cluster.</span><span class="sxs-lookup"><span data-stu-id="a4da7-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="a4da7-167">Enviar trabalhos</span><span class="sxs-lookup"><span data-stu-id="a4da7-167">Submit jobs</span></span>
<span data-ttu-id="a4da7-168">**Enviar trabalhos MapReduce**</span><span class="sxs-lookup"><span data-stu-id="a4da7-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="a4da7-169">Veja [Executar amostras de MapReduce do Hadoop no HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a4da7-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="a4da7-170">**Enviar trabalhos Hive**</span><span class="sxs-lookup"><span data-stu-id="a4da7-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="a4da7-171">Veja [Executar consultas do Hive usando o SDK do .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a4da7-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="a4da7-172">**Enviar trabalhos Pig**</span><span class="sxs-lookup"><span data-stu-id="a4da7-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="a4da7-173">Veja [Executar trabalhos do Pig usando o SDK do .NET](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a4da7-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="a4da7-174">**Para enviar trabalhos de Sqoop**</span><span class="sxs-lookup"><span data-stu-id="a4da7-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="a4da7-175">Consulte [Usar o Sqoop com o HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a4da7-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="a4da7-176">**Para enviar trabalhos de Oozie**</span><span class="sxs-lookup"><span data-stu-id="a4da7-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="a4da7-177">Consulte [Usar o Oozie com Hadoop para definir e executar um fluxo de trabalho no HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="a4da7-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="a4da7-178">Carregar dados no armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="a4da7-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="a4da7-179">Veja [Carregar dados no HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="a4da7-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="a4da7-180">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a4da7-180">See Also</span></span>
* [<span data-ttu-id="a4da7-181">Documentação de referência do SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4da7-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="a4da7-182">[Administrar o HDInsight usando o Portal do Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="a4da7-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="a4da7-183">[Administrar o HDInsight usando uma interface de linha de comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="a4da7-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="a4da7-184">[Criar clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="a4da7-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="a4da7-185">[Carregar dados no HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a4da7-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a4da7-186">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="a4da7-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


