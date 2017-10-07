---
title: clusters de aaaManage Hadoop no HDInsight com o PowerShell - Azure | Microsoft Docs
description: "Saiba como tarefas tooperform administrativa para Olá clusters Hadoop em HDInsight usando o PowerShell do Azure."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Gerenciar clusters Hadoop no HDInsight Usando o PowerShell do Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

PowerShell do Azure é um ambiente de script poderoso que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de suas cargas de trabalho no Azure. Neste artigo, você aprenderá como usam o toomanage a clusters de Hadoop em HDInsight do Azure usando um console local do PowerShell do Azure por meio de saudação do Windows PowerShell. Para lista de saudação do hello cmdlets do HDInsight PowerShell, consulte [referência de cmdlet do HDInsight][hdinsight-powershell-reference].

**Pré-requisitos**

Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Instale o Azure PowerShell
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Se você instalou o Azure PowerShell versão 0.9x, deve desinstalá-lo antes de instalar uma versão mais recente.

toocheck versão Olá Olá instalada do PowerShell:

    Get-Module *azure*

toouninstall Olá versão mais antiga, executar programas e recursos no painel de controle de saudação.

## <a name="create-clusters"></a>Criar clusters
Confira [Criar clusters baseados em Linux no HDInsight usando o Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Listar clusters
Olá toolist de comando a seguir ao use todos os clusters na assinatura atual hello:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Mostrar cluster
Use Olá comando tooshow detalhes de um cluster específico na assinatura atual Olá a seguir:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Excluir clusters
Use Olá comando toodelete um cluster a seguir:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

Você também pode excluir um cluster, removendo o grupo de recursos de saudação que contém o cluster de saudação. Observe que isso excluirá todos os recursos de saudação no grupo de hello, incluindo a conta de armazenamento padrão de saudação.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Dimensionar clusters
dimensionando o recurso de cluster de saudação permite toochange número de saudação de nós de trabalho usado por um cluster que está em execução no Azure HDInsight sem ter que toore-criar o cluster de saudação.

> [!NOTE]
> Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis. Se você não tiver certeza da versão de saudação do cluster, você pode verificar a página de propriedades de saudação.  Confira [Listar e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

impacto de saudação do alterando o número de saudação de nós de dados para cada tipo de cluster HDInsight com suporte:

* O Hadoop

    Você perfeitamente pode aumentar o número de saudação de nós de trabalho em um cluster de Hadoop que está sendo executado sem afetar todos os trabalhos pendentes ou em execução. Novos trabalhos também podem ser enviados enquanto Olá operação está em andamento. Falhas em uma operação de dimensionamento são controladas normalmente para que hello cluster seja sempre deixado em um estado funcional.

    Quando um cluster Hadoop é reduzido, reduzindo o número de saudação de nós de dados, alguns dos serviços de saudação em cluster Olá são reiniciados. Isso faz com que todas as e pendentes toofail trabalhos na conclusão de saudação do hello a operação de dimensionamento. No entanto, você pode, reenviar trabalhos Olá após a conclusão da operação de saudação.
* HBase

    Sem problemas, você pode adicionar ou remover o cluster de HBase tooyour nós enquanto ele está em execução. Servidores regionais são balanceados automaticamente dentro de alguns minutos após o término da operação de dimensionamento de saudação. No entanto, você pode equilibrar manualmente servidores regionais Olá fazendo logon em toohello um nó principal do cluster e em execução hello comandos a seguir em uma janela de prompt de comando:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    Sem problemas, você pode adicionar ou remover o cluster de profusão de tooyour de nós de dados enquanto ele está em execução. Mas, após a conclusão bem-sucedida da operação de dimensionamento de saudação, você precisará de topologia de saudação toorebalance.

    A redistribuição pode ser feita de duas maneiras:

  * Interface da Web Storm
  * Ferramenta CLI (interface de linha de comando)

    Consulte toohello [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.

    Interface da web Hello Storm está disponível no cluster do HDInsight hello:

    ![HDInsight storm dimensionar novo balanceamento](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Aqui está um exemplo como toouse Olá CLI comando topologia de profusão de saudação toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Olá toochange tamanho do cluster Hadoop usando o Azure PowerShell, execute Olá a seguir de comando de um computador cliente:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Conceder/revogar acesso
Clusters HDInsight tem Olá serviços da web HTTP (todos esses serviços têm pontos de extremidade RESTful) a seguir:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Por padrão, esses serviços são concedidos para acesso. Você pode revogar/conceder acesso de saudação. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> Revogando concedendo/acesso hello, redefinirá senha e nome de usuário de cluster hello.
>
>

Isso também pode ser feito por meio do Portal de saudação. Consulte [HDInsight administrar usando Olá portal do Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Atualizar credenciais de usuário HTTP
É Olá mesmo procedimento como [acesso Grant/revoke HTTP](#grant/revoke-access). Se foi concedida cluster Olá Olá acesso HTTP, você deve primeiro revogá-lo.  E, em seguida, conceder acesso de saudação com novas credenciais de usuário HTTP.

## <a name="find-hello-default-storage-account"></a>Localizar a conta de armazenamento saudação padrão
saudação de script do Powershell a seguir demonstra como tooget Olá nome de conta de armazenamento padrão e Olá chave de conta de armazenamento padrão para um cluster.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Localizar o grupo de recursos de saudação
No modo do Gerenciador de recursos de hello, cada cluster HDInsight pertence tooan grupo de recursos do Azure.  grupo de recursos de saudação toofind:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Enviar trabalhos
**trabalhos de MapReduce toosubmit**

Veja [Executar exemplos do MapReduce do Hadoop no HDInsight baseado em Windows](hdinsight-run-samples.md).

**trabalhos de Hive toosubmit**

Veja [Executar consultas do Hive usando o PowerShell](hdinsight-hadoop-use-hive-powershell.md)

**trabalhos de Pig toosubmit**

[Consulte Executar trabalhos do Pig usando o PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**trabalhos de Sqoop toosubmit**

Consulte [Usar o Sqoop com o HDInsight](hdinsight-use-sqoop.md).

**toosubmit Oozie trabalhos**

Consulte [Oozie de uso com toodefine Hadoop e executar um fluxo de trabalho no HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Carregue o armazenamento de Blob de tooAzure de dados
Consulte [carregar dados tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Consulte também
* [Documentação de referência do cmdlet do HDInsight][hdinsight-powershell-reference]
* [Administrar HDInsight usando Olá portal do Azure][hdinsight-admin-portal]
* [Administrar o HDInsight usando uma interface de linha de comando][hdinsight-admin-cli]
* [Criar clusters HDInsight][hdinsight-provision]
* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Enviar trabalhos Hadoop de forma programática][hdinsight-submit-jobs]
* [Introdução ao Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
