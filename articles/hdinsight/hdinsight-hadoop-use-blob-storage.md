---
title: "dados aaaQuery do HDFS compatível com o armazenamento do Azure - HDInsight do Azure | Microsoft Docs"
description: "Saiba como os dados de tooquery do armazenamento do Azure e do repositório Azure Data Lake toostore resultados da análise."
keywords: "armazenamento de blobs, hdfs, dados estruturados, dados não estruturados, data lake store, entrada do Hadoop, saída do Hadoop, armazenamento do hadoop, entrada do hdfs, saída do hdfs, armazenamento do hdfs, wasb do azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Usar o Armazenamento do Azure com clusters HDInsight

dados tooanalyze no cluster HDInsight, você pode armazenar dados de saudação no armazenamento do Azure, o repositório Azure Data Lake ou ambos. Ambas as opções de armazenamento permitem que você exclua toosafely clusters de HDInsight que são usados para a computação sem perda de dados de usuário.

Hadoop oferece suporte a uma noção saudação padrão do sistema de arquivos. sistema de arquivos padrão Olá implica um esquema padrão e uma autoridade. Ele também pode ser usado tooresolve os caminhos relativos. Durante a saudação o processo de criação de cluster HDInsight, você pode especificar um contêiner de blob no armazenamento do Azure como sistema de arquivos padrão hello ou com HDInsight 3.5, você pode selecionar armazenamento do Azure ou repositório Azure Data Lake como sistema de arquivos padrão Olá com algumas exceções. Para dar suporte a saudação de usando o repositório Data Lake como saudação padrão e vinculado de armazenamento, consulte [Availabilities para cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

Neste artigo, você aprenderá como funciona o Armazenamento do Azure com clusters HDInsight. toolearn como repositório Data Lake funciona com clusters de HDInsight, consulte [clusters do repositório Azure Data Lake uso com o Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md). Para saber mais sobre a criação de um cluster HDInsight, veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

O Armazenamento do Azure é uma solução de armazenamento de uso geral que se integra perfeitamente com o HDInsight. HDInsight pode usar um contêiner de blob no armazenamento do Azure como sistema de arquivos padrão Olá para cluster hello. Através de uma interface de (HDFS) do sistema de arquivos distribuído Hadoop, todo o conjunto de componentes em HDInsight Olá pode operar diretamente nos dados estruturados ou não estruturados armazenados como blobs.

> [!WARNING]
> Há várias opções disponíveis ao criar uma conta de Armazenamento do Azure. Olá, a tabela a seguir fornece informações sobre quais opções são suportadas com HDInsight:
> 
> | Tipo de conta de armazenamento | Camada de armazenamento | Suporte com o HDInsight |
> | ------- | ------- | ------- |
> | Conta de armazenamento de uso geral | Standard | __Sim__ |
> | &nbsp; | Premium | Não |
> | Conta de Armazenamento de Blobs | Dinâmica | Não |
> | &nbsp; | Estática | Não |

Não é recomendável que você use o contêiner de blob saudação padrão para armazenar dados de negócios. Excluindo contêiner de blob padrão Olá depois de cada tooreduce use o custo de armazenamento é uma prática recomendada. Observação contêiner saudação padrão contém o aplicativo e sistema de logs. Verifique tooretrieve-se de que logs de saudação antes de excluir o contêiner de saudação.

Não há suporte para o compartilhamento de um contêiner de blobs para vários clusters.

## <a name="hdinsight-storage-architecture"></a>Arquitetura de armazenamento do HDInsight
Olá diagrama a seguir fornece uma exibição abstrata de saudação HDInsight a arquitetura de armazenamento do uso do armazenamento do Azure:

![Clusters de Hadoop usam Olá HDFS API tooaccess e armazenam dados estruturados e no armazenamento de Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Arquitetura de armazenamento do HDInsight")

HDInsight fornece acesso toohello distribuída arquivo sistema localmente anexado toohello nós de computação. Este sistema de arquivos pode ser acessado usando Olá totalmente qualificado URI, por exemplo:

    hdfs://<namenodehost>/<path>

Além disso, HDInsight permite tooaccess dados armazenados no armazenamento do Azure. Olá sintaxe é:

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

Veja algumas considerações ao usar a conta de armazenamento do Azure com clusters HDInsight.

* **Contêineres em contas de armazenamento Olá tooa conectado de cluster:** porque Olá nome de conta e chave estão associados com cluster Olá durante a criação, você tem blobs toohello acesso completo esses contêineres.

* **Contêineres do públicos ou blobs públicos em contas de armazenamento que não estão conectados cluster tooa:** , você tem permissão somente leitura toohello blobs em contêineres de saudação.
  
  > [!NOTE]
  > Contêineres do públicos permitem que você tooget uma lista de todos os blobs que estão disponíveis no contêiner e obter metadados do contêiner. Blobs públicos permitem blobs de saudação tooaccess somente se você souber a URL exata hello. Para obter mais informações, consulte <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">restringir acesso toocontainers e blobs</a>.
  > 
  > 
* **Contêineres privados em contas de armazenamento que não estão conectados cluster tooa:** você não pode acessar blobs Olá em contêineres hello, a menos que você definir conta de armazenamento hello quando você enviar trabalhos de WebHCat hello. Isso será explicado mais adiante neste artigo.

contas de armazenamento de saudação que são definidas no processo de criação de saudação e suas chaves são armazenadas no %HADOOP_HOME%/conf/core-site.xml em nós de cluster de saudação. comportamento padrão de saudação do HDInsight é toouse contas de armazenamento de saudação definidas no arquivo de Core-site.XML hello. Você pode modificar essa configuração usando [Ambari](./hdinsight-hadoop-manage-ambari.md)

Vários trabalhos do WebHCat, incluindo Hive, MapReduce, streaming de Hadoop e Pig, podem conter uma descrição de contas de armazenamento e metadados (normalmente funciona para Pig com contas de armazenamento, mas não para metadados). (Isso funciona atualmente com o Pig para contas de armazenamento, mas não para metadados.) Para obter mais informações, consulte [Usando um Cluster HDInsight com metastores e contas de armazenamento alternativas](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).

Os blobs podem ser usados para dados estruturados e não estruturados. Os contêineres de blob armazenam dados como pares de chave/valor, e não há nenhuma hierarquia de diretório. No entanto, caractere de barra (/) do hello pode ser usado em Olá toomake de nome da chave, ele aparece como se um arquivo é armazenado em uma estrutura de diretório. Por exemplo, a chave de um blob pode ser *input/log1.txt*. Não real *entrada* diretório existe, mas devido a presença de toohello de caractere de barra Olá no nome da chave hello, ele tem aparência de saudação de um caminho de arquivo.

## <a id="benefits"></a>Benefícios do Armazenamento do Azure
Olá implícita custo de desempenho de recursos de armazenamento e clusters de computação não compartilhando mitigado pela maneira Olá clusters de computação de saudação são criados os recursos de conta de armazenamento toohello fechar dentro Olá região do Azure, em rede de alta velocidade Olá faz eficiente para nós de computação Olá tooaccess Olá dados dentro do armazenamento do Azure.

Há vários benefícios associados ao armazenamento de dados de saudação no armazenamento do Azure, em vez de HDFS:

* **Compartilhamento e reutilização de dados:** dados Olá no HDFS estão localizados dentro do cluster de computação de saudação. Somente aplicativos Olá que têm acesso toohello compute cluster pode usar dados de saudação por meio de APIs de HDFS. dados de saudação no armazenamento do Azure podem ser acessados por meio de saudação APIs HDFS ou Olá [APIs de REST do armazenamento de Blob][blob-storage-restAPI]. Assim, um conjunto maior de aplicativos (incluindo outros clusters de HDInsight) e ferramentas pode ser usado tooproduce e consumir dados de saudação.
* **Arquivamento de dados:** armazenar dados no armazenamento do Azure permite que os clusters de HDInsight Olá usados para computação toobe excluído com segurança sem perda de dados de usuário.
* **Custo de armazenamento de dados:** armazenando dados em DFS de longo prazo de saudação é mais caro do que armazenar dados saudação no armazenamento do Azure, porque o custo de saudação de um cluster de computação é maior do que o custo de saudação do armazenamento do Azure. Além disso, como dados de saudação não têm toobe recarregado para cada geração de cluster de computação, você está salvando também os custos de carregamento de dados.
* **Expansão elástica:** HDFS embora fornece um sistema de arquivos expandido, escala Olá é determinada pelo número de saudação de nós que você cria para seu cluster. Alterar escala Olá pode se tornar um processo mais complicado que depender elástica hello dimensionar os recursos que você obtém automaticamente no armazenamento do Azure.
* **Replicação geográfica:** seu Armazenamento do Azure pode ser replicado geograficamente. Embora isso fornece recuperação geográfica e a redundância de dados, um failover toohello replicado geograficamente local severos afeta o desempenho e ele pode incorrer em custos adicionais. Portanto, nossa recomendação é toochoose Olá da replicação geográfica cuidadosamente e somente se o valor Olá dados saudação vale a pena custo adicional de saudação.

Determinados trabalhos MapReduce e os pacotes podem criar resultados intermediários que você não deseja realmente toostore no armazenamento do Azure. Nesse caso, você pode decidir dados Olá toostore Olá HDFS local. Na verdade, o HDInsight usa o DFS para vários desses resultados intermediários em trabalhos Hive e outros processos.

> [!NOTE]
> A maioria dos comandos HDFS (como <b>ls</b>, <b>copyFromLocal</b> e <b>mkdir</b>) ainda funciona conforme o esperado. Olá somente os comandos que são específicos de toohello HDFS implementação nativa (que é chamado tooas DFS), como <b>fschk</b> e <b>dfsadmin</b>, mostrar um comportamento diferente no armazenamento do Azure.
> 
> 

## <a name="create-blob-containers"></a>Criar contêineres de blob
toouse blobs, primeiro você cria um [conta de armazenamento do Azure][azure-storage-create]. Como parte disso, você deve especificar uma região do Azure em que a conta de armazenamento de saudação é criada. cluster Hello e conta de armazenamento Olá devem ser hospedados em Olá mesma região. banco de dados do SQL Server metastore Olá Hive e Oozie metastore também deve estar localizado do banco de dados do SQL Server Olá mesma região.

Independentemente de onde ele reside, cada blob que você criar pertence tooa contêiner na sua conta de armazenamento do Azure. Esse contêiner pode ser um contêiner de armazenamento de blob existente criado fora do HDInsight, ou pode ser um contêiner criado para um cluster HDInsight.

contêiner de Blob padrão Olá armazena informações específicas do cluster, como logs e o histórico de trabalho. Não compartilhe um contêiner de armazenamento de blob padrão com vários clusters HDInsight. Isso pode corromper o histórico de trabalhos. É recomendável toouse um contêiner diferente para cada cluster e colocar os dados compartilhados em uma conta de armazenamento vinculado especificada na implantação de todos os clusters, em vez da conta de armazenamento padrão de saudação. Para obter mais informações sobre como configurar contas de armazenamento vinculadas, veja [Criar clusters HDInsight][hdinsight-creation]. No entanto, você pode reutilizar um contêiner de armazenamento padrão depois que o cluster HDInsight original de saudação foi excluído. Para clusters do HBase, você poderá manter, na verdade, dados e esquema de tabela do HBase Olá criando um novo cluster HBase usando o contêiner de blob do saudação padrão que é usado por um cluster HBase que foi excluído.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Use Olá portal do Azure
Ao criar um cluster HDInsight do hello Portal, você tem detalhes da conta de armazenamento tooprovide Olá Olá opções (conforme mostrado abaixo). Você também pode especificar se deseja que uma conta de armazenamento adicionais associados cluster hello e, nesse caso, escolha de repositório Data Lake ou outro blob de armazenamento do Azure como armazenamento adicional da saudação.

![Fonte de dados de criação do hadoop do HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> Não há suporte para usando uma conta de armazenamento adicional no cluster do HDInsight Olá um local diferente.


### <a name="use-azure-powershell"></a>Usar PowerShell do Azure
Se você [instalado e configurado o Azure PowerShell][powershell-install], você pode usar o hello a seguir de saudação do Azure PowerShell prompt toocreate uma conta de armazenamento e o contêiner:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Usar a CLI do Azure

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Se você tiver [instalado e configurado Olá CLI do Azure](../cli-install-nodejs.md), seguinte Olá comando pode ser usado tooa conta de armazenamento e contêiner.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Olá `--type` parâmetro indica como a conta de armazenamento Olá é replicada. Para saber mais, veja [Replicação do Armazenamento do Azure](../storage/storage-redundancy.md). Não use ZRS, pois o ZRS não dá suporte ao blob de páginas, arquivo, tabela ou fila.
> 
> 

Você está toospecify solicitadas Olá região geográfica que Olá conta de armazenamento é criada no. Você deve criar a conta de armazenamento Olá no hello mesma região que você planeja criar seu cluster HDInsight.

Depois de criar a conta de armazenamento Olá, use Olá chaves de conta de armazenamento do comando tooretrieve Olá a seguir:

    azure storage account keys list <storageaccountname>

toocreate um contêiner, use Olá comando a seguir:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Arquivos de endereços no armazenamento do Azure
Olá esquema URI para acessar arquivos no armazenamento do Azure do HDInsight é:

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

o esquema de URI Olá fornece acesso não criptografado (com hello *wasb:* prefixo) e SSL criptografadas acesso (com *wasbs*). É recomendável usar *wasbs* sempre que possível, mesmo quando o acesso a dados que residem dentro de Olá mesma região no Azure.

Olá &lt;BlobStorageContainerName&gt; identifica nome Olá Olá do contêiner de blob no armazenamento do Azure.
Olá &lt;StorageAccountName&gt; identifica o nome de conta de armazenamento do Azure hello. Um FQDN (nome de domínio totalmente qualificado) é necessário.

Se nem &lt;BlobStorageContainerName&gt; nem &lt;StorageAccountName&gt; tiver sido especificado, sistema de arquivos padrão de saudação é usado. Para arquivos Olá no sistema de arquivos padrão hello, você pode usar um caminho relativo ou um caminho absoluto. Por exemplo, Olá *Hadoop-Examples.jar mapreduce* arquivo vem com clusters de HDInsight pode ser chamado tooby usando um dos seguintes hello:

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> nome de arquivo Hello <i>Hadoop-Examples.jar</i> em clusters de versões 2.1 e 1.6 HDInsight.
> 
> 

Olá &lt;caminho&gt; é o nome de caminho HDFS de arquivo ou diretório de saudação. Como os contêineres no Armazenamento do Azure são apenas um repositório de chave-valor, não há nenhum sistema de arquivos hierárquico verdadeiro. Um caractere "/" dentro de uma chave de blob é interpretado como um separador de diretório. Por exemplo, o nome de blob Olá para *Hadoop-Examples.jar mapreduce* é:

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Ao trabalhar com blobs fora do HDInsight, a maioria dos utilitários não reconhece o formato WASB hello e em vez disso, espera um formato de caminho básicas, como `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Acessar blobs 


### <a name="access-blobs-using-azure-powershell"></a> Usar o Azure PowerShell
> [!NOTE]
> comandos de saudação nesta seção fornecem um exemplo básico de como usar o PowerShell tooaccess dados armazenados em blobs. Para obter um exemplo mais completo que é personalizado para trabalhar com HDInsight, consulte Olá [ferramentas HDInsight](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Use Olá comando toolist Olá relacionados ao blob cmdlets a seguir:

    Get-Command *blob*

![Lista de cmdlets do PowerShell relacionados ao blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Carregar arquivos
Consulte [carregar dados tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Baixar arquivos
Olá, script a seguir baixa uma pasta atual do toohello de blob de bloco. Executando o script hello, antes de alterar pasta de tooa de diretório Olá onde você tem permissões de gravação.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Fornecer o nome do grupo de recursos de saudação e nome do cluster Olá, você pode usar o hello código a seguir:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Excluir arquivos
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Listar arquivos
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Executar consultas do Hive usando uma conta de armazenamento indefinida
Este exemplo mostra como toolist uma pasta da conta de armazenamento que não é definida durante a Olá o processo de criação.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Usar a CLI do Azure
Use Olá comandos toolist Olá relacionados ao blob de comandos a seguir:

    azure storage blob

**Exemplo de como usar um arquivo de tooupload de CLI do Azure**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Exemplo de como usar um arquivo de toodownload de CLI do Azure**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Exemplo de como usar um arquivo de toodelete de CLI do Azure**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Exemplo de como usar arquivos de toolist CLI do Azure**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Usar contas de armazenamento adicionais

Ao criar um cluster HDInsight, você deve especificar conta de armazenamento do Azure Olá que deseja tooassociate com ele. Além disso toothis conta de armazenamento, você pode adicionar contas de armazenamento adicional da saudação mesmo assinatura do Azure ou em diferentes assinaturas do Azure durante o processo de criação de saudação ou depois de um cluster foi criado. Para obter instruções sobre como adicionar mais contas de armazenamento, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!WARNING]
> Não há suporte para usando uma conta de armazenamento adicional no cluster do HDInsight Olá um local diferente.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toouse HDFS compatível com o armazenamento do Azure com HDInsight. Isso permite que você toobuild escalonável e de longo prazo, arquivamento soluções de aquisição de dados e uso HDInsight toounlock Olá informações dentro de saudação armazenada estruturados e dados não estruturados.

Para obter mais informações, consulte:

* [Introdução ao Azure HDInsight][hdinsight-get-started]
* [Introdução ao Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Usar o Hive com o HDInsight][hdinsight-use-hive]
* [Usar o Pig com o HDInsight][hdinsight-use-pig]
* [Usar assinaturas de acesso compartilhado do Azure Storage toorestrict acesso toodata com HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
