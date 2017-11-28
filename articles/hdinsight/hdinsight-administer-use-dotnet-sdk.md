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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="5fc1a-103">Gerenciar clusters Hadoop no HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="5fc1a-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="5fc1a-104">Saiba como toomanage HDInsight clusters usando [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="5fc1a-105">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="5fc1a-105">**Prerequisites**</span></span>

<span data-ttu-id="5fc1a-106">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="5fc1a-107">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-107">**An Azure subscription**.</span></span> <span data-ttu-id="5fc1a-108">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="5fc1a-109">Conecte-se tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5fc1a-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="5fc1a-110">Você precisa Olá pacotes do Nuget a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="5fc1a-111">Olá exemplo de código a seguir mostra como clusters de tooconnect tooAzure para que você possa administrar HDInsight em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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

<span data-ttu-id="5fc1a-112">Você deverá ver um aviso ao executar este programa.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="5fc1a-113">Se você não quiser prompt de saudação toosee, consulte [criar aplicativos .NET HDInsight de autenticação não interativo](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="5fc1a-114">Criar clusters</span><span class="sxs-lookup"><span data-stu-id="5fc1a-114">Create clusters</span></span>
<span data-ttu-id="5fc1a-115">Consulte [baseados em Linux criar clusters HDInsight usando Olá SDK .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="5fc1a-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="5fc1a-116">Listar clusters</span><span class="sxs-lookup"><span data-stu-id="5fc1a-116">List clusters</span></span>
<span data-ttu-id="5fc1a-117">Olá trecho de código a seguir mostra os clusters e algumas propriedades:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="5fc1a-118">Excluir clusters</span><span class="sxs-lookup"><span data-stu-id="5fc1a-118">Delete clusters</span></span>
<span data-ttu-id="5fc1a-119">Use Olá seguindo o trecho de código toodelete um cluster de forma síncrona ou assíncrona:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="5fc1a-120">Dimensionar clusters</span><span class="sxs-lookup"><span data-stu-id="5fc1a-120">Scale clusters</span></span>
<span data-ttu-id="5fc1a-121">dimensionando o recurso de cluster de saudação permite toochange número de saudação de nós de trabalho usado por um cluster que está em execução no Azure HDInsight sem ter que toore-criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5fc1a-122">Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="5fc1a-123">Se você não tiver certeza da versão de saudação do cluster, você pode verificar a página de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="5fc1a-124">Confira [Listar e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="5fc1a-125">impacto de saudação do alterando o número de saudação de nós de dados para cada tipo de cluster HDInsight com suporte:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="5fc1a-126">O Hadoop</span><span class="sxs-lookup"><span data-stu-id="5fc1a-126">Hadoop</span></span>
  
    <span data-ttu-id="5fc1a-127">Você perfeitamente pode aumentar o número de saudação de nós de trabalho em um cluster de Hadoop que está sendo executado sem afetar todos os trabalhos pendentes ou em execução.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="5fc1a-128">Novos trabalhos também podem ser enviados enquanto Olá operação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="5fc1a-129">Falhas em uma operação de dimensionamento são controladas normalmente para que hello cluster seja sempre deixado em um estado funcional.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="5fc1a-130">Quando um cluster Hadoop é reduzido, reduzindo o número de saudação de nós de dados, alguns dos serviços de saudação em cluster Olá são reiniciados.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="5fc1a-131">Isso faz com que todas as e pendentes toofail trabalhos na conclusão de saudação do hello a operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="5fc1a-132">No entanto, você pode, reenviar trabalhos Olá após a conclusão da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="5fc1a-133">HBase</span><span class="sxs-lookup"><span data-stu-id="5fc1a-133">HBase</span></span>
  
    <span data-ttu-id="5fc1a-134">Sem problemas, você pode adicionar ou remover o cluster de HBase tooyour nós enquanto ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="5fc1a-135">Servidores regionais são balanceados automaticamente dentro de alguns minutos após o término da operação de dimensionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="5fc1a-136">No entanto, você pode equilibrar manualmente servidores regionais Olá fazendo logon no nó principal de saudação do cluster e em execução hello comandos a seguir em uma janela de prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="5fc1a-137">Storm</span><span class="sxs-lookup"><span data-stu-id="5fc1a-137">Storm</span></span>
  
    <span data-ttu-id="5fc1a-138">Sem problemas, você pode adicionar ou remover o cluster de profusão de tooyour de nós de dados enquanto ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="5fc1a-139">Mas, após a conclusão bem-sucedida da operação de dimensionamento de saudação, você precisará de topologia de saudação toorebalance.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="5fc1a-140">A redistribuição pode ser feita de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="5fc1a-141">Interface da Web Storm</span><span class="sxs-lookup"><span data-stu-id="5fc1a-141">Storm web UI</span></span>
  * <span data-ttu-id="5fc1a-142">Ferramenta CLI (interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="5fc1a-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="5fc1a-143">Consulte toohello [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="5fc1a-144">Interface da web Hello Storm está disponível no cluster do HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![Redistribuir escala do Storm do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="5fc1a-146">Aqui está um exemplo como toouse Olá CLI comando topologia de profusão de saudação toorebalance:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="5fc1a-147">Olá seguindo o trecho de código mostra como tooresize um cluster de forma síncrona ou assíncrona:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="5fc1a-148">Conceder/revogar acesso</span><span class="sxs-lookup"><span data-stu-id="5fc1a-148">Grant/revoke access</span></span>
<span data-ttu-id="5fc1a-149">Clusters HDInsight tem Olá serviços da web HTTP (todos esses serviços têm pontos de extremidade RESTful) a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="5fc1a-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="5fc1a-150">ODBC</span></span>
* <span data-ttu-id="5fc1a-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="5fc1a-151">JDBC</span></span>
* <span data-ttu-id="5fc1a-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="5fc1a-152">Ambari</span></span>
* <span data-ttu-id="5fc1a-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="5fc1a-153">Oozie</span></span>
* <span data-ttu-id="5fc1a-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="5fc1a-154">Templeton</span></span>

<span data-ttu-id="5fc1a-155">Por padrão, esses serviços são concedidos para acesso.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-155">By default, these services are granted for access.</span></span> <span data-ttu-id="5fc1a-156">Você pode revogar/conceder acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="5fc1a-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="5fc1a-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="5fc1a-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="5fc1a-159">Revogando concedendo/acesso hello, redefinirá senha e nome de usuário de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="5fc1a-160">Isso também pode ser feito por meio do Portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="5fc1a-161">Consulte [HDInsight administrar usando Olá portal do Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="5fc1a-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="5fc1a-162">Atualizar credenciais de usuário HTTP</span><span class="sxs-lookup"><span data-stu-id="5fc1a-162">Update HTTP user credentials</span></span>
<span data-ttu-id="5fc1a-163">É Olá mesmo procedimento como [acesso Grant/revoke HTTP](#grant/revoke-access). Se foi concedida cluster Olá Olá acesso HTTP, você deve primeiro revogá-lo.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="5fc1a-164">E, em seguida, conceder acesso de saudação com novas credenciais de usuário HTTP.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="5fc1a-165">Localizar a conta de armazenamento saudação padrão</span><span class="sxs-lookup"><span data-stu-id="5fc1a-165">Find hello default storage account</span></span>
<span data-ttu-id="5fc1a-166">saudação de trecho de código a seguir demonstra como tooget Olá nome de conta de armazenamento padrão e Olá chave de conta de armazenamento padrão para um cluster.</span><span class="sxs-lookup"><span data-stu-id="5fc1a-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="5fc1a-167">Enviar trabalhos</span><span class="sxs-lookup"><span data-stu-id="5fc1a-167">Submit jobs</span></span>
<span data-ttu-id="5fc1a-168">**trabalhos de MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="5fc1a-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="5fc1a-169">Veja [Executar amostras de MapReduce do Hadoop no HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="5fc1a-170">**trabalhos de Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="5fc1a-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="5fc1a-171">Veja [Executar consultas do Hive usando o SDK do .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="5fc1a-172">**trabalhos de Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="5fc1a-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="5fc1a-173">Veja [Executar trabalhos do Pig usando o SDK do .NET](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="5fc1a-174">**trabalhos de Sqoop toosubmit**</span><span class="sxs-lookup"><span data-stu-id="5fc1a-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="5fc1a-175">Consulte [Usar o Sqoop com o HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="5fc1a-176">**toosubmit Oozie trabalhos**</span><span class="sxs-lookup"><span data-stu-id="5fc1a-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="5fc1a-177">Consulte [Oozie de uso com toodefine Hadoop e executar um fluxo de trabalho no HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="5fc1a-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="5fc1a-178">Carregue o armazenamento de Blob de tooAzure de dados</span><span class="sxs-lookup"><span data-stu-id="5fc1a-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="5fc1a-179">Consulte [carregar dados tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="5fc1a-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="5fc1a-180">Consulte também</span><span class="sxs-lookup"><span data-stu-id="5fc1a-180">See Also</span></span>
* [<span data-ttu-id="5fc1a-181">Documentação de referência do SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="5fc1a-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="5fc1a-182">[Administrar HDInsight usando Olá portal do Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="5fc1a-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="5fc1a-183">[Administrar o HDInsight usando uma interface de linha de comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="5fc1a-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="5fc1a-184">[Criar clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="5fc1a-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="5fc1a-185">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="5fc1a-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="5fc1a-186">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="5fc1a-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


