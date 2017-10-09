---
title: aaaUse Kafka Apache com Storm no HDInsight - Azure | Microsoft Docs
description: "O Apache Kafka é instalado com o Apache Storm no HDInsight. Saiba como toowrite tooKafka e, em seguida, ler, usando Olá KafkaBolt e KafkaSpout componentes fornecidos com Storm. Também aprenderá como toouse Olá fluxo framework toodefine e enviar topologias Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="e1cc3-105">Usar o Apache Kafka (visualização) com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1cc3-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="e1cc3-106">Saiba como toouse Apache Storm tooread de e escrever tooApache Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="e1cc3-107">Este exemplo também demonstra como sistema usado pelo HDInsight do arquivo de dados de toosave de uma topologia de Storm toohello compatível com o HDFS.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="e1cc3-108">etapas de saudação neste documento criam um grupo de recursos do Azure que contém tanto uma profusão de HDInsight e um Kafka no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="e1cc3-109">Esses agrupamentos são ambos localizados em uma rede Virtual do Azure, que permite Olá Storm cluster toodirectly Olá cluster Kafka se comunicam.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="e1cc3-110">Quando você concluir etapas Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="e1cc3-111">Obter o código de saudação</span><span class="sxs-lookup"><span data-stu-id="e1cc3-111">Get hello code</span></span>

<span data-ttu-id="e1cc3-112">Olá código de exemplo hello usado neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="e1cc3-113">toocompile este projeto, você precisa Olá seguinte configuração para o seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="e1cc3-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="e1cc3-115">HDInsight 3.5 ou superior exige Java 8.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="e1cc3-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="e1cc3-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="e1cc3-117">Um cliente SSH (é necessário Olá `ssh` e `scp` comandos) - para obter informações, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="e1cc3-118">Um editor de texto ou IDE.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-118">A text editor or IDE.</span></span>

<span data-ttu-id="e1cc3-119">Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK em sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="e1cc3-120">No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="e1cc3-121">`JAVA_HOME`-deve apontar toohello diretório onde hello JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="e1cc3-122">`PATH`-deve conter Olá caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="e1cc3-123">`JAVA_HOME`(ou caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="e1cc3-124">`JAVA_HOME\bin`(ou caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="e1cc3-125">diretório de saudação onde Maven está instalado.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="e1cc3-126">Criar clusters de saudação</span><span class="sxs-lookup"><span data-stu-id="e1cc3-126">Create hello clusters</span></span>

<span data-ttu-id="e1cc3-127">Apache Kafka no HDInsight não fornece acesso toohello Kafka agentes sobre Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="e1cc3-128">Qualquer coisa que fala tooKafka deve estar no hello mesma rede virtual do Azure como nós Olá Olá cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="e1cc3-129">Neste exemplo, Olá Kafka e clusters Storm estão localizados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="e1cc3-130">Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clusters Storm e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="e1cc3-132">Outros serviços em cluster hello como SSH e Ambari podem ser acessados pela Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="e1cc3-133">Para obter mais informações sobre portas públicas de saudação disponíveis com o HDInsight, consulte [portas e URIs usados por HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="e1cc3-134">Embora você pode criar uma rede virtual do Azure, Kafka, e Storm clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="e1cc3-135">Toodeploy uma rede virtual do Azure, Kafka, as etapas a seguir do uso hello e Storm clusters tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="e1cc3-136">Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="e1cc3-137">Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="e1cc3-138">Ele cria Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="e1cc3-139">Grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cc3-139">Azure resource group</span></span>
    * <span data-ttu-id="e1cc3-140">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cc3-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="e1cc3-141">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cc3-141">Azure Storage account</span></span>
    * <span data-ttu-id="e1cc3-142">Kafka no HDInsight versão 3.6 (três nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="e1cc3-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="e1cc3-143">Storm no HDInsight versão 3.6 (três nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="e1cc3-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="e1cc3-144">disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="e1cc3-145">Este modelo cria um cluster de Kafka que contém três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="e1cc3-146">Olá usar entradas de saudação toopopulate diretrizes a seguir em hello **implantação personalizada** folha:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="e1cc3-148">**Grupo de recursos**: Crie um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="e1cc3-149">Esse grupo contém o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="e1cc3-150">**Local**: selecione um tooyou geograficamente fechar do local.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="e1cc3-151">**Nome do Cluster base**: esse valor é usado como nome de base Olá para clusters de saudação Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="e1cc3-152">Por exemplo, inserir **hdi** cria um cluster Storm chamado **storm-hdi** e um cluster Kafka chamado **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="e1cc3-153">**Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para clusters de saudação Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="e1cc3-154">**Senha de logon de cluster**: senha do usuário administrador Olá para clusters de saudação Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="e1cc3-155">**Nome de usuário SSH**: Olá toocreate de usuário SSH para clusters de saudação Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="e1cc3-156">**Senha SSH**: senha Olá para usuário SSH Olá Olá Storm e Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="e1cc3-157">Saudação de leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="e1cc3-158">Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="e1cc3-159">Demora cerca de 20 minutos toocreate clusters hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="e1cc3-160">Após a criação dos recursos de hello, folha Olá Olá para grupo de recursos é exibida.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="e1cc3-162">Observe que os nomes de saudação de clusters de HDInsight Olá ficam **profusão de nome de base** e **kafka nome de base**, onde nome base é o nome da saudação fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="e1cc3-163">Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="e1cc3-164">Entendendo o código Olá</span><span class="sxs-lookup"><span data-stu-id="e1cc3-164">Understanding hello code</span></span>

<span data-ttu-id="e1cc3-165">Este projeto contém duas topologias:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-165">This project contains two topologies:</span></span>

* <span data-ttu-id="e1cc3-166">**KafkaWriter**: definidos por Olá **writer.yaml** arquivo, esta topologia grava tooKafka sentenças aleatório usando Olá KafkaBolt fornecido com o Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="e1cc3-167">Essa topologia usa um personalizado **SentenceSpout** sentenças aleatório do componente toogenerate.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="e1cc3-168">**KafkaReader**: definidos por Olá **reader.yaml** arquivo, esta topologia lê dados de Kafka usando Olá KafkaSpout fornecido com o Apache Storm e logs Olá toostdout de dados.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="e1cc3-169">Essa topologia usa o hello Storm HdfsBolt toowrite dados toodefault armazenamento para cluster Storm de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="e1cc3-170">Flux</span><span class="sxs-lookup"><span data-stu-id="e1cc3-170">Flux</span></span>

<span data-ttu-id="e1cc3-171">topologias de saudação são definidas usando [fluxo](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="e1cc3-172">Fluxo foi introduzido no Storm 0.10.x e permite que você tooseparate configuração de topologia de saudação do código de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="e1cc3-173">Para topologias que usam a estrutura do fluxo de Olá, topologia Olá é definida em um arquivo YAML.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="e1cc3-174">arquivo YAML de saudação pode ser incluído como parte da topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="e1cc3-175">Ele também pode ser um arquivo autônomo usado ao enviar a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="e1cc3-176">O Flux também dá suporte à substituição de variáveis em tempo de execução, o que é usado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="e1cc3-177">Olá seguintes parâmetros são definidos em tempo de execução para essas topologias:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="e1cc3-178">`${kafka.topic}`: nome de saudação do hello Kafka tópico topologias Olá leitura/gravação para.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="e1cc3-179">`${kafka.broker.hosts}`: Olá hospeda esse Olá Kafka os agentes executado em.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="e1cc3-180">informações de agente de Hello são usadas pelo Olá KafkaBolt ao gravar tooKafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="e1cc3-181">`${kafka.zookeeper.hosts}`: hosts Olá Zookeeper executado na Olá cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="e1cc3-182">Para obter mais informações sobre as topologias do Flux, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="e1cc3-183">Baixe e compilar o projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="e1cc3-183">Download and compile hello project</span></span>

1. <span data-ttu-id="e1cc3-184">Em seu ambiente de desenvolvimento, baixe o projeto de saudação do [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), abra uma linha de comando e altere diretórios toohello local que você baixou o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="e1cc3-185">De saudação **hdinsight-storm java kafka** diretório a seguir Olá use projeto de saudação toocompile de comando e cria um pacote para implantação:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="e1cc3-186">processo de pacote de saudação cria um arquivo chamado `KafkaTopology-1.0-SNAPSHOT.jar` em Olá `target` directory.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="e1cc3-187">Use Olá comandos toocopy Olá pacote tooyour Storm a seguir no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="e1cc3-188">Substituir **nome de usuário** com nome de usuário SSH Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="e1cc3-189">Substituir **nome base** com o nome de base Olá usados ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="e1cc3-190">Quando solicitado, insira a senha Olá usada durante a criação de clusters de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="e1cc3-191">Configurar a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="e1cc3-191">Configure hello topology</span></span>

1. <span data-ttu-id="e1cc3-192">Use uma saudação toodiscover métodos a seguir Olá hosts de broker Kafka:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e1cc3-193">Olá Bash exemplo supõe que `$CLUSTERNAME` contém nome de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="e1cc3-194">Ele também pressupõe que [jq](https://stedolan.github.io/jq/) esteja instalado.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="e1cc3-195">Quando solicitado, insira a senha Olá Olá cluster conta de logon.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="e1cc3-196">valor de saudação retornado é semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="e1cc3-197">Embora possa haver mais de dois hosts de agente para o cluster, não é necessário tooprovide uma lista completa de todos os tooclients de hosts.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="e1cc3-198">Um ou dois são suficientes.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-198">One or two is enough.</span></span>

2. <span data-ttu-id="e1cc3-199">Use uma saudação hosts de Kafka Zookeeper métodos toodiscover Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e1cc3-200">Olá Bash exemplo supõe que `$CLUSTERNAME` contém nome de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="e1cc3-201">Ele também pressupõe que [jq](https://stedolan.github.io/jq/) esteja instalado.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="e1cc3-202">Quando solicitado, insira a senha Olá Olá cluster conta de logon.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="e1cc3-203">valor de saudação retornado é semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="e1cc3-204">Embora haja mais de dois nós Zookeeper, não é necessário tooprovide uma lista completa de todos os tooclients de hosts.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="e1cc3-205">Um ou dois são suficientes.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-205">One or two is enough.</span></span>

    <span data-ttu-id="e1cc3-206">Salve esse valor, pois ele é usado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="e1cc3-207">Editar saudação `dev.properties` arquivo na raiz de saudação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="e1cc3-208">Adicione hello Broker e linhas correspondentes do toohello Zookeeper hosts informações neste arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="e1cc3-209">Olá exemplo a seguir é configurado com os valores de exemplo hello de etapas anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="e1cc3-210">Salvar Olá `dev.properties` arquivo e usar o hello após o comando tooupload-cluster Storm de toohello:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="e1cc3-211">Substituir **nome de usuário** com nome de usuário SSH Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="e1cc3-212">Substituir **nome base** com o nome de base Olá usados ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="e1cc3-213">Iniciar o gravador de saudação</span><span class="sxs-lookup"><span data-stu-id="e1cc3-213">Start hello writer</span></span>

1. <span data-ttu-id="e1cc3-214">Use Olá seguindo o cluster de Storm toohello tooconnect usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="e1cc3-215">Substituir **nome de usuário** com nome de usuário SSH Olá usado ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="e1cc3-216">Substituir **nome base** com o nome de base Olá usado ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="e1cc3-217">Quando solicitado, insira a senha Olá usada durante a criação de clusters de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="e1cc3-218">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e1cc3-219">De Olá conexão SSH, use Olá Olá do comando toocreate tópico Kafka usado pelo topologia Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="e1cc3-220">Substituir `$KAFKAZKHOSTS` com hello Zookeeper hospedar as informações recuperadas na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="e1cc3-221">De cluster da saudação SSH conexão toohello Storm, use Olá topologia de gravador de saudação do comando toostart a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="e1cc3-222">Olá parâmetros usados com este comando são:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="e1cc3-223">`org.apache.storm.flux.Flux`: Use fluxo tooconfigure e execute esta topologia.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="e1cc3-224">`--remote`: Envie Olá tooNimbus de topologia.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="e1cc3-225">topologia de saudação é distribuída entre nós de trabalho Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="e1cc3-226">`-R /writer.yaml`: Olá usar `writer.yaml` tooconfigure topologia de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="e1cc3-227">`-R`indica que esse recurso está incluído no arquivo jar de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="e1cc3-228">É na raiz de saudação do jar hello, portanto `/writer.yaml` é Olá tooit de caminho.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="e1cc3-229">`--filter`: Preencher entradas no hello `writer.yaml` topologia usando valores de saudação `dev.properties` arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="e1cc3-230">Olá, por exemplo, o valor de saudação `kafka.topic` entrada no arquivo hello é usado tooreplace Olá `${kafka.topic}` entrada em definição de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="e1cc3-231">Após o início de topologia Olá use Olá tooverify de comando que está gravando dados toohello tópico Kafka a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="e1cc3-232">Substituir `$KAFKAZKHOSTS` com hello Zookeeper hospedar as informações recuperadas na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="e1cc3-233">Esse comando usa um script que acompanham o tópico de saudação do Kafka toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="e1cc3-234">Após um momento, ele deve ser iniciado retornando aleatórias sentenças que foram gravadas toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="e1cc3-235">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="e1cc3-236">Use Ctrl + c toostop script de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="e1cc3-237">Leitor de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="e1cc3-237">Start hello reader</span></span>

1. <span data-ttu-id="e1cc3-238">De cluster da saudação SSH sessão toohello Storm, use Olá topologia de leitor de saudação do comando toostart a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="e1cc3-239">Depois de iniciada a topologia hello, abra Olá profusão de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="e1cc3-240">Essa interface do usuário da Web está localizada em https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="e1cc3-241">Substituir __nome base__ com o nome de base Olá usado quando Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="e1cc3-242">Quando solicitado, use o nome de logon do administrador de saudação (padrão, `admin`) e a senha usada durante a saudação cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="e1cc3-243">Você verá um toohello semelhante de página da web imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-243">You see a web page similar toohello following image:</span></span>

    ![Interface do Usuário do Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="e1cc3-245">Olá profusão de interface do usuário, selecione Olá __kafka leitor__ link no hello __Resumo da topologia__ seção toodisplay informações sobre Olá __kafka leitor__ topologia.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Na seção topologia do resumida da interface da web hello Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="e1cc3-247">toodisplay informações sobre as instâncias de saudação do componente de raio do agente de log hello, selecione Olá __raio de agente de log__ link no hello __parafusos (tempo de todos os)__ seção.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Link de raio de agente na seção de parafusos Olá](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="e1cc3-249">Em Olá __executores__ seção, selecione um link no hello __porta__ log de toodisplay de coluna de informações sobre essa instância do componente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Link de executores](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="e1cc3-251">log Olá contém um log de saudação da leitura dos dados Olá tópico Kafka.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="e1cc3-252">informações de Olá no log de saudação são semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="e1cc3-253">Parar topologias Olá</span><span class="sxs-lookup"><span data-stu-id="e1cc3-253">Stop hello topologies</span></span>

<span data-ttu-id="e1cc3-254">De um cluster Storm do SSH sessão toohello, use Olá topologias de profusão de saudação de toostop comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cc3-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="e1cc3-255">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="e1cc3-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e1cc3-256">Como criam etapas de saudação neste documento hello de clusters no mesmo grupo de recursos do Azure, você pode excluir o grupo de recursos Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="e1cc3-257">Excluindo grupo de recursos de saudação remove todos os recursos criados por este documento a seguir.</span><span class="sxs-lookup"><span data-stu-id="e1cc3-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1cc3-258">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1cc3-258">Next steps</span></span>

<span data-ttu-id="e1cc3-259">Para obter mais topologias de exemplo que podem ser usadas com o Storm no HDInsight, confira [Topologias Storm de exemplo e componentes](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e1cc3-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="e1cc3-260">Para obter informações sobre como implantar e monitorar topologias no HDInsight baseado em Linux, confira [Implantar e gerenciar topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e1cc3-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>