---
title: Usar modelos do Azure para criar o HDInsight e o Data Lake Store | Microsoft Docs
description: Usar modelos do Resource Manager do Azure para criar e usar clusters HDInsight com o Azure Data Lake Store
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
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="da13c-103">Criar o cluster HDInsight com o Data Lake Store usando o modelo do Resource Manager do Azure</span><span class="sxs-lookup"><span data-stu-id="da13c-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da13c-104">Usando o Portal</span><span class="sxs-lookup"><span data-stu-id="da13c-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="da13c-105">Usando o PowerShell (para o armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="da13c-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="da13c-106">Usando o PowerShell (para o armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="da13c-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="da13c-107">Usando o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="da13c-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="da13c-108">Aprenda a usar o Azure PowerShell para configurar um cluster HDInsight com o Azure Data Lake Store **como o armazenamento adicional**.</span><span class="sxs-lookup"><span data-stu-id="da13c-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="da13c-109">Para tipos de cluster compatíveis, o Data Lake Store pode ser usado como um armazenamento padrão ou uma conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="da13c-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="da13c-110">Quando o Data Lake Store é usado como armazenamento adicional, a conta de armazenamento padrão para os clusters ainda será Blobs de Armazenamento do Azure (WASB) e os arquivos relacionados ao cluster (como logs, etc.) ainda serão gravados no armazenamento padrão, embora os dados que você queira processar possam ser armazenados em uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="da13c-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="da13c-111">O uso do Repositório Data Lake como uma conta de armazenamento adicional não afeta o desempenho ou a capacidade de leitura/gravação no armazenamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="da13c-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="da13c-112">Usando o Data Lake Store para armazenamento do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="da13c-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="da13c-113">Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="da13c-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="da13c-114">A opção para criar clusters HDInsight com acesso ao Data Lake Store como armazenamento padrão está disponível para o HDInsight versão 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="da13c-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="da13c-115">A opção para criar clusters HDInsight com acesso ao Data Lake Store como armazenamento adicional está disponível para o HDInsight versões 3.2, 3.4, 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="da13c-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="da13c-116">Neste artigo, provisionaremos um cluster Hadoop com o Repositório Data Lake como armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="da13c-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="da13c-117">Para obter instruções sobre como criar um cluster Hadoop com o Data Lake Store como armazenamento padrão, veja [Criar um cluster HDInsight com o Data Lake Store usando o Portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="da13c-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da13c-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da13c-118">Prerequisites</span></span>
<span data-ttu-id="da13c-119">Antes de começar este tutorial, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="da13c-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="da13c-120">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="da13c-120">**An Azure subscription**.</span></span> <span data-ttu-id="da13c-121">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da13c-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="da13c-122">**Azure PowerShell 1.0 ou superior**.</span><span class="sxs-lookup"><span data-stu-id="da13c-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="da13c-123">Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da13c-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="da13c-124">**Entidade de serviço do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="da13c-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="da13c-125">As etapas neste tutorial fornecem instruções sobre como criar uma entidade de serviço no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da13c-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="da13c-126">No entanto, você deve ser administrador do Azure AD para poder criar uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="da13c-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="da13c-127">Se você for administrador do Azure AD, poderá ignorar esse pré-requisito e continuar com o tutorial.</span><span class="sxs-lookup"><span data-stu-id="da13c-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="da13c-128">**Se você não for um administrador do Azure AD**, não poderá executar as etapas necessárias para criar uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="da13c-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="da13c-129">Nesse caso, o administrador do Azure AD deverá primeiro criar uma entidade de serviço antes de criar um cluster HDInsight com Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="da13c-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="da13c-130">Além disso, a entidade de serviço deve ser criada usando um certificado, conforme descrito em [Criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="da13c-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="da13c-131">Criar um cluster HDInsight com o Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da13c-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="da13c-132">O modelo do Resource Manager e os pré-requisitos para usar o modelo estão disponíveis no GitHub em [Implantar um cluster HDInsight Linux com o novo Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="da13c-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="da13c-133">Siga as instruções fornecidas neste link para criar um cluster HDInsight com o Azure Data Lake Store como o armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="da13c-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="da13c-134">As instruções no link mencionado acima exigem o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da13c-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="da13c-135">Antes de iniciar as instruções, verifique se você está conectado com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="da13c-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="da13c-136">Na área de trabalho, abra uma nova janela do Azure PowerShell e insira o trecho a seguir.</span><span class="sxs-lookup"><span data-stu-id="da13c-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="da13c-137">Quando solicitado a fazer logon, lembre-se de fazer logon como o proprietário ou um dos administradores da assinatura:</span><span class="sxs-lookup"><span data-stu-id="da13c-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="da13c-138">Carregue os exemplos de dados no Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da13c-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="da13c-139">O modelo do Resource Manager cria uma nova conta do Data Lake Store e associa-a com o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da13c-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="da13c-140">Você deve carregar alguns dados de exemplo no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="da13c-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="da13c-141">Você precisará desses dados posteriormente no tutorial para executar trabalhos de um cluster HDInsight que acessa dados no repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da13c-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="da13c-142">Para obter instruções sobre como carregar dados, consulte [Carregar um arquivo no Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="da13c-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="da13c-143">Se estiver procurando alguns dados de exemplo para carregar, é possível obter a pasta **Dados da Ambulância** no [Repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="da13c-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="da13c-144">Definir ACLs relevantes nos dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="da13c-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="da13c-145">Para verificar se os dados de exemplo que você carregou estão acessíveis do cluster HDInsight, você deverá garantir que o aplicativo do Azure AD que é usado para estabelecer a identidade entre o cluster HDInsight e o Data Lake Store tem acesso para o arquivo/pasta que você está tentando acessar.</span><span class="sxs-lookup"><span data-stu-id="da13c-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="da13c-146">Para fazer isso, execute as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="da13c-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="da13c-147">Localize o nome do aplicativo do Azure AD que está associado ao cluster HDInsight e o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="da13c-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="da13c-148">Uma maneira para procurar o nome é abrir a folha do cluster HDInsight que você criou usando o modelo do Resource Manager, clique na guia **Identidade do Cluster AAD** e procure o valor do **Nome de exibição da entidade de serviço**.</span><span class="sxs-lookup"><span data-stu-id="da13c-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="da13c-149">Agora, forneça acesso a esse aplicativo do Azure AD no arquivo/pasta que você deseja acessar do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da13c-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="da13c-150">Para definir as ACLs certas no arquivo/pasta no Data Lake Store, consulte [Protegendo dados no Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="da13c-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="da13c-151">Executar trabalhos de teste no cluster HDInsight para usar o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="da13c-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="da13c-152">Após a configuração de um cluster HDInsight, você poderá executar trabalhos de teste no cluster a fim de testar se o cluster HDInsight pode acessar o Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da13c-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="da13c-153">Para fazer isso, executaremos um exemplo de trabalho do Hive que cria uma tabela usando os exemplos de dados que você carregou anteriormente em seu Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da13c-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="da13c-154">Nesta seção, você acessará um cluster Linux HDInsight por SSH e executará uma consulta Hive de exemplo.</span><span class="sxs-lookup"><span data-stu-id="da13c-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="da13c-155">Se você está usando um cliente Windows, é recomendável usar o **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="da13c-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="da13c-156">Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="da13c-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="da13c-157">Uma vez conectado, inicie a CLI do Hive usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="da13c-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="da13c-158">Usando a CLI, insira as instruções a seguir para criar uma nova tabela chamada **vehicles** usando os dados de exemplo no Repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="da13c-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="da13c-159">Você deverá ver um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="da13c-159">You should see an output similar to the following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="da13c-160">Repositório Data Lake usando comandos do HDFS</span><span class="sxs-lookup"><span data-stu-id="da13c-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="da13c-161">Após a configuração do cluster HDInsight para usar o Repositório Data Lake, você poderá usar os comandos do shell HDFS para acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="da13c-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="da13c-162">Nesta seção, você acessará um cluster Linux HDInsight por SSH e executará comandos do HDFS.</span><span class="sxs-lookup"><span data-stu-id="da13c-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="da13c-163">Se você está usando um cliente Windows, é recomendável usar o **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="da13c-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="da13c-164">Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="da13c-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="da13c-165">Uma vez conectado, use o comando do sistema de arquivos HDFS a seguir para listar os arquivos no Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da13c-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="da13c-166">Isso deve listar o arquivo carregado anteriormente no Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da13c-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="da13c-167">Você também pode usar o comando `hdfs dfs -put` para carregar alguns arquivos no Repositório Data Lake e usar `hdfs dfs -ls` para verificar se os arquivos foram carregados com êxito.</span><span class="sxs-lookup"><span data-stu-id="da13c-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="da13c-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da13c-168">Next steps</span></span>
* [<span data-ttu-id="da13c-169">Copiar dados de Armazenamento de Blobs do Azure para o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da13c-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
