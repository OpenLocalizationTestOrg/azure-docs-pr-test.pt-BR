---
title: "Streaming Estruturado do Apache Spark com Kafka – Azure HDInsight | Microsoft Docs"
description: "Saiba como usar o streaming do Apache Spark (DStream) para transmitir dados para dentro ou fora do Apache Kafka. Neste exemplo, você deve transmitir dados usando um bloco de anotações do Jupyter do Spark no HDInsight."
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
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="cb46c-104">Use o Streaming Estruturado do Spark com o Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb46c-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="cb46c-105">Saiba como usar o Streaming Estruturado do Spark para ler dados do Apache Kafka no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb46c-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="cb46c-106">O streaming estruturado do Spark é um mecanismo de processamento de fluxo baseado no Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="cb46c-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="cb46c-107">Ele permite expressar cálculos de streaming do mesmo modo que cálculos de lote em dados estáticos.</span><span class="sxs-lookup"><span data-stu-id="cb46c-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="cb46c-108">Para obter mais informações sobre Streaming Estruturado, consulte o [Guia de Programação de Streaming Estruturado [Versão Alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="cb46c-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb46c-109">Este exemplo usou o Spark 2.1 no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="cb46c-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="cb46c-110">O Streaming Estruturado é considerado __versão alfa__ no Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="cb46c-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="cb46c-111">As etapas neste documento criam um grupo de recursos do Azure que contém um Spark no HDInsight e um Kafka no cluster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb46c-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="cb46c-112">Esses clusters são ambos localizados em uma Rede Virtual do Azure, que permite que o cluster Spark se comunique diretamente com o cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="cb46c-113">Quando você terminar as etapas neste documento, lembre-se de excluir os clusters para evitar cobranças em excesso.</span><span class="sxs-lookup"><span data-stu-id="cb46c-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="cb46c-114">Criar os clusters</span><span class="sxs-lookup"><span data-stu-id="cb46c-114">Create the clusters</span></span>

<span data-ttu-id="cb46c-115">Apache Kafka no HDInsight não fornece acesso para Agentes de Kafka pela internet pública.</span><span class="sxs-lookup"><span data-stu-id="cb46c-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="cb46c-116">Qualquer coisa que se comunique com Kafka deve estar na mesma rede virtual do Azure que os nós no cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="cb46c-117">Para este exemplo, clusters de Spark e Kafka estão localizados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb46c-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="cb46c-118">O diagrama a seguir mostra como a comunicação flui entre os clusters:</span><span class="sxs-lookup"><span data-stu-id="cb46c-118">The following diagram shows how communication flows between the clusters:</span></span>

![Diagrama de clusters Spark e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="cb46c-120">O serviço Kafka é limitado a comunicação dentro da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cb46c-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="cb46c-121">Outros serviços no cluster, como SSH e Ambari, podem ser acessados pela Internet.</span><span class="sxs-lookup"><span data-stu-id="cb46c-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="cb46c-122">Para obter mais informações sobre as portas públicas disponíveis com o HDInsight, consulte [portas e URIs usados pelo HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="cb46c-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="cb46c-123">Enquanto você pode criar uma rede virtual do Azure, Kafka e clusters de Spark manualmente, é mais fácil usar um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb46c-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="cb46c-124">Use as seguintes etapas para implantar uma rede virtual do Azure, Kafka e clusters de Spark para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb46c-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="cb46c-125">Use o botão a seguir para entrar no Azure e abra o modelo do Gerenciador de Recursos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb46c-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="cb46c-126">O modelo do Azure Resource Manager está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="cb46c-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="cb46c-127">Este modelo cria os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="cb46c-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="cb46c-128">Um cluster Kafka no HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="cb46c-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="cb46c-129">Um cluster Spark no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="cb46c-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="cb46c-130">Uma Rede Virtual do Azure, que contém os clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb46c-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cb46c-131">O bloco de anotações de streaming estruturado usado neste exemplo requer o Spark no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="cb46c-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="cb46c-132">Se você usar uma versão anterior do Spark no HDInsight, você receberá erros ao usar o bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="cb46c-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="cb46c-133">Use as seguintes informações para preencher as entradas na folha de **Implantação personalizada** :</span><span class="sxs-lookup"><span data-stu-id="cb46c-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="cb46c-135">**Grupo de recursos**: Crie um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="cb46c-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="cb46c-136">Esse grupo contém o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb46c-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="cb46c-137">**Local**: escolha um local geograficamente perto de você.</span><span class="sxs-lookup"><span data-stu-id="cb46c-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="cb46c-138">**Nome do Cluster de base**: esse valor é usado como o nome de base para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="cb46c-139">Por exemplo, inserir **hdi** cria um cluster Spark chamado hdi__ spark e um cluster Kafka chamado **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="cb46c-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="cb46c-140">**Nome de usuário de logon do cluster**: O nome de usuário do administrador para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="cb46c-141">**Senha de logon do cluster**: A senha de usuário do administrador para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="cb46c-142">**Nome de usuário SSH**: O usuário SSH para criar para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="cb46c-143">**Senha SSH**: a senha para o usuário SSH dos clusters Kafka e Spark.</span><span class="sxs-lookup"><span data-stu-id="cb46c-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="cb46c-144">Leia **Termos e Condições**, e depois selecione **Concordo com os termos e condições declarados acima**.</span><span class="sxs-lookup"><span data-stu-id="cb46c-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="cb46c-145">Por fim, marque **Fixar no painel** e selecione **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="cb46c-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="cb46c-146">Demora cerca de 20 minutos para criar os clusters.</span><span class="sxs-lookup"><span data-stu-id="cb46c-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="cb46c-147">Depois que os recursos tiverem sido criados, você será redirecionado para a folha do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cb46c-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![Folha do grupo de recursos para rede virtual e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="cb46c-149">Observe que os nomes dos clusters HDInsight são **spark-BASENAME** e **kafka-BASENAME**, em que BASENAME é o nome fornecido para o modelo.</span><span class="sxs-lookup"><span data-stu-id="cb46c-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="cb46c-150">Você usa esses nomes em etapas posteriores ao se conectar aos clusters.</span><span class="sxs-lookup"><span data-stu-id="cb46c-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="cb46c-151">Obter os agentes de Kafka</span><span class="sxs-lookup"><span data-stu-id="cb46c-151">Get the Kafka brokers</span></span>

<span data-ttu-id="cb46c-152">O código neste exemplo conecta-se aos hosts de agente Kafka no cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="cb46c-153">Para localizar os hosts de agente Kafka, use o exemplo do PowerShell ou Bash a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb46c-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
> <span data-ttu-id="cb46c-154">Este exemplo espera `$PASSWORD` para conter a senha para o logon de cluster e `$CLUSTERNAME` para conter o nome do cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="cb46c-155">Este exemplo usa o utilitário [jq](https://stedolan.github.io/jq/) para analisar dados fora do documento JSON.</span><span class="sxs-lookup"><span data-stu-id="cb46c-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="cb46c-156">A saída é semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb46c-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="cb46c-157">Salve essas informações, pois elas são usadas nas diversas etapas deste documento.</span><span class="sxs-lookup"><span data-stu-id="cb46c-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="cb46c-158">Obter os blocos de anotações</span><span class="sxs-lookup"><span data-stu-id="cb46c-158">Get the notebooks</span></span>

<span data-ttu-id="cb46c-159">O código do exemplo descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="cb46c-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="cb46c-160">Carregar os blocos de anotações</span><span class="sxs-lookup"><span data-stu-id="cb46c-160">Upload the notebooks</span></span>

<span data-ttu-id="cb46c-161">Use as etapas a seguir para carregar os blocos de anotações do projeto para o Spark no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cb46c-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="cb46c-162">No navegador da Web, conecte-se ao bloco de anotações do Jupyter em seu cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="cb46c-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="cb46c-163">Na URL a seguir, substitua `CLUSTERNAME` pelo nome do cluster Kafka:</span><span class="sxs-lookup"><span data-stu-id="cb46c-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="cb46c-164">Quando solicitado, insira o nome de usuário e senha que você inseriu ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="cb46c-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="cb46c-165">No canto superior direito da página, use o botão __Carregar__ para carregar o arquivo __Stream-Tweets-To_Kafka.ipynb__ no cluster.</span><span class="sxs-lookup"><span data-stu-id="cb46c-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="cb46c-166">Selecione __Abrir__ para iniciar o upload.</span><span class="sxs-lookup"><span data-stu-id="cb46c-166">Select __Open__ to start the upload.</span></span>

    ![Use o botão Carregar para selecionar e carregar um notebook](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selecione o arquivo KafkaStreaming.ipynb](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="cb46c-169">Localize a entrada __Stream-Tweets-To_Kafka.ipynb__ na lista de blocos de anotações e selecione o botão __Carregar__ ao lado dela.</span><span class="sxs-lookup"><span data-stu-id="cb46c-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Use o botão Carregar ao lado da entrada KafkaStreaming.ipynb para carregá-la para o servidor de notebook](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="cb46c-171">Repita as etapas de 1 a 3 para carregar o bloco de anotações __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="cb46c-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="cb46c-172">Carregar tweets no Kafka</span><span class="sxs-lookup"><span data-stu-id="cb46c-172">Load tweets into Kafka</span></span>

<span data-ttu-id="cb46c-173">Depois que o arquivo foi carregado, selecione a entrada __Stream-Tweets-To_Kafka.ipynb__ para abrir o bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="cb46c-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="cb46c-174">Siga as etapas no bloco de anotações para carregar tweets no Kafka.</span><span class="sxs-lookup"><span data-stu-id="cb46c-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="cb46c-175">Processar tweets usando o streaming estruturado do Spark</span><span class="sxs-lookup"><span data-stu-id="cb46c-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="cb46c-176">Na home page do Jupyter Notebook, selecione a entrada __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="cb46c-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="cb46c-177">Siga as etapas no bloco de anotações para carregar tweets de Kafka usando o Streaming Estruturado do Spark.</span><span class="sxs-lookup"><span data-stu-id="cb46c-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb46c-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb46c-178">Next steps</span></span>

<span data-ttu-id="cb46c-179">Agora que você aprendeu a usar o Streaming Estruturado do Spark, consulte os documentos a seguir para saber mais sobre como trabalhar com Spark e Kafka:</span><span class="sxs-lookup"><span data-stu-id="cb46c-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="cb46c-180">[Como usar o streaming do Spark (DStream) com Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="cb46c-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="cb46c-181">Iniciar com o bloco de anotações do Jupyter e Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb46c-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)