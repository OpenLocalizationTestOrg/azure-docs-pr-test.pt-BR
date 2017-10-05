---
title: "Usar o R no HDInsight para personalizar clusters – Azure | Microsoft Docs"
description: "Saiba como instalar R usando a Ação de Script e usar R em clusters HDInsight."
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
ms.openlocfilehash: 5b9b793d49217acd9f0c6c518596a7afb5600d69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="b3b5b-103">Instalar e usar R em clusters Hadoop do HDInsight (visualização)</span><span class="sxs-lookup"><span data-stu-id="b3b5b-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="b3b5b-104">Saiba como personalizar o cluster HDInsight baseado em Windows com R usando a Ação de Script, e como usar o R em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="b3b5b-105">A [oferta do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) inclui o Servidor R como parte do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="b3b5b-106">Isso permite que os scripts R usem o MapReduce e o Spark para executar cálculos distribuídos.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="b3b5b-107">Para obter mais informações, confira [Introdução ao uso do Servidor R no HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="b3b5b-108">Para obter informações sobre como usar o R com um cluster baseado no Linux, veja [Instalar e usar o R em clusters Hadoop do HDinsight (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="b3b5b-109">Você pode instalar o R em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="b3b5b-110">Um script de exemplo para instalar o R em um cluster HDInsight está disponível em um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="b3b5b-111">**Artigos relacionados**</span><span class="sxs-lookup"><span data-stu-id="b3b5b-111">**Related articles**</span></span>

* [<span data-ttu-id="b3b5b-112">Instalar e usar R em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="b3b5b-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="b3b5b-113">[Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3b5b-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="b3b5b-114">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="b3b5b-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="b3b5b-115">Desenvolver scripts de Ação de Script para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3b5b-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="b3b5b-116">O que é R?</span><span class="sxs-lookup"><span data-stu-id="b3b5b-116">What is R?</span></span>
<span data-ttu-id="b3b5b-117">O <a href="http://www.r-project.org/" target="_blank">Projeto R para computação de estatísticas</a> é uma linguagem de software livre e um ambiente de computação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="b3b5b-118">O R fornece centenas de funções estatísticas de compilação e uma linguagem própria de programação que combina aspectos da programação funcional e orientada a objeto.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="b3b5b-119">Ele também fornece recursos abrangentes de gráficos.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="b3b5b-120">O R é o ambiente de programação preferencial para a maioria dos profissionais estatísticos e cientistas em uma ampla variedade de campos.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="b3b5b-121">O R é compatível com o armazenamento de Blob do Azure (WASB) para que os dados armazenados nele possam ser processados usando R no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="b3b5b-122">Instalar R</span><span class="sxs-lookup"><span data-stu-id="b3b5b-122">Install R</span></span>
<span data-ttu-id="b3b5b-123">Um [exemplo de script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) para instalar o R em um cluster HDInsight está disponível em um blob somente leitura no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="b3b5b-124">Esta seção oferece instruções sobre como usar o script de exemplo ao criar o cluster usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b3b5b-125">O script de exemplo foi introduzido com o cluster HDInsight versão 3.1.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="b3b5b-126">Para obter mais informações sobre versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="b3b5b-127">Ao criar um cluster HDInsight no Portal, clique em **Configuração Opcional** e em **Ações de Script**.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="b3b5b-128">Na página **Ações de Script** , insira os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="b3b5b-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="b3b5b-129">![Usar Ação de Script para personalizar um cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Usar Ação de Script para personalizar um cluster")</span><span class="sxs-lookup"><span data-stu-id="b3b5b-129">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="b3b5b-130">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b3b5b-130">Property</span></span></th><th><span data-ttu-id="b3b5b-131">Valor</span><span class="sxs-lookup"><span data-stu-id="b3b5b-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="b3b5b-132">Nome</span><span class="sxs-lookup"><span data-stu-id="b3b5b-132">Name</span></span></td>
            <td><span data-ttu-id="b3b5b-133">Especifique um nome para a ação de script, por exemplo, <b>Instalar R</b>.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="b3b5b-134">URI do script</span><span class="sxs-lookup"><span data-stu-id="b3b5b-134">Script URI</span></span></td>
            <td><span data-ttu-id="b3b5b-135">Especifique o URI para o script que é chamado para personalizar o cluster, por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="b3b5b-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="b3b5b-136">Tipo de nó</span><span class="sxs-lookup"><span data-stu-id="b3b5b-136">Node Type</span></span></td>
            <td><span data-ttu-id="b3b5b-137">Especifique os nós em que o script de personalização deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="b3b5b-138">Você pode escolher <b>Todos os Nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="b3b5b-139">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b3b5b-139">Parameters</span></span></td>
            <td><span data-ttu-id="b3b5b-140">Especifique os parâmetros, se exigido pelo script.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="b3b5b-141">No entanto, o script para instalar o R não requer nenhum parâmetro, por isso você pode deixá-los em branco.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="b3b5b-142">Você pode adicionar mais de uma ação de script para instalar vários componentes no cluster.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="b3b5b-143">Depois de adicionar os scripts, clique na marca de seleção para iniciar a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="b3b5b-144">Você também pode usar o script para instalar o R no HDInsight usando o PowerShell do Azure ou o SDK do .NET do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="b3b5b-145">Instruções para esses procedimentos são fornecidas posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="b3b5b-146">Executar scripts de R</span><span class="sxs-lookup"><span data-stu-id="b3b5b-146">Run R scripts</span></span>
<span data-ttu-id="b3b5b-147">Esta seção descreve como executar um script de R no cluster Hadoop com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="b3b5b-148">**Estabelecer uma conexão da Área de Trabalho Remota para o cluster**: no Portal, habilite a Área de Trabalho Remota para o cluster que você criou com o R instalado e conecte-se ao cluster.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="b3b5b-149">Para instruções, consulte [Conectar-se a clusters HDInsight usando RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="b3b5b-150">**Abrir o console do R**: a instalação de R coloca um link para o console de R na área de trabalho do nó principal.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="b3b5b-151">Clique para abrir o console de R.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="b3b5b-152">**Executar o script de R**: o script de R pode ser executado diretamente do console de R colando-o, selecionando-o e pressionando ENTER.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="b3b5b-153">Este é um script de exemplo simples que gera os números de 1 a 100 e, em seguida, os multiplica por 2.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="b3b5b-154">As duas primeiras linhas chamam as bibliotecas R Hadoop que são instaladas com o R. A linha final imprime os resultados no console.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="b3b5b-155">O resultado deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="b3b5b-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="b3b5b-156">Instalar o R usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3b5b-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="b3b5b-157">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="b3b5b-158">O exemplo demonstra como instalar o Spark usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="b3b5b-159">Você precisa personalizar o script para usar [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="b3b5b-160">Instalar o R usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b3b5b-160">Install R using .NET SDK</span></span>
<span data-ttu-id="b3b5b-161">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="b3b5b-162">O exemplo demonstra como instalar o Spark usando o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="b3b5b-163">Você precisa personalizar o script para usar [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="b3b5b-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="b3b5b-164">Confira também</span><span class="sxs-lookup"><span data-stu-id="b3b5b-164">See also</span></span>
* [<span data-ttu-id="b3b5b-165">Instalar e usar R em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="b3b5b-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="b3b5b-166">[Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3b5b-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="b3b5b-167">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="b3b5b-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="b3b5b-168">Desenvolver scripts de Ação de Script para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3b5b-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="b3b5b-169">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark</span><span class="sxs-lookup"><span data-stu-id="b3b5b-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="b3b5b-170">[Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de Ação de Script sobre a instalação do Giraph</span><span class="sxs-lookup"><span data-stu-id="b3b5b-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="b3b5b-171">[Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md): exemplo de Ação de Script sobre a instalação do Solr.</span><span class="sxs-lookup"><span data-stu-id="b3b5b-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
