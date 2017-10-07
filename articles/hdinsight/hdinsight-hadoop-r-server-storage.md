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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Soluções de Armazenamento do Azure para R Server no HDInsight

Microsoft R Server no HDInsight tem uma variedade de dados de toopersist de soluções de armazenamento, código ou objetos que contêm resultados da análise. Eles incluem hello as opções a seguir:

- [Blob do Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Armazenamento do Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/)
- [Armazenamento de Arquivos do Azure](https://azure.microsoft.com/services/storage/files/)

Você também tem a opção de saudação do acesso a várias contas de armazenamento do Azure ou contêineres com o grupo HDI. Armazenamento de arquivo do Azure é uma opção de armazenamento de dados conveniente para uso no nó de borda Olá que permite que você toomount um compartilhamento de arquivos de armazenamento do Azure para, por exemplo, Olá Linux sistema de arquivos. Mas os compartilhamentos de arquivos do Azure podem ser montados e usados por qualquer sistema que tenha um SO com suporte, como Windows ou Linux. 

Ao criar um cluster Hadoop no HDInsight, você especifica uma conta de **Armazenamento do Azure** ou um **Data Lake Store**. Um contêiner de armazenamento específico dessa conta contém do sistema de arquivo hello para cluster Olá criados por você (por exemplo, Olá Hadoop o sistema de arquivos distribuído). Para obter mais informações e diretrizes, consulte:

- [Usar o Armazenamento do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Usar o Data Lake Store com clusters Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md). 

Para obter mais informações sobre soluções de armazenamento do Azure hello, consulte [tooMicrosoft Introdução armazenamento do Azure](../storage/common/storage-introduction.md). 

Para obter orientação sobre como selecionar a opção toouse de armazenamento mais apropriado Olá para seu cenário, consulte [Decidindo quando toouse Azure Blobs, arquivos do Azure ou discos de dados do Azure](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Usar várias contas de Armazenamento de Blobs do Azure com o R Server

Se necessário, você pode acessar várias contas de armazenamento ou contêineres do Azure com o cluster HDI. toodo assim, você precisa toospecify hello mais contas de armazenamento no hello da interface do usuário quando você cria o cluster hello e, em seguida, siga estas etapas toouse com R Server.

> [!WARNING]
> Por motivos de desempenho, Olá cluster HDInsight é criado no hello mesmo data center da conta de armazenamento primário Olá que você especificar. Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá um local diferente.

1. Crie um cluster HDInsight com um nome de conta de armazenamento de **storage1** e um contêiner padrão chamado **container1**.
2. Especifique uma conta de armazenamento adicional chamada **storage2**.  
3. Copiar Olá mycsv.csv arquivo toohello /share diretório e executar uma análise em arquivo.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. No código de R, defina o nó de nome hello muito**padrão,** e defina seu tooprocess de arquivo e diretório.  

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

Todos Olá conta de armazenamento do arquivo e diretório referências ponto toohello wasb://container1@storage1.blob.core.windows.net. Isso é hello **conta de armazenamento padrão** associado a cluster do HDInsight hello.

Agora, vamos supor que você deseja tooprocess um arquivo chamado mySpecial.csv localizado em Olá /private diretório de **container2** na **Armazenamento2 do**.

Em seu código R, aponte Olá nome nó referência toohello **Armazenamento2 do** conta de armazenamento.


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

Todos os Olá diretório e arquivo referências agora toohello ponto da conta de armazenamento wasb://container2@storage2.blob.core.windows.net. Isso é hello **nome do nó** que você especificou.

Você tem tooconfigure Olá /user RevoShare/<SSH username> do **Armazenamento2 do** da seguinte maneira:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Usar um Azure Data Lake Store com o R Server

toouse Data Lake armazena com sua conta de HDInsight, é necessário toogive seu repositório Azure Data Lake do cluster acesso tooeach que você deseja toouse. Para obter instruções sobre como toouse Olá toocreate portal do Azure um HDInsight cluster com uma conta do repositório Azure Data Lake como armazenamento padrão da saudação ou como um armazenamento adicional, consulte [criar um cluster HDInsight com repositório Data Lake usando o portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Você, em seguida, usar Olá armazenamento em seu script R muito como você fez uma conta de armazenamento do Azure secundário, conforme descrito no procedimento anterior hello.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Adicionar tooyour de acesso do cluster do Azure Data Lake armazena
Você pode acessar um repositório Data Lake usando uma Entidade de Serviço do Azure AD (Azure Active Directory) que está associada ao cluster do HDInsight.

tooadd uma entidade de serviço do AD do Azure:

1. Quando você cria seu cluster HDInsight, selecione **Cluster AAD identidade** de saudação **fonte de dados** guia.

2. Em Olá **Cluster AAD identidade** caixa de diálogo **Selecione entidade de serviço do AD**, selecione **criar novo**.

Depois que você nomeie Olá entidade de serviço e cria uma senha para ele, clique em **gerenciar o acesso de ADLS** tooassociate Olá armazena da entidade de serviço com o Data Lake.

Também é possível tooadd cluster acesso tooone ou mais Data Lake armazena após a criação do cluster. Abra Olá entrada portal do Azure para um repositório Data Lake e vá muito**Data Explorer > acesso > Adicionar**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Como tooaccess Olá repositório Data Lake do servidor de R

Depois que você deu a acessar o repositório de Data Lake tooa, você pode usar o repositório Olá R Server em HDInsight hello como uma conta de armazenamento do Azure secundário. Olá somente a diferença é o prefixo Olá **wasb: / /** muda muito**publicitário: / /** da seguinte maneira:


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


Olá comandos a seguir são usados tooconfigure Olá conta de armazenamento do Data Lake com o diretório de RevoShare Olá e adicione CSV de exemplo hello do exemplo anterior hello:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Usar o Armazenamento de Arquivos do Azure com o R Server

Também é uma opção de armazenamento de dados conveniente para uso no nó de borda Olá chamado [arquivos do Azure] ((https://azure.microsoft.com/services/storage/files/). Ele permite toomount um toohello de compartilhamento de arquivo de armazenamento do Azure sistema de arquivos do Linux. Esta opção pode ser útil para armazenar arquivos de dados, os scripts de R e objetos de resultado que talvez sejam necessárias mais tarde, especialmente quando ele torna o sistema de arquivos nativo sentido toouse Olá no nó de borda de saudação em vez do HDFS. 

A principal vantagem dos arquivos do Azure é um arquivo hello compartilhamentos podem ser montados e usados por qualquer sistema que tenha um sistema operacional com suporte, como Windows ou Linux. Por exemplo, ele pode ser usado por outro cluster do HDInsight que você ou alguém em sua equipe tenha, por uma VM do Azure ou até mesmo por um sistema local. Para obter mais informações, consulte:

- [Como toouse armazenamento de arquivo do Azure com Linux](../storage/files/storage-how-to-use-files-linux.md)
- [Como toouse armazenamento de arquivo do Azure no Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Próximas etapas

Agora que você entende as opções de armazenamento do Azure hello, os links de uso a seguir Olá toodiscover maneiras de obter as tarefas de ciência de dados feitas com o servidor do R no HDInsight.

* [Visão geral do Servidor R no HDInsight](hdinsight-hadoop-r-server-overview.md)
* [Get started with R server on Hadoop (Introdução ao servidor R no Hadoop)](hdinsight-hadoop-r-server-get-started.md)
* [Adicionar servidor RStudio tooHDInsight (se não adicionado durante a criação do cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opções de contexto de computação para o Servidor R no HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)

