---
title: aaaDeploy e gerenciar as topologias do Apache Storm no HDInsight | Microsoft Docs
description: "Saiba como toodeploy, monitorar e gerenciar topologias Apache Storm usando Olá profusão de painel no HDInsight. Use as ferramentas do Hadoop para Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="cae80-104">Implantar e gerenciar topologias Apache Storm no HDInsight baseado no Windows</span><span class="sxs-lookup"><span data-stu-id="cae80-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="cae80-105">Olá profusão de painel permite que você tooeasily implantar e executar o cluster HDInsight do Apache Storm topologias tooyour usando seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="cae80-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="cae80-106">Você também pode usar o hello painel toomonitor e gerenciar topologias em execução.</span><span class="sxs-lookup"><span data-stu-id="cae80-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="cae80-107">Se você usar o Visual Studio, ferramentas do HDInsight Olá para o Visual Studio fornecem recursos semelhantes no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cae80-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="cae80-108">Olá profusão de painel e recursos Storm Olá Olá ferramentas HDInsight dependem Olá profusão de REST API, que pode ser usado toocreate suas próprias soluções de monitoramento e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="cae80-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cae80-109">etapas de saudação neste documento exigem uma tempestade no cluster HDInsight que usa o Windows como sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="cae80-110">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="cae80-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cae80-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cae80-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="cae80-112">Para obter informações sobre como implantar e gerenciar topologias Storm com um cluster HDInsight que usa Linux, veja [Implantar e gerenciar topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="cae80-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cae80-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cae80-113">Prerequisites</span></span>

* <span data-ttu-id="cae80-114">**Apache Storm no HDInsight** - veja [Introdução ao Apache Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started.md) para obter as etapas de criação de um cluster.</span><span class="sxs-lookup"><span data-stu-id="cae80-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="cae80-115">Para Olá **Storm painel**: um navegador da web modernos que dá suporte a HTML5.</span><span class="sxs-lookup"><span data-stu-id="cae80-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="cae80-116">Para **Visual Studio** -2.5.1 do SDK do Azure ou mais recente e hello ferramentas HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cae80-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="cae80-117">Consulte [começar a usar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall e configurar as ferramentas do HDInsight Olá para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cae80-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="cae80-118">Um dos Olá seguintes versões do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="cae80-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="cae80-119">Visual Studio 2012 com Atualização 4</span><span class="sxs-lookup"><span data-stu-id="cae80-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="cae80-120">Visual Studio 2013 com Atualização 4 ou Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="cae80-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="cae80-121">Visual Studio 2015 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="cae80-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="cae80-122">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="cae80-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="cae80-123">Painel Storm</span><span class="sxs-lookup"><span data-stu-id="cae80-123">Storm Dashboard</span></span>

<span data-ttu-id="cae80-124">Olá profusão de painel é uma página da web disponível no seu cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="cae80-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="cae80-125">Olá URL é **https://&lt;clustername >.azurehdinsight.net/**, onde **clustername** é nome de saudação do seu Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cae80-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="cae80-126">Na parte superior do hello da saudação profusão de painel, selecione **topologia enviar**.</span><span class="sxs-lookup"><span data-stu-id="cae80-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="cae80-127">Siga as instruções de saudação em Olá página toorun uma topologia de amostra ou tooupload e execute uma topologia que você criou.</span><span class="sxs-lookup"><span data-stu-id="cae80-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Olá Enviar página topologia][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="cae80-129">Interface do Usuário do Storm</span><span class="sxs-lookup"><span data-stu-id="cae80-129">Storm UI</span></span>

<span data-ttu-id="cae80-130">Olá profusão de painel, selecione Olá **profusão de interface do usuário** link.</span><span class="sxs-lookup"><span data-stu-id="cae80-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="cae80-131">Isso exibe informações sobre o cluster Olá, em adição tooany executando topologias.</span><span class="sxs-lookup"><span data-stu-id="cae80-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![Olá storm ui][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="cae80-133">Com algumas versões do Internet Explorer, você pode descobrir que Olá que profusão de interface do usuário não são atualizados depois que você visitou primeiro-lo.</span><span class="sxs-lookup"><span data-stu-id="cae80-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="cae80-134">Por exemplo, ele não pode mostrar novas topologias de saudação enviada por você, ou pode exibir uma topologia como ativo quando você o desativada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cae80-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="cae80-135">A Microsoft está ciente desse problema e está trabalhando em uma solução.</span><span class="sxs-lookup"><span data-stu-id="cae80-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="cae80-136">Página principal</span><span class="sxs-lookup"><span data-stu-id="cae80-136">Main page</span></span>

<span data-ttu-id="cae80-137">página principal de saudação do hello profusão de interface do usuário fornece Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="cae80-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="cae80-138">**Resumo do cluster**: informações básicas sobre cluster de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="cae80-139">**Resumo da topologia**: uma lista das topologias em execução.</span><span class="sxs-lookup"><span data-stu-id="cae80-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="cae80-140">Use links Olá tooview esta seção obter mais informações sobre topologias específicas.</span><span class="sxs-lookup"><span data-stu-id="cae80-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="cae80-141">**Resumo do Supervisor**: informações sobre o supervisor de profusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="cae80-142">**Configuração de Nimbus**: configuração Nimbus para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="cae80-143">Resumo da topologia</span><span class="sxs-lookup"><span data-stu-id="cae80-143">Topology summary</span></span>

<span data-ttu-id="cae80-144">Selecionar um link de saudação **Resumo da topologia** seção exibe Olá informações sobre topologia Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cae80-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="cae80-145">**Resumo de topologia**: informações básicas sobre a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="cae80-146">**Ações de topologia**: ações de gerenciamento que você pode executar para a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="cae80-147">**Ativar**: retoma o processamento de uma topologia de desativada.</span><span class="sxs-lookup"><span data-stu-id="cae80-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="cae80-148">**Desativar**: pausa uma topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="cae80-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="cae80-149">**Reequilibrar**: ajusta o paralelismo de saudação da topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="cae80-150">Você deve reequilibrar topologias em execução depois que você tenha alterado Olá número de nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="cae80-151">Isso permite Olá topologia tooadjust paralelismo toocompensate para Olá aumentando ou diminuindo o número de nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="cae80-152">Para obter mais informações, consulte [Noções básicas sobre o paralelismo de saudação de uma topologia de Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="cae80-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="cae80-153">**Kill**: encerra uma topologia Storm depois Olá especificada de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="cae80-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="cae80-154">**Estatísticas de topologia**: estatísticas sobre a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="cae80-155">Use os links de Olá Olá **janela** coluna tooset Olá período para Olá restantes entradas na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="cae80-156">**Spouts**: Olá spouts usados pelo topologia hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="cae80-157">Use os links de saudação na tooview seção para obter mais informações sobre spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="cae80-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="cae80-158">**Bolts**: Olá parafusos usados pelo topologia hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="cae80-159">Use os links de saudação na tooview seção para obter mais informações sobre parafusos específicos.</span><span class="sxs-lookup"><span data-stu-id="cae80-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="cae80-160">**Configuração de topologia**: configuração de saudação da topologia de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="cae80-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="cae80-161">Resumo de Spout e Bolt</span><span class="sxs-lookup"><span data-stu-id="cae80-161">Spout and Bolt summary</span></span>

<span data-ttu-id="cae80-162">Selecionando um spout da saudação **Spouts** ou **Bolts** seções exibe Olá informações sobre o item de saudação selecionada a seguir:</span><span class="sxs-lookup"><span data-stu-id="cae80-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="cae80-163">**Resumo de componente**: informações básicas sobre spout hello ou raio.</span><span class="sxs-lookup"><span data-stu-id="cae80-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="cae80-164">**Estatísticas de spout/raio**: estatísticas sobre Olá spout ou parafuso.</span><span class="sxs-lookup"><span data-stu-id="cae80-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="cae80-165">Use os links de Olá Olá **janela** coluna tooset Olá período para Olá restantes entradas na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="cae80-166">**Estatísticas de entrada** (incluem apenas): consumidos pelo raio de saudação de fluxos de entrada de informações sobre hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="cae80-167">**Estatísticas de saída**: informações sobre fluxos de saudação emitidos por essa spout ou parafuso.</span><span class="sxs-lookup"><span data-stu-id="cae80-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="cae80-168">**Executores**: informações sobre instâncias de saudação do spout hello ou raio.</span><span class="sxs-lookup"><span data-stu-id="cae80-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="cae80-169">Selecione Olá **porta** gerada de um log de informações de diagnóstico de entrada para tooview um executor específico para essa instância.</span><span class="sxs-lookup"><span data-stu-id="cae80-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="cae80-170">**Erros**: qualquer informação de erro para este spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="cae80-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="cae80-171">Ferramentas do HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cae80-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="cae80-172">Ferramentas do HDInsight Olá pode ser usado toosubmit c# ou híbrido topologias tooyour cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="cae80-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="cae80-173">Olá, as etapas a seguir usa um aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cae80-173">hello following steps use a sample application.</span></span> <span data-ttu-id="cae80-174">Para obter informações sobre como criar seus próprio topologias usando ferramentas do HDInsight hello, consulte [desenvolver c# topologias usando ferramentas do HDInsight Olá para o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cae80-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="cae80-175">Usar Olá etapas toodeploy uma profusão de tooyour do exemplo a seguir no cluster HDInsight, exibir e gerenciar a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="cae80-176">Se já não tiver instalado a versão mais recente Olá de saudação ferramentas HDInsight para Visual Studio, consulte [começar a usar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cae80-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="cae80-177">Abra o Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="cae80-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="cae80-178">Em Olá **novo projeto** caixa de diálogo caixa, expanda **instalado** > **modelos**e, em seguida, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cae80-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="cae80-179">Saudação de modelos, selecione lista **profusão de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="cae80-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="cae80-180">Na parte inferior do Olá Olá da caixa de diálogo, digite um nome para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![imagem](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="cae80-182">Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cae80-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cae80-183">Se solicitado, insira as credenciais de logon de saudação para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cae80-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="cae80-184">Se você tiver mais de uma assinatura, faça logon toohello que contém seu Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cae80-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="cae80-185">Selecione seu Storm no cluster HDInsight Olá **Cluster Storm** lista suspensa e selecione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="cae80-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="cae80-186">Você pode monitorar se o envio de saudação foi bem-sucedida usando Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="cae80-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="cae80-187">Quando a topologia de saudação foi enviada com êxito, Olá **Storm topologias** para cluster Olá deve aparecer.</span><span class="sxs-lookup"><span data-stu-id="cae80-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="cae80-188">Selecione topologia Olá Olá listar tooview informações sobre Olá executando topologia.</span><span class="sxs-lookup"><span data-stu-id="cae80-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![monitor do visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="cae80-190">Você também pode exibir **Topologias Storm** no **Gerenciador de Servidores** expandindo **Azure** > **HDInsight** e clicando com o botão direito do mouse em um Storm no cluster do HDInsight e selecionando **Exibir Topologias Storm**.</span><span class="sxs-lookup"><span data-stu-id="cae80-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="cae80-191">Selecione a forma de Olá Olá spouts ou bolts tooview informações sobre esses componentes.</span><span class="sxs-lookup"><span data-stu-id="cae80-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="cae80-192">Uma nova janela será aberta para cada item selecionado.</span><span class="sxs-lookup"><span data-stu-id="cae80-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cae80-193">nome de saudação da topologia de saudação é o nome de classe de Olá da topologia de saudação (nesse caso, `HelloWord`,) com um carimbo de hora anexado.</span><span class="sxs-lookup"><span data-stu-id="cae80-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="cae80-194">De saudação **Resumo da topologia** exibição, selecione **Kill** toostop topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cae80-195">Topologias Storm continuam em execução até que eles sejam interrompidos ou Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="cae80-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="cae80-196">API REST</span><span class="sxs-lookup"><span data-stu-id="cae80-196">REST API</span></span>

<span data-ttu-id="cae80-197">Olá profusão de interface do usuário é criada sobre Olá API REST, para que você possa executar gerenciamento semelhantes e funcionalidade de monitoramento usando a API REST de saudação.</span><span class="sxs-lookup"><span data-stu-id="cae80-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="cae80-198">Você pode usar ferramentas personalizadas do toocreate Olá API REST para gerenciar e monitorar as topologias Storm.</span><span class="sxs-lookup"><span data-stu-id="cae80-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="cae80-199">Para obter mais informações, veja [API REST da interface do usuário do Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="cae80-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="cae80-200">Olá informações a seguir são específicos toousing Olá API de REST do Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cae80-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="cae80-201">URI de base</span><span class="sxs-lookup"><span data-stu-id="cae80-201">Base URI</span></span>

<span data-ttu-id="cae80-202">Olá URI base para Olá API REST em clusters de HDInsight é **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, onde **clustername** é o nome de saudação do seu Storm em Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cae80-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="cae80-203">Autenticação</span><span class="sxs-lookup"><span data-stu-id="cae80-203">Authentication</span></span>

<span data-ttu-id="cae80-204">Solicitações toohello devem usar a API REST **autenticação básica**, portanto, você usa o nome do administrador de cluster de HDInsight de saudação e a senha.</span><span class="sxs-lookup"><span data-stu-id="cae80-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="cae80-205">Porque a autenticação básica é enviada usando o texto não criptografado, você deve **sempre** usar comunicações toosecure HTTPS com cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="cae80-206">Valores de retorno</span><span class="sxs-lookup"><span data-stu-id="cae80-206">Return values</span></span>

<span data-ttu-id="cae80-207">Informações que são retornadas da saudação REST API só pode ser usada em cluster hello ou máquinas virtuais em Olá mesma rede Virtual do Azure como cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cae80-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="cae80-208">Por exemplo, nome de domínio totalmente qualificado de saudação (FQDN) retornado para os servidores de Zookeeper não ser acessível de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="cae80-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cae80-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cae80-209">Next Steps</span></span>

<span data-ttu-id="cae80-210">Agora que você aprendeu como topologias toodeploy e monitor usando Olá profusão de painel, saiba como:</span><span class="sxs-lookup"><span data-stu-id="cae80-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="cae80-211">Desenvolver c# topologias usando ferramentas do HDInsight Olá para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cae80-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="cae80-212">Desenvolver topologias baseadas em Java usando Maven</span><span class="sxs-lookup"><span data-stu-id="cae80-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="cae80-213">Para obter mais topologias de exemplo, consulte [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cae80-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
