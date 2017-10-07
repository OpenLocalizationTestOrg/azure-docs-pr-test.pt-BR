---
title: "soluções de armazenamento aaaAzure R Server no HDInsight - Azure | Microsoft Docs"
description: "Saiba mais sobre Olá armazenamento diferentes opções disponíveis toousers ao servidor do R no HDInsight"
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
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="7b8f0-103">Soluções de Armazenamento do Azure para R Server no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b8f0-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="7b8f0-104">Microsoft R Server no HDInsight tem uma variedade de dados de toopersist de soluções de armazenamento, código ou objetos que contêm resultados da análise.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="7b8f0-105">Eles incluem hello as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b8f0-105">These include hello following options:</span></span>

- [<span data-ttu-id="7b8f0-106">Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="7b8f0-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="7b8f0-107">Armazenamento do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="7b8f0-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="7b8f0-108">Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="7b8f0-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="7b8f0-109">Você também tem a opção de saudação do acesso a várias contas de armazenamento do Azure ou contêineres com o grupo HDI.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="7b8f0-110">Armazenamento de arquivo do Azure é uma opção de armazenamento de dados conveniente para uso no nó de borda Olá que permite que você toomount um compartilhamento de arquivos de armazenamento do Azure para, por exemplo, Olá Linux sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="7b8f0-111">Mas os compartilhamentos de arquivos do Azure podem ser montados e usados por qualquer sistema que tenha um SO com suporte, como Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="7b8f0-112">Ao criar um cluster Hadoop no HDInsight, você especifica uma conta de **Armazenamento do Azure** ou um **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="7b8f0-113">Um contêiner de armazenamento específico dessa conta contém do sistema de arquivo hello para cluster Olá criados por você (por exemplo, Olá Hadoop o sistema de arquivos distribuído).</span><span class="sxs-lookup"><span data-stu-id="7b8f0-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="7b8f0-114">Para obter mais informações e diretrizes, consulte:</span><span class="sxs-lookup"><span data-stu-id="7b8f0-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="7b8f0-115">Usar o Armazenamento do Azure com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b8f0-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="7b8f0-116">[Usar o Data Lake Store com clusters Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="7b8f0-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="7b8f0-117">Para obter mais informações sobre soluções de armazenamento do Azure hello, consulte [tooMicrosoft Introdução armazenamento do Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b8f0-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="7b8f0-118">Para obter orientação sobre como selecionar a opção toouse de armazenamento mais apropriado Olá para seu cenário, consulte [Decidindo quando toouse Azure Blobs, arquivos do Azure ou discos de dados do Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="7b8f0-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="7b8f0-119">Usar várias contas de Armazenamento de Blobs do Azure com o R Server</span><span class="sxs-lookup"><span data-stu-id="7b8f0-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="7b8f0-120">Se necessário, você pode acessar várias contas de armazenamento ou contêineres do Azure com o cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="7b8f0-121">toodo assim, você precisa toospecify hello mais contas de armazenamento no hello da interface do usuário quando você cria o cluster hello e, em seguida, siga estas etapas toouse com R Server.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="7b8f0-122">Por motivos de desempenho, Olá cluster HDInsight é criado no hello mesmo data center da conta de armazenamento primário Olá que você especificar.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="7b8f0-123">Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá um local diferente.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="7b8f0-124">Crie um cluster HDInsight com um nome de conta de armazenamento de **storage1** e um contêiner padrão chamado **container1**.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="7b8f0-125">Especifique uma conta de armazenamento adicional chamada **storage2**.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="7b8f0-126">Copiar Olá mycsv.csv arquivo toohello /share diretório e executar uma análise em arquivo.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="7b8f0-127">No código de R, defina o nó de nome hello muito**padrão,** e defina seu tooprocess de arquivo e diretório.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="7b8f0-128">Todos Olá conta de armazenamento do arquivo e diretório referências ponto toohello wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="7b8f0-129">Isso é hello **conta de armazenamento padrão** associado a cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="7b8f0-130">Agora, vamos supor que você deseja tooprocess um arquivo chamado mySpecial.csv localizado em Olá /private diretório de **container2** na **Armazenamento2 do**.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="7b8f0-131">Em seu código R, aponte Olá nome nó referência toohello **Armazenamento2 do** conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="7b8f0-132">Todos os Olá diretório e arquivo referências agora toohello ponto da conta de armazenamento wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="7b8f0-133">Isso é hello **nome do nó** que você especificou.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="7b8f0-134">Você tem tooconfigure Olá /user RevoShare/<SSH username> do **Armazenamento2 do** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7b8f0-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="7b8f0-135">Usar um Azure Data Lake Store com o R Server</span><span class="sxs-lookup"><span data-stu-id="7b8f0-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="7b8f0-136">toouse Data Lake armazena com sua conta de HDInsight, é necessário toogive seu repositório Azure Data Lake do cluster acesso tooeach que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="7b8f0-137">Para obter instruções sobre como toouse Olá toocreate portal do Azure um HDInsight cluster com uma conta do repositório Azure Data Lake como armazenamento padrão da saudação ou como um armazenamento adicional, consulte [criar um cluster HDInsight com repositório Data Lake usando o portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b8f0-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="7b8f0-138">Você, em seguida, usar Olá armazenamento em seu script R muito como você fez uma conta de armazenamento do Azure secundário, conforme descrito no procedimento anterior hello.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="7b8f0-139">Adicionar tooyour de acesso do cluster do Azure Data Lake armazena</span><span class="sxs-lookup"><span data-stu-id="7b8f0-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="7b8f0-140">Você pode acessar um repositório Data Lake usando uma Entidade de Serviço do Azure AD (Azure Active Directory) que está associada ao cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="7b8f0-141">tooadd uma entidade de serviço do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="7b8f0-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="7b8f0-142">Quando você cria seu cluster HDInsight, selecione **Cluster AAD identidade** de saudação **fonte de dados** guia.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="7b8f0-143">Em Olá **Cluster AAD identidade** caixa de diálogo **Selecione entidade de serviço do AD**, selecione **criar novo**.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="7b8f0-144">Depois que você nomeie Olá entidade de serviço e cria uma senha para ele, clique em **gerenciar o acesso de ADLS** tooassociate Olá armazena da entidade de serviço com o Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="7b8f0-145">Também é possível tooadd cluster acesso tooone ou mais Data Lake armazena após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="7b8f0-146">Abra Olá entrada portal do Azure para um repositório Data Lake e vá muito**Data Explorer > acesso > Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="7b8f0-147">Como tooaccess Olá repositório Data Lake do servidor de R</span><span class="sxs-lookup"><span data-stu-id="7b8f0-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="7b8f0-148">Depois que você deu a acessar o repositório de Data Lake tooa, você pode usar o repositório Olá R Server em HDInsight hello como uma conta de armazenamento do Azure secundário.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="7b8f0-149">Olá somente a diferença é o prefixo Olá **wasb: / /** muda muito**publicitário: / /** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7b8f0-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="7b8f0-150">Olá comandos a seguir são usados tooconfigure Olá conta de armazenamento do Data Lake com o diretório de RevoShare Olá e adicione CSV de exemplo hello do exemplo anterior hello:</span><span class="sxs-lookup"><span data-stu-id="7b8f0-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="7b8f0-151">Usar o Armazenamento de Arquivos do Azure com o R Server</span><span class="sxs-lookup"><span data-stu-id="7b8f0-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="7b8f0-152">Também é uma opção de armazenamento de dados conveniente para uso no nó de borda Olá chamado [arquivos do Azure] ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="7b8f0-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="7b8f0-153">Ele permite toomount um toohello de compartilhamento de arquivo de armazenamento do Azure sistema de arquivos do Linux.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="7b8f0-154">Esta opção pode ser útil para armazenar arquivos de dados, os scripts de R e objetos de resultado que talvez sejam necessárias mais tarde, especialmente quando ele torna o sistema de arquivos nativo sentido toouse Olá no nó de borda de saudação em vez do HDFS.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="7b8f0-155">A principal vantagem dos arquivos do Azure é um arquivo hello compartilhamentos podem ser montados e usados por qualquer sistema que tenha um sistema operacional com suporte, como Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="7b8f0-156">Por exemplo, ele pode ser usado por outro cluster do HDInsight que você ou alguém em sua equipe tenha, por uma VM do Azure ou até mesmo por um sistema local.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="7b8f0-157">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="7b8f0-157">For more information, see:</span></span>

- [<span data-ttu-id="7b8f0-158">Como toouse armazenamento de arquivo do Azure com Linux</span><span class="sxs-lookup"><span data-stu-id="7b8f0-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="7b8f0-159">Como toouse armazenamento de arquivo do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="7b8f0-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="7b8f0-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b8f0-160">Next steps</span></span>

<span data-ttu-id="7b8f0-161">Agora que você entende as opções de armazenamento do Azure hello, os links de uso a seguir Olá toodiscover maneiras de obter as tarefas de ciência de dados feitas com o servidor do R no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b8f0-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="7b8f0-162">Visão geral do Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b8f0-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="7b8f0-163">Get started with R server on Hadoop (Introdução ao servidor R no Hadoop)</span><span class="sxs-lookup"><span data-stu-id="7b8f0-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="7b8f0-164">Adicionar servidor RStudio tooHDInsight (se não adicionado durante a criação do cluster)</span><span class="sxs-lookup"><span data-stu-id="7b8f0-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="7b8f0-165">Opções de contexto de computação para o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b8f0-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

