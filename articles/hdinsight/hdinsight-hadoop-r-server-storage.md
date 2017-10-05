---
title: "Soluções de Armazenamento do Azure para R Server no HDInsight – Azure | Microsoft Docs"
description: "Conheça as diferentes opções de armazenamento disponíveis para usuários com o Servidor R no HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="29120-103">Soluções de Armazenamento do Azure para R Server no HDInsight</span><span class="sxs-lookup"><span data-stu-id="29120-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="29120-104">O Microsoft R Server no HDInsight tem uma variedade de soluções de armazenamento para manter os dados, código ou objetos que contêm resultados da análise.</span><span class="sxs-lookup"><span data-stu-id="29120-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="29120-105">Elas incluem as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="29120-105">These include the following options:</span></span>

- [<span data-ttu-id="29120-106">Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="29120-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="29120-107">Armazenamento do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="29120-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="29120-108">Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="29120-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="29120-109">Você também tem a opção de acessar várias contas de armazenamento ou contêineres do Azure com o cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="29120-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="29120-110">O Armazenamento de Arquivos do Azure é uma opção de armazenamento de dados conveniente para uso no nó de borda, que permite a você montar um compartilhamento de arquivos do Armazenamento do Azure para, por exemplo, o sistema de arquivos do Linux.</span><span class="sxs-lookup"><span data-stu-id="29120-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="29120-111">Mas os compartilhamentos de arquivos do Azure podem ser montados e usados por qualquer sistema que tenha um SO com suporte, como Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="29120-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="29120-112">Ao criar um cluster Hadoop no HDInsight, você especifica uma conta de **Armazenamento do Azure** ou um **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="29120-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="29120-113">Um contêiner de armazenamento específico dessa conta mantém o sistema de arquivos do cluster que você cria (por exemplo, o Sistema de Arquivos Distribuído Hadoop).</span><span class="sxs-lookup"><span data-stu-id="29120-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="29120-114">Para obter mais informações e diretrizes, consulte:</span><span class="sxs-lookup"><span data-stu-id="29120-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="29120-115">Usar o Armazenamento do Azure com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="29120-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="29120-116">[Usar o Data Lake Store com clusters Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="29120-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="29120-117">Para obter mais informações sobre as soluções de Armazenamento do Azure, consulte: [Introdução ao Armazenamento do Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29120-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="29120-118">Para obter diretrizes sobre como selecionar a opção de armazenamento mais apropriada para usar em seu cenário, consulte [Decidindo quando usar Blobs do Azure, Arquivos do Azure ou Discos de Dados do Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="29120-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="29120-119">Usar várias contas de Armazenamento de Blobs do Azure com o R Server</span><span class="sxs-lookup"><span data-stu-id="29120-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="29120-120">Se necessário, você pode acessar várias contas de armazenamento ou contêineres do Azure com o cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="29120-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="29120-121">Para isso, você precisa especificar as contas de armazenamento adicionais a interface do usuário ao criar o cluster e, depois, seguir estas etapas para usá-las no R Server.</span><span class="sxs-lookup"><span data-stu-id="29120-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="29120-122">Para fins de desempenho, o cluster HDInsight é criado no mesmo datacenter que a conta de armazenamento primária especificada.</span><span class="sxs-lookup"><span data-stu-id="29120-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="29120-123">Não há suporte para o uso de uma conta de armazenamento em um local diferente do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29120-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="29120-124">Crie um cluster HDInsight com um nome de conta de armazenamento de **storage1** e um contêiner padrão chamado **container1**.</span><span class="sxs-lookup"><span data-stu-id="29120-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="29120-125">Especifique uma conta de armazenamento adicional chamada **storage2**.</span><span class="sxs-lookup"><span data-stu-id="29120-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="29120-126">Copie o arquivo mycsv.csv para o diretório /share e execute a análise nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="29120-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="29120-127">No código R, defina o nó do nome como **default** e defina o diretório e arquivo a serem processados.</span><span class="sxs-lookup"><span data-stu-id="29120-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="29120-128">Todas as referências de diretório e arquivo apontam para a conta de armazenamento wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="29120-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="29120-129">Essa é a **conta de armazenamento padrão** associada ao cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29120-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="29120-130">Agora, suponha que você queira processar um arquivo chamado mySpecial.csv, localizado no diretório /private de **container2** em **storage2**.</span><span class="sxs-lookup"><span data-stu-id="29120-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="29120-131">No código R, aponte a referência de nó de nome para a conta de armazenamento **storage2** .</span><span class="sxs-lookup"><span data-stu-id="29120-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="29120-132">Todas as referências de diretório e arquivo agora apontam para a conta de armazenamento wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="29120-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="29120-133">Esse é o **Nome de Nó** que você especificou.</span><span class="sxs-lookup"><span data-stu-id="29120-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="29120-134">Você precisa configurar o diretório /user/RevoShare/<SSH username> no **storage2** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="29120-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="29120-135">Usar um Azure Data Lake Store com o R Server</span><span class="sxs-lookup"><span data-stu-id="29120-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="29120-136">Para usar repositórios Data Lake com sua conta do HDInsight, você precisa dar ao cluster acesso a cada repositório do Azure Data Lake que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="29120-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="29120-137">Para obter instruções sobre como usar o Portal do Azure pra criar um cluster HDInsight com uma conta do Azure Data Lake Store como armazenamento padrão ou um repositório adicional, veja [Criar um cluster HDInsight com o Data Lake Store usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29120-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="29120-138">Você usa o repositório no script R de forma semelhante a como você fez com uma conta de armazenamento do Azure secundária, conforme descrito no procedimento anterior.</span><span class="sxs-lookup"><span data-stu-id="29120-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="29120-139">Adicionar acesso de cluster aos repositórios Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="29120-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="29120-140">Você pode acessar um repositório Data Lake usando uma Entidade de Serviço do Azure AD (Azure Active Directory) que está associada ao cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29120-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="29120-141">Para adicionar uma Entidade de Serviço do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="29120-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="29120-142">Ao criar o cluster do HDInsight, selecione **Identidade do Cluster AAD** na guia **Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="29120-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="29120-143">Na caixa de diálogo **Identidade de Cluster AAD**, em **Selecionar Entidade de Serviço do AD**, selecione **Criar novo**.</span><span class="sxs-lookup"><span data-stu-id="29120-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="29120-144">Depois de dar um nome à Entidade de Serviço e criar uma senha para ela, clique em **Gerenciar Acesso de ADLS** para associar a Entidade de Serviço aos seus repositórios Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="29120-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="29120-145">Também é possível adicionar o acesso do cluster a um ou mais Data Lake Stores após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="29120-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="29120-146">Abra a entrada do Portal do Azure para um Data Lake Store e vá para **Data Explorer > Acessar > Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="29120-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="29120-147">Como acessar o Data Lake Store do R Server</span><span class="sxs-lookup"><span data-stu-id="29120-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="29120-148">Após obter acesso a um repositório Data Lake, você pode usar o repositório no Servidor R no HDInsight da forma como faria com uma conta de armazenamento do Azure secundária.</span><span class="sxs-lookup"><span data-stu-id="29120-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="29120-149">A única diferença é que o prefixo **wasb://** se altera para **adl://** como segue:</span><span class="sxs-lookup"><span data-stu-id="29120-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="29120-150">Os comandos a seguir são usados para configurar a conta de armazenamento Data Lake com o diretório RevoShare e adicionar o arquivo .csv de exemplo do exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="29120-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="29120-151">Usar o Armazenamento de Arquivos do Azure com o R Server</span><span class="sxs-lookup"><span data-stu-id="29120-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="29120-152">Também há uma opção de armazenamento de dados conveniente para uso no nó de borda, chamada [Arquivos do Azure]((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="29120-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="29120-153">Esse recurso permite montar um compartilhamento de arquivos do Armazenamento do Azure para o sistema de arquivos do Linux.</span><span class="sxs-lookup"><span data-stu-id="29120-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="29120-154">Essa opção pode ser útil para armazenar arquivos de dados, scripts R e objetos de resultado que podem ser necessários posteriormente, especialmente quando fizer sentido usar o sistema de arquivos nativo no nó de borda em vez do HDFS.</span><span class="sxs-lookup"><span data-stu-id="29120-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="29120-155">Uma grande vantagem dos Arquivos do Azure é que os compartilhamentos de arquivos podem ser montados e usados por qualquer sistema que tenha um sistema operacional com suporte, como Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="29120-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="29120-156">Por exemplo, ele pode ser usado por outro cluster do HDInsight que você ou alguém em sua equipe tenha, por uma VM do Azure ou até mesmo por um sistema local.</span><span class="sxs-lookup"><span data-stu-id="29120-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="29120-157">Para obter mais informações, confira:</span><span class="sxs-lookup"><span data-stu-id="29120-157">For more information, see:</span></span>

- [<span data-ttu-id="29120-158">Como utilizar o Armazenamento de Arquivos do Azure com Linux</span><span class="sxs-lookup"><span data-stu-id="29120-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="29120-159">Como utilizar o Armazenamento de Arquivos do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="29120-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="29120-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29120-160">Next steps</span></span>

<span data-ttu-id="29120-161">Agora que você entende as opções de armazenamento do Azure, use os links a seguir para descobrir maneiras de realizar tarefas de ciência de dados com o R Server no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29120-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="29120-162">Visão geral do Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="29120-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="29120-163">Get started with R server on Hadoop (Introdução ao servidor R no Hadoop)</span><span class="sxs-lookup"><span data-stu-id="29120-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="29120-164">Adicionar Servidor do RStudio ao HDInsight (se não instalado durante a criação de cluster)</span><span class="sxs-lookup"><span data-stu-id="29120-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="29120-165">Opções de contexto de computação para o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="29120-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

