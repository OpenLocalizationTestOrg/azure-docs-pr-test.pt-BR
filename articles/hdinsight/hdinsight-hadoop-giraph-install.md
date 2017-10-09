---
title: clusters aaaInstall e uso de Giraph no Hadoop no HDInsight - Azure | Microsoft Docs
description: Saiba como toocustomize HDInsight cluster com Giraph e toouse Giraph.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Instalar e usar o Giraph em clusters HDInsight baseados no Windows

Saiba como toocustomize Windows com base no cluster HDInsight com Giraph usando a ação de Script e toouse Giraph tooprocess em larga escala gráficos. Para obter informações sobre como usar o Giraph com um cluster baseado no Linux, consulte [Instalar o Giraph em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows. O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obter informações sobre como tooinstall Giraph em um cluster HDInsight baseados em Linux, consulte [Giraph instalar em clusters de HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).


Você pode instalar o Giraph em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*. Tooinstall um script de exemplo Giraph em um cluster HDInsight está disponível de um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). script de exemplo Hello funciona apenas com a versão 3.1 do cluster HDInsight. Para obter mais informações sobre as versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).

**Artigos relacionados**

* [Instalar o Giraph em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight
* [Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.
* [Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-giraph"></a>O que é Giraph?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight. Gráficos de modelar relações entre objetos, como conexões Olá entre roteadores em uma rede grande como saudação da Internet, ou relações entre as pessoas em redes sociais (às vezes chamado tooas um gráfico social). Processamento de gráfico permite que você tooreason sobre relações de saudação entre objetos em um gráfico, como:

* Identificar possíveis amigos com base em suas relações atuais.
* Identificando a rota mais curta Olá entre dois computadores em uma rede.
* Calculando a classificação de página Olá das páginas da Web.

## <a name="install-giraph-using-portal"></a>Instalar o Giraph usando o Portal
1. Começar a criar um cluster usando Olá **criação personalizada** opção, conforme descrito em [Hadoop criar clusters de HDInsight](hdinsight-provision-clusters.md).
2. Em Olá **ações de Script** página do Assistente de saudação, clique em **Adicionar ação de script** tooprovide detalhes sobre a ação de script hello, conforme mostrado abaixo:

    ![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize de ação de Script de Use um cluster")

    <table border='1'>
        <tr><th>Propriedade</th><th>Valor</th></tr>
        <tr><td>Nome</td>
            <td>Especifique um nome para a ação de script hello. Por exemplo, <b>Instalar o Giraph</b>.</td></tr>
        <tr><td>URI do script</td>
            <td>Especifique o script hello de toohello de identificador de recurso uniforme (URI) que é invocado toocustomize Olá cluster. Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>Tipo de nó</td>
            <td>Especifica Olá nós em que o script de personalização de saudação é executado. Você pode escolher <b>Todos os nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.
        <tr><td>parâmetros</td>
            <td>Especifica parâmetros de hello, se exigido pelo script hello. Olá script tooinstall Giraph não requer nenhum parâmetro, você poderá deixar isso em branco.</td></tr>
    </table>

    Você pode adicionar mais de um tooinstall de ação de script vários componentes no cluster hello. Depois de adicionar scripts de saudação, clique em Olá toostart de marca de seleção Criar cluster hello.

## <a name="use-giraph"></a>Usar o Giraph
Usamos Olá SimpleShortestPathsComputation exemplo toodemonstrate Olá basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementação para localizar o caminho mais curto de saudação entre objetos em um gráfico. Use Olá etapas tooupload Olá exemplo hello e dados exemplo jar, executar um trabalho usando o exemplo de SimpleShortestPathsComputation hello e, em seguida, exibir hello resultados a seguir.

1. Carregar um tooAzure de arquivo de dados de exemplo armazenamento de Blob. Em sua estação de trabalho local, crie um novo arquivo chamado **tiny_graph.txt**. Ela deve conter Olá linhas seguintes:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Carregar Olá tiny_graph.txt arquivo toohello armazenamento primário para o cluster HDInsight. Para obter instruções sobre como tooupload dados, consulte [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md).

    Esses dados descrevem uma relação entre objetos em um gráfico direcionado, usando o formato de saudação [fonte\_id, fonte\_valor [[dest\_id], [borda\_valor],...]]. Cada linha representa uma relação entre um objeto **source\_id** e um ou mais objetos **dest\_id**. Olá **borda\_valor** (ou peso) pode ser pensada como intensidade hello ou distância de conexão Olá entre **source_id** e **dest\_id**.

    Desenhado, e usando o valor hello (ou peso) como a distância Olá entre objetos, Olá acima dados poderia se parecer com:

    ![tiny_graph.txt Desenhado como círculos com linhas de distância variável entre](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Execute o exemplo de SimpleShortestPathsComputation hello. Use Olá seguindo o exemplo hello do Azure PowerShell cmdlets toorun usando o arquivo de tiny_graph.txt hello como entrada.

    > [!IMPORTANT]
    > O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017. Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.
    >
    > Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure. Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    Olá, o exemplo acima, substitua **clustername** com nome de saudação do cluster HDInsight com Giraph instalado.
3. Exibir resultados de saudação. Quando tiver terminado de trabalho hello, Olá resultados serão armazenados em dois arquivos de saída no hello **wasb: / / / exemplo/out/shotestpaths** pasta. Olá arquivos são chamados **parte-m-00001** e **parte-m-00002**. Execute Olá saída de hello toodownload e exibir as etapas a seguir:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Isso criará Olá **saída/exemplo/shortestpaths** estrutura de diretório no diretório atual de saudação na sua estação de trabalho e download Olá duas saída arquivos toothat local.

    Saudação de uso **Cat** cmdlet toodisplay Olá conteúdo arquivos hello:

        Cat example/output/shortestpaths/part*

    saída de Hello deve aparecer a seguir toohello semelhante:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    exemplo de SimpleShortestPathComputation Hello é toostart codificado com o objeto ID 1 e localizar Olá shortest path tooother objetos. Para a saída de hello deve ser lidos como `destination_id distance`, onde distância é Olá valor (ou peso) das bordas Olá percorridas entre o objeto ID 1 e ID de destino hello.

    Visualizar isso, você pode verificar os resultados de saudação percorrerem caminhos mais curto Olá ID 1 e todos os outros objetos. Observe que Olá caminho mais curto entre ID 1 e 4 ID é 5. Essa é a distância total Olá entre <span style="color:orange">ID 1 e 3</span>e, em seguida, <span style="color:red">ID 3 e 4</span>.

    ![Desenho dos objetos como círculos com os percursos mais curtos entre](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Instalar o Giraph usando o Azure PowerShell
Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemplo Hello demonstra como tooinstall Spark usando o PowerShell do Azure. Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Instalar o Giraph usando o SDK do .NET
Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemplo Hello demonstra como tooinstall Spark usando Olá .NET SDK. Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>Consulte também
* [Instalar o Giraph em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight
* [Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.
* [Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)
* [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark.
* [Instalar R em clusters HDInsight][hdinsight-install-r]: exemplo de Ação de Script sobre a instalação do R.
* [Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md): exemplo de Ação de Script sobre a instalação do Solr.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
