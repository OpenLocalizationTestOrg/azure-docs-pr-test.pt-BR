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
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="20b18-103">Instalar e usar R em clusters Hadoop do HDInsight (visualização)</span><span class="sxs-lookup"><span data-stu-id="20b18-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="20b18-104">Saiba como toocustomize Windows baseado em cluster HDInsight com R usando a ação de Script e como clusters de toouse R no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20b18-104">Learn how toocustomize Windows based HDInsight cluster with R using Script Action, and how toouse R on HDInsight clusters.</span></span> <span data-ttu-id="20b18-105">Olá [HDInsight oferta](https://azure.microsoft.com/pricing/details/hdinsight/) inclui R Server como parte do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20b18-105">hello [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="20b18-106">Isso permite que scripts R toouse MapReduce e Spark cálculos de toorun distribuído.</span><span class="sxs-lookup"><span data-stu-id="20b18-106">This allows R scripts toouse MapReduce and Spark toorun distributed computations.</span></span> <span data-ttu-id="20b18-107">Para saber mais, veja [Introdução ao uso do Servidor R no HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="20b18-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="20b18-108">Para obter informações sobre como usar o R com um cluster baseado no Linux, veja [Instalar e usar o R em clusters Hadoop do HDinsight (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="20b18-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="20b18-109">Você pode instalar o R em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*.</span><span class="sxs-lookup"><span data-stu-id="20b18-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="20b18-110">Tooinstall um script de exemplo R em um cluster HDInsight está disponível de um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="20b18-110">A sample script tooinstall R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="20b18-111">**Artigos relacionados**</span><span class="sxs-lookup"><span data-stu-id="20b18-111">**Related articles**</span></span>

* [<span data-ttu-id="20b18-112">Instalar e usar R em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="20b18-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="20b18-113">[Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="20b18-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="20b18-114">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="20b18-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="20b18-115">Desenvolver scripts de Ação de Script para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="20b18-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="20b18-116">O que é R?</span><span class="sxs-lookup"><span data-stu-id="20b18-116">What is R?</span></span>
<span data-ttu-id="20b18-117">Olá <a href="http://www.r-project.org/" target="_blank">projeto de R para computação estatística</a> é uma linguagem de código aberto e o ambiente de computação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="20b18-117">hello <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="20b18-118">O R fornece centenas de funções estatísticas de compilação e uma linguagem própria de programação que combina aspectos da programação funcional e orientada a objeto.</span><span class="sxs-lookup"><span data-stu-id="20b18-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="20b18-119">Ele também fornece recursos abrangentes de gráficos.</span><span class="sxs-lookup"><span data-stu-id="20b18-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="20b18-120">R é o ambiente de programação preferida Olá para mais profissional estatísticos e cientistas em uma ampla variedade de campos.</span><span class="sxs-lookup"><span data-stu-id="20b18-120">R is hello preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="20b18-121">O R é compatível com o armazenamento de Blob do Azure (WASB) para que os dados armazenados nele possam ser processados usando R no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20b18-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="20b18-122">Instalar R</span><span class="sxs-lookup"><span data-stu-id="20b18-122">Install R</span></span>
<span data-ttu-id="20b18-123">Um [script de exemplo](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R em um cluster HDInsight está disponível de um blob somente leitura no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="20b18-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="20b18-124">Esta seção fornece instruções sobre como toouse Olá script de exemplo durante a criação de cluster hello usando Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="20b18-124">This section provides instructions about how toouse hello sample script while creating hello cluster using hello Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="20b18-125">script de exemplo Hello foi introduzida com a versão 3.1 do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20b18-125">hello sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="20b18-126">Para obter mais informações sobre versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="20b18-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="20b18-127">Quando você cria um cluster HDInsight da saudação Portal, clique em **configuração opcional**e, em seguida, clique em **ações de Script**.</span><span class="sxs-lookup"><span data-stu-id="20b18-127">When you create an HDInsight cluster from hello Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="20b18-128">Em Olá **ações de Script** insira Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="20b18-128">On hello **Script Actions** page, enter hello following values:</span></span>

    <span data-ttu-id="20b18-129">![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize de ação de Script de Use um cluster")</span><span class="sxs-lookup"><span data-stu-id="20b18-129">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="20b18-130">Propriedade</span><span class="sxs-lookup"><span data-stu-id="20b18-130">Property</span></span></th><th><span data-ttu-id="20b18-131">Valor</span><span class="sxs-lookup"><span data-stu-id="20b18-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="20b18-132">Nome</span><span class="sxs-lookup"><span data-stu-id="20b18-132">Name</span></span></td>
            <td><span data-ttu-id="20b18-133">Especifique um nome para a ação de script hello, por exemplo, <b>instalar R</b>.</span><span class="sxs-lookup"><span data-stu-id="20b18-133">Specify a name for hello script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="20b18-134">URI do script</span><span class="sxs-lookup"><span data-stu-id="20b18-134">Script URI</span></span></td>
            <td><span data-ttu-id="20b18-135">Especificar Olá URI toohello script que é invocado toocustomize cluster do hello, por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="20b18-135">Specify hello URI toohello script that is invoked toocustomize hello cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="20b18-136">Tipo de nó</span><span class="sxs-lookup"><span data-stu-id="20b18-136">Node Type</span></span></td>
            <td><span data-ttu-id="20b18-137">Especifica Olá nós em que o script de personalização de saudação é executado.</span><span class="sxs-lookup"><span data-stu-id="20b18-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="20b18-138">Você pode escolher <b>Todos os Nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.</span><span class="sxs-lookup"><span data-stu-id="20b18-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="20b18-139">parâmetros</span><span class="sxs-lookup"><span data-stu-id="20b18-139">Parameters</span></span></td>
            <td><span data-ttu-id="20b18-140">Especifica parâmetros de hello, se exigido pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="20b18-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="20b18-141">No entanto, Olá tooinstall de script R não requer nenhum parâmetro, você poderá deixar isso em branco.</span><span class="sxs-lookup"><span data-stu-id="20b18-141">However, hello script tooinstall R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="20b18-142">Você pode adicionar mais de um tooinstall de ação de script vários componentes no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="20b18-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="20b18-143">Depois de adicionar scripts de saudação, clique em Olá toostart de marca de seleção Criar cluster hello.</span><span class="sxs-lookup"><span data-stu-id="20b18-143">After you have added hello scripts, click hello check mark toostart crating hello cluster.</span></span>

<span data-ttu-id="20b18-144">Você também pode usar o hello tooinstall de script R no HDInsight usando o Azure PowerShell ou hello HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="20b18-144">You can also use hello script tooinstall R on HDInsight by using Azure PowerShell or hello HDInsight .NET SDK.</span></span> <span data-ttu-id="20b18-145">Instruções para esses procedimentos são fornecidas posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="20b18-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="20b18-146">Executar scripts de R</span><span class="sxs-lookup"><span data-stu-id="20b18-146">Run R scripts</span></span>
<span data-ttu-id="20b18-147">Esta seção descreve como o script hello Hadoop toorun um R cluster com HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20b18-147">This section describes how toorun an R script on hello Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="20b18-148">**Estabelecer um cluster de toohello de conexão de área de trabalho remota**: da saudação Portal, habilitar a área de trabalho remota para cluster Olá criado com R instalado e conecte toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="20b18-148">**Establish a Remote Desktop connection toohello cluster**: From hello Portal, enable Remote Desktop for hello cluster you created with R installed, and then connect toohello cluster.</span></span> <span data-ttu-id="20b18-149">Para obter instruções, consulte [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="20b18-149">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="20b18-150">**Console aberto Olá R**: instalação Olá R coloca um console de toohello R link na área de trabalho de saudação do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="20b18-150">**Open hello R console**: hello R installation puts a link toohello R console on hello desktop of hello head node.</span></span> <span data-ttu-id="20b18-151">Clique no console do tooopen Olá R.</span><span class="sxs-lookup"><span data-stu-id="20b18-151">Click on it tooopen hello R console.</span></span>
3. <span data-ttu-id="20b18-152">**Execute o script hello R**: script hello R pode ser executado diretamente no console de saudação R colando-o, selecionando-o e pressionando ENTER.</span><span class="sxs-lookup"><span data-stu-id="20b18-152">**Run hello R script**: hello R script can be run directly from hello R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="20b18-153">Este é um script de exemplo simples que gera Olá números de 1 too100 e multiplica por 2.</span><span class="sxs-lookup"><span data-stu-id="20b18-153">Here is a simple example script that generates hello numbers 1 too100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="20b18-154">Olá duas primeiras linhas chamada hello RHadoop bibliotecas que são instaladas com R. Olá linha final imprime Olá resultados toohello console.</span><span class="sxs-lookup"><span data-stu-id="20b18-154">hello first two lines call hello RHadoop libraries that are installed with R. hello final line prints hello results toohello console.</span></span> <span data-ttu-id="20b18-155">saída de Hello deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="20b18-155">hello output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="20b18-156">Instalar o R usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="20b18-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="20b18-157">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="20b18-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="20b18-158">exemplo Hello demonstra como tooinstall Spark usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="20b18-158">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="20b18-159">Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="20b18-159">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="20b18-160">Instalar o R usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="20b18-160">Install R using .NET SDK</span></span>
<span data-ttu-id="20b18-161">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="20b18-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="20b18-162">exemplo Hello demonstra como tooinstall Spark usando Olá .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="20b18-162">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="20b18-163">Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="20b18-163">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="20b18-164">Consulte também</span><span class="sxs-lookup"><span data-stu-id="20b18-164">See also</span></span>
* [<span data-ttu-id="20b18-165">Instalar e usar R em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="20b18-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="20b18-166">[Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="20b18-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="20b18-167">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="20b18-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="20b18-168">Desenvolver scripts de Ação de Script para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="20b18-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="20b18-169">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark</span><span class="sxs-lookup"><span data-stu-id="20b18-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="20b18-170">[Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de Ação de Script sobre a instalação do Giraph</span><span class="sxs-lookup"><span data-stu-id="20b18-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="20b18-171">[Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md): exemplo de Ação de Script sobre a instalação do Solr.</span><span class="sxs-lookup"><span data-stu-id="20b18-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
