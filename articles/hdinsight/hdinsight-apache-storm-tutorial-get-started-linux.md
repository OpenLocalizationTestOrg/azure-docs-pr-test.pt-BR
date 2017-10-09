---
title: exemplos de starter aaaStorm no Apache Storm no HDInsight - Azure | Microsoft Docs
description: "Saiba como análise de big data toodo e processar dados em tempo real usando o Apache Storm e Olá exemplos starter storm no HDInsight."
keywords: storm-starter, exemplo do apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="16cda-104">Introdução ao Apache Storm no HDInsight usando Olá storm starter exemplos</span><span class="sxs-lookup"><span data-stu-id="16cda-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="16cda-105">Saiba como toouse Apache Storm HDInsight usando Olá exemplos storm starter.</span><span class="sxs-lookup"><span data-stu-id="16cda-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="16cda-106">O Apache Storm é um sistema de computação escalável, tolerante a falhas, distribuído e em tempo real para o processamento de fluxos de dados.</span><span class="sxs-lookup"><span data-stu-id="16cda-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="16cda-107">Com o Storm no Azure HDInsight, você pode criar um cluster Storm baseado em nuvem que execute análise de big data em tempo real.</span><span class="sxs-lookup"><span data-stu-id="16cda-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16cda-108">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="16cda-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="16cda-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="16cda-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16cda-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="16cda-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="16cda-111">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="16cda-111">**An Azure subscription**.</span></span> <span data-ttu-id="16cda-112">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="16cda-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="16cda-113">**Familiaridade com o SSH e o SCP**.</span><span class="sxs-lookup"><span data-stu-id="16cda-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="16cda-114">Para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="16cda-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="16cda-115">Criar um cluster Storm</span><span class="sxs-lookup"><span data-stu-id="16cda-115">Create a Storm cluster</span></span>

<span data-ttu-id="16cda-116">Use Olá seguindo as etapas toocreate uma tempestade no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="16cda-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="16cda-117">De saudação [portal do Azure](https://portal.azure.com), selecione **+ novo**, **Intelligence + análise**e, em seguida, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="16cda-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Criar um cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="16cda-119">De saudação **Noções básicas sobre** folha, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="16cda-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="16cda-120">**Nome do cluster**: nome de saudação do cluster do HDInsight de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="16cda-121">**Assinatura**: selecione Olá toouse de assinatura.</span><span class="sxs-lookup"><span data-stu-id="16cda-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="16cda-122">**Nome de usuário de logon de cluster** e **senha de logon de Cluster**: logon Olá ao acessar o cluster Olá via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="16cda-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="16cda-123">Você usa esses serviços de tooaccess de credenciais como saudação da interface do usuário do Ambari Web ou a API REST.</span><span class="sxs-lookup"><span data-stu-id="16cda-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="16cda-124">**Secure Shell (SSH) username**: logon Olá usado ao acessar o cluster Olá via SSH.</span><span class="sxs-lookup"><span data-stu-id="16cda-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="16cda-125">Por padrão senha Olá é Olá igual à senha de logon de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="16cda-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="16cda-126">**Grupo de recursos**: Olá recurso grupo toocreate Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="16cda-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="16cda-127">**Local**: Olá região do Azure toocreate Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="16cda-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Escolha a assinatura](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="16cda-129">Selecione **tipo de Cluster**, e conjunto Olá seguindo os valores na Olá **configuração de Cluster** folha:</span><span class="sxs-lookup"><span data-stu-id="16cda-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="16cda-130">**Tipo de Cluster**: Storm</span><span class="sxs-lookup"><span data-stu-id="16cda-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="16cda-131">**Sistema Operacional**: Linux</span><span class="sxs-lookup"><span data-stu-id="16cda-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="16cda-132">**Versão**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="16cda-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="16cda-133">**Camada de Cluster**: Padrão</span><span class="sxs-lookup"><span data-stu-id="16cda-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="16cda-134">Por fim, use Olá **selecione** toosave configurações de botão.</span><span class="sxs-lookup"><span data-stu-id="16cda-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Selecione o tipo de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="16cda-136">Depois de selecionar o tipo de cluster hello, use Olá __selecione__ tooset Olá cluster tipo de botão.</span><span class="sxs-lookup"><span data-stu-id="16cda-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="16cda-137">Em seguida, use Olá __próximo__ configuração básica do botão toofinish.</span><span class="sxs-lookup"><span data-stu-id="16cda-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="16cda-138">De saudação **armazenamento** folha, selecione ou crie uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="16cda-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="16cda-139">Para obter etapas Olá neste documento, deixe Olá outros campos nesta folha com valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="16cda-140">Saudação de uso __próximo__ configuração de armazenamento de toosave do botão.</span><span class="sxs-lookup"><span data-stu-id="16cda-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Definir configurações de conta de armazenamento Olá para HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="16cda-142">De saudação **resumo** folha, examinar a configuração de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="16cda-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="16cda-143">Saudação de uso __editar__ links toochange todas as configurações que estão incorretas.</span><span class="sxs-lookup"><span data-stu-id="16cda-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="16cda-144">Por fim, use o cluster de saudação do the__Create__ botão toocreate.</span><span class="sxs-lookup"><span data-stu-id="16cda-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Resumo da configuração do cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="16cda-146">Pode demorar até o cluster de saudação de toocreate too20 minutos.</span><span class="sxs-lookup"><span data-stu-id="16cda-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="16cda-147">Executar uma amostra do storm-starter no HDInsight</span><span class="sxs-lookup"><span data-stu-id="16cda-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="16cda-148">Conecte o cluster do HDInsight toohello usando SSH:</span><span class="sxs-lookup"><span data-stu-id="16cda-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="16cda-149">Se você usou uma senha toosecure sua conta de usuário SSH, é solicitada tooentê-lo.</span><span class="sxs-lookup"><span data-stu-id="16cda-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="16cda-150">Se você usou uma chave pública, você pode precisar usar Olá `-i` toospecify parâmetro hello chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="16cda-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="16cda-151">Por exemplo: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="16cda-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="16cda-152">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="16cda-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="16cda-153">Use Olá comando toostart uma topologia de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="16cda-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="16cda-154">Em versões anteriores do HDInsight, o nome da classe de saudação da topologia de saudação é `storm.starter.WordCountTopology` em vez de `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="16cda-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="16cda-155">Esse comando inicia a topologia de WordCount do exemplo hello no cluster hello, com um nome amigável do 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="16cda-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="16cda-156">Ele gera aleatoriamente frases e a ocorrência de saudação de contagem de cada palavra em frases hello.</span><span class="sxs-lookup"><span data-stu-id="16cda-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16cda-157">Ao enviar seu próprio cluster toohello de topologias, primeiro você deve copiar o arquivo jar de saudação contendo cluster Olá antes de usar o hello `storm` comando.</span><span class="sxs-lookup"><span data-stu-id="16cda-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="16cda-158">Saudação de uso `scp` arquivo de saudação do comando toocopy.</span><span class="sxs-lookup"><span data-stu-id="16cda-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="16cda-159">Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="16cda-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="16cda-160">exemplo de WordCount Hello e outros exemplos storm starter, já estão incluídos no cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="16cda-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="16cda-161">Se você estiver interessado em Exibir código-fonte para obter exemplos de starter storm Olá Olá, você pode encontrar o código de saudação em [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="16cda-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="16cda-162">O link é para o Storm 1.1, que é fornecido com o HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="16cda-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="16cda-163">Para outras versões do Storm, use Olá __ramificação__ botão na parte superior de saudação do hello página tooselect uma versão diferente do Storm.</span><span class="sxs-lookup"><span data-stu-id="16cda-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="16cda-164">Topologia de saudação do monitor</span><span class="sxs-lookup"><span data-stu-id="16cda-164">Monitor hello topology</span></span>

<span data-ttu-id="16cda-165">Olá profusão de interface do usuário fornece uma interface da web para trabalhar com a execução de topologias e está incluída no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16cda-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="16cda-166">Use Olá topologia de saudação toomonitor etapas usando Olá profusão de interface do usuário a seguir:</span><span class="sxs-lookup"><span data-stu-id="16cda-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="16cda-167">Olá toodisplay profusão de interface de usuário, abra uma web navegador toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="16cda-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="16cda-168">Substituir **CLUSTERNAME** com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="16cda-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="16cda-169">Se for solicitado tooprovide um nome de usuário e senha, insira o administrador de cluster de saudação (administrador) e a senha que você usou quando criar cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="16cda-170">Em **Resumo da topologia**, selecione Olá **wordcount** entrada hello **nome** coluna.</span><span class="sxs-lookup"><span data-stu-id="16cda-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="16cda-171">Informações sobre topologia de saudação são exibidas.</span><span class="sxs-lookup"><span data-stu-id="16cda-171">Information about hello topology is displayed.</span></span>

    ![Painel do Storm com informações da topologia do storm-starter WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="16cda-173">Esta página fornece Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="16cda-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="16cda-174">**Estatísticas de topologia** -informações básicas sobre o desempenho de topologia hello, organizados em janelas de tempo.</span><span class="sxs-lookup"><span data-stu-id="16cda-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="16cda-175">Selecionando uma janela de tempo de saudação do tempo específico janela alterações das informações exibidas em outras seções da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="16cda-176">**Spouts** -informações básicas sobre spouts, incluindo o último erro de saudação retornado por cada spout.</span><span class="sxs-lookup"><span data-stu-id="16cda-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="16cda-177">**Bolts** -informações básicas sobre bolts.</span><span class="sxs-lookup"><span data-stu-id="16cda-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="16cda-178">**Configuração de topologia** -informações detalhadas sobre configuração de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="16cda-179">Essa página também fornece ações que podem ser executadas na topologia hello:</span><span class="sxs-lookup"><span data-stu-id="16cda-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="16cda-180">**Ativar** - retoma o processamento de uma topologia desativada.</span><span class="sxs-lookup"><span data-stu-id="16cda-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="16cda-181">**Desativar** - pausa uma topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="16cda-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="16cda-182">**Reequilibrar** -ajusta o paralelismo de saudação da topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="16cda-183">Você deve reequilibrar topologias em execução depois que você tenha alterado Olá número de nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="16cda-184">Rebalanceamento ajusta o paralelismo toocompensate para número de saudação aumentado/reduzido de nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="16cda-185">Para obter mais informações, consulte [Noções básicas sobre o paralelismo de saudação de uma topologia Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="16cda-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="16cda-186">**Kill** -encerra uma topologia Storm depois Olá especificada de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="16cda-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="16cda-187">Nessa página, selecione uma entrada de saudação **Spouts** ou **Bolts** seção.</span><span class="sxs-lookup"><span data-stu-id="16cda-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="16cda-188">Informações sobre o componente de saudação selecionado são exibidas.</span><span class="sxs-lookup"><span data-stu-id="16cda-188">Information about hello selected component is displayed.</span></span>

    ![Painel do Storm com informações sobre os componentes selecionados.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="16cda-190">Esta página exibe o saudação informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="16cda-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="16cda-191">**Estatísticas de spout/raio** -informações básicas sobre o desempenho de componente hello, organizados em janelas de tempo.</span><span class="sxs-lookup"><span data-stu-id="16cda-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="16cda-192">Selecionando uma janela de tempo de saudação do tempo específico janela alterações das informações exibidas em outras seções da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="16cda-193">**Estatísticas de entrada** (incluem apenas) - informações sobre os componentes que geram dados consumidos pelo raio hello.</span><span class="sxs-lookup"><span data-stu-id="16cda-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="16cda-194">**Estatísticas de saída** -informações sobre dados emitidos por este bolt.</span><span class="sxs-lookup"><span data-stu-id="16cda-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="16cda-195">**Executores** -informações sobre instâncias deste componente.</span><span class="sxs-lookup"><span data-stu-id="16cda-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="16cda-196">**Erros** -erros produzidos por este componente.</span><span class="sxs-lookup"><span data-stu-id="16cda-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="16cda-197">Ao exibir detalhes de saudação de um spout ou raio, selecione uma entrada da saudação **porta** coluna Olá **executores** tooview detalhes para uma instância específica do componente de saudação de seção.</span><span class="sxs-lookup"><span data-stu-id="16cda-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="16cda-198">Neste exemplo, hello word **sete** ocorreu 1493957 vezes.</span><span class="sxs-lookup"><span data-stu-id="16cda-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="16cda-199">Essa contagem é quantas vezes word Olá foi encontrado desde que esta topologia foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="16cda-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="16cda-200">Parar a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="16cda-200">Stop hello topology</span></span>

<span data-ttu-id="16cda-201">Retornar toohello **Resumo da topologia** página topologia de contagem de palavras hello e selecione Olá **Kill** botão da saudação **ações de topologia** seção.</span><span class="sxs-lookup"><span data-stu-id="16cda-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="16cda-202">Quando solicitado, insira 10 para Olá toowait de segundos antes de parar a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="16cda-203">Após o período de tempo limite de saudação topologia Olá deixará de aparecer quando você visita Olá **profusão de interface do usuário** seção do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="16cda-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="16cda-204">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="16cda-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="16cda-205">Se você tiver um problema com a criação de clusters HDInsight, consulte [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="16cda-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="16cda-206"><a id="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16cda-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="16cda-207">Neste tutorial do Apache Storm, você aprendeu os fundamentos de saudação do trabalho com Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16cda-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="16cda-208">Em seguida, Aprenda como muito[topologias em Java desenvolver usando Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="16cda-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="16cda-209">Se você já estiver familiarizado com o desenvolvimento baseado em Java topologias e deseja toodeploy um tooHDInsight de topologia existente, consulte [implantar e gerenciar as topologias do Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="16cda-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="16cda-210">Se você for um desenvolvedor .NET, poderá criar topologias em C# ou híbridas C#/Java usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16cda-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="16cda-211">Para obter mais informações, consulte [Desenvolver topologias C# para o Apache Storm no HDInsight usando ferramentas do Hadoop para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="16cda-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="16cda-212">Para topologias de exemplo que podem ser usadas com Storm no HDInsight, consulte Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="16cda-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="16cda-213">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="16cda-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
