---
title: "Streaming do Apache Spark com Kafka – Azure HDInsight | Microsoft Docs"
description: "Saiba como usar o Apache Spark para transmitir dados dentro ou fora do Apache Kafka usando o DStreams. Neste exemplo, você deve transmitir dados usando um bloco de anotações do Jupyter do Spark no HDInsight."
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="77865-105">Exemplo de streaming do Apache Spark (DStream) com o Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="77865-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="77865-106">Saiba como usar o Apache Spark para transmitir dados dentro ou fora do Apache Kafka no HDInsight usando o DStreams.</span><span class="sxs-lookup"><span data-stu-id="77865-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="77865-107">Este exemplo usa um bloco de anotações do Jupyter que é executado no cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="77865-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="77865-108">As etapas neste documento criam um grupo de recursos do Azure que contém um Spark no HDInsight e um Kafka no cluster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77865-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="77865-109">Esses clusters são ambos localizados em uma Rede Virtual do Azure, que permite que o cluster Spark se comunique diretamente com o cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="77865-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="77865-110">Quando você terminar as etapas neste documento, lembre-se de excluir os clusters para evitar cobranças em excesso.</span><span class="sxs-lookup"><span data-stu-id="77865-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="77865-111">Criar os clusters</span><span class="sxs-lookup"><span data-stu-id="77865-111">Create the clusters</span></span>

<span data-ttu-id="77865-112">Apache Kafka no HDInsight não fornece acesso para Agentes de Kafka pela internet pública.</span><span class="sxs-lookup"><span data-stu-id="77865-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="77865-113">Qualquer coisa que se comunique com Kafka deve estar na mesma rede virtual do Azure que os nós no cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="77865-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="77865-114">Para este exemplo, clusters de Spark e Kafka estão localizados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="77865-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="77865-115">O diagrama a seguir mostra como a comunicação flui entre os clusters:</span><span class="sxs-lookup"><span data-stu-id="77865-115">The following diagram shows how communication flows between the clusters:</span></span>

![Diagrama de clusters Spark e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="77865-117">Embora Kafka em si esteja limitado a comunicação na rede virtual, outros serviços do cluster, como o SSH e Ambari podem ser acessados pela Internet.</span><span class="sxs-lookup"><span data-stu-id="77865-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="77865-118">Para obter mais informações sobre as portas públicas disponíveis com o HDInsight, consulte [portas e URIs usados pelo HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="77865-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="77865-119">Enquanto você pode criar uma rede virtual do Azure, Kafka e clusters de Spark manualmente, é mais fácil usar um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77865-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="77865-120">Use as seguintes etapas para implantar uma rede virtual do Azure, Kafka e clusters de Spark para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="77865-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="77865-121">Use o botão a seguir para entrar no Azure e abra o modelo do Gerenciador de Recursos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="77865-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="77865-122">O modelo do Azure Resource Manager está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="77865-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="77865-123">Para garantir a disponibilidade do Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="77865-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="77865-124">Este modelo cria um cluster de Kafka que contém três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="77865-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="77865-125">Este modelo cria um cluster HDInsight 3.6 para Kafka e Spark.</span><span class="sxs-lookup"><span data-stu-id="77865-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="77865-126">Use as seguintes informações para preencher as entradas na folha de **Implantação personalizada** :</span><span class="sxs-lookup"><span data-stu-id="77865-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="77865-128">**Grupo de recursos**: Crie um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="77865-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="77865-129">Esse grupo contém o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77865-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="77865-130">**Local**: escolha um local geograficamente perto de você.</span><span class="sxs-lookup"><span data-stu-id="77865-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="77865-131">**Nome do Cluster de base**: esse valor é usado como o nome de base para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="77865-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="77865-132">Por exemplo, inserir **hdi** cria um cluster Spark chamado hdi__ spark e um cluster Kafka chamado **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="77865-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="77865-133">**Nome de usuário de logon do cluster**: O nome de usuário do administrador para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="77865-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="77865-134">**Senha de logon do cluster**: A senha de usuário do administrador para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="77865-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="77865-135">**Nome de usuário SSH**: O usuário SSH para criar para os clusters Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="77865-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="77865-136">**Senha SSH**: a senha para o usuário SSH dos clusters Kafka e Spark.</span><span class="sxs-lookup"><span data-stu-id="77865-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="77865-137">Leia **Termos e Condições**, e depois selecione **Concordo com os termos e condições declarados acima**.</span><span class="sxs-lookup"><span data-stu-id="77865-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="77865-138">Por fim, marque **Fixar no painel** e selecione **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="77865-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="77865-139">Demora cerca de 20 minutos para criar os clusters.</span><span class="sxs-lookup"><span data-stu-id="77865-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="77865-140">Quando os recursos tiverem sido criados, você será redirecionado para uma folha do grupo de recursos que contém os clusters e o painel da Web.</span><span class="sxs-lookup"><span data-stu-id="77865-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Folha do grupo de recursos para rede virtual e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="77865-142">Observe que os nomes dos clusters HDInsight são **spark-BASENAME** e **kafka-BASENAME**, em que BASENAME é o nome fornecido para o modelo.</span><span class="sxs-lookup"><span data-stu-id="77865-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="77865-143">Você usa esses nomes em etapas posteriores ao se conectar aos clusters.</span><span class="sxs-lookup"><span data-stu-id="77865-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="77865-144">Usar os blocos de anotações</span><span class="sxs-lookup"><span data-stu-id="77865-144">Use the notebooks</span></span>

<span data-ttu-id="77865-145">O código de exemplo descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="77865-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="77865-146">Siga as etapas no arquivo `README.md` para concluir este exemplo.</span><span class="sxs-lookup"><span data-stu-id="77865-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="77865-147">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="77865-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="77865-148">Como as etapas neste documento criam ambos os clusters no mesmo grupo de recursos do Azure, você pode excluir o grupo de recursos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="77865-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="77865-149">Excluir o grupo remove todos os recursos criados por este documento, a rede Virtual do Azure e a conta de armazenamento usada pelos clusters.</span><span class="sxs-lookup"><span data-stu-id="77865-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77865-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77865-150">Next steps</span></span>

<span data-ttu-id="77865-151">Neste exemplo, você aprendeu a usar o Spark para ler e gravar em Kafka.</span><span class="sxs-lookup"><span data-stu-id="77865-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="77865-152">Use os links a seguir para descobrir outras maneiras de trabalhar com Kafka:</span><span class="sxs-lookup"><span data-stu-id="77865-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="77865-153">Introdução ao Apache Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="77865-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="77865-154">Use MirrorMaker para criar uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="77865-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="77865-155">Use o Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="77865-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

