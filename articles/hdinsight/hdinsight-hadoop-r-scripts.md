---
title: aaaUse R em clusters do HDInsight toocustomize - Azure | Microsoft Docs
description: "Saiba como tooinstall R usando scripts de ação e use R em clusters de HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Instalar e usar R em clusters Hadoop do HDInsight (visualização)

Saiba como toocustomize Windows baseado em cluster HDInsight com R usando a ação de Script e como clusters de toouse R no HDInsight. Olá [HDInsight oferta](https://azure.microsoft.com/pricing/details/hdinsight/) inclui R Server como parte do seu cluster HDInsight. Isso permite que scripts R toouse MapReduce e Spark cálculos de toorun distribuído. Para saber mais, veja [Introdução ao uso do Servidor R no HDInsight](hdinsight-hadoop-r-server-get-started.md). Para obter informações sobre como usar o R com um cluster baseado no Linux, veja [Instalar e usar o R em clusters Hadoop do HDinsight (Linux)](hdinsight-hadoop-r-scripts-linux.md).

Você pode instalar o R em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*. Tooinstall um script de exemplo R em um cluster HDInsight está disponível de um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Artigos relacionados**

* [Instalar e usar R em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre como criar clusters HDInsight
* [Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script
* [Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>O que é R?
Olá <a href="http://www.r-project.org/" target="_blank">projeto de R para computação estatística</a> é uma linguagem de código aberto e o ambiente de computação de estatísticas. O R fornece centenas de funções estatísticas de compilação e uma linguagem própria de programação que combina aspectos da programação funcional e orientada a objeto. Ele também fornece recursos abrangentes de gráficos. R é o ambiente de programação preferida Olá para mais profissional estatísticos e cientistas em uma ampla variedade de campos.

O R é compatível com o armazenamento de Blob do Azure (WASB) para que os dados armazenados nele possam ser processados usando R no HDInsight.  

## <a name="install-r"></a>Instalar R
Um [script de exemplo](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R em um cluster HDInsight está disponível de um blob somente leitura no armazenamento do Azure. Esta seção fornece instruções sobre como toouse Olá script de exemplo durante a criação de cluster hello usando Olá Portal do Azure.

> [!NOTE]
> script de exemplo Hello foi introduzida com a versão 3.1 do cluster HDInsight. Para obter mais informações sobre versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).
>
>

1. Quando você cria um cluster HDInsight da saudação Portal, clique em **configuração opcional**e, em seguida, clique em **ações de Script**.
2. Em Olá **ações de Script** insira Olá valores a seguir:

    ![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize de ação de Script de Use um cluster")

    <table border='1'>
        <tr><th>Propriedade</th><th>Valor</th></tr>
        <tr><td>Nome</td>
            <td>Especifique um nome para a ação de script hello, por exemplo, <b>instalar R</b>.</td></tr>
        <tr><td>URI do script</td>
            <td>Especificar Olá URI toohello script que é invocado toocustomize cluster do hello, por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Tipo de nó</td>
            <td>Especifica Olá nós em que o script de personalização de saudação é executado. Você pode escolher <b>Todos os Nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.
        <tr><td>parâmetros</td>
            <td>Especifica parâmetros de hello, se exigido pelo script hello. No entanto, Olá tooinstall de script R não requer nenhum parâmetro, você poderá deixar isso em branco.</td></tr>
    </table>

    Você pode adicionar mais de um tooinstall de ação de script vários componentes no cluster hello. Depois de adicionar scripts de saudação, clique em Olá toostart de marca de seleção Criar cluster hello.

Você também pode usar o hello tooinstall de script R no HDInsight usando o Azure PowerShell ou hello HDInsight .NET SDK. Instruções para esses procedimentos são fornecidas posteriormente neste artigo.

## <a name="run-r-scripts"></a>Executar scripts de R
Esta seção descreve como o script hello Hadoop toorun um R cluster com HDInsight.

1. **Estabelecer um cluster de toohello de conexão de área de trabalho remota**: da saudação Portal, habilitar a área de trabalho remota para cluster Olá criado com R instalado e conecte toohello cluster. Para obter instruções, consulte [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Console aberto Olá R**: instalação Olá R coloca um console de toohello R link na área de trabalho de saudação do nó principal hello. Clique no console do tooopen Olá R.
3. **Execute o script hello R**: script hello R pode ser executado diretamente no console de saudação R colando-o, selecionando-o e pressionando ENTER. Este é um script de exemplo simples que gera Olá números de 1 too100 e multiplica por 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Olá duas primeiras linhas chamada hello RHadoop bibliotecas que são instaladas com R. Olá linha final imprime Olá resultados toohello console. saída de Hello deve ter esta aparência:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Instalar o R usando o Azure PowerShell
Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemplo Hello demonstra como tooinstall Spark usando o PowerShell do Azure. Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>Instalar o R usando o SDK do .NET
Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemplo Hello demonstra como tooinstall Spark usando Olá .NET SDK. Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Consulte também
* [Instalar e usar R em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre como criar clusters HDInsight
* [Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script
* [Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)
* [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark
* [Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de Ação de Script sobre a instalação do Giraph
* [Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md): exemplo de Ação de Script sobre a instalação do Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
