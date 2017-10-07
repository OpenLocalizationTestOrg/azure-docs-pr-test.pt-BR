---
title: "aaaUse toocreate de modelos do Azure HDInsight e repositório Data Lake | Microsoft Docs"
description: "Use o Gerenciador de recursos do Azure modelos toocreate e usar clusters de HDInsight com repositório Azure Data Lake"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="e6215-103">Criar o cluster HDInsight com o Data Lake Store usando o modelo do Resource Manager do Azure</span><span class="sxs-lookup"><span data-stu-id="e6215-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6215-104">Usando o Portal</span><span class="sxs-lookup"><span data-stu-id="e6215-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="e6215-105">Usando o PowerShell (para o armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="e6215-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="e6215-106">Usando o PowerShell (para o armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="e6215-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="e6215-107">Usando o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="e6215-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="e6215-108">Saiba como toouse do Azure PowerShell tooconfigure um HDInsight cluster com repositório Azure Data Lake, **como armazenamento adicional**.</span><span class="sxs-lookup"><span data-stu-id="e6215-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="e6215-109">Para tipos de cluster compatíveis, o Data Lake Store pode ser usado como um armazenamento padrão ou uma conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="e6215-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="e6215-110">Quando o repositório Data Lake é usado como armazenamento adicional, conta de armazenamento padrão Olá para clusters de saudação ainda estará Blobs de armazenamento do Azure (WASB) e arquivos relacionados ao cluster de saudação (como logs, etc.) são gravados ainda armazenamento padrão de toohello, enquanto os dados de saudação que você deseja tooprocess podem ser armazenados em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e6215-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="e6215-111">Usando o repositório Data Lake como uma conta de armazenamento adicional não afeta o desempenho e o hello capacidade tooread/gravação toohello armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e6215-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="e6215-112">Usando o Data Lake Store para armazenamento do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6215-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="e6215-113">Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="e6215-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="e6215-114">Clusters de HDInsight toocreate opção com acesso tooData Lake repositório como armazenamento padrão está disponível para HDInsight versão 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="e6215-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="e6215-115">Clusters de HDInsight toocreate opção com acesso tooData Lake repositório como armazenamento adicional está disponível para HDInsight versões 3.2, 3.4, 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="e6215-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="e6215-116">Neste artigo, provisionaremos um cluster Hadoop com o Repositório Data Lake como armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="e6215-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="e6215-117">Para obter instruções sobre como toocreate um Hadoop de cluster com o repositório Data Lake como armazenamento padrão, consulte [criar um cluster HDInsight com repositório Data Lake usando o Portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6215-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6215-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e6215-118">Prerequisites</span></span>
<span data-ttu-id="e6215-119">Antes de começar este tutorial, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e6215-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="e6215-120">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e6215-120">**An Azure subscription**.</span></span> <span data-ttu-id="e6215-121">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6215-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e6215-122">**Azure PowerShell 1.0 ou superior**.</span><span class="sxs-lookup"><span data-stu-id="e6215-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="e6215-123">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e6215-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e6215-124">**Entidade de serviço do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e6215-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="e6215-125">As etapas deste tutorial fornecem instruções sobre como toocreate uma entidade de serviço no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6215-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="e6215-126">No entanto, você deve ser um toocreate capaz do AD do Azure administrador toobe uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="e6215-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="e6215-127">Se você for um administrador do AD do Azure, você pode ignorar esse pré-requisito e continuar com o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="e6215-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="e6215-128">**Se você não for um administrador do AD do Azure**, não será capaz de tooperform Olá etapas necessárias toocreate uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="e6215-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="e6215-129">Nesse caso, o administrador do Azure AD deverá primeiro criar uma entidade de serviço antes de criar um cluster HDInsight com Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e6215-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="e6215-130">Além disso, Olá entidade de serviço deve ser criada usando um certificado, conforme descrito em [criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="e6215-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="e6215-131">Criar um cluster HDInsight com o Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e6215-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="e6215-132">modelo do Gerenciador de recursos de saudação e Olá pré-requisitos para usar o modelo de hello, estão disponíveis no GitHub em [implantar um cluster HDInsight Linux com o novo repositório do Data Lake](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="e6215-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="e6215-133">Siga as instruções de Olá fornecidas no toocreate link um cluster HDInsight com repositório Azure Data Lake como armazenamento adicional da saudação.</span><span class="sxs-lookup"><span data-stu-id="e6215-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="e6215-134">instruções de Olá Olá link mencionados acima exigem o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6215-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="e6215-135">Antes de iniciar as instruções, verifique se que você fizer logon no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6215-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="e6215-136">Na área de trabalho, abra uma nova janela do PowerShell do Azure e insira Olá trechos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e6215-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="e6215-137">Quando solicitada toolog, certifique-se de você fazer logon como uma saudação admininistrators/proprietário da assinatura:</span><span class="sxs-lookup"><span data-stu-id="e6215-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="e6215-138">Carregar repositório exemplo dados toohello Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e6215-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="e6215-139">modelo do Gerenciador de recursos de saudação cria uma nova conta do repositório Data Lake e associa ao cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e6215-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="e6215-140">Agora, você deve carregar alguns dados de exemplo toohello repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e6215-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="e6215-141">Você precisará esses dados posteriormente em trabalhos toorun tutorial Olá de um cluster HDInsight que acessam dados em Olá repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e6215-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="e6215-142">Para obter instruções sobre como tooupload dados, consulte [carregar um arquivo tooyour repositório Data Lake](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="e6215-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="e6215-143">Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="e6215-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="e6215-144">Definir ACLs relevantes em dados de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="e6215-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="e6215-145">toomake se os dados de exemplo hello que você carregar são acessíveis do cluster do HDInsight hello, você deve garantir que o aplicativo hello AD do Azure que é a identidade tooestablish usado entre o cluster do HDInsight hello e repositório Data Lake tenha acesso toohello arquivo/pasta é a tentativa de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e6215-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="e6215-146">toodo isso, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e6215-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="e6215-147">Localize o nome de saudação do hello aplicativo AD do Azure que está associado ao cluster HDInsight e Olá repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e6215-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="e6215-148">Toolook unidirecional para nome hello é criada usando o modelo do Gerenciador de recursos de saudação folha de cluster tooopen Olá HDInsight, clique em Olá **Cluster AAD identidade** guia e procure o valor de saudação do **entidade de serviço Nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="e6215-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="e6215-149">Agora, fornecem acesso toothis aplicativo AD do Azure no hello arquivo/pasta que você deseja tooaccess do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e6215-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="e6215-150">o direito de saudação de tooset ACLs Olá arquivo/pasta no repositório Data Lake, consulte [proteção de dados no repositório Data Lake](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="e6215-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="e6215-151">Executar trabalhos de teste em Olá HDInsight cluster toouse Olá repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="e6215-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="e6215-152">Depois de configurar um cluster HDInsight, você pode executar trabalhos de teste em Olá cluster tootest que Olá HDInsight cluster pode acessar o repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e6215-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="e6215-153">toodo assim, iremos executar um trabalho de Hive de exemplo que cria uma tabela usando dados de exemplo hello que você carregou anteriormente repositório tooyour Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e6215-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="e6215-154">Nesta seção, você vai SSH em um cluster HDInsight Linux e execução Olá um exemplo de consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="e6215-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="e6215-155">Se você está usando um cliente Windows, é recomendável usar o **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="e6215-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="e6215-156">Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e6215-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="e6215-157">Uma vez conectado, inicie Olá CLI do Hive usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6215-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="e6215-158">Usando Olá CLI, insira Olá seguindo as instruções toocreate uma nova tabela nomeada **veículos** com dados de exemplo hello Olá repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="e6215-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="e6215-159">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6215-159">You should see an output similar toohello following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="e6215-160">Repositório Data Lake usando comandos do HDFS</span><span class="sxs-lookup"><span data-stu-id="e6215-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="e6215-161">Quando você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello, você pode usar comandos de shell do hello HDFS tooaccess Olá repositório.</span><span class="sxs-lookup"><span data-stu-id="e6215-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="e6215-162">Nesta seção, você vai SSH em um cluster HDInsight Linux e execução Olá comandos HDFS.</span><span class="sxs-lookup"><span data-stu-id="e6215-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="e6215-163">Se você está usando um cliente Windows, é recomendável usar o **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="e6215-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="e6215-164">Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e6215-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="e6215-165">Uma vez conectado, use Olá arquivos HDFS filesystem comando toolist Olá no hello repositório Data Lake a seguir.</span><span class="sxs-lookup"><span data-stu-id="e6215-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="e6215-166">Isso deve listar arquivo hello que você carregou anteriormente repositório toohello Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e6215-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="e6215-167">Você também pode usar o hello `hdfs dfs -put` comando tooupload toohello alguns arquivos repositório Data Lake e, em seguida, usar `hdfs dfs -ls` tooverify arquivos Olá foram carregados com êxito.</span><span class="sxs-lookup"><span data-stu-id="e6215-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e6215-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6215-168">Next steps</span></span>
* [<span data-ttu-id="e6215-169">Copiar dados do repositório Azure armazenamento de Blobs tooData Lake</span><span class="sxs-lookup"><span data-stu-id="e6215-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
