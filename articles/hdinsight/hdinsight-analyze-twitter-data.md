---
title: "Analisar dados do Twitter com o Hadoop no HDInsight – Azure | Microsoft Docs"
description: "Saiba como usar o Hive para analisar dados do Twitter com Hadoop no HDInsight para encontrar a frequência de uso de uma determinada palavra."
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
ms.openlocfilehash: 711d364c36c3aba699326f4a76d42891ba3219fb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="31ddc-103">Analisar dados do Twitter usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="31ddc-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="31ddc-104">Sites sociais são uma das forças principais para a adoção de big data.</span><span class="sxs-lookup"><span data-stu-id="31ddc-104">Social websites are one of the major driving forces for big-data adoption.</span></span> <span data-ttu-id="31ddc-105">APIs públicas fornecidas por sites, como o Twitter, são uma fonte útil de dados para analisar e compreender as tendências populares.</span><span class="sxs-lookup"><span data-stu-id="31ddc-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="31ddc-106">Neste tutorial, você obterá tweets usando o API de streaming do Twitter e, em seguida, usará o Apache Hive no HDInsight do Azure para obter uma lista de usuários do Twitter que enviaram mais tweets contendo uma determinada palavra.</span><span class="sxs-lookup"><span data-stu-id="31ddc-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31ddc-107">As etapas deste documento exigem um cluster HDInsight baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="31ddc-107">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="31ddc-108">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="31ddc-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="31ddc-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="31ddc-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="31ddc-110">Para obter as etapas específicas para um cluster baseado em Linux, confira [Analisar dados do Twitter usando o Hive no HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="31ddc-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31ddc-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="31ddc-111">Prerequisites</span></span>
<span data-ttu-id="31ddc-112">Antes de começar este tutorial, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="31ddc-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="31ddc-113">**Uma estação de trabalho** com o PowerShell do Azure instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="31ddc-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="31ddc-114">Para executar scripts do Windows PowerShell, você deve executar o PowerShell do Azure como administrador e configurar a política de execução como *RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="31ddc-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span></span> <span data-ttu-id="31ddc-115">Consulte [Executar scripts do Windows PowerShell][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="31ddc-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="31ddc-116">Antes de executar scripts do Windows PowerShell, verifique se você está conectado à sua assinatura do Azure usando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="31ddc-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="31ddc-117">Se você tiver várias assinaturas do Azure, use o seguinte cmdlet para definir a assinatura atual:</span><span class="sxs-lookup"><span data-stu-id="31ddc-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="31ddc-118">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="31ddc-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="31ddc-119">As etapas neste documento usam os novos cmdlets do HDInsight que funcionam com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31ddc-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="31ddc-120">Siga as etapas em [Instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para instalar a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31ddc-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="31ddc-121">Se você tiver scripts que precisam ser modificados para usar os novos cmdlets que funcionam com o Azure Resource Manager, confira [Migrando para as ferramentas de desenvolvimento baseadas no Azure Resource Manager dos clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="31ddc-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="31ddc-122">**Um cluster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="31ddc-123">Para obter informações sobre como provisionar um cluster, consulte [Introdução ao HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="31ddc-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="31ddc-124">Você precisará do nome do cluster posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="31ddc-124">You will need the cluster name later in the tutorial.</span></span>

<span data-ttu-id="31ddc-125">A tabela a seguir lista os arquivos usados neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="31ddc-125">The following table lists the files used in this tutorial:</span></span>

| <span data-ttu-id="31ddc-126">Arquivos</span><span class="sxs-lookup"><span data-stu-id="31ddc-126">Files</span></span> | <span data-ttu-id="31ddc-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="31ddc-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31ddc-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="31ddc-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="31ddc-129">Os dados de origem para o trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="31ddc-129">The source data for the Hive job.</span></span> |
| <span data-ttu-id="31ddc-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="31ddc-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="31ddc-131">A pasta de saída para o trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="31ddc-131">The output folder for the Hive job.</span></span> <span data-ttu-id="31ddc-132">O nome do arquivo de saída do trabalho do Hive padrão é **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-132">The default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="31ddc-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="31ddc-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="31ddc-134">O arquivo de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="31ddc-134">The HiveQL script file.</span></span> |
| <span data-ttu-id="31ddc-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="31ddc-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="31ddc-136">O status do trabalho do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="31ddc-136">The Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="31ddc-137">Obter feed do Twitter</span><span class="sxs-lookup"><span data-stu-id="31ddc-137">Get Twitter feed</span></span>
<span data-ttu-id="31ddc-138">Neste tutorial, você usará as [APIs de streaming do Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="31ddc-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="31ddc-139">A API de streaming específica do Twitter que você usará é [statuses/filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="31ddc-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="31ddc-140">Um arquivo contendo 10.000 tweets e o arquivo de script do Hive (abordado na próxima seção) foram carregados em um contêiner de Blob público.</span><span class="sxs-lookup"><span data-stu-id="31ddc-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="31ddc-141">Você pode ignorar esta seção se quiser usar os arquivos carregados.</span><span class="sxs-lookup"><span data-stu-id="31ddc-141">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="31ddc-142">[Dados de tweets](https://dev.twitter.com/docs/platform-objects/tweets) são armazenados no formato JSON (JavaScript Object Notation) que contém uma estrutura aninhada complexa.</span><span class="sxs-lookup"><span data-stu-id="31ddc-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="31ddc-143">Em vez de escrever várias linhas de código usando uma linguagem de programação convencional, você pode transformar essa estrutura aninhada em uma tabela do Hive para que possa ser consultada por uma linguagem semelhante à SQL chamada HiveQL.</span><span class="sxs-lookup"><span data-stu-id="31ddc-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="31ddc-144">O Twitter usa OAuth para oferecer acesso autorizado à sua API.</span><span class="sxs-lookup"><span data-stu-id="31ddc-144">Twitter uses OAuth to provide authorized access to its API.</span></span> <span data-ttu-id="31ddc-145">OAuth é um protocolo de autenticação que permite ao usuários aprovar os aplicativos para atuar em seu nome sem compartilhar sua senha.</span><span class="sxs-lookup"><span data-stu-id="31ddc-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span></span> <span data-ttu-id="31ddc-146">Mais informações podem ser encontradas em [oauth.net](http://oauth.net/) ou no excelente [Guia para iniciantes do OAuth](http://hueniverse.com/oauth/) no Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="31ddc-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="31ddc-147">A primeira etapa para usar OAuth é criar um novo aplicativo no site do desenvolvedor do Twitter.</span><span class="sxs-lookup"><span data-stu-id="31ddc-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span></span>

<span data-ttu-id="31ddc-148">**Para criar um aplicativo do Twitter**</span><span class="sxs-lookup"><span data-stu-id="31ddc-148">**To create a Twitter application**</span></span>

1. <span data-ttu-id="31ddc-149">Entre em [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="31ddc-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="31ddc-150">Clique no link **Inscreva-se agora** se você não tem uma conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="31ddc-150">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="31ddc-151">Clique em **Criar Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="31ddc-152">Digite o **Nome**, a **Descrição** e o **Site**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="31ddc-153">Você pode fazer uma URL para o campo **Site** .</span><span class="sxs-lookup"><span data-stu-id="31ddc-153">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="31ddc-154">A tabela a seguir mostra alguns valores de exemplo para usar:</span><span class="sxs-lookup"><span data-stu-id="31ddc-154">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="31ddc-155">Campo</span><span class="sxs-lookup"><span data-stu-id="31ddc-155">Field</span></span> | <span data-ttu-id="31ddc-156">Valor</span><span class="sxs-lookup"><span data-stu-id="31ddc-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="31ddc-157">Nome</span><span class="sxs-lookup"><span data-stu-id="31ddc-157">Name</span></span> |<span data-ttu-id="31ddc-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="31ddc-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="31ddc-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="31ddc-159">Description</span></span> |<span data-ttu-id="31ddc-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="31ddc-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="31ddc-161">Site</span><span class="sxs-lookup"><span data-stu-id="31ddc-161">Website</span></span> |<span data-ttu-id="31ddc-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="31ddc-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="31ddc-163">Marque **Sim, eu concordo** e, em seguida, clique em **Criar seu aplicativo do Twitter**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="31ddc-164">Clique na guia **Permissões** .</span><span class="sxs-lookup"><span data-stu-id="31ddc-164">Click the **Permissions** tab.</span></span> <span data-ttu-id="31ddc-165">A permissão padrão é **Somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-165">The default permission is **Read only**.</span></span> <span data-ttu-id="31ddc-166">Isso é suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="31ddc-166">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="31ddc-167">Clique na guia **Chaves e Tokens de acesso** .</span><span class="sxs-lookup"><span data-stu-id="31ddc-167">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="31ddc-168">Clique em **Criar meu token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-168">Click **Create my access token**.</span></span>
8. <span data-ttu-id="31ddc-169">Clique em **OAuth de teste** no canto superior direito da página.</span><span class="sxs-lookup"><span data-stu-id="31ddc-169">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="31ddc-170">Anote a **chave do consumidor**, o **Segredo do consumidor**, o **Token de acesso** e o **Segredo do token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-170">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="31ddc-171">Você precisará dos valores mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="31ddc-171">You will need the values later in the tutorial.</span></span>

<span data-ttu-id="31ddc-172">Neste tutorial, você usará o Windows PowerShell para fazer a chamada de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="31ddc-172">In this tutorial, you will use Windows PowerShell to make the web service call.</span></span> <span data-ttu-id="31ddc-173">Para ver um exemplo de C# .NET, consulte [Analisar sentimento no Twitter em tempo real com HBase no HDInsight][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="31ddc-173">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="31ddc-174">A outra ferramenta popular para fazer chamadas de serviço da Web é o [*Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="31ddc-174">The other popular tool to make web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="31ddc-175">O Curl pode ser baixado [aqui][curl-download].</span><span class="sxs-lookup"><span data-stu-id="31ddc-175">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="31ddc-176">Quando usar o comando curl no Windows, use aspas duplas, em vez de aspas simples, para os valores de opção.</span><span class="sxs-lookup"><span data-stu-id="31ddc-176">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>

<span data-ttu-id="31ddc-177">**Para obter tweets**</span><span class="sxs-lookup"><span data-stu-id="31ddc-177">**To get tweets**</span></span>

1. <span data-ttu-id="31ddc-178">Abra o ISE (ambiente de script integrado) do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31ddc-178">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="31ddc-179">(Na tela Iniciar do Windows 8, digite **PowerShell_ISE** e, em seguida, clique em **ISE do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-179">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="31ddc-180">Consulte [Iniciar o Windows PowerShell no Windows 8 e no Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="31ddc-180">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="31ddc-181">Copie o seguinte script no painel de script:</span><span class="sxs-lookup"><span data-stu-id="31ddc-181">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
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

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="31ddc-182">Defina as cinco a oito primeiras variáveis no script:</span><span class="sxs-lookup"><span data-stu-id="31ddc-182">Set the first five to eight variables in the script:</span></span>

    <span data-ttu-id="31ddc-183">Variável</span><span class="sxs-lookup"><span data-stu-id="31ddc-183">Variable</span></span>|<span data-ttu-id="31ddc-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="31ddc-184">Description</span></span>
    ---|---
    <span data-ttu-id="31ddc-185">$clusterName</span><span class="sxs-lookup"><span data-stu-id="31ddc-185">$clusterName</span></span>|<span data-ttu-id="31ddc-186">Esse é o nome do cluster HDInsight em que você deseja executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31ddc-186">This is the name of the HDInsight cluster where you want to run the application.</span></span>
    <span data-ttu-id="31ddc-187">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="31ddc-187">$oauth_consumer_key</span></span>|<span data-ttu-id="31ddc-188">Esta é a **chave de consumidor** do aplicativo do Twitter que você anotou anteriormente ao criar esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31ddc-188">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span></span>
    <span data-ttu-id="31ddc-189">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="31ddc-189">$oauth_consumer_secret</span></span>|<span data-ttu-id="31ddc-190">Este é o **segredo de consumidor** do aplicativo do Twitter que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="31ddc-190">This is the Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="31ddc-191">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="31ddc-191">$oauth_token</span></span>|<span data-ttu-id="31ddc-192">Este é o **token de acesso** do aplicativo do Twitter que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="31ddc-192">This is the Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="31ddc-193">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="31ddc-193">$oauth_token_secret</span></span>|<span data-ttu-id="31ddc-194">Este é o **segredo de token de acesso** do aplicativo do Twitter que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="31ddc-194">This is the Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="31ddc-195">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="31ddc-195">$destBlobName</span></span>|<span data-ttu-id="31ddc-196">É o nome de saída do blob.</span><span class="sxs-lookup"><span data-stu-id="31ddc-196">This is the output blob name.</span></span> <span data-ttu-id="31ddc-197">O valor padrão é **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-197">The default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="31ddc-198">Se alterar o valor padrão, você precisará atualizar os scripts do Windows PowerShell adequadamente.</span><span class="sxs-lookup"><span data-stu-id="31ddc-198">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="31ddc-199">$trackString</span><span class="sxs-lookup"><span data-stu-id="31ddc-199">$trackString</span></span>|<span data-ttu-id="31ddc-200">O serviço da Web retornará tweets relacionados a essas palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="31ddc-200">The web service will return tweets related to these keywords.</span></span> <span data-ttu-id="31ddc-201">O valor padrão é **Azure, Nuvem, HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-201">The default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="31ddc-202">Se alterar o valor padrão, você atualizará os scripts do Windows PowerShell adequadamente.</span><span class="sxs-lookup"><span data-stu-id="31ddc-202">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="31ddc-203">$lineMax</span><span class="sxs-lookup"><span data-stu-id="31ddc-203">$lineMax</span></span>|<span data-ttu-id="31ddc-204">O valor determina quantos tweets o script lerá.</span><span class="sxs-lookup"><span data-stu-id="31ddc-204">The value determines how many tweets the script will read.</span></span> <span data-ttu-id="31ddc-205">Leva aproximadamente três minutos para ler 100 tweets.</span><span class="sxs-lookup"><span data-stu-id="31ddc-205">It takes about three minutes to read 100 tweets.</span></span> <span data-ttu-id="31ddc-206">Você pode definir um número maior, mas levará mais tempo para fazer o download.</span><span class="sxs-lookup"><span data-stu-id="31ddc-206">You can set a larger number, but it will take more time to download.</span></span>

1. <span data-ttu-id="31ddc-207">Pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="31ddc-207">Press **F5** to run the script.</span></span> <span data-ttu-id="31ddc-208">Se você tiver problemas, como alternativa, selecione todas as linhas e então pressione **F8**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-208">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
2. <span data-ttu-id="31ddc-209">Você deverá ver a mensagem "Concluído!"</span><span class="sxs-lookup"><span data-stu-id="31ddc-209">You shall see "Complete!"</span></span> <span data-ttu-id="31ddc-210">no final da saída.</span><span class="sxs-lookup"><span data-stu-id="31ddc-210">at the end of the output.</span></span> <span data-ttu-id="31ddc-211">Qualquer mensagem de erro será exibida em vermelho.</span><span class="sxs-lookup"><span data-stu-id="31ddc-211">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="31ddc-212">Como um procedimento de validação, você pode verificar o arquivo de saída, **/tutorials/twitter/data/tweets.txt**, em seu armazenamento de blob do Azure usando um gerenciador de armazenamento do Azure ou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="31ddc-212">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="31ddc-213">Para um exemplo de script do Windows PowerShell para listagem de arquivos, consulte [Usar o Armazenamento de Blobs com o HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="31ddc-213">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="31ddc-214">Criar o script HiveQL</span><span class="sxs-lookup"><span data-stu-id="31ddc-214">Create HiveQL script</span></span>
<span data-ttu-id="31ddc-215">Usando o PowerShell do Azure, você pode executar várias instruções HiveQL uma por vez ou empacotar a instrução HiveQL em um arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="31ddc-215">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="31ddc-216">Neste tutorial, você irá criar um script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="31ddc-216">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="31ddc-217">O arquivo de script deve ser carregado para o armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="31ddc-217">The script file must be uploaded to Azure Blob storage.</span></span> <span data-ttu-id="31ddc-218">Na próxima seção, você executará o arquivo de script usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="31ddc-218">In the next section, you will run the script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="31ddc-219">O arquivo de script do Hive e um arquivo contendo 10.000 tweets foram carregados em um contêiner de Blob público.</span><span class="sxs-lookup"><span data-stu-id="31ddc-219">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="31ddc-220">Você pode ignorar esta seção se quiser usar os arquivos carregados.</span><span class="sxs-lookup"><span data-stu-id="31ddc-220">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="31ddc-221">O script HiveQL executará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="31ddc-221">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="31ddc-222">**Remova a tabela tweets_raw**, caso a tabela já exista.</span><span class="sxs-lookup"><span data-stu-id="31ddc-222">**Drop the tweets_raw table** in case the table already exists.</span></span>
2. <span data-ttu-id="31ddc-223">**Crie a tabela tweets_raw do Hive**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-223">**Create the tweets_raw Hive table**.</span></span> <span data-ttu-id="31ddc-224">Essa tabela Hive estruturada temporária contém os dados para mais processamento de ETL (extração, transformação e carregamento).</span><span class="sxs-lookup"><span data-stu-id="31ddc-224">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="31ddc-225">Para obter informações sobre partições, consulte o [tutorial do Hive][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="31ddc-225">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="31ddc-226">**Carregue os dados** da pasta de origem, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="31ddc-226">**Load data** from the source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="31ddc-227">O conjunto de dados grande de tweets aninhados no formato JSON agora foi transformado em uma estrutura de tabela temporária do Hive.</span><span class="sxs-lookup"><span data-stu-id="31ddc-227">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="31ddc-228">**Remova a tabela de tweets** , caso a tabela já exista.</span><span class="sxs-lookup"><span data-stu-id="31ddc-228">**Drop the tweets table** in case the table already exists.</span></span>
5. <span data-ttu-id="31ddc-229">**Crie a tabela de tweets**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-229">**Create the tweets table**.</span></span> <span data-ttu-id="31ddc-230">Antes de consultar o conjunto de dados de tweets usando o Hive, você precisa executar outro processo de ETL.</span><span class="sxs-lookup"><span data-stu-id="31ddc-230">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span></span> <span data-ttu-id="31ddc-231">Esse processo de ETL define um esquema de tabela mais detalhado para os dados armazenados na tabela "twitter_raw".</span><span class="sxs-lookup"><span data-stu-id="31ddc-231">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span></span>
6. <span data-ttu-id="31ddc-232">**Insira tabela de substituição**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-232">**Insert overwrite table**.</span></span> <span data-ttu-id="31ddc-233">Este script complexo do Hive iniciará um conjunto de longos trabalhos do MapReduce pelo cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="31ddc-233">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span></span> <span data-ttu-id="31ddc-234">Dependendo do seu conjunto de dados e do tamanho do cluster, o processo pode demorar cerca de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="31ddc-234">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="31ddc-235">**Insira diretório de substituição**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-235">**Insert overwrite directory**.</span></span> <span data-ttu-id="31ddc-236">Execute uma consulta e passe o conjunto de dados para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="31ddc-236">Run a query and output the dataset to a file.</span></span> <span data-ttu-id="31ddc-237">Essa consulta retornará uma lista de usuários do Twitter que enviou a maioria dos tweets que contêm a palavra "Azure".</span><span class="sxs-lookup"><span data-stu-id="31ddc-237">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span></span>

<span data-ttu-id="31ddc-238">**Para criar um script do Hive e carregá-lo para o Azure**</span><span class="sxs-lookup"><span data-stu-id="31ddc-238">**To create a Hive script and upload it to Azure**</span></span>

1. <span data-ttu-id="31ddc-239">Abra o ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31ddc-239">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="31ddc-240">Copie o seguinte script no painel de script:</span><span class="sxs-lookup"><span data-stu-id="31ddc-240">Copy the following script into the script pane:</span></span>

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="31ddc-241">Defina as duas primeiras variáveis no script:</span><span class="sxs-lookup"><span data-stu-id="31ddc-241">Set the first two variables in the script:</span></span>

   | <span data-ttu-id="31ddc-242">Variável</span><span class="sxs-lookup"><span data-stu-id="31ddc-242">Variable</span></span> | <span data-ttu-id="31ddc-243">Descrição</span><span class="sxs-lookup"><span data-stu-id="31ddc-243">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="31ddc-244">$clusterName</span><span class="sxs-lookup"><span data-stu-id="31ddc-244">$clusterName</span></span> |<span data-ttu-id="31ddc-245">Digite o nome do cluster HDInsight onde você deseja executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31ddc-245">Enter the HDInsight cluster name where you want to run the application.</span></span> |
   |  <span data-ttu-id="31ddc-246">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="31ddc-246">$subscriptionID</span></span> |<span data-ttu-id="31ddc-247">Insira sua ID da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="31ddc-247">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="31ddc-248">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="31ddc-248">$sourceDataPath</span></span> |<span data-ttu-id="31ddc-249">O local do armazenamento de Blob do Azure é onde as consultas de Hive lerão os dados.</span><span class="sxs-lookup"><span data-stu-id="31ddc-249">The Azure Blob storage location where the Hive queries will read the data from.</span></span> <span data-ttu-id="31ddc-250">Não é necessário alterar essa variável.</span><span class="sxs-lookup"><span data-stu-id="31ddc-250">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="31ddc-251">$outputPath</span><span class="sxs-lookup"><span data-stu-id="31ddc-251">$outputPath</span></span> |<span data-ttu-id="31ddc-252">O local de armazenamento de Blob do Azure onde as consultas de Hive produzirão os resultados.</span><span class="sxs-lookup"><span data-stu-id="31ddc-252">The Azure Blob storage location where the Hive queries will output the results.</span></span> <span data-ttu-id="31ddc-253">Não é necessário alterar essa variável.</span><span class="sxs-lookup"><span data-stu-id="31ddc-253">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="31ddc-254">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="31ddc-254">$hqlScriptFile</span></span> |<span data-ttu-id="31ddc-255">O local e o nome de arquivo do arquivo de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="31ddc-255">The location and the file name of the HiveQL script file.</span></span> <span data-ttu-id="31ddc-256">Não é necessário alterar essa variável.</span><span class="sxs-lookup"><span data-stu-id="31ddc-256">You don't need to change this variable.</span></span> |
4. <span data-ttu-id="31ddc-257">Pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="31ddc-257">Press **F5** to run the script.</span></span> <span data-ttu-id="31ddc-258">Se você tiver problemas, como alternativa, selecione todas as linhas e então pressione **F8**.</span><span class="sxs-lookup"><span data-stu-id="31ddc-258">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
5. <span data-ttu-id="31ddc-259">Você deverá ver a mensagem "Concluído!"</span><span class="sxs-lookup"><span data-stu-id="31ddc-259">You shall see "Complete!"</span></span> <span data-ttu-id="31ddc-260">no final da saída.</span><span class="sxs-lookup"><span data-stu-id="31ddc-260">at the end of the output.</span></span> <span data-ttu-id="31ddc-261">Qualquer mensagem de erro será exibida em vermelho.</span><span class="sxs-lookup"><span data-stu-id="31ddc-261">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="31ddc-262">Como procedimento de validação, você pode verificar o arquivo de saída, **/tutorials/twitter/twitter.hql**, em seu armazenamento de blob do Azure usando um gerenciador de armazenamento do Azure ou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="31ddc-262">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="31ddc-263">Para um exemplo de script do Windows PowerShell para listagem de arquivos, consulte [Usar o Armazenamento de Blobs com o HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="31ddc-263">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="31ddc-264">Processar os dados do Twitter usando o Hive</span><span class="sxs-lookup"><span data-stu-id="31ddc-264">Process Twitter data by using Hive</span></span>
<span data-ttu-id="31ddc-265">Você concluiu todo o trabalho de preparação.</span><span class="sxs-lookup"><span data-stu-id="31ddc-265">You have finished all the preparation work.</span></span> <span data-ttu-id="31ddc-266">Agora, você pode chamar o script do Hive e verificar os resultados.</span><span class="sxs-lookup"><span data-stu-id="31ddc-266">Now, you can invoke the Hive script and check the results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="31ddc-267">Enviar um trabalho do Hive</span><span class="sxs-lookup"><span data-stu-id="31ddc-267">Submit a Hive job</span></span>
<span data-ttu-id="31ddc-268">Use o seguinte script do Windows PowerShell para executar o script do Hive.</span><span class="sxs-lookup"><span data-stu-id="31ddc-268">Use the following Windows PowerShell script to run the Hive script.</span></span> <span data-ttu-id="31ddc-269">Você precisará definir a primeira variável.</span><span class="sxs-lookup"><span data-stu-id="31ddc-269">You will need to set the first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="31ddc-270">Para usar os tweets e o script HiveQL carregado nas duas últimas seções, defina $hqlScriptFile para "/tutorials/twitter/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="31ddc-270">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="31ddc-271">Para usar os que foram carregados em um blob público para você, defina $hqlScriptFile como "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="31ddc-271">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
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

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a><span data-ttu-id="31ddc-272">Verificar os resultados</span><span class="sxs-lookup"><span data-stu-id="31ddc-272">Check the results</span></span>
<span data-ttu-id="31ddc-273">Use o seguinte script do Windows PowerShell para verificar a saída de trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="31ddc-273">Use the following Windows PowerShell script to check the Hive job output.</span></span> <span data-ttu-id="31ddc-274">Você precisará definir as duas primeiras variáveis.</span><span class="sxs-lookup"><span data-stu-id="31ddc-274">You will need to set the first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
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
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> A tabela Hive usa \001 como o delimitador de campo. <span data-ttu-id="31ddc-276">O delimitador não é visível na saída.</span><span class="sxs-lookup"><span data-stu-id="31ddc-276">The delimiter is not visible in the output.</span></span>

<span data-ttu-id="31ddc-277">Depois que os resultados da análise tiverem sido colocados no armazenamento de BLOBs do Azure, é possível exportar os dados para um banco de dados SQL/SQL Server do Azure, exportar os dados para o Excel usando Power Query ou conectar seu aplicativo aos dados usando o Driver ODBC do Hive.</span><span class="sxs-lookup"><span data-stu-id="31ddc-277">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span></span> <span data-ttu-id="31ddc-278">Para obter mais informações, consulte [Usar Sqoop com HDInsight][hdinsight-use-sqoop], [Analisar os dados de atraso de voo usando o HDInsight][hdinsight-analyze-flight-delay-data], [Conectar o Excel ao HDInsight com o Power Query][hdinsight-power-query] e [Conectar o Excel ao HDInsight com o driver ODBC do Microsoft Hive][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="31ddc-278">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="31ddc-279">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31ddc-279">Next steps</span></span>
<span data-ttu-id="31ddc-280">Neste tutorial vimos como transformar o conjunto de dados não estruturado JSON em tabela estruturada do Hive para consultar, explorar e analisar dados do Twitter usando o HDInsight no Azure.</span><span class="sxs-lookup"><span data-stu-id="31ddc-280">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="31ddc-281">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="31ddc-281">To learn more, see:</span></span>

* <span data-ttu-id="31ddc-282">[Introdução ao HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="31ddc-282">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="31ddc-283">[Analisar sentimento no Twitter em tempo real com HBase no HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="31ddc-283">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="31ddc-284">[Analisar dados de atraso de voo usando o HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="31ddc-284">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="31ddc-285">[Conectar o Excel ao HDInsight com o Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="31ddc-285">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="31ddc-286">[Conectar o Excel ao HDInsight com o driver ODBC do Microsoft Hive][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="31ddc-286">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="31ddc-287">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="31ddc-287">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
