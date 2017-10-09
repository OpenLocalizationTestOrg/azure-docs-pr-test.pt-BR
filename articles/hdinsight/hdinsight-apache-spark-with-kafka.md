---
title: aaaApache Spark streaming com Kafka - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse dados de toostream Spark Apache Spark entrando ou saindo Apache Kafka usando DStreams. Neste exemplo, você deve transmitir dados usando um bloco de anotações do Jupyter do Spark no HDInsight."
keywords: exemplo de kafka, zookeeper kafka, streaming do kafka para Spark, exemplo de streaming do spark com o kafka
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="c155b-105">Exemplo de streaming do Apache Spark (DStream) com o Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c155b-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="c155b-106">Saiba como toouse dados de toostream Spark Apache Spark entrando ou saindo Kafka do Apache no HDInsight usando DStreams.</span><span class="sxs-lookup"><span data-stu-id="c155b-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="c155b-107">Este exemplo usa um bloco de anotações do Jupyter que é executado no cluster do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="c155b-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="c155b-108">etapas de saudação neste documento criam um grupo de recursos do Azure que contém um Spark no HDInsight tanto um Kafka no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c155b-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="c155b-109">Esses agrupamentos são ambos localizados em uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Spark Olá cluster Kafka se comunicam.</span><span class="sxs-lookup"><span data-stu-id="c155b-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="c155b-110">Quando você concluir etapas Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.</span><span class="sxs-lookup"><span data-stu-id="c155b-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="c155b-111">Criar clusters de saudação</span><span class="sxs-lookup"><span data-stu-id="c155b-111">Create hello clusters</span></span>

<span data-ttu-id="c155b-112">Apache Kafka no HDInsight não fornece acesso toohello Kafka agentes sobre Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="c155b-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="c155b-113">Qualquer coisa que fala tooKafka deve estar no hello mesma rede virtual do Azure como nós Olá Olá cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="c155b-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="c155b-114">Neste exemplo, Olá Kafka e clusters do Spark estão localizados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c155b-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="c155b-115">Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:</span><span class="sxs-lookup"><span data-stu-id="c155b-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clusters Spark e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="c155b-117">Embora Kafka em si é toocommunication limitado na rede virtual hello, outros serviços em cluster hello como SSH e Ambari podem ser acessados pela Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="c155b-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="c155b-118">Para obter mais informações sobre portas públicas de saudação disponíveis com o HDInsight, consulte [portas e URIs usados por HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="c155b-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="c155b-119">Embora você possa criar uma rede virtual do Azure, Kafka e Spark clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c155b-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="c155b-120">Toodeploy uma rede virtual do Azure, Kafka, as etapas a seguir do uso hello e Spark clusters tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c155b-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="c155b-121">Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="c155b-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="c155b-122">Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="c155b-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c155b-123">disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c155b-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="c155b-124">Este modelo cria um cluster de Kafka que contém três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c155b-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="c155b-125">Este modelo cria um cluster HDInsight 3.6 para Kafka e Spark.</span><span class="sxs-lookup"><span data-stu-id="c155b-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="c155b-126">Olá usar entradas de saudação toopopulate informações a seguir no hello **implantação personalizada** folha:</span><span class="sxs-lookup"><span data-stu-id="c155b-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="c155b-128">**Grupo de recursos**: Crie um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="c155b-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="c155b-129">Esse grupo contém o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c155b-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="c155b-130">**Local**: selecione um tooyou geograficamente fechar do local.</span><span class="sxs-lookup"><span data-stu-id="c155b-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="c155b-131">**Nome do Cluster base**: esse valor é usado como nome de base Olá para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="c155b-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="c155b-132">Por exemplo, inserir **hdi** cria um cluster Spark chamado hdi__ spark e um cluster Kafka chamado **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="c155b-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="c155b-133">**Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="c155b-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c155b-134">**Senha de logon de cluster**: senha do usuário administrador Olá para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="c155b-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c155b-135">**Nome de usuário SSH**: Olá toocreate de usuário SSH para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="c155b-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c155b-136">**Senha SSH**: senha Olá para usuário SSH Olá Olá Spark e Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="c155b-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="c155b-137">Saudação de leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.</span><span class="sxs-lookup"><span data-stu-id="c155b-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="c155b-138">Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**.</span><span class="sxs-lookup"><span data-stu-id="c155b-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="c155b-139">Demora cerca de 20 minutos toocreate clusters hello.</span><span class="sxs-lookup"><span data-stu-id="c155b-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="c155b-140">Após a criação dos recursos Olá, será redirecionado tooa folha Olá grupo de recursos que contém hello e clusters do painel da web.</span><span class="sxs-lookup"><span data-stu-id="c155b-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="c155b-142">Observe que os nomes de saudação de clusters de HDInsight Olá ficam **nome base do spark** e **kafka nome de base**, onde nome base é o nome da saudação fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="c155b-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="c155b-143">Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="c155b-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="c155b-144">Usar blocos de anotações de saudação</span><span class="sxs-lookup"><span data-stu-id="c155b-144">Use hello notebooks</span></span>

<span data-ttu-id="c155b-145">Olá código de exemplo hello descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="c155b-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="c155b-146">Siga as etapas de Olá Olá `README.md` arquivo toocomplete neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c155b-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="c155b-147">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="c155b-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="c155b-148">Como criam etapas de saudação neste documento hello de clusters no mesmo grupo de recursos do Azure, você pode excluir o grupo de recursos Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c155b-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="c155b-149">Excluir grupo de saudação remove todos os recursos criados seguindo este documento, Olá rede Virtual do Azure e conta de armazenamento usados pelo clusters hello.</span><span class="sxs-lookup"><span data-stu-id="c155b-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c155b-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c155b-150">Next steps</span></span>

<span data-ttu-id="c155b-151">Neste exemplo, você aprendeu como toouse despertar tooread e gravar tooKafka.</span><span class="sxs-lookup"><span data-stu-id="c155b-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="c155b-152">Use Olá toodiscover links a seguir outra maneiras toowork Kafka:</span><span class="sxs-lookup"><span data-stu-id="c155b-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="c155b-153">Introdução ao Apache Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c155b-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="c155b-154">Use MirrorMaker toocreate uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c155b-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="c155b-155">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c155b-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

