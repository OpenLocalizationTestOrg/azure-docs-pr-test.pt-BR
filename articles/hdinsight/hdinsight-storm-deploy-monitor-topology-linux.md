---
title: Implantar e gerenciar topologias Apache Storm no HDInsight baseado em Linux | Microsoft Docs
description: Aprenda a implantar, monitorar e gerenciar topologias do Apache Storm usando o Painel do Storm no HDInsight baseado em Linux. Use as ferramentas do Hadoop para Visual Studio.
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
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="a3dd3-104">Implantar e gerenciar topologias Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a3dd3-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="a3dd3-105">Neste documento, conheça as noções básicas de gerenciamento e monitoramento de topologias Storm em execução no Storm em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3dd3-106">As etapas deste artigo exigem um Storm baseado em Linux no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="a3dd3-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a3dd3-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="a3dd3-109">Para obter informações sobre as topologias de implantação e monitoramento em HDInsight baseado em Windows, consulte [Implantar e gerenciar topologias do Apache Storm no HDInsight baseado em Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="a3dd3-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a3dd3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3dd3-110">Prerequisites</span></span>

* <span data-ttu-id="a3dd3-111">**Storm baseado em Linux no cluster HDInsight**: consulte [Introdução com o Apache Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) para etapas para criar um cluster</span><span class="sxs-lookup"><span data-stu-id="a3dd3-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="a3dd3-112">(Opcional) **Familiaridade com SSH e SCP**: para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="a3dd3-113">(Opcional) **Visual Studio**: SDK do Azure 2.5.1 ou mais novo e as Ferramentas do Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="a3dd3-114">Para obter mais informações, consulte [Introdução ao uso das Ferramentas do Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="a3dd3-115">Uma das seguintes versões do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="a3dd3-116">Visual Studio 2012 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="a3dd3-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="a3dd3-117">Visual Studio 2013 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="a3dd3-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="a3dd3-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a3dd3-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="a3dd3-119">Visual Studio 2015 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="a3dd3-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="a3dd3-120">Visual Studio 2017 (qualquer edição).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="a3dd3-121">As Ferramentas do Data Lake para Visual Studio 2017 são instaladas como parte da Carga de Trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="a3dd3-122">Enviar uma topologia: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3dd3-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="a3dd3-123">As Ferramentas do HDInsight podem ser usadas para enviar topologias C# ou híbridas para seu cluster do Storm.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="a3dd3-124">As etapas a seguir usam um aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-124">The following steps use a sample application.</span></span> <span data-ttu-id="a3dd3-125">Para obter informações sobre como criar suas próprias topologias usando as Ferramentas do HDInsight, consulte [Desenvolver topologias em C# usando as Ferramentas do HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="a3dd3-126">Se você ainda não instalou a última versão das Ferramentas do Data Lake para Visual Studio, consulte [Introdução ao uso das Ferramentas do Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a3dd3-127">Anteriormente, as Ferramentas do Data Lake para Visual Studio se chamavam Ferramentas do HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="a3dd3-128">As Ferramentas do Data Lake para Visual Studio são incluídas na __Carga de Trabalho do Azure__ do Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="a3dd3-129">Abra o Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="a3dd3-130">Na caixa de diálogo **Novo Projeto**, expanda **Instalados** > **Modelos** e selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="a3dd3-131">Na lista de modelos, selecione **Amostra do Storm**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="a3dd3-132">Na parte inferior da caixa de diálogo, digite um nome para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![imagem](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="a3dd3-134">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Enviar para o Storm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a3dd3-135">Se solicitado, insira as credenciais de logon para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="a3dd3-136">Se você tiver mais de uma assinatura, faça o logon naquela que contém seu Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="a3dd3-137">Selecione seu Storm no cluster HDInsight no menu suspenso **Cluster Storm** e selecione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="a3dd3-138">Você pode monitorar se o envio teve êxito ou não usando a janela **Saída** .</span><span class="sxs-lookup"><span data-stu-id="a3dd3-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="a3dd3-139">Enviar uma topologia: SSH e o comando do Storm</span><span class="sxs-lookup"><span data-stu-id="a3dd3-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="a3dd3-140">Use o SSH para conectar ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="a3dd3-141">Substitua o **USERNAME** pelo nome do seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="a3dd3-142">Substitua o **CLUSTERNAME** pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="a3dd3-143">Para saber mais sobre como usar o SSH para se conectar ao cluster HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a3dd3-144">Use o comando a seguir para iniciar uma topologia de exemplo:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="a3dd3-145">Esse comando inicia a topologia de WordCount de exemplo no cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="a3dd3-146">Essa topologia gera frases aleatoriamente e conta a ocorrência de cada palavra nas frases.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a3dd3-147">Ao enviar a topologia para o cluster, primeiro você deverá copiar o arquivo jar com o cluster antes de usar o comando `storm`.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="a3dd3-148">Para copiar o arquivo para o cluster, é possível usar o comando `scp`.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="a3dd3-149">Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="a3dd3-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="a3dd3-150">O exemplo de WordCount e outros exemplos de storm starter já estão incluídos no cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="a3dd3-151">Enviar uma topologia: de forma programática</span><span class="sxs-lookup"><span data-stu-id="a3dd3-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="a3dd3-152">Você pode implantar programaticamente uma topologia para Storm no HDInsight por meio da comunicação com o serviço Nimbus hospedado no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="a3dd3-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) fornece um exemplo de aplicativo Java que demonstra como implantar e iniciar uma topologia por meio do serviço Nimbus.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="a3dd3-154">Monitorar e gerenciar: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3dd3-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="a3dd3-155">Quando uma topologia for enviada com êxito usando o Visual Studio, a exibição **Topologias do Storm** do cluster será mostrada.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="a3dd3-156">Selecione a topologia da lista para exibir informações sobre a topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-156">Select the topology from the list to view information about the running topology.</span></span>

![monitor do visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="a3dd3-158">Você também pode exibir **Topologias Storm** no **Gerenciador de Servidores** expandindo **Azure** > **HDInsight** e clicando com o botão direito do mouse em um Storm no cluster do HDInsight e selecionando **Exibir Topologias Storm**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="a3dd3-159">Escolha a forma dos spouts ou bolts para exibir informações sobre esses componentes.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="a3dd3-160">Uma nova janela será aberta para cada item selecionado.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="a3dd3-161">Desativar e reativar</span><span class="sxs-lookup"><span data-stu-id="a3dd3-161">Deactivate and reactivate</span></span>

<span data-ttu-id="a3dd3-162">A desativação de uma topologia pausa até que seja interrompido ou reativado.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="a3dd3-163">Para executar essas operações, use os botões __Desativar__ e __Reativar__ na parte superior do __Resumo da Topologia__.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="a3dd3-164">Rebalanceamento</span><span class="sxs-lookup"><span data-stu-id="a3dd3-164">Rebalance</span></span>

<span data-ttu-id="a3dd3-165">Rebalancear uma topologia permite que o sistema revise o paralelismo da topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="a3dd3-166">Por exemplo, se você tiver redimensionado o cluster para adicionar mais anotações, o rebalanceamento permitirá que uma topologia veja os novos nós.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="a3dd3-167">Para redistribuir uma topologia, use o botão __Redistribuir__ na parte superior do __Resumo da Topologia__.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="a3dd3-168">Rebalancear uma topologia primeiro desativa a topologia, em seguida, redistribui os trabalhos uniformemente no cluster e finalmente retorna a topologia para o estado que estava antes do rebalanceamento.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="a3dd3-169">Portanto, se a topologia estava ativa, ela ficará ativa novamente.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="a3dd3-170">Se ela foi desativada, ela permanecerá desativada.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="a3dd3-171">Encerrar uma topologia</span><span class="sxs-lookup"><span data-stu-id="a3dd3-171">Kill a topology</span></span>

<span data-ttu-id="a3dd3-172">As topologias Storm continuarão em execução até serem paradas ou até que o cluster seja excluído.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="a3dd3-173">Para interromper uma topologia, use o botão __Encerrar__ na parte superior do __Resumo da Topologia__.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="a3dd3-174">Monitorar e gerenciar: SSH e o comando Storm</span><span class="sxs-lookup"><span data-stu-id="a3dd3-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="a3dd3-175">O `storm` utilitário permite que você trabalhe com as topologias de execução na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="a3dd3-176">Use `storm -h` para uma lista completa de comandos.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="a3dd3-177">Topologias de lista</span><span class="sxs-lookup"><span data-stu-id="a3dd3-177">List topologies</span></span>

<span data-ttu-id="a3dd3-178">Use o comando a seguir para listar todas as topologias em execução:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="a3dd3-179">Esse comando retorna informações semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="a3dd3-180">Desativar e reativar</span><span class="sxs-lookup"><span data-stu-id="a3dd3-180">Deactivate and reactivate</span></span>

<span data-ttu-id="a3dd3-181">A desativação de uma topologia pausa até que seja interrompido ou reativado.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="a3dd3-182">Use o seguinte comando para desativar e reativar:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="a3dd3-183">Eliminar uma topologia em execução</span><span class="sxs-lookup"><span data-stu-id="a3dd3-183">Kill a running topology</span></span>

<span data-ttu-id="a3dd3-184">As topologias Storm, depois de iniciadas, continuarão em execução até serem interrompidas.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="a3dd3-185">Para interrompê-la, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="a3dd3-186">Rebalanceamento</span><span class="sxs-lookup"><span data-stu-id="a3dd3-186">Rebalance</span></span>

<span data-ttu-id="a3dd3-187">Rebalancear uma topologia permite que o sistema revise o paralelismo da topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="a3dd3-188">Por exemplo, se você tiver redimensionado o cluster para adicionar mais anotações, o rebalanceamento permitirá que uma topologia veja os novos nós.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="a3dd3-189">Rebalancear uma topologia primeiro desativa a topologia, em seguida, redistribui os trabalhos uniformemente no cluster e finalmente retorna a topologia para o estado que estava antes do rebalanceamento.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="a3dd3-190">Portanto, se a topologia estava ativa, ela ficará ativa novamente.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="a3dd3-191">Se ela foi desativada, ela permanecerá desativada.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="a3dd3-192">Monitorar e gerenciar: interface do usuário do Storm</span><span class="sxs-lookup"><span data-stu-id="a3dd3-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="a3dd3-193">A IU do Storm fornece uma interface Web para trabalhar com as topologias em funcionamento, e é incluída no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="a3dd3-194">Para ver a interface de usuário do Storm, use um navegador da Web para abrir **https://CLUSTERNAME.azurehdinsight.net/stormui**, em que **CLUSTERNAME** é o nome do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a3dd3-195">Se solicitado a forneça um nome de usuário e senha, insira o administrador de cluster (admin) e a senha que você usou ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="a3dd3-196">Página principal</span><span class="sxs-lookup"><span data-stu-id="a3dd3-196">Main page</span></span>

<span data-ttu-id="a3dd3-197">A página principal da interface do usuário do Storm fornece as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="a3dd3-198">**Resumo do cluster**: informações básicas sobre o cluster do Storm</span><span class="sxs-lookup"><span data-stu-id="a3dd3-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="a3dd3-199">**Resumo da topologia**: uma lista das topologias em execução.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="a3dd3-200">Use os links desta seção para exibir mais informações sobre topologias específicas.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="a3dd3-201">**Resumo do Supervisor**: informações sobre o supervisor do Storm.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="a3dd3-202">**Configuração do Nimbus**: configuração do Nimbus para o cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="a3dd3-203">Resumo da topologia</span><span class="sxs-lookup"><span data-stu-id="a3dd3-203">Topology summary</span></span>

<span data-ttu-id="a3dd3-204">Selecionar um link na seção **Resumo da topologia** exibirá as seguintes informações sobre a topologia:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="a3dd3-205">**Resumo da topologia**: informações básicas sobre a topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="a3dd3-206">**Ações da topologia**: ações de gerenciamento que podem ser executadas para a topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="a3dd3-207">**Ativar**: retoma o processamento de uma topologia de desativada.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="a3dd3-208">**Desativar**: pausa uma topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="a3dd3-209">**Reequilibrar**: ajusta o paralelismo da topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="a3dd3-210">Você deve reequilibrar topologias em execução depois de alterar o número de nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="a3dd3-211">Essa operação permite que a topologia ajuste o paralelismo para compensar o aumento ou a diminuição do número de nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="a3dd3-212">Para saber mais, consulte <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Noções básicas sobre o paralelismo de uma topologia do Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="a3dd3-213">**Eliminar**: encerra uma topologia Storm após o tempo limite especificado.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="a3dd3-214">**Estatísticas da topologia**: estatísticas sobre a topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="a3dd3-215">Para definir o período de tempo para as entradas restantes na página, use os links da coluna **Janela**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="a3dd3-216">**Spouts**: os spouts usados pela topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="a3dd3-217">Use os links desta seção para exibir mais informações sobre spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="a3dd3-218">**Bolts**: os bolts usados pela topologia.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="a3dd3-219">Use os links desta seção para exibir mais informações sobre bolts específicos.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="a3dd3-220">**Configuração da topologia**: a configuração da topologia selecionada.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="a3dd3-221">Resumo de Spout e Bolt</span><span class="sxs-lookup"><span data-stu-id="a3dd3-221">Spout and Bolt summary</span></span>

<span data-ttu-id="a3dd3-222">Selecionar um spout nas seções **Spouts** ou **Bolts** exibirá as seguintes informações sobre o item selecionado:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="a3dd3-223">**Resumo do componente**: informações básicas sobre o spout ou o bolt.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="a3dd3-224">**Estatísticas de Spout/Bolt**: estatísticas sobre o spout ou o bolt.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="a3dd3-225">Para definir o período de tempo para as entradas restantes na página, use os links da coluna **Janela**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="a3dd3-226">**Estatísticas de entrada** (somente bolt): informações sobre os streams de entrada consumidos pelo bolt.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="a3dd3-227">**Estatísticas de saída**: informações sobre os streams emitidos por esse spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="a3dd3-228">**Executores**: informações sobre as instâncias do spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="a3dd3-229">Selecione a entrada **Porta** gerada por um executor específico para exibir um log de informações de diagnóstico produzido para esta instância.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="a3dd3-230">**Erros**: qualquer informação de erro para este spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="a3dd3-231">Monitorar e gerenciar: API REST</span><span class="sxs-lookup"><span data-stu-id="a3dd3-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="a3dd3-232">A interface do usuário do Storm é criada sobre a API REST e, portanto, você pode realizar gerenciamento semelhante e monitorar a funcionalidade usando a API REST.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="a3dd3-233">Você pode usar a API REST para criar ferramentas personalizadas para o gerenciamento e o monitoramento de topologias Storm.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="a3dd3-234">Para obter mais informações, veja [API REST da interface do usuário do Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="a3dd3-235">As informações a seguir são específicas para o uso da API REST com Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3dd3-236">A API do REST Storm não está disponível publicamente pela Internet, e deve ser acessada usando um túnel SSH para o nó principal do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="a3dd3-237">Para obter informações sobre como criar e usar um túnel SSH, consulte [Usar um túnel SSH para acessar a interface do usuário da Web do Ambari, ResourceManager, JobHistory, NameNode, Oozie e outras interfaces do usuário da Web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="a3dd3-238">URI de base</span><span class="sxs-lookup"><span data-stu-id="a3dd3-238">Base URI</span></span>

<span data-ttu-id="a3dd3-239">O URI base da API REST em clusters HDInsight baseados em Linux está disponível no nó de cabeçalho em **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="a3dd3-240">O nome de domínio do nó de cabeçalho é gerado durante a criação do cluster e não é estático.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="a3dd3-241">Você pode encontrar o FQDN (Nome de Domínio Totalmente Qualificado) para o nó de cabeçalho do cluster de várias maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="a3dd3-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="a3dd3-242">**De uma sessão SSH**: use o comando `headnode -f` de uma sessão SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="a3dd3-243">**Do Ambari Web**: selecione **Serviços** na parte superior da página, em seguida, selecione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="a3dd3-244">Na guia **Resumo** selecione **Servidor de IU do Storm**.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="a3dd3-245">O FQDN do nó que a interface do usuário do Storm e a API REST estão executando está na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="a3dd3-246">**Da API REST do Ambari**: use o comando `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` para recuperar informações sobre o nó no qual a interface do usuário do Storm e a API REST estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="a3dd3-247">Substitua **SENHA** pela senha do administrador do cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="a3dd3-248">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="a3dd3-249">Na resposta, a entrada "host_name" contém o FQDN do nó.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="a3dd3-250">Autenticação</span><span class="sxs-lookup"><span data-stu-id="a3dd3-250">Authentication</span></span>

<span data-ttu-id="a3dd3-251">As solicitações para a API REST devem usar a **autenticação básica**e, portanto, você usará o nome do administrador e a senha do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="a3dd3-252">Como a autenticação básica é enviada usando texto não criptografado, você **sempre** deverá usar HTTPS para proteger as comunicações com o cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="a3dd3-253">Valores de retorno</span><span class="sxs-lookup"><span data-stu-id="a3dd3-253">Return values</span></span>

<span data-ttu-id="a3dd3-254">As informações retornadas da API REST só poderão ser usadas dentro do cluster ou de máquinas virtuais na mesma Rede Virtual do Azure que o cluster.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="a3dd3-255">Por exemplo, o FQDN (nome de domínio totalmente qualificado) retornado para servidores Zookeeper não é acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="a3dd3-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3dd3-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3dd3-256">Next Steps</span></span>

<span data-ttu-id="a3dd3-257">Agora que você aprendeu a implantar e monitorar topologias usando o Painel do Storm, saiba como [Desenvolver topologias baseadas em Java usando Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="a3dd3-258">Para obter mais topologias de exemplo, consulte [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a3dd3-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
