---
title: "aaaUse repositório Data Lake com Hadoop no HDInsight do Azure | Microsoft Docs"
description: "Saiba como os dados de tooquery do repositório Azure Data Lake e toostore resultados da análise."
keywords: "armazenamento de blobs, hdfs, dados estruturados, dados não estruturados, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Usar o Data Lake Store com clusters Azure HDInsight

dados de tooanalyze no cluster HDInsight, você pode armazenar dados de saudação ou em [armazenamento do Azure](../storage/common/storage-introduction.md), [repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md), ou ambos. Ambas as opções de armazenamento permitem que você exclua toosafely clusters de HDInsight que são usados para a computação sem perda de dados de usuário.

Neste artigo, você aprenderá como o Data Lake Store funciona com clusters do HDInsight. toolearn como o armazenamento do Azure funciona com clusters de HDInsight, consulte [clusters de armazenamento do Azure Use com o Azure HDInsight](hdinsight-hadoop-use-blob-storage.md). Para saber mais sobre a criação de um cluster HDInsight, veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!NOTE]
> O Data Lake Store é sempre acessado por meio de um canal seguro, portanto não há nenhum nome do esquema de sistema de arquivos `adls`. Use sempre `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Disponibilidade para clusters do HDInsight

Hadoop oferece suporte a uma noção saudação padrão do sistema de arquivos. sistema de arquivos padrão Olá implica um esquema padrão e uma autoridade. Ele também pode ser usado tooresolve os caminhos relativos. Durante o processo de criação do cluster do HDInsight hello, você pode especificar um contêiner de blob no armazenamento do Azure como sistema de arquivos padrão hello, ou com HDInsight 3.5 e versões mais recentes, você pode selecionar armazenamento do Azure ou repositório Azure Data Lake como sistema de arquivos padrão Olá com um algumas exceções. 

Os clusters HDInsight podem usar o Data Lake Store de duas maneiras:

* Como o armazenamento padrão da saudação
* Como armazenamento adicional, com o Azure Storage Blob como o armazenamento padrão.

A partir de agora, apenas algumas das Olá HDInsight cluster usando o repositório Data Lake como armazenamento padrão e as contas de armazenamento adicionais de suporte de tipos/versões:

| Tipo de cluster HDInsight | Data Lake Store como armazenamento padrão | Data Lake Store como armazenamento adicional| Observações |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight versão 3.6 | Sim | Sim | |
| HDInsight versão 3.5 | Sim | Sim | Com exceção de saudação do HBase|
| HDInsight versão 3.4 | Não | Sim | |
| HDInsight versão 3.3 | Não | Não | |
| HDInsight versão 3.2 | Não | Sim | |
| HDInsight Premium (camada)| Não | Não | |
| Storm | | |Você pode usar dados do repositório Data Lake toowrite de uma topologia Storm. Também é possível usar o Data Lake Store para dados de referência que, em seguida, podem ser lidos por uma topologia do Storm.|

Usando o repositório Data Lake como uma conta de armazenamento adicional não afetam o desempenho ou tooread de capacidade de saudação ou gravar tooAzure armazenamento de cluster hello.


## <a name="use-data-lake-store-as-default-storage"></a>Usar o Data Lake Store como armazenamento padrão

Quando HDInsight é implantado com o repositório Data Lake como armazenamento padrão, os arquivos de relacionadas ao cluster de saudação são armazenados no repositório Data Lake em Olá local a seguir:

    adl://mydatalakestore/<cluster_root_path>/

onde `<cluster_root_path>` é o nome de saudação de uma pasta que você criar no repositório Data Lake. Especificando um caminho raiz para cada cluster, você pode usar Olá a mesma conta de repositório Data Lake para mais de um cluster. Portanto, você terá uma configuração em que:

* Cluster1 pode usar o caminho de saudação`adl://mydatalakestore/cluster1storage`
* Cluster2 pode usar o caminho de saudação`adl://mydatalakestore/cluster2storage`

Observe que ambos Olá use clusters Olá mesma conta do repositório Data Lake **mydatalakestore**. Cada cluster tem acesso tooits possui o sistema de arquivos raiz no repositório Data Lake. Olá experiência de implantação do portal do Azure em particular solicitará que você toouse um nome de pasta, como **/clusters/\<clustername >** para caminho de raiz de saudação.

toobe toouse capaz de um repositório Data Lake como armazenamento padrão, você deve conceder toohello de acesso principal do serviço Olá caminhos a seguir:

- raiz de conta do repositório Data Lake Hello.  Por exemplo: adl://mydatalakestore/.
- pasta de saudação para todas as pastas de cluster.  Por exemplo: adl://mydatalakestore/clusters.
- pasta Olá cluster hello.  Por exemplo: adl://mydatalakestore/clusters/cluster1storage.

Para saber mais sobre como criar a entidade de segurança e conceder acesso, consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).


## <a name="use-data-lake-store-as-additional-storage"></a>Usar o Data Lake Store como armazenamento adicional

Você pode usar o repositório Data Lake como armazenamento adicional para o cluster hello. Nesses casos, armazenamento padrão da saudação cluster pode ser um Blob de armazenamento do Azure ou uma conta do repositório Data Lake. Se você estiver executando trabalhos de HDInsight em relação aos dados Olá armazenados no repositório Data Lake como armazenamento adicional, você deve usar arquivos de toohello Olá caminho totalmente qualificado. Por exemplo:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Observe que não há nenhum **cluster_root_path** na URL de saudação agora. Isso ocorre porque o repositório Data Lake não está um armazenamento padrão nesse caso você toodo só precisa fornecer Olá caminho toohello arquivos.

toobe toouse capaz de um repositório Data Lake como armazenamento adicional, você só precisa toogrant Olá acesso principal toohello caminhos de serviço de onde os arquivos são armazenados.  Por exemplo:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Para saber mais sobre como criar a entidade de segurança e conceder acesso, consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Usar mais de uma conta do Data Lake Store

Adicionar uma conta do repositório Data Lake como adicionais e adicionar mais de um repositório do Data Lake contas são realizadas, fornecendo permissão de cluster do HDInsight Olá em dados em uma ou mais contas de repositório Data Lake. Consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurar acesso ao Data Lake Store

tooconfigure acesso ao repositório Data Lake do seu cluster HDInsight, você deve ter uma entidade de serviço do Azure Active directory (AD do Azure). Somente um administrador do Azure AD pode criar uma entidade de serviço. entidade de serviço Olá deve ser criada com um certificado. Para obter mais informações, consulte [Configurar acesso ao Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) e [Criar entidade de serviço com certificado autoassinado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Se você for repositório toouse Azure Data Lake como armazenamento adicional para o cluster HDInsight, é altamente recomendável que você faça isso durante a criação de cluster Olá conforme descrito neste artigo. Adicionar repositório Azure Data Lake como armazenamento adicional tooan cluster HDInsight existente é um processo complicado e sujeito a tooerrors.
>

## <a name="access-files-from-hello-cluster"></a>Acessar arquivos do cluster Olá

Há várias maneiras que você pode acessar arquivos Olá no repositório Data Lake de um cluster HDInsight.

* **Usando o nome totalmente qualificado da saudação**. Com essa abordagem, você fornecer o arquivo de toohello de caminho completo de saudação que você deseja tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Usando o formato de caminho reduzido Olá**. Com essa abordagem, você deve substituir caminho Olá a raiz do cluster toohello com publicitário: / / /. Portanto, o exemplo hello acima, você pode substituir `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` com `adl:///`.

        adl:///<file path>

* **Usando o caminho relativo Olá**. Com essa abordagem, você fornece apenas Olá relativo caminho toohello arquivo que você deseja tooaccess. Por exemplo, se Olá caminho completo toohello arquivo:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    Você pode acessar Olá mesmo arquivo sample.log usando este caminho relativo, em vez disso.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Criar clusters de HDInsight com acessar o repositório de Lake tooData

Use Olá siga os links para obter instruções detalhadas de como toocreate clusters de HDInsight com acessar o repositório de Lake tooData.

* [Usando o Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [Usando o PowerShell (com o Data Lake Store como o armazenamento padrão)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Usando o PowerShell (com o Data Lake Store como o armazenamento adicional)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Usando modelos do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toouse repositório Azure Data Lake HDFS compatível com HDInsight. Isso permite que você toobuild escalonável e de longo prazo, arquivamento soluções de aquisição de dados e uso HDInsight toounlock Olá informações dentro de saudação armazenada estruturados e dados não estruturados.

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
