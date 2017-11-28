---
title: aaaDeploy e gerenciar as topologias do Apache Storm no HDInsight baseados em Linux | Microsoft Docs
description: "Saiba como toodeploy, monitorar e gerenciar topologias Apache Storm usando Olá profusão de painel no HDInsight baseados em Linux. Use as ferramentas do Hadoop para Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="66431-104">Implantar e gerenciar topologias Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="66431-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="66431-105">Neste documento, conheça os fundamentos de saudação do gerenciamento e monitoramento topologias Storm em execução em Storm em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66431-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66431-106">Olá etapas neste artigo exigem uma tempestade baseados em Linux no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66431-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="66431-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="66431-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="66431-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="66431-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="66431-109">Para obter informações sobre as topologias de implantação e monitoramento em HDInsight baseado em Windows, consulte [Implantar e gerenciar topologias do Apache Storm no HDInsight baseado em Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="66431-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="66431-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66431-110">Prerequisites</span></span>

* <span data-ttu-id="66431-111">**Storm baseado em Linux no cluster HDInsight**: consulte [Introdução com o Apache Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) para etapas para criar um cluster</span><span class="sxs-lookup"><span data-stu-id="66431-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="66431-112">(Opcional) **Familiaridade com SSH e SCP**: para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="66431-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="66431-113">(Opcional) **Visual Studio**: SDK do Azure 2.5.1 ou mais recente e hello Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66431-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="66431-114">Para obter mais informações, consulte [Introdução ao uso das Ferramentas do Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="66431-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="66431-115">Um dos Olá seguintes versões do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="66431-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="66431-116">Visual Studio 2012 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="66431-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="66431-117">Visual Studio 2013 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="66431-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="66431-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="66431-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="66431-119">Visual Studio 2015 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="66431-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="66431-120">Visual Studio 2017 (qualquer edição).</span><span class="sxs-lookup"><span data-stu-id="66431-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="66431-121">Data Lake Tools para Visual Studio de 2017 são instalados como parte da saudação carga de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="66431-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="66431-122">Enviar uma topologia: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66431-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="66431-123">Ferramentas do HDInsight Olá pode ser usado toosubmit c# ou híbrido topologias tooyour cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="66431-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="66431-124">Olá, as etapas a seguir usa um aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="66431-124">hello following steps use a sample application.</span></span> <span data-ttu-id="66431-125">Para obter informações sobre como criar seus próprio topologias usando ferramentas do HDInsight hello, consulte [desenvolver c# topologias usando ferramentas do HDInsight Olá para o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="66431-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="66431-126">Se já não tiver instalado a versão mais recente Olá das ferramentas de Data Lake Olá para o Visual Studio, consulte [começar a usar Data Lake Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="66431-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="66431-127">Olá Data Lake Tools para Visual Studio foram anteriormente chamado hello ferramentas do HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66431-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="66431-128">Data Lake Tools para Visual Studio são incluídos no hello __carga de trabalho do Azure__ para 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66431-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="66431-129">Abra o Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="66431-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="66431-130">Em Olá **novo projeto** caixa de diálogo caixa, expanda **instalado** > **modelos**e, em seguida, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="66431-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="66431-131">Saudação de modelos, selecione lista **profusão de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="66431-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="66431-132">Na parte inferior do Olá Olá da caixa de diálogo, digite um nome para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="66431-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![imagem](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="66431-134">Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="66431-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="66431-135">Se solicitado, insira as credenciais de logon de saudação para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="66431-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="66431-136">Se você tiver mais de uma assinatura, faça logon toohello que contém seu Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66431-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="66431-137">Selecione seu Storm no cluster HDInsight Olá **Cluster Storm** lista suspensa e selecione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="66431-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="66431-138">Você pode monitorar se o envio de saudação foi bem-sucedida usando Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="66431-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="66431-139">Enviar uma topologia: SSH e hello profusão de comando</span><span class="sxs-lookup"><span data-stu-id="66431-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="66431-140">Use SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="66431-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="66431-141">Substituir **USERNAME** nome de saudação do seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="66431-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="66431-142">Substitua o **CLUSTERNAME** pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="66431-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="66431-143">Para obter mais informações sobre como usar SSH tooconnect tooyour HDInsight de cluster, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="66431-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="66431-144">Use Olá comando toostart uma topologia de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="66431-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="66431-145">Esse comando inicia a topologia de WordCount do exemplo hello no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="66431-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="66431-146">Essa topologia gerar aleatoriamente frases e a ocorrência de saudação de contagem de cada palavra em frases hello.</span><span class="sxs-lookup"><span data-stu-id="66431-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="66431-147">Ao enviar o cluster de toohello de topologia, primeiro você deve copiar o arquivo jar de saudação contendo cluster Olá antes de usar o hello `storm` comando.</span><span class="sxs-lookup"><span data-stu-id="66431-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="66431-148">cluster do toocopy Olá arquivos toohello, você pode usar o hello `scp` comando.</span><span class="sxs-lookup"><span data-stu-id="66431-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="66431-149">Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="66431-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="66431-150">exemplo de WordCount Hello e obter outros exemplos de starter storm, já estão incluídos no cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="66431-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="66431-151">Enviar uma topologia: de forma programática</span><span class="sxs-lookup"><span data-stu-id="66431-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="66431-152">Programaticamente, você pode implantar um tooStorm de topologia no HDInsight comunicando-se com hello serviço Nimbus hospedado no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="66431-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="66431-153">[https://GitHub.com/Azure-Samples/hdinsight-Java-Deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) fornece um exemplo de aplicativo Java que demonstra como toodeploy e iniciar uma topologia através de Olá serviço Nimbus.</span><span class="sxs-lookup"><span data-stu-id="66431-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="66431-154">Monitorar e gerenciar: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66431-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="66431-155">Quando uma topologia tiver sido enviada com êxito usando o Visual Studio, Olá **Storm topologias** exibir para Olá cluster aparece.</span><span class="sxs-lookup"><span data-stu-id="66431-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="66431-156">Selecione topologia Olá Olá listar tooview informações sobre Olá executando topologia.</span><span class="sxs-lookup"><span data-stu-id="66431-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![monitor do visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="66431-158">Você também pode exibir **Topologias Storm** no **Gerenciador de Servidores** expandindo **Azure** > **HDInsight** e clicando com o botão direito do mouse em um Storm no cluster do HDInsight e selecionando **Exibir Topologias Storm**.</span><span class="sxs-lookup"><span data-stu-id="66431-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="66431-159">Selecione a forma de Olá Olá spouts ou bolts tooview informações sobre esses componentes.</span><span class="sxs-lookup"><span data-stu-id="66431-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="66431-160">Uma nova janela será aberta para cada item selecionado.</span><span class="sxs-lookup"><span data-stu-id="66431-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="66431-161">Desativar e reativar</span><span class="sxs-lookup"><span data-stu-id="66431-161">Deactivate and reactivate</span></span>

<span data-ttu-id="66431-162">A desativação de uma topologia pausa até que seja interrompido ou reativado.</span><span class="sxs-lookup"><span data-stu-id="66431-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="66431-163">tooperform essas operações, use Olá __desativar__ e __reativar__ botões na parte superior de saudação do hello __Resumo da topologia__.</span><span class="sxs-lookup"><span data-stu-id="66431-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="66431-164">Rebalanceamento</span><span class="sxs-lookup"><span data-stu-id="66431-164">Rebalance</span></span>

<span data-ttu-id="66431-165">Rebalanceamento uma topologia permite Olá sistema toorevise Olá paralelismo topologia hello.</span><span class="sxs-lookup"><span data-stu-id="66431-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="66431-166">Por exemplo, se você tiver redimensionado Olá cluster tooadd mais notas, rebalanceamento permite que uma topologia de toosee Olá novos nós.</span><span class="sxs-lookup"><span data-stu-id="66431-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="66431-167">toorebalance uma topologia, use Olá __reequilibrar__ botão na parte superior de saudação do hello __Resumo da topologia__.</span><span class="sxs-lookup"><span data-stu-id="66431-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="66431-168">Rebalanceamento uma topologia de primeiro desativa a topologia de saudação, redistribui os trabalhadores uniformemente em cluster hello e finalmente retorna Olá topologia toohello estado antes de rebalanceamento ocorrer.</span><span class="sxs-lookup"><span data-stu-id="66431-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="66431-169">Então se topologia Olá estava ativa, ele fica ativo novamente.</span><span class="sxs-lookup"><span data-stu-id="66431-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="66431-170">Se ela foi desativada, ela permanecerá desativada.</span><span class="sxs-lookup"><span data-stu-id="66431-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="66431-171">Encerrar uma topologia</span><span class="sxs-lookup"><span data-stu-id="66431-171">Kill a topology</span></span>

<span data-ttu-id="66431-172">Topologias Storm continuam em execução até que eles sejam interrompidos ou Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="66431-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="66431-173">toostop uma topologia, use Olá __Kill__ botão na parte superior de saudação do hello __Resumo da topologia__.</span><span class="sxs-lookup"><span data-stu-id="66431-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="66431-174">Monitorar e gerenciar: SSH e hello profusão de comando</span><span class="sxs-lookup"><span data-stu-id="66431-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="66431-175">Olá `storm` utilitário permite que você toowork com a execução de topologias de linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="66431-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="66431-176">Use `storm -h` para uma lista completa de comandos.</span><span class="sxs-lookup"><span data-stu-id="66431-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="66431-177">Topologias de lista</span><span class="sxs-lookup"><span data-stu-id="66431-177">List topologies</span></span>

<span data-ttu-id="66431-178">Use Olá toolist de comando a seguir todas as topologias em execução:</span><span class="sxs-lookup"><span data-stu-id="66431-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="66431-179">Esse comando retorna informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="66431-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="66431-180">Desativar e reativar</span><span class="sxs-lookup"><span data-stu-id="66431-180">Deactivate and reactivate</span></span>

<span data-ttu-id="66431-181">A desativação de uma topologia pausa até que seja interrompido ou reativado.</span><span class="sxs-lookup"><span data-stu-id="66431-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="66431-182">Use Olá toodeactivate de comando a seguir e reativar:</span><span class="sxs-lookup"><span data-stu-id="66431-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="66431-183">Eliminar uma topologia em execução</span><span class="sxs-lookup"><span data-stu-id="66431-183">Kill a running topology</span></span>

<span data-ttu-id="66431-184">As topologias Storm, depois de iniciadas, continuarão em execução até serem interrompidas.</span><span class="sxs-lookup"><span data-stu-id="66431-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="66431-185">toostop uma topologia, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="66431-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="66431-186">Rebalanceamento</span><span class="sxs-lookup"><span data-stu-id="66431-186">Rebalance</span></span>

<span data-ttu-id="66431-187">Rebalanceamento uma topologia permite Olá sistema toorevise Olá paralelismo topologia hello.</span><span class="sxs-lookup"><span data-stu-id="66431-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="66431-188">Por exemplo, se você tiver redimensionado Olá cluster tooadd mais notas, rebalanceamento permite que uma topologia de toosee Olá novos nós.</span><span class="sxs-lookup"><span data-stu-id="66431-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="66431-189">Rebalanceamento uma topologia de primeiro desativa a topologia de saudação, redistribui os trabalhadores uniformemente em cluster hello e finalmente retorna Olá topologia toohello estado antes de rebalanceamento ocorrer.</span><span class="sxs-lookup"><span data-stu-id="66431-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="66431-190">Então se topologia Olá estava ativa, ele fica ativo novamente.</span><span class="sxs-lookup"><span data-stu-id="66431-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="66431-191">Se ela foi desativada, ela permanecerá desativada.</span><span class="sxs-lookup"><span data-stu-id="66431-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="66431-192">Monitorar e gerenciar: interface do usuário do Storm</span><span class="sxs-lookup"><span data-stu-id="66431-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="66431-193">Olá profusão de interface do usuário fornece uma interface da web para trabalhar com a execução de topologias e está incluída no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66431-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="66431-194">Olá tooview Storm da interface do usuário, use um tooopen do navegador da web **https://CLUSTERNAME.azurehdinsight.net/stormui**, onde **CLUSTERNAME** é o nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="66431-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="66431-195">Se for solicitado tooprovide um nome de usuário e senha, insira o administrador de cluster de saudação (administrador) e a senha que você usou quando criar cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="66431-196">Página principal</span><span class="sxs-lookup"><span data-stu-id="66431-196">Main page</span></span>

<span data-ttu-id="66431-197">página principal de saudação do hello profusão de interface do usuário fornece Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="66431-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="66431-198">**Resumo do cluster**: informações básicas sobre cluster de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="66431-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="66431-199">**Resumo da topologia**: uma lista das topologias em execução.</span><span class="sxs-lookup"><span data-stu-id="66431-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="66431-200">Use links Olá tooview esta seção obter mais informações sobre topologias específicas.</span><span class="sxs-lookup"><span data-stu-id="66431-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="66431-201">**Resumo do Supervisor**: informações sobre o supervisor de profusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="66431-202">**Configuração de Nimbus**: configuração Nimbus para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="66431-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="66431-203">Resumo da topologia</span><span class="sxs-lookup"><span data-stu-id="66431-203">Topology summary</span></span>

<span data-ttu-id="66431-204">Selecionar um link de saudação **Resumo da topologia** seção exibe Olá informações sobre topologia Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="66431-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="66431-205">**Resumo de topologia**: informações básicas sobre a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="66431-206">**Ações de topologia**: ações de gerenciamento que você pode executar para a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="66431-207">**Ativar**: retoma o processamento de uma topologia de desativada.</span><span class="sxs-lookup"><span data-stu-id="66431-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="66431-208">**Desativar**: pausa uma topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="66431-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="66431-209">**Reequilibrar**: ajusta o paralelismo de saudação da topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="66431-210">Você deve reequilibrar topologias em execução depois que você tenha alterado Olá número de nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="66431-211">Esta operação permite Olá topologia tooadjust paralelismo toocompensate para Olá aumentando ou diminuindo o número de nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="66431-212">Para obter mais informações, consulte <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Noções básicas sobre o paralelismo de saudação de uma topologia Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="66431-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="66431-213">**Kill**: encerra uma topologia Storm depois Olá especificada de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="66431-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="66431-214">**Estatísticas de topologia**: estatísticas sobre a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="66431-215">tooset Olá período de tempo para Olá restantes entradas na página de saudação, use os links de Olá Olá **janela** coluna.</span><span class="sxs-lookup"><span data-stu-id="66431-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="66431-216">**Spouts**: Olá spouts usados pelo topologia hello.</span><span class="sxs-lookup"><span data-stu-id="66431-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="66431-217">Use os links de saudação na tooview seção para obter mais informações sobre spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="66431-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="66431-218">**Bolts**: Olá parafusos usados pelo topologia hello.</span><span class="sxs-lookup"><span data-stu-id="66431-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="66431-219">Use os links de saudação na tooview seção para obter mais informações sobre parafusos específicos.</span><span class="sxs-lookup"><span data-stu-id="66431-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="66431-220">**Configuração de topologia**: configuração de saudação da topologia de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="66431-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="66431-221">Resumo de Spout e Bolt</span><span class="sxs-lookup"><span data-stu-id="66431-221">Spout and Bolt summary</span></span>

<span data-ttu-id="66431-222">Selecionando um spout da saudação **Spouts** ou **Bolts** seções exibe Olá informações sobre o item de saudação selecionada a seguir:</span><span class="sxs-lookup"><span data-stu-id="66431-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="66431-223">**Resumo de componente**: informações básicas sobre spout hello ou raio.</span><span class="sxs-lookup"><span data-stu-id="66431-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="66431-224">**Estatísticas de spout/raio**: estatísticas sobre Olá spout ou parafuso.</span><span class="sxs-lookup"><span data-stu-id="66431-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="66431-225">tooset Olá período de tempo para Olá restantes entradas na página de saudação, use os links de Olá Olá **janela** coluna.</span><span class="sxs-lookup"><span data-stu-id="66431-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="66431-226">**Estatísticas de entrada** (incluem apenas): consumidos pelo raio de saudação de fluxos de entrada de informações sobre hello.</span><span class="sxs-lookup"><span data-stu-id="66431-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="66431-227">**Estatísticas de saída**: informações sobre fluxos de saudação emitidos por essa spout ou parafuso.</span><span class="sxs-lookup"><span data-stu-id="66431-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="66431-228">**Executores**: informações sobre instâncias de saudação do spout hello ou raio.</span><span class="sxs-lookup"><span data-stu-id="66431-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="66431-229">Selecione Olá **porta** gerada de um log de informações de diagnóstico de entrada para tooview um executor específico para essa instância.</span><span class="sxs-lookup"><span data-stu-id="66431-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="66431-230">**Erros**: qualquer informação de erro para este spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="66431-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="66431-231">Monitorar e gerenciar: API REST</span><span class="sxs-lookup"><span data-stu-id="66431-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="66431-232">Olá profusão de interface do usuário é criada sobre Olá API REST, para que você possa executar gerenciamento semelhantes e funcionalidade de monitoramento usando a API REST de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="66431-233">Você pode usar ferramentas personalizadas do toocreate Olá API REST para gerenciar e monitorar as topologias Storm.</span><span class="sxs-lookup"><span data-stu-id="66431-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="66431-234">Para obter mais informações, veja [API REST da interface do usuário do Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="66431-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="66431-235">Olá informações a seguir são específicos toousing Olá API de REST do Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="66431-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66431-236">Olá profusão de REST API não está disponível publicamente em Olá internet e deve ser acessado usando um SSH túnel toohello HDInsight nó principal do cluster.</span><span class="sxs-lookup"><span data-stu-id="66431-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="66431-237">Para obter informações sobre como criar e usar um túnel SSH, consulte [tooaccess Use SSH túnel Ambari web da interface do usuário, ResourceManager, JobHistory, NameNode, Oozie e outras interfaces do usuário da web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="66431-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="66431-238">URI de base</span><span class="sxs-lookup"><span data-stu-id="66431-238">Base URI</span></span>

<span data-ttu-id="66431-239">Olá URI de base para a API REST de saudação em clusters HDInsight baseados em Linux está disponível no nó de cabeçalho de saudação em **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="66431-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="66431-240">nome de domínio de saudação do nó principal Olá é gerado durante a criação do cluster e não é estático.</span><span class="sxs-lookup"><span data-stu-id="66431-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="66431-241">Você pode encontrar o nome de domínio totalmente qualificado (FQDN) Olá para o nó principal do cluster de saudação de várias maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="66431-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="66431-242">**Em uma sessão SSH**: usar o comando Olá `headnode -f` de um cluster de toohello sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="66431-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="66431-243">**Do Ambari Web**: selecione **serviços** da parte superior de saudação da página hello, em seguida, selecione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="66431-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="66431-244">De saudação **resumo** guia, selecione **profusão de interface do usuário servidor**.</span><span class="sxs-lookup"><span data-stu-id="66431-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="66431-245">Olá FQDN do nó Olá Olá profusão de interface do usuário e a API REST está em execução é no início de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="66431-246">**Na API de REST do Ambari**: usar o comando Olá `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve informações sobre o nó Olá Olá profusão de interface do usuário e a API REST estão em execução no.</span><span class="sxs-lookup"><span data-stu-id="66431-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="66431-247">Substituir **senha** com a senha de administrador Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="66431-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="66431-248">Substituir **CLUSTERNAME** com o nome do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="66431-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="66431-249">Em resposta hello, entrada de "host_name" hello contém Olá FQDN do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="66431-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="66431-250">Autenticação</span><span class="sxs-lookup"><span data-stu-id="66431-250">Authentication</span></span>

<span data-ttu-id="66431-251">Solicitações toohello devem usar a API REST **autenticação básica**, portanto, você usa o nome do administrador de cluster de HDInsight de saudação e a senha.</span><span class="sxs-lookup"><span data-stu-id="66431-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="66431-252">Porque a autenticação básica é enviada usando o texto não criptografado, você deve **sempre** usar comunicações toosecure HTTPS com cluster hello.</span><span class="sxs-lookup"><span data-stu-id="66431-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="66431-253">Valores de retorno</span><span class="sxs-lookup"><span data-stu-id="66431-253">Return values</span></span>

<span data-ttu-id="66431-254">Informações que são retornadas da saudação REST API só pode ser usada em cluster hello ou máquinas virtuais em Olá mesma rede Virtual do Azure como cluster hello.</span><span class="sxs-lookup"><span data-stu-id="66431-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="66431-255">Por exemplo, nome de domínio totalmente qualificado de saudação (FQDN) retornado para os servidores de Zookeeper não estará acessível de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="66431-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66431-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66431-256">Next Steps</span></span>

<span data-ttu-id="66431-257">Agora que você aprendeu como topologias toodeploy e monitor usando Olá profusão de painel, saiba como muito[topologias em Java desenvolver usando Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="66431-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="66431-258">Para obter mais topologias de exemplo, consulte [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="66431-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
