---
title: dados de aaaUpload para trabalhos de Hadoop em HDInsight | Microsoft Docs
description: "Saiba como tooupload e acessar dados para trabalhos de Hadoop no HDInsight usando Olá CLI do Azure, Azure Storage Explorer, Azure PowerShell, linha de comando do Hadoop hello ou Sqoop."
keywords: hadoop de etl, inserindo dados no hadoop, carregar dados no hadoop
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Carregar dados para trabalhos do Hadoop no HDInsight
O Azure HDInsight oferece um HDFS (Sistema de Arquivos Distribuído) do Hadoop completo no armazenamento de blob do Azure. Ele foi projetado como uma extensão HDFS tooprovide uma perfeita experiência toocustomers. Ele permite que todo o conjunto de componentes em Olá Hadoop ecossistema toooperate diretamente nos dados de saudação gerencia hello. O armazenamento de blob do Azure e o HDFS são sistemas de arquivos distintos otimizados para armazenamento de dados e computação nesses dados. Para obter informações sobre os benefícios de saudação do uso de armazenamento de BLOBs do Azure, consulte [armazenamento de BLOBs do Azure Use com HDInsight][hdinsight-storage].

**Pré-requisitos**

Observe Olá requisito a seguir antes de começar:

* Um cluster Azure HDInsight. Para obter instruções, consulte [Introdução ao Azure HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision].

## <a name="why-blob-storage"></a>Por que o armazenamento de blob?
HDInsight do Azure clusters normalmente são implantados toorun trabalhos de MapReduce e clusters hello serão descartados depois de concluir essas tarefas. Manter os dados de saudação em clusters HDFS Olá após a conclusão computações seria uma forma caro toostore esses dados. Armazenamento de BLOBs do Azure é altamente disponível, altamente escalonável e de alta capacidade, a opção de armazenamento de baixo custo e podem ser compartilhadas para dados que são processada usando HDInsight de toobe. Armazenando dados em um blob permite que os clusters de HDInsight Olá que são usados para computação toobe lançado com segurança sem perda de dados.

### <a name="directories"></a>Diretórios
Os contêineres de armazenamento de blob do Azure armazenam dados como pares de chave/valor e não há nenhuma hierarquia de diretório. No entanto hello "/" caractere pode ser usado em Olá nome da chave toomake ele aparece como se um arquivo é armazenado em uma estrutura de diretório. O HDInsight os vê como se fossem diretórios reais.

Por exemplo, a chave de um blob pode ser *input/log1.txt*. Nenhum diretório real de "entrado" existe, mas devido a presença de toohello de saudação caractere "/" no nome da chave Olá, ele tem a aparência de saudação de um caminho de arquivo.

Por isso, se você usar as ferramentas do Gerenciador do Azure, poderá perceber alguns arquivos de 0 byte. Esses arquivos têm duas finalidades:

* Se houver pastas vazias, eles marcam de existência de saudação da pasta hello. Armazenamento de BLOBs do Azure é bastante inteligente tooknow que exista um blob denominado foo/barra, há uma pasta chamada **foo**. Mas Olá toosignify de maneira somente uma pasta vazia chamada **foo** é ter esse arquivo especial de 0 byte em vigor.
* Mantenham metadados especial que é necessário por Olá Hadoop sistema de arquivos, especialmente permissões hello e proprietários para pastas de saudação.

## <a name="command-line-utilities"></a>Utilitários de linha de comando
A Microsoft fornece Olá toowork utilitários com o armazenamento de BLOBs do Azure a seguir:

| Ferramenta | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Interface de Linha de Comando do Azure][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Comando do Hadoop](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Embora Olá CLI do Azure, Azure PowerShell e AzCopy podem ser usados de fora do Azure, Olá Hadoop comando só está disponível no cluster do HDInsight hello e só permite carregar dados do sistema de arquivos local Olá para armazenamento de BLOBs do Azure.
>
>

### <a id="xplatcli"></a>Azure CLI
Olá CLI do Azure é uma ferramenta de plataforma cruzada que permite que você toomanage do Azure services. Use Olá armazenamento de Blob etapas tooupload dados tooAzure a seguir:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Instalar e configurar Olá CLI do Azure para Mac, Linux e Windows](../cli-install-nodejs.md).
2. Abra um prompt de comando, bash ou outro shell e usar Olá tooauthenticate tooyour assinatura do Azure a seguir.

        azure login

    Quando solicitado, digite Olá nome de usuário e senha para a sua assinatura.
3. Digite hello contas de armazenamento de saudação do comando toolist para sua assinatura a seguir:

        azure storage account list
4. Conta de armazenamento Olá Select que contém o blob Olá toowork, você deseja usar Olá comando tooretrieve Olá chave desta conta a seguir:

        azure storage account keys list <storage-account-name>

    Isso deve retornar as chaves **Primária** e **Secundária**. Saudação de cópia **primário** valor de chave, pois ele será usado nas etapas Avançar hello.
5. Use Olá tooretrieve comando uma lista de contêineres de blob na conta de armazenamento Olá a seguir:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Use Olá tooupload comandos a seguir e baixar arquivos toohello blob:

   * tooupload um arquivo:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload um arquivo:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Se você sempre trabalhará com hello mesma conta de armazenamento, você pode definir Olá seguintes variáveis de ambiente em vez de especificar a conta de saudação e a chave para cada comando:
>
> * **AZURE\_armazenamento\_conta**: nome de conta de armazenamento Olá
> * **AZURE\_armazenamento\_acesso\_chave**: chave de conta de armazenamento Olá
>
>

### <a id="powershell"></a>PowerShell do Azure
PowerShell do Azure é um ambiente de script que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de suas cargas de trabalho no Azure. Para obter informações sobre como configurar toorun sua estação de trabalho do PowerShell do Azure, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload tooAzure um arquivo local armazenamento de Blob**

1. Console do Azure PowerShell Olá aberta com as instruções no [instalar e configurar o Azure PowerShell](/powershell/azure/overview).
2. Defina valores Olá Olá cinco primeiros variáveis em Olá script a seguir:

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Olá colar o script em hello Azure PowerShell console toorun-toocopy arquivo de saudação.

Por exemplo, PowerShell scripts criados toowork com HDInsight, consulte [ferramentas HDInsight](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>AzCopy
AzCopy é uma ferramenta de linha de comando que é projetado toosimplify tarefa de saudação de transferência de dados dentro e fora de uma conta de armazenamento do Azure. Você pode usá-lo como uma ferramenta independente ou incorporar essa ferramenta em um aplicativo existente. [Baixar o AzCopy][azure-azcopy-download].

Olá sintaxe AzCopy é:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Para saber mais, consulte [AzCopy – Carregando/baixando arquivos para Blobs do Azure][azure-azcopy].

### <a id="commandline"></a>Linha de comando do Hadoop
linha de comando do Hadoop Olá só é útil para armazenar dados no armazenamento de blob quando dados saudação já estão presentes no nó principal do cluster hello.

Saudação de toouse ordem Hadoop comando, você deve primeiro se conectar toohello um nó principal usando um dos métodos a seguir de saudação:

* **HDInsight baseado em Windows**: [conecte-se usando a área de trabalho remota](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight baseados em Linux**: conectar-se usando o SSH ([Olá comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) ou [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Uma vez conectado, você pode usar o hello tooupload sintaxe toostorage um arquivo a seguir.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Por exemplo, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Como sistema de arquivos padrão Olá para HDInsight está no armazenamento de BLOBs do Azure, /example/data.txt, na verdade, está no armazenamento de BLOBs do Azure. Você também pode consultar o arquivo toohello como:

    wasb:///example/data/data.txt

ou o

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Para obter uma lista dos outros comandos Hadoop que trabalham com os arquivos, consulte [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> Em clusters de HBase, tamanho de bloco saudação padrão usado quando a gravação de dados é 256KB. Enquanto isso funciona bem quando usando APIs do HBase ou APIs REST, usando Olá `hadoop` ou `hdfs dfs` dados de toowrite comandos maiores ~ 12 GB resulta em um erro. Consulte Olá [exceção de armazenamento para gravação no blob](#storageexception) seção abaixo para obter mais informações.
>
>

## <a name="graphical-clients"></a>Clientes gráficos
Também há vários aplicativos que fornecem uma interface gráfica para trabalhar com o Armazenamento do Azure. a seguir Olá é uma lista de alguns desses aplicativos:

| Cliente | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Ferramentas do Microsoft Visual Studio para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Cloud Storage Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Explorer](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Ferramentas do Visual Studio para HDInsight
Para obter mais informações, consulte [recursos vinculados do hello navegar](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Gerenciador de Armazenamento do Azure
*Azure Storage Explorer* é uma ferramenta útil para inspecionar e alterar dados de saudação em blobs. É uma ferramenta de software livre que pode ser baixada em [http://storageexplorer.com/](http://storageexplorer.com/). Olá código-fonte está disponível a partir deste link também.

Antes de usar a ferramenta hello, você deve saber a sua chave de nome e uma conta de conta do armazenamento do Azure. Para obter instruções sobre como obter essas informações, consulte hello "como: exibir, copiar e regenerar as contas de armazenamento de chaves de acesso" seção [criar, gerenciar ou excluir uma conta de armazenamento][azure-create-storage-account].

1. Execute o Azure Storage Explorer. Se isso for Olá primeira vez você executou Olá Storage Explorer, você será solicitado para Olá **nome da conta _Storage** e **chave da conta de armazenamento**. Se você tiver executado antes, use Olá **adicionar** botão tooadd um novo nome de conta de armazenamento e a chave.

    Digite hello nome e chave Olá conta de armazenamento usada por seu cluster HDInsight e, em seguida, selecione **Salvar & Abrir**.

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. Na lista de Olá da esquerda de toohello contêineres da interface de saudação, clique em nome Olá Olá do contêiner de que está associado ao seu cluster HDInsight. Por padrão, é o nome de saudação do cluster do HDInsight Olá, mas pode ser diferente se você digitou um nome específico ao criar o cluster de saudação.
3. Na barra de ferramentas Olá, selecione o ícone de carregamento de saudação.

    ![Barra de ferramentas com ícone de upload destacado](./media/hdinsight-upload-data/toolbar.png)
4. Especifique um tooupload de arquivo e, em seguida, clique em **abrir**. Quando solicitado, selecione **carregar** raiz de toohello de arquivos tooupload Olá Olá do contêiner de armazenamento. Se você quiser caminho específico de tooa tooupload de arquivo hello, digite o caminho de saudação no hello **destino** campo e, em seguida, selecione **carregar**.

    ![Caixa de diálogo de upload do arquivo](./media/hdinsight-upload-data/fileupload.png)

    Depois que o arquivo hello concluiu o carregamento, você pode usá-lo de trabalhos no cluster do HDInsight hello.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Montar o Armazenamento de Blob do Azure como uma unidade Local
Confira [Montar o Armazenamento de Blob do Azure como uma unidade Local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Serviços
### <a name="azure-data-factory"></a>Fábrica de dados do Azure
Olá serviço fábrica de dados do Azure é um serviço totalmente gerenciado para compor serviços de movimentação de dados, processamento de dados e armazenamento de dados em pipelines de produção de dados simplificada, escalonável e confiável.

A fábrica de dados do Azure pode ser usado toomove dados no armazenamento de BLOBs do Azure, ou toocreate pipelines de dados que usam recursos de HDInsight diretamente como Hive e Pig.

Para obter mais informações, consulte Olá [documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop é uma ferramenta desenvolvida de dados tootransfer entre Hadoop e bancos de dados relacionais. Você pode usá-lo tooimport dados de um sistema de gerenciamento de banco de dados relacional (RDBMS), como SQL Server, MySQL ou Oracle no sistema de arquivo hello distribuído de Hadoop (HDFS), transformar dados Olá no Hadoop MapReduce ou Hive e, em seguida, exportar dados de saudação volta para um RDBMS.

Para obter mais informações, consulte [Usar Sqoop com HDInsight][hdinsight-use-sqoop].

## <a name="development-sdks"></a>SDKs de desenvolvimento
Armazenamento de BLOBs do Azure também pode ser acessado usando um SDK do Azure de saudação linguagens de programação a seguir:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Para obter mais informações sobre como instalar os SDKs do Azure hello, consulte [downloads do Azure](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Solucionar problemas
### <a id="storageexception"></a>Exceção de armazenamento para gravar no blob
**Sintomas**: ao usar o hello `hadoop` ou `hdfs dfs` comandos toowrite arquivos que são ~ 12 GB ou maior, em um cluster HBase, você pode encontrar hello erro a seguir:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Causa**: HBase em HDInsight clusters de tamanho de bloco de tooa padrão de 256 KB ao escrever armazenamento tooAzure. Enquanto isso funciona para APIs do HBase ou APIs REST, resultará em um erro ao usar o hello `hadoop` ou `hdfs dfs` utilitários de linha de comando.

**Resolução**: Use `fs.azure.write.request.size` toospecify um maior tamanho de bloco. Você pode fazer isso em uma base por uso usando Olá `-D` parâmetro. Olá, a seguir é um exemplo que usa esse parâmetro com hello `hadoop` comando:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

Você também pode aumentar o valor de saudação do `fs.azure.write.request.size` global usando o Ambari. Olá etapas a seguir podem ser usado toochange valor de saudação em Olá da interface do usuário do Ambari Web:

1. Em seu navegador, vá toohello Ambari Web UI para seu cluster. Isso é https://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster.

    Quando solicitado, insira o nome de saudação do administrador e a senha para cluster Olá.
2. Olá lado esquerdo da tela hello, selecione **HDFS**e, em seguida, selecione Olá **configurações** guia.
3. Em Olá **filtro...**  , digite `fs.azure.write.request.size`. Isso exibirá o campo hello e o valor atual no meio de saudação da página de saudação.
4. Altere o valor de saudação de 262144 (256KB) toohello novo valor. Por exemplo, 4194304 (4 MB).

![Imagem de alterar o valor de saudação por meio da interface do usuário do Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Para obter mais informações sobre como usar o Ambari, consulte [gerenciar clusters HDInsight usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Próximas etapas
Agora que você sabe como ler dados tooget em HDInsight, Olá toolearn artigos a seguir como tooperform análise:

* [Introdução ao Azure HDInsight][hdinsight-get-started]
* [Enviar trabalhos Hadoop de forma programática][hdinsight-submit-jobs]
* [Usar o Hive com o HDInsight][hdinsight-use-hive]
* [Usar o Pig com o HDInsight][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
