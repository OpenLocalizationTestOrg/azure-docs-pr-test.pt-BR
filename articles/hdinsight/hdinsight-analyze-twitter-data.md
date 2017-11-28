---
title: aaaAnalyze dados Twitter com Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse Hive tooanalyze Twitter dados no Hadoop em HDInsight toofind Olá frequência de uso de uma palavra específica."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="00683-103">Analisar dados do Twitter usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="00683-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="00683-104">Sites sociais são uma saudação principais forças para adoção de dados grandes.</span><span class="sxs-lookup"><span data-stu-id="00683-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="00683-105">APIs públicas fornecidas por sites, como o Twitter, são uma fonte útil de dados para analisar e compreender as tendências populares.</span><span class="sxs-lookup"><span data-stu-id="00683-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="00683-106">Neste tutorial, você obterá tweets usando um API de streaming de Twitter e, em seguida, usar o Apache Hive no Azure HDInsight tooget uma lista de usuários do Twitter que enviou Olá tweets mais que continha uma palavra específica.</span><span class="sxs-lookup"><span data-stu-id="00683-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00683-107">Olá, as etapas neste documento exigem um cluster HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="00683-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="00683-108">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="00683-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="00683-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="00683-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="00683-110">Para etapas específicas tooa baseados em Linux cluster consulte [Twitter analisar dados usando Hive no HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="00683-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00683-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00683-111">Prerequisites</span></span>
<span data-ttu-id="00683-112">Antes de começar este tutorial, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="00683-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="00683-113">**Uma estação de trabalho** com o PowerShell do Azure instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="00683-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="00683-114">tooexecute scripts do Windows PowerShell, você deve executar o Azure PowerShell como administrador e definir a política de execução Olá muito*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="00683-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="00683-115">Consulte [Executar scripts do Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="00683-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="00683-116">Antes de executar scripts do Windows PowerShell, verifique se que você está conectado tooyour assinatura do Azure usando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="00683-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="00683-117">Se você tiver várias assinaturas do Azure, use Olá assinatura atual do cmdlet tooset Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="00683-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="00683-118">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="00683-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="00683-119">Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="00683-120">Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="00683-121">Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="00683-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="00683-122">**Um cluster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="00683-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="00683-123">Para obter informações sobre como provisionar um cluster, consulte [Introdução ao HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="00683-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="00683-124">Você precisará nome do cluster hello mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="00683-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="00683-125">Olá tabela a seguir lista os arquivos de saudação usados neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="00683-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="00683-126">Arquivos</span><span class="sxs-lookup"><span data-stu-id="00683-126">Files</span></span> | <span data-ttu-id="00683-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="00683-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="00683-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="00683-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="00683-129">dados de origem Olá para o trabalho de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="00683-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="00683-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="00683-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="00683-131">Olá a pasta de saída para o trabalho de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="00683-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="00683-132">Olá nome de arquivo de saída padrão Hive trabalho é **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="00683-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="00683-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="00683-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="00683-134">arquivo de script HiveQL Hello.</span><span class="sxs-lookup"><span data-stu-id="00683-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="00683-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="00683-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="00683-136">Olá status do trabalho Hadoop.</span><span class="sxs-lookup"><span data-stu-id="00683-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="00683-137">Obter feed do Twitter</span><span class="sxs-lookup"><span data-stu-id="00683-137">Get Twitter feed</span></span>
<span data-ttu-id="00683-138">Neste tutorial, você usará Olá [APIs de streaming do Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="00683-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="00683-139">Olá específico Twitter streaming API que você usará é [status/filtro][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="00683-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="00683-140">Um arquivo contendo 10.000 tweets e o arquivo de script de Hive hello (abordado na próxima seção, Olá) foi carregado em um contêiner de Blob público.</span><span class="sxs-lookup"><span data-stu-id="00683-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="00683-141">Você pode ignorar esta seção se você quiser toouse Olá carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="00683-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="00683-142">[TWEETS dados](https://dev.twitter.com/docs/platform-objects/tweets) são armazenados em formato de notação JSON (JavaScript Object) Olá que contém uma estrutura aninhada complexa.</span><span class="sxs-lookup"><span data-stu-id="00683-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="00683-143">Em vez de escrever várias linhas de código usando uma linguagem de programação convencional, você pode transformar essa estrutura aninhada em uma tabela do Hive para que possa ser consultada por uma linguagem semelhante à SQL chamada HiveQL.</span><span class="sxs-lookup"><span data-stu-id="00683-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="00683-144">Twitter usa OAuth tooprovide autorizado acesso tooits API.</span><span class="sxs-lookup"><span data-stu-id="00683-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="00683-145">OAuth é um protocolo de autenticação que permite que os usuários tooapprove aplicativos tooact em seu nome sem compartilhar sua senha.</span><span class="sxs-lookup"><span data-stu-id="00683-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="00683-146">Mais informações podem ser encontradas em [oauth.net](http://oauth.net/) ou em Olá excelente [tooOAuth de guia do Iniciante](http://hueniverse.com/oauth/) de Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="00683-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="00683-147">saudação de primeira etapa toouse OAuth é toocreate um novo aplicativo no site do desenvolvedor do Twitter hello.</span><span class="sxs-lookup"><span data-stu-id="00683-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="00683-148">**toocreate um aplicativo do Twitter**</span><span class="sxs-lookup"><span data-stu-id="00683-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="00683-149">Entrar muito[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="00683-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="00683-150">Clique em Olá **inscrever-se agora** link se você não tiver uma conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="00683-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="00683-151">Clique em **Criar Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="00683-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="00683-152">Digite o **Nome**, a **Descrição** e o **Site**.</span><span class="sxs-lookup"><span data-stu-id="00683-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="00683-153">Você pode fazer backup de uma URL para Olá **site** campo.</span><span class="sxs-lookup"><span data-stu-id="00683-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="00683-154">Olá, a tabela a seguir mostra algumas toouse de valores de exemplo:</span><span class="sxs-lookup"><span data-stu-id="00683-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="00683-155">Campo</span><span class="sxs-lookup"><span data-stu-id="00683-155">Field</span></span> | <span data-ttu-id="00683-156">Valor</span><span class="sxs-lookup"><span data-stu-id="00683-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="00683-157">Nome</span><span class="sxs-lookup"><span data-stu-id="00683-157">Name</span></span> |<span data-ttu-id="00683-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="00683-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="00683-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="00683-159">Description</span></span> |<span data-ttu-id="00683-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="00683-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="00683-161">Site</span><span class="sxs-lookup"><span data-stu-id="00683-161">Website</span></span> |<span data-ttu-id="00683-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="00683-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="00683-163">Marque **Sim, eu concordo** e, em seguida, clique em **Criar seu aplicativo do Twitter**.</span><span class="sxs-lookup"><span data-stu-id="00683-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="00683-164">Clique em Olá **permissões** guia saudação padrão permissão é **somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="00683-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="00683-165">Isso é suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="00683-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="00683-166">Clique em Olá **chaves e Tokens de acesso** guia.</span><span class="sxs-lookup"><span data-stu-id="00683-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="00683-167">Clique em **Criar meu token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="00683-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="00683-168">Clique em **teste OAuth** no canto superior direito de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="00683-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="00683-169">Anote a **chave do consumidor**, o **Segredo do consumidor**, o **Token de acesso** e o **Segredo do token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="00683-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="00683-170">Você precisará valores hello mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="00683-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="00683-171">Neste tutorial, você usará a chamada de serviço da web do Windows PowerShell toomake hello.</span><span class="sxs-lookup"><span data-stu-id="00683-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="00683-172">Para ver um exemplo de C# .NET, consulte [Analisar sentimento no Twitter em tempo real com HBase no HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="00683-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="00683-173">Olá outras chamadas de serviço web popular ferramenta toomake é [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="00683-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="00683-174">O Curl pode ser baixado [aqui][curl-download].</span><span class="sxs-lookup"><span data-stu-id="00683-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="00683-175">Quando você usar o comando de ondulação Olá no Windows, use aspas duplas em vez de aspas simples para os valores de opção hello.</span><span class="sxs-lookup"><span data-stu-id="00683-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="00683-176">**tweets tooget**</span><span class="sxs-lookup"><span data-stu-id="00683-176">**tooget tweets**</span></span>

1. <span data-ttu-id="00683-177">Abra Olá Windows PowerShell Integrated Scripting ISE (ambiente).</span><span class="sxs-lookup"><span data-stu-id="00683-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="00683-178">(Na tela inicial do Windows 8 hello, digite **PowerShell_ISE** e, em seguida, clique em **o Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="00683-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="00683-179">Consulte [Iniciar o Windows PowerShell no Windows 8 e no Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="00683-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="00683-180">Copie Olá script a seguir no painel de script hello:</span><span class="sxs-lookup"><span data-stu-id="00683-180">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="00683-181">Defina as variáveis de tooeight cinco primeiros da saudação no script hello:</span><span class="sxs-lookup"><span data-stu-id="00683-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="00683-182">Variável</span><span class="sxs-lookup"><span data-stu-id="00683-182">Variable</span></span>|<span data-ttu-id="00683-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="00683-183">Description</span></span>
    ---|---
    <span data-ttu-id="00683-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="00683-184">$clusterName</span></span>|<span data-ttu-id="00683-185">Este é o nome de saudação do cluster do HDInsight Olá onde você deseja que o aplicativo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="00683-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="00683-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="00683-186">$oauth_consumer_key</span></span>|<span data-ttu-id="00683-187">Este é o aplicativo do Twitter hello **chave do consumidor** você anotou anteriormente quando você criou o aplicativo do Twitter hello.</span><span class="sxs-lookup"><span data-stu-id="00683-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="00683-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="00683-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="00683-189">Este é o aplicativo do Twitter hello **segredo do consumidor** você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="00683-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="00683-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="00683-190">$oauth_token</span></span>|<span data-ttu-id="00683-191">Este é o aplicativo do Twitter hello **token de acesso** você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="00683-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="00683-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="00683-192">$oauth_token_secret</span></span>|<span data-ttu-id="00683-193">Este é o aplicativo do Twitter hello **segredo do token de acesso** você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="00683-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="00683-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="00683-194">$destBlobName</span></span>|<span data-ttu-id="00683-195">Este é o nome de blob de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="00683-195">This is hello output blob name.</span></span> <span data-ttu-id="00683-196">valor padrão de saudação é **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="00683-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="00683-197">Se você alterar o valor padrão de saudação, você precisará scripts de Windows PowerShell Olá tooupdate adequadamente.</span><span class="sxs-lookup"><span data-stu-id="00683-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="00683-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="00683-198">$trackString</span></span>|<span data-ttu-id="00683-199">serviço web de saudação retornará toothese relacionados de tweets palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="00683-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="00683-200">valor padrão de saudação é **HDInsight do Azure, a nuvem,**.</span><span class="sxs-lookup"><span data-stu-id="00683-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="00683-201">Se você alterar o valor padrão de saudação, você atualizará scripts do Windows PowerShell Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="00683-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="00683-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="00683-202">$lineMax</span></span>|<span data-ttu-id="00683-203">valor de Olá determina quantos script hello de tweets será lida.</span><span class="sxs-lookup"><span data-stu-id="00683-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="00683-204">Leva aproximadamente três minutos tooread 100 tweets.</span><span class="sxs-lookup"><span data-stu-id="00683-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="00683-205">Você pode definir um número maior, mas levará mais toodownload de tempo.</span><span class="sxs-lookup"><span data-stu-id="00683-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="00683-206">Pressione **F5** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="00683-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="00683-207">Se você tiver problemas, como alternativa, selecione todas as linhas de saudação e, em seguida, pressione **F8**.</span><span class="sxs-lookup"><span data-stu-id="00683-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="00683-208">Você deverá ver a mensagem "Concluído!"</span><span class="sxs-lookup"><span data-stu-id="00683-208">You shall see "Complete!"</span></span> <span data-ttu-id="00683-209">no final da saudação da saída de hello.</span><span class="sxs-lookup"><span data-stu-id="00683-209">at hello end of hello output.</span></span> <span data-ttu-id="00683-210">Qualquer mensagem de erro será exibida em vermelho.</span><span class="sxs-lookup"><span data-stu-id="00683-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="00683-211">Como um procedimento de validação, você pode verificar o arquivo de saída de hello, **/tutorials/twitter/data/tweets.txt**, no armazenamento de BLOBs do Azure usando um Gerenciador de armazenamento do Azure ou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="00683-212">Para um exemplo de script do Windows PowerShell para listagem de arquivos, consulte [Usar o Armazenamento de Blobs com o HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="00683-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="00683-213">Criar o script HiveQL</span><span class="sxs-lookup"><span data-stu-id="00683-213">Create HiveQL script</span></span>
<span data-ttu-id="00683-214">Usando o PowerShell do Azure, você pode executar várias instruções HiveQL um em uma hora ou instrução de estilo de saudação de pacote em um arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="00683-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="00683-215">Neste tutorial, você irá criar um script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="00683-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="00683-216">arquivo de script Hello deve ser carregado tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="00683-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="00683-217">Na próxima seção, Olá, execute o arquivo de script hello usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="00683-218">arquivo de script de Hive Hello e um arquivo que contém a 10.000 tweets foi carregados em um contêiner de Blob público.</span><span class="sxs-lookup"><span data-stu-id="00683-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="00683-219">Você pode ignorar esta seção se você quiser toouse Olá carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="00683-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="00683-220">Olá script HiveQL executará o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="00683-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="00683-221">**Descartar Olá tweets_raw tabela** no caso de Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="00683-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="00683-222">**Criar tabela de Hive Olá tweets_raw**.</span><span class="sxs-lookup"><span data-stu-id="00683-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="00683-223">Essa seção temporária estruturada tabela contém dados de saudação para mais extrair, transformar e carregar o processamento (ETL).</span><span class="sxs-lookup"><span data-stu-id="00683-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="00683-224">Para obter informações sobre partições, consulte o [tutorial do Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="00683-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="00683-225">**Carregar dados** da pasta de origem hello, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="00683-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="00683-226">Olá tweets grande conjunto de dados no formato aninhado de JSON agora foi transformado em uma estrutura de tabela temporária do Hive.</span><span class="sxs-lookup"><span data-stu-id="00683-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="00683-227">**A tabela DROP Olá tweets** no caso de Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="00683-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="00683-228">**Criar tabela de tweets Olá**.</span><span class="sxs-lookup"><span data-stu-id="00683-228">**Create hello tweets table**.</span></span> <span data-ttu-id="00683-229">Antes que você pode consultar o conjunto de dados do hello tweets usando Hive, é necessário toorun outro processo ETL.</span><span class="sxs-lookup"><span data-stu-id="00683-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="00683-230">Esse processo ETL define um esquema de tabela mais detalhado para dados Olá armazenado na tabela de "twitter_raw" hello.</span><span class="sxs-lookup"><span data-stu-id="00683-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="00683-231">**Insira tabela de substituição**.</span><span class="sxs-lookup"><span data-stu-id="00683-231">**Insert overwrite table**.</span></span> <span data-ttu-id="00683-232">Esse script de Hive complexas para iniciar um conjunto de trabalhos de MapReduce longo por cluster de Hadoop de saudação.</span><span class="sxs-lookup"><span data-stu-id="00683-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="00683-233">Dependendo de seu conjunto de dados e hello o tamanho do cluster, isso pode levar cerca de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="00683-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="00683-234">**Insira diretório de substituição**.</span><span class="sxs-lookup"><span data-stu-id="00683-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="00683-235">Execute um arquivo de tooa de conjunto de dados de saudação de consulta e de saída.</span><span class="sxs-lookup"><span data-stu-id="00683-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="00683-236">Essa consulta retornará uma lista de usuários do Twitter que enviou a maioria dos tweets que contêm a palavra de hello "Azure".</span><span class="sxs-lookup"><span data-stu-id="00683-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="00683-237">**toocreate uma seção de script e carregá-lo tooAzure**</span><span class="sxs-lookup"><span data-stu-id="00683-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="00683-238">Abra o ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00683-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="00683-239">Copie Olá script a seguir no painel de script hello:</span><span class="sxs-lookup"><span data-stu-id="00683-239">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="00683-240">Defina primeiro duas variáveis de saudação no script hello:</span><span class="sxs-lookup"><span data-stu-id="00683-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="00683-241">Variável</span><span class="sxs-lookup"><span data-stu-id="00683-241">Variable</span></span> | <span data-ttu-id="00683-242">Descrição</span><span class="sxs-lookup"><span data-stu-id="00683-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="00683-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="00683-243">$clusterName</span></span> |<span data-ttu-id="00683-244">Insira o nome do cluster HDInsight Olá onde você deseja que o aplicativo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="00683-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="00683-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="00683-245">$subscriptionID</span></span> |<span data-ttu-id="00683-246">Insira sua ID da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="00683-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="00683-247">$sourceDataPath</span></span> |<span data-ttu-id="00683-248">Olá local de armazenamento de BLOBs do Azure, onde consultas de Hive Olá lê dados de saudação do.</span><span class="sxs-lookup"><span data-stu-id="00683-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="00683-249">Você não precisa toochange essa variável.</span><span class="sxs-lookup"><span data-stu-id="00683-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="00683-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="00683-250">$outputPath</span></span> |<span data-ttu-id="00683-251">Olá onde a consultas de Hive Olá produzirá resultados da saudação de local de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="00683-252">Você não precisa toochange essa variável.</span><span class="sxs-lookup"><span data-stu-id="00683-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="00683-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="00683-253">$hqlScriptFile</span></span> |<span data-ttu-id="00683-254">local de Hello e nome do arquivo Olá Olá HiveQL do arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="00683-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="00683-255">Você não precisa toochange essa variável.</span><span class="sxs-lookup"><span data-stu-id="00683-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="00683-256">Pressione **F5** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="00683-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="00683-257">Se você tiver problemas, como alternativa, selecione todas as linhas de saudação e, em seguida, pressione **F8**.</span><span class="sxs-lookup"><span data-stu-id="00683-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="00683-258">Você deverá ver a mensagem "Concluído!"</span><span class="sxs-lookup"><span data-stu-id="00683-258">You shall see "Complete!"</span></span> <span data-ttu-id="00683-259">no final da saudação da saída de hello.</span><span class="sxs-lookup"><span data-stu-id="00683-259">at hello end of hello output.</span></span> <span data-ttu-id="00683-260">Qualquer mensagem de erro será exibida em vermelho.</span><span class="sxs-lookup"><span data-stu-id="00683-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="00683-261">Como um procedimento de validação, você pode verificar o arquivo de saída de hello, **/tutorials/twitter/twitter.hql**, no armazenamento de BLOBs do Azure usando um Gerenciador de armazenamento do Azure ou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="00683-262">Para um exemplo de script do Windows PowerShell para listagem de arquivos, consulte [Usar o Armazenamento de Blobs com o HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="00683-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="00683-263">Processar os dados do Twitter usando o Hive</span><span class="sxs-lookup"><span data-stu-id="00683-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="00683-264">Você concluiu a todo o trabalho de preparação hello.</span><span class="sxs-lookup"><span data-stu-id="00683-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="00683-265">Agora, você pode invocar o script do Hive hello e Olá resultados da verificação.</span><span class="sxs-lookup"><span data-stu-id="00683-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="00683-266">Enviar um trabalho do Hive</span><span class="sxs-lookup"><span data-stu-id="00683-266">Submit a Hive job</span></span>
<span data-ttu-id="00683-267">Use Olá a seguir de script do Windows PowerShell script toorun Olá Hive.</span><span class="sxs-lookup"><span data-stu-id="00683-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="00683-268">Você precisará primeira variável do tooset hello.</span><span class="sxs-lookup"><span data-stu-id="00683-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="00683-269">Olá toouse tweets e Olá script HiveQL carregado em duas últimas seções hello, conjunto $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="00683-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="00683-270">Olá toouse aqueles que foram carregados blob público tooa para você, defina $hqlScriptFile muito"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="00683-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a><span data-ttu-id="00683-271">Resultados da verificação de saudação</span><span class="sxs-lookup"><span data-stu-id="00683-271">Check hello results</span></span>
<span data-ttu-id="00683-272">Saudação de uso após a saída de trabalho do Windows PowerShell script toocheck hello Hive.</span><span class="sxs-lookup"><span data-stu-id="00683-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="00683-273">Você precisará primeiro duas variáveis do tooset hello.</span><span class="sxs-lookup"><span data-stu-id="00683-273">You will need tooset hello first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabela de Hive Olá usa \001 Olá delimitador de campo. <span data-ttu-id="00683-275">delimitador de saudação não estiver visível na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="00683-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="00683-276">Depois que os resultados de análise de saudação foram colocados no armazenamento de BLOBs do Azure, exportar Olá dados tooan SQL Azure banco de dados/SQL server, exportar Olá dados tooExcel usando o Power Query ou conectar-se os dados do aplicativo toohello usando Olá Hive ODBC Driver.</span><span class="sxs-lookup"><span data-stu-id="00683-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="00683-277">Para obter mais informações, consulte [Sqoop de uso com o HDInsight][hdinsight-use-sqoop], [analisar dados de atraso de voo usando HDInsight][hdinsight-analyze-flight-delay-data], [ Conectar Excel tooHDInsight com o Power Query][hdinsight-power-query], e [tooHDInsight Excel conectar-se com hello Microsoft ODBC Driver Hive][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="00683-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="00683-278">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00683-278">Next steps</span></span>
<span data-ttu-id="00683-279">Neste tutorial, vimos como tootransform um conjunto de dados JSON não estruturado em um tooquery estruturado de tabela de Hive, explorar e analisar dados do Twitter usando o HDInsight no Azure.</span><span class="sxs-lookup"><span data-stu-id="00683-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="00683-280">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="00683-280">toolearn more, see:</span></span>

* <span data-ttu-id="00683-281">[Introdução ao HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="00683-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="00683-282">[Analisar sentimento no Twitter em tempo real com HBase no HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="00683-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="00683-283">[Analisar dados de atraso de voo usando o HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="00683-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="00683-284">[Conectar Excel tooHDInsight com o Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="00683-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="00683-285">[Conectar Excel tooHDInsight com hello Microsoft ODBC Driver Hive][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="00683-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="00683-286">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="00683-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
