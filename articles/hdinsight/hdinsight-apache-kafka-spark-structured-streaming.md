---
title: aaaApache Spark Streaming estruturado com Kafka - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Apache Spark streaming (DStream) tooget dados entrando ou saindo Kafka do Apache. Neste exemplo, você deve transmitir dados usando um bloco de anotações do Jupyter do Spark no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="1a03c-104">Use o Streaming Estruturado do Spark com o Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a03c-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="1a03c-105">Saiba como toouse Spark estruturado fluxo de dados de tooread do Apache Kafka no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a03c-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="1a03c-106">O streaming estruturado do Spark é um mecanismo de processamento de fluxo baseado no Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="1a03c-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="1a03c-107">Ele permite que você tooexpress cálculos de streaming Olá igual a computação de lote em dados estáticos.</span><span class="sxs-lookup"><span data-stu-id="1a03c-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="1a03c-108">Para obter mais informações sobre fluxo estruturado, consulte Olá [estruturado Streaming guia de programação [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="1a03c-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a03c-109">Este exemplo usou o Spark 2.1 no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="1a03c-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="1a03c-110">O Streaming Estruturado é considerado __versão alfa__ no Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="1a03c-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="1a03c-111">etapas de saudação neste documento criam um grupo de recursos do Azure que contém um Spark no HDInsight tanto um Kafka no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a03c-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="1a03c-112">Esses agrupamentos são ambos localizados em uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Spark Olá cluster Kafka se comunicam.</span><span class="sxs-lookup"><span data-stu-id="1a03c-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="1a03c-113">Quando você concluir etapas Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.</span><span class="sxs-lookup"><span data-stu-id="1a03c-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="1a03c-114">Criar clusters de saudação</span><span class="sxs-lookup"><span data-stu-id="1a03c-114">Create hello clusters</span></span>

<span data-ttu-id="1a03c-115">Apache Kafka no HDInsight não fornece acesso toohello Kafka agentes sobre Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="1a03c-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="1a03c-116">Qualquer coisa que fala tooKafka deve estar no hello mesma rede virtual do Azure como nós Olá Olá cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a03c-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="1a03c-117">Neste exemplo, Olá Kafka e clusters do Spark estão localizados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a03c-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="1a03c-118">Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:</span><span class="sxs-lookup"><span data-stu-id="1a03c-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clusters Spark e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="1a03c-120">Olá serviço Kafka é toocommunication limitado na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1a03c-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="1a03c-121">Outros serviços em cluster hello, como SSH e Ambari, podem ser acessados pela Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="1a03c-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="1a03c-122">Para obter mais informações sobre portas públicas de saudação disponíveis com o HDInsight, consulte [portas e URIs usados por HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="1a03c-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="1a03c-123">Embora você possa criar uma rede virtual do Azure, Kafka e Spark clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a03c-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="1a03c-124">Toodeploy uma rede virtual do Azure, Kafka, as etapas a seguir do uso hello e Spark clusters tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a03c-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="1a03c-125">Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="1a03c-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="1a03c-126">Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="1a03c-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="1a03c-127">Este modelo cria Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a03c-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="1a03c-128">Um cluster Kafka no HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="1a03c-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="1a03c-129">Um cluster Spark no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="1a03c-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="1a03c-130">Uma rede Virtual do Azure, que contém os clusters de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1a03c-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1a03c-131">notebook streaming estruturado Olá usado neste exemplo requer Spark no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="1a03c-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="1a03c-132">Se você usar uma versão anterior do Spark no HDInsight, você recebe erros ao usar o bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a03c-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="1a03c-133">Olá usar entradas de saudação toopopulate informações a seguir no hello **implantação personalizada** folha:</span><span class="sxs-lookup"><span data-stu-id="1a03c-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="1a03c-135">**Grupo de recursos**: Crie um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="1a03c-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="1a03c-136">Esse grupo contém o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1a03c-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="1a03c-137">**Local**: selecione um tooyou geograficamente fechar do local.</span><span class="sxs-lookup"><span data-stu-id="1a03c-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="1a03c-138">**Nome do Cluster base**: esse valor é usado como nome de base Olá para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a03c-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="1a03c-139">Por exemplo, inserir **hdi** cria um cluster Spark chamado hdi__ spark e um cluster Kafka chamado **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="1a03c-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="1a03c-140">**Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a03c-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="1a03c-141">**Senha de logon de cluster**: senha do usuário administrador Olá para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a03c-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="1a03c-142">**Nome de usuário SSH**: Olá toocreate de usuário SSH para clusters de saudação Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a03c-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="1a03c-143">**Senha SSH**: senha Olá para usuário SSH Olá Olá Spark e Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="1a03c-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="1a03c-144">Saudação de leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.</span><span class="sxs-lookup"><span data-stu-id="1a03c-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="1a03c-145">Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**.</span><span class="sxs-lookup"><span data-stu-id="1a03c-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="1a03c-146">Demora cerca de 20 minutos toocreate clusters hello.</span><span class="sxs-lookup"><span data-stu-id="1a03c-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="1a03c-147">Após a criação dos recursos Olá, você é redirecionado toohello folha de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1a03c-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="1a03c-149">Observe que os nomes de saudação de clusters de HDInsight Olá ficam **nome base do spark** e **kafka nome de base**, onde nome base é o nome da saudação fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="1a03c-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="1a03c-150">Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="1a03c-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="1a03c-151">Obter Olá Kafka agentes</span><span class="sxs-lookup"><span data-stu-id="1a03c-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="1a03c-152">o código neste exemplo Hello conecta toohello Kafka hosts no cluster Kafka de saudação do agente.</span><span class="sxs-lookup"><span data-stu-id="1a03c-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="1a03c-153">toofind Olá hosts de broker Kafka, use Olá PowerShell ou Bash exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a03c-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="1a03c-154">Este exemplo espera `$PASSWORD` toocontain senha de saudação para logon de cluster Olá, e `$CLUSTERNAME` toocontain nome de saudação do hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a03c-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="1a03c-155">Este exemplo usa Olá [jq](https://stedolan.github.io/jq/) dados do utilitário tooparse fora do documento JSON hello.</span><span class="sxs-lookup"><span data-stu-id="1a03c-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="1a03c-156">saudação de saída é similar toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a03c-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="1a03c-157">Salve essas informações, como ele é usado no hello seguintes seções deste documento.</span><span class="sxs-lookup"><span data-stu-id="1a03c-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="1a03c-158">Obter blocos de anotações de saudação</span><span class="sxs-lookup"><span data-stu-id="1a03c-158">Get hello notebooks</span></span>

<span data-ttu-id="1a03c-159">Olá código de exemplo hello descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="1a03c-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="1a03c-160">Carregar os blocos de anotações de saudação</span><span class="sxs-lookup"><span data-stu-id="1a03c-160">Upload hello notebooks</span></span>

<span data-ttu-id="1a03c-161">Use Olá seguir etapas tooupload Olá blocos de anotações de saudação projeto tooyour Spark no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1a03c-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="1a03c-162">No navegador da web, conecte-se de anotações do Jupyter toohello em seu cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="1a03c-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="1a03c-163">Olá seguindo a URL, substitua `CLUSTERNAME` com nome de saudação do cluster Kafka:</span><span class="sxs-lookup"><span data-stu-id="1a03c-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="1a03c-164">Quando solicitado, insira o logon de cluster da saudação (admin) e a senha usada ao criar cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1a03c-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="1a03c-165">Olá superior direita da página Olá, use Olá __carregar__ saudação do botão tooupload __fluxo Tweets To_Kafka.ipynb__ cluster toohello de arquivos.</span><span class="sxs-lookup"><span data-stu-id="1a03c-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="1a03c-166">Selecione __abrir__ toostart carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a03c-166">Select __Open__ toostart hello upload.</span></span>

    ![Use Olá tooselect de botão de carregamento e carregar um bloco de anotações](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selecione o arquivo de KafkaStreaming.ipynb Olá](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="1a03c-169">Localize Olá __fluxo Tweets To_Kafka.ipynb__ entrada na lista de saudação do blocos de anotações e selecione __carregar__ botão ao lado dela.</span><span class="sxs-lookup"><span data-stu-id="1a03c-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Carregamento de saudação do uso botão ao lado de tooupload de entrada KafkaStreaming.ipynb Olá-servidor de notebook toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="1a03c-171">Repita as etapas de saudação do tooload de 1 a 3 __Spark-estruturado-Streaming-de-Kafka.ipynb__ notebook.</span><span class="sxs-lookup"><span data-stu-id="1a03c-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="1a03c-172">Carregar tweets no Kafka</span><span class="sxs-lookup"><span data-stu-id="1a03c-172">Load tweets into Kafka</span></span>

<span data-ttu-id="1a03c-173">Depois de carregar arquivos hello, selecionar Olá __fluxo Tweets To_Kafka.ipynb__ notebook de saudação do tooopen de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a03c-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="1a03c-174">Siga as etapas de Olá Olá notebook tooload tweets em Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a03c-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="1a03c-175">Processar tweets usando o streaming estruturado do Spark</span><span class="sxs-lookup"><span data-stu-id="1a03c-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="1a03c-176">Olá home page do Jupyter Notebook, selecione Olá __Spark-estruturado-Streaming-de-Kafka.ipynb__ entrada.</span><span class="sxs-lookup"><span data-stu-id="1a03c-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="1a03c-177">Siga as etapas de Olá Olá notebook tooload tweets de Kafka usando fluxo estruturado do Spark.</span><span class="sxs-lookup"><span data-stu-id="1a03c-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a03c-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a03c-178">Next steps</span></span>

<span data-ttu-id="1a03c-179">Agora que você aprendeu como toouse Spark estruturado Streaming, consulte Olá documentos toolearn mais sobre como trabalhar com Spark e Kafka a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a03c-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="1a03c-180">[Como toouse despertar streaming (DStream) com Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="1a03c-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="1a03c-181">Iniciar com o bloco de anotações do Jupyter e Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a03c-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)