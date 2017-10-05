---
title: Exemplos de storm-starter no Apache Storm no HDInsight - Azure | Microsoft Docs
description: "Saiba como fazer a análise de big data e processar dados em tempo real usando o Apache Storm e os exemplos de storm-starter no HDInsight."
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
ms.openlocfilehash: 83fc6db1ddb43eb87e7c58684505d7196c1e53d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-the-storm-starter-examples"></a><span data-ttu-id="d0840-104">Introdução ao Apache Storm no HDInsight usando os exemplos do storm-starter</span><span class="sxs-lookup"><span data-stu-id="d0840-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span></span>

<span data-ttu-id="d0840-105">Saiba como usar o Apache Storm no HDInsight usando os exemplos de storm-starter.</span><span class="sxs-lookup"><span data-stu-id="d0840-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span></span>

<span data-ttu-id="d0840-106">O Apache Storm é um sistema de computação escalável, tolerante a falhas, distribuído e em tempo real para o processamento de fluxos de dados.</span><span class="sxs-lookup"><span data-stu-id="d0840-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="d0840-107">Com o Storm no Azure HDInsight, você pode criar um cluster Storm baseado em nuvem que execute análise de big data em tempo real.</span><span class="sxs-lookup"><span data-stu-id="d0840-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0840-108">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="d0840-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d0840-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d0840-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0840-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d0840-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="d0840-111">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d0840-111">**An Azure subscription**.</span></span> <span data-ttu-id="d0840-112">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d0840-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="d0840-113">**Familiaridade com o SSH e o SCP**.</span><span class="sxs-lookup"><span data-stu-id="d0840-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="d0840-114">Para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d0840-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="d0840-115">Criar um cluster Storm</span><span class="sxs-lookup"><span data-stu-id="d0840-115">Create a Storm cluster</span></span>

<span data-ttu-id="d0840-116">Use as seguintes etapas para criar um cluster Storm no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d0840-116">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="d0840-117">No [portal do Azure](https://portal.azure.com), selecione **+ NOVO**, **Inteligência + Análises** e **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d0840-117">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Criar um cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="d0840-119">Na folha **Básico** , insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="d0840-119">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="d0840-120">**Nome do cluster**: o nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0840-120">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="d0840-121">**Assinatura**: selecione a assinatura a ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="d0840-121">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="d0840-122">**Nome de usuário de logon do cluster** e **Senha de logon do cluster**: logon ao acessar o cluster por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d0840-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="d0840-123">Você pode usar essas credenciais para acessar serviços como a interface do usuário da Web do Ambari ou a API REST.</span><span class="sxs-lookup"><span data-stu-id="d0840-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="d0840-124">**Nome de usuário do SSH (Secure Shell)**: o logon usado ao acessar o cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="d0840-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="d0840-125">Por padrão, a senha é a mesma do logon do cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-125">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="d0840-126">**Grupo de Recursos**: o grupo de recursos para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-126">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="d0840-127">**Local**: a região do Azure para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-127">**Location**: The Azure region to create the cluster in.</span></span>

    ![Escolha a assinatura](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="d0840-129">Selecione **Tipo de cluster** e defina os seguintes valores na folha **Configuração de Cluster**:</span><span class="sxs-lookup"><span data-stu-id="d0840-129">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="d0840-130">**Tipo de Cluster**: Storm</span><span class="sxs-lookup"><span data-stu-id="d0840-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="d0840-131">**Sistema Operacional**: Linux</span><span class="sxs-lookup"><span data-stu-id="d0840-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="d0840-132">**Versão**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="d0840-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="d0840-133">**Camada de Cluster**: Padrão</span><span class="sxs-lookup"><span data-stu-id="d0840-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="d0840-134">Por fim, use o botão **Selecionar** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="d0840-134">Finally, use the **Select** button to save settings.</span></span>

    ![Selecione o tipo de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="d0840-136">Depois de selecionar o tipo de cluster, use o botão __Selecionar__ para definir o tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-136">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="d0840-137">Em seguida, use o botão __Avançar__ para concluir a configuração básica.</span><span class="sxs-lookup"><span data-stu-id="d0840-137">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="d0840-138">Na folha **Armazenamento**, selecione ou crie uma Conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d0840-138">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="d0840-139">Para as etapas neste documento, deixe os outros campos nessa folha com os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="d0840-139">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="d0840-140">Use o botão __Avançar__ para salvar a configuração de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d0840-140">Use the __Next__ button to save storage configuration.</span></span>

    ![Definir as configurações de conta de armazenamento do HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="d0840-142">Na folha **Resumo**, examine a configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-142">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="d0840-143">Use os links __Editar__ para alterar as configurações que estão incorretas.</span><span class="sxs-lookup"><span data-stu-id="d0840-143">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="d0840-144">Por fim, use o botão __Criar__ para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-144">Finally, use the__Create__ button to create the cluster.</span></span>

    ![Resumo da configuração do cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="d0840-146">Pode levar até 20 minutos para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-146">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="d0840-147">Executar uma amostra do storm-starter no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0840-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="d0840-148">Conecte-se ao cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="d0840-148">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="d0840-149">Caso você tenha usado uma senha para proteger sua conta de usuário do SSH, ela será solicitada.</span><span class="sxs-lookup"><span data-stu-id="d0840-149">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="d0840-150">Se você tiver usado uma chave pública, talvez precise usar o parâmetro `-i` para especificar a chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="d0840-150">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="d0840-151">Por exemplo: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="d0840-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="d0840-152">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d0840-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d0840-153">Use o comando a seguir para iniciar uma topologia de exemplo:</span><span class="sxs-lookup"><span data-stu-id="d0840-153">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="d0840-154">Em versões anteriores do HDInsight, o nome de classe da topologia é `storm.starter.WordCountTopology` em vez de `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="d0840-154">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="d0840-155">Esse comando inicia a topologia WordCount de exemplo no cluster, com um nome amigável de 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="d0840-155">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="d0840-156">Ela gera sentenças aleatoriamente e conta a ocorrência de cada palavra nas sentenças.</span><span class="sxs-lookup"><span data-stu-id="d0840-156">It randomly generates sentences and count the occurrence of each word in the sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0840-157">Ao enviar suas próprias topologias para o cluster, primeiro você deverá copiar o arquivo jar com o cluster antes de usar o comando `storm`.</span><span class="sxs-lookup"><span data-stu-id="d0840-157">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="d0840-158">Use o comando `scp` para copiar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="d0840-158">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="d0840-159">Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="d0840-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="d0840-160">O exemplo de WordCount e outros exemplos de storm starter já estão incluídos no cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="d0840-160">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="d0840-161">Se você estiver interessado em ver a fonte dos exemplos do storm-starter, poderá encontrar o código em [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="d0840-161">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="d0840-162">O link é para o Storm 1.1, que é fornecido com o HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="d0840-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="d0840-163">Para outras versões do Storm, use o botão __Ramificação__ na parte superior da página para selecionar uma versão diferente do Storm.</span><span class="sxs-lookup"><span data-stu-id="d0840-163">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="d0840-164">Monitorar a topologia</span><span class="sxs-lookup"><span data-stu-id="d0840-164">Monitor the topology</span></span>

<span data-ttu-id="d0840-165">A IU do Storm fornece uma interface Web para trabalhar com as topologias em funcionamento, e é incluída no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0840-165">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="d0840-166">Use as etapas a seguir para monitorar a topologia usando a interface do usuário do Storm:</span><span class="sxs-lookup"><span data-stu-id="d0840-166">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="d0840-167">Para exibir a interface do usuário do Storm, abra um navegador da Web e acesse https://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="d0840-167">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="d0840-168">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-168">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0840-169">Se solicitado a forneça um nome de usuário e senha, insira o administrador de cluster (admin) e a senha que você usou ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-169">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="d0840-170">Em **Resumo da topologia**, selecione a entrada **wordcount** na coluna **Nome**.</span><span class="sxs-lookup"><span data-stu-id="d0840-170">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="d0840-171">São exibidas informações sobre a topologia.</span><span class="sxs-lookup"><span data-stu-id="d0840-171">Information about the topology is displayed.</span></span>

    ![Painel do Storm com informações da topologia do storm-starter WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="d0840-173">Esta página fornece as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="d0840-173">This page provides the following information:</span></span>

    * <span data-ttu-id="d0840-174">**Estatísticas de topologia** -informações básicas sobre o desempenho de topologia, organizadas em janelas de tempo.</span><span class="sxs-lookup"><span data-stu-id="d0840-174">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d0840-175">A seleção de uma janela de tempo específica altera a janela de tempo das informações exibidas em outras seções da página.</span><span class="sxs-lookup"><span data-stu-id="d0840-175">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="d0840-176">**Spouts** -informações básicas sobre spouts, incluindo o último erro retornado por cada spout.</span><span class="sxs-lookup"><span data-stu-id="d0840-176">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="d0840-177">**Bolts** -informações básicas sobre bolts.</span><span class="sxs-lookup"><span data-stu-id="d0840-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="d0840-178">**Configuração de topologia** -informações detalhadas sobre a configuração de topologia.</span><span class="sxs-lookup"><span data-stu-id="d0840-178">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="d0840-179">Esta página também fornece ações que podem ser executadas na topologia:</span><span class="sxs-lookup"><span data-stu-id="d0840-179">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="d0840-180">**Ativar** - retoma o processamento de uma topologia desativada.</span><span class="sxs-lookup"><span data-stu-id="d0840-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="d0840-181">**Desativar** - pausa uma topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="d0840-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="d0840-182">**Reequilibrar** - ajusta o paralelismo da topologia.</span><span class="sxs-lookup"><span data-stu-id="d0840-182">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="d0840-183">Você deve reequilibrar topologias em execução depois de alterar o número de nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-183">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="d0840-184">A redistribuição ajusta o paralelismo para compensar o aumento/diminuição do número de nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="d0840-184">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="d0840-185">Para saber mais, consulte [Noções básicas sobre o paralelismo de uma topologia do Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="d0840-185">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="d0840-186">**Eliminar** - encerra uma topologia do Storm após o tempo limite especificado.</span><span class="sxs-lookup"><span data-stu-id="d0840-186">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="d0840-187">Nessa página, selecione uma entrada da seção **Spouts** ou **Bolts**.</span><span class="sxs-lookup"><span data-stu-id="d0840-187">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="d0840-188">São exibidas informações sobre o componente selecionado.</span><span class="sxs-lookup"><span data-stu-id="d0840-188">Information about the selected component is displayed.</span></span>

    ![Painel do Storm com informações sobre os componentes selecionados.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="d0840-190">Esta página exibe as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="d0840-190">This page displays the following information:</span></span>

    * <span data-ttu-id="d0840-191">**Estatísticas de spout/bolt** -informações básicas sobre o desempenho de componente, organizadas em janelas de tempo.</span><span class="sxs-lookup"><span data-stu-id="d0840-191">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d0840-192">A seleção de uma janela de tempo específica altera a janela de tempo das informações exibidas em outras seções da página.</span><span class="sxs-lookup"><span data-stu-id="d0840-192">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="d0840-193">**Estatísticas de entrada** (somente bolt) - informações sobre componentes que geram dados consumidos pelo bolt.</span><span class="sxs-lookup"><span data-stu-id="d0840-193">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="d0840-194">**Estatísticas de saída** -informações sobre dados emitidos por este bolt.</span><span class="sxs-lookup"><span data-stu-id="d0840-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="d0840-195">**Executores** -informações sobre instâncias deste componente.</span><span class="sxs-lookup"><span data-stu-id="d0840-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="d0840-196">**Erros** -erros produzidos por este componente.</span><span class="sxs-lookup"><span data-stu-id="d0840-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="d0840-197">Ao exibir os detalhes de um spout ou bolt, selecione uma entrada da coluna **Porta** na seção **Executores** para exibir detalhes de uma instância específica do componente.</span><span class="sxs-lookup"><span data-stu-id="d0840-197">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="d0840-198">Neste exemplo, a palavra **sete** ocorreu 1493957 vezes.</span><span class="sxs-lookup"><span data-stu-id="d0840-198">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="d0840-199">Essa contagem é a quantidade de vezes que a palavra foi encontrada desde que a topologia foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="d0840-199">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="d0840-200">Parar a topologia</span><span class="sxs-lookup"><span data-stu-id="d0840-200">Stop the topology</span></span>

<span data-ttu-id="d0840-201">Volte para a página **Resumo da topologia** para a topologia de contagem de palavras e, em seguida, selecione o botão **Eliminar** da seção **Ações de topologia**.</span><span class="sxs-lookup"><span data-stu-id="d0840-201">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="d0840-202">Quando solicitado, insira 10 para os segundos a aguardar antes da interrupção da topologia.</span><span class="sxs-lookup"><span data-stu-id="d0840-202">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="d0840-203">Após o período de tempo limite, a topologia não será mais exibida quando você visitar a seção **Interface do usuário do Storm** do painel.</span><span class="sxs-lookup"><span data-stu-id="d0840-203">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="d0840-204">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="d0840-204">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="d0840-205">Se você tiver um problema com a criação de clusters HDInsight, consulte [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="d0840-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="d0840-206"><a id="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0840-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="d0840-207">Nesse tutorial do Apache Storm você aprendeu os fundamentos do trabalho com o Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0840-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="d0840-208">A seguir, aprenda a [Desenvolver topologias baseadas em Java usando o Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d0840-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="d0840-209">Se você já está familiarizado com o desenvolvimento de topologias baseadas em Java e deseja implantar uma topologia existente no HDInsight, consulte [Implantar e gerenciar topologias Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d0840-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="d0840-210">Se você for um desenvolvedor .NET, poderá criar topologias em C# ou híbridas C#/Java usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0840-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="d0840-211">Para obter mais informações, consulte [Desenvolver topologias C# para o Apache Storm no HDInsight usando ferramentas do Hadoop para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d0840-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="d0840-212">Por exemplo, topologias que podem ser usadas com o Storm no HDInsight. Confira os exemplos abaixo:</span><span class="sxs-lookup"><span data-stu-id="d0840-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="d0840-213">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0840-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
