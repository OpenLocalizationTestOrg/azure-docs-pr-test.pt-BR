---
title: "aaaUse de atividades personalizadas em um pipeline da fábrica de dados do Azure"
description: "Saiba como atividades personalizadas toocreate e usá-los em um pipeline da fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="5dd54-103">Usar atividades personalizadas em um pipeline do Data Factory do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd54-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5dd54-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="5dd54-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="5dd54-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="5dd54-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5dd54-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="5dd54-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5dd54-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="5dd54-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5dd54-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="5dd54-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5dd54-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5dd54-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5dd54-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5dd54-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5dd54-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="5dd54-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5dd54-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5dd54-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5dd54-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="5dd54-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="5dd54-114">Há dois tipos de atividades que você pode usar em um pipeline do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5dd54-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="5dd54-115">[As atividades de movimentação de dados](data-factory-data-movement-activities.md) toomove dados entre [suporte para armazenamentos de dados de origem e do coletor](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="5dd54-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="5dd54-116">[Atividades de transformação de dados](data-factory-data-transformation-activities.md) tootransform dados usando compute serviços como HDInsight do Azure, o lote do Azure e o aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="5dd54-117">toomove dados para/de um repositório de dados que não dão suporte a fábrica de dados, crie um **atividade personalizada** com seu próprios dados movimentação lógica e use hello atividade em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="5dd54-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="5dd54-118">Da mesma forma, tootransform/processar dados de forma que não é suportado pela fábrica de dados, criar uma atividade personalizada com sua própria lógica de transformação de dados e usar a atividade de saudação em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="5dd54-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="5dd54-119">Você pode configurar uma atividade personalizada toorun em uma **do Azure Batch** pool de máquinas virtuais ou baseado em Windows **HDInsight do Azure** cluster.</span><span class="sxs-lookup"><span data-stu-id="5dd54-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="5dd54-120">Ao usar o Azure Batch, você só pode utilizar um pool de Lote do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="5dd54-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="5dd54-121">Ao passo que, ao usar o HDInsight, você pode usar um cluster HDInsight existente ou um cluster criado automaticamente para você sob demanda no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5dd54-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="5dd54-122">Olá, passo a passo fornece instruções passo a passo para criar uma atividade personalizada do .NET e usar atividades personalizadas Olá em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="5dd54-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="5dd54-123">Olá passo a passo usa um **do Azure Batch** serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="5dd54-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="5dd54-124">serviço vinculado toouse um HDInsight do Azure, você cria um serviço vinculado do tipo **HDInsight** (seu próprio cluster HDInsight) ou **HDInsightOnDemand** (fábrica de dados cria um cluster HDInsight sob demanda).</span><span class="sxs-lookup"><span data-stu-id="5dd54-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="5dd54-125">Em seguida, configure Olá toouse de atividade personalizada serviço vinculado do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="5dd54-126">Consulte [serviços vinculados do uso do Azure HDInsight](#use-hdinsight-compute-service) seção para obter detalhes sobre o uso de atividade personalizada do Azure HDInsight toorun hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="5dd54-127">atividades personalizadas de .NET Olá executadas somente em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="5dd54-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5dd54-128">Uma alternativa para essa limitação é toouse Olá mapa reduzir atividade toorun Java código personalizado em um cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="5dd54-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5dd54-129">Outra opção é toouse um pool de lote do Azure de atividades personalizadas de toorun de VMs em vez de usar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="5dd54-130">Não é possível toouse um Gateway de gerenciamento de dados de uma atividade personalizada tooaccess locais fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="5dd54-131">Atualmente, [Data Management Gateway](data-factory-data-management-gateway.md) suporta apenas a atividade de cópia de saudação e a atividade de procedimento armazenado na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="5dd54-132">Passo a passo: criar uma atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="5dd54-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="5dd54-133">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5dd54-133">Prerequisites</span></span>
* <span data-ttu-id="5dd54-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="5dd54-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="5dd54-135">Baixar e instalar o [SDK .NET do Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="5dd54-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="5dd54-136">Pré-requisitos de Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd54-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="5dd54-137">Olá instruções passo a passo, você executa suas atividades personalizadas do .NET usando o lote do Azure como um recurso de computação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="5dd54-138">**Lote do Azure** é uma plataforma de serviço para execução paralela em grande escala e de aplicativos HPC (computação) com eficiência na nuvem de saudação de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="5dd54-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="5dd54-139">Lote do Azure agenda toorun de trabalho de computação intensa no gerenciada **coleção de máquinas virtuais**, pode automaticamente escala de computação e necessidades de saudação toomeet recursos de seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="5dd54-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="5dd54-140">Consulte [Noções básicas do lote do Azure] [ batch-technical-overview] artigo para uma visão geral detalhada da saudação serviço de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="5dd54-141">Tutorial de hello, crie uma conta de lote do Azure com um pool de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5dd54-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="5dd54-142">Aqui estão as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="5dd54-142">Here are hello steps:</span></span>

1. <span data-ttu-id="5dd54-143">Criar um **conta de lote do Azure** usando Olá [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5dd54-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="5dd54-144">Consulte o artigo [Criar e gerenciar uma conta do Lote do Azure][batch-create-account] para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="5dd54-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="5dd54-145">Anote o nome da conta do Azure Batch hello, chave de conta, URI e nome do pool.</span><span class="sxs-lookup"><span data-stu-id="5dd54-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="5dd54-146">É necessário que eles toocreate um serviço vinculado do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="5dd54-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="5dd54-147">Na página inicial de saudação para conta de lote do Azure, você vê um **URL** em Olá formato a seguir: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5dd54-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="5dd54-148">Neste exemplo, **myaccount** é nome de saudação do hello conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="5dd54-149">URI usado na definição de serviço vinculada de saudação é a URL de saudação sem nome hello da conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="5dd54-150">Por exemplo: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5dd54-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="5dd54-151">Clique em **chaves** no menu à esquerda do hello e Olá cópia **chave de acesso primário**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="5dd54-152">toouse um pool existente, clique em **Pools** no menu hello e anote Olá **ID** do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="5dd54-153">Se você não tiver um pool existente, mova toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="5dd54-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="5dd54-154">Crie um pool do **Lote do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="5dd54-155">Em Olá [portal do Azure](https://portal.azure.com), clique em **procurar** no hello menus à esquerda e clique em **contas em lotes**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="5dd54-156">Selecione sua saudação do lote do Azure conta tooopen **conta em lotes** folha.</span><span class="sxs-lookup"><span data-stu-id="5dd54-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="5dd54-157">Clique no bloco **Pools** .</span><span class="sxs-lookup"><span data-stu-id="5dd54-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="5dd54-158">Em Olá **Pools** folha, clique no botão Adicionar na saudação da barra de ferramentas tooadd um pool.</span><span class="sxs-lookup"><span data-stu-id="5dd54-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="5dd54-159">Insira uma ID para o pool de saudação (ID do Pool).</span><span class="sxs-lookup"><span data-stu-id="5dd54-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="5dd54-160">Saudação de Observação **ID do pool de saudação**; é necessário ao criar a solução de fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="5dd54-161">Especifique **Windows Server 2012 R2** para configuração da família de sistemas operacionais de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="5dd54-162">Selecione um **camada de preços de nó**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="5dd54-163">Digite **2** como valor para Olá **destino dedicado** configuração.</span><span class="sxs-lookup"><span data-stu-id="5dd54-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="5dd54-164">Digite **2** como valor para Olá **tarefas máxima por nó** configuração.</span><span class="sxs-lookup"><span data-stu-id="5dd54-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="5dd54-165">Clique em **Okey** toocreate pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="5dd54-166">Anote Olá **ID** do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="5dd54-167">Etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="5dd54-167">High-level steps</span></span>
<span data-ttu-id="5dd54-168">Aqui estão Olá duas etapas de alto nível que fazem parte deste passo a passo:</span><span class="sxs-lookup"><span data-stu-id="5dd54-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="5dd54-169">Crie uma atividade personalizada que contenha uma lógica simples de processamento/transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="5dd54-170">Crie uma fábrica de dados do Azure com um pipeline que usa a atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="5dd54-171">Criar uma atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="5dd54-171">Create a custom activity</span></span>
<span data-ttu-id="5dd54-172">toocreate uma atividade personalizada do .NET, crie um **biblioteca de classes .NET** projeto com uma classe que implementa que **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="5dd54-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="5dd54-173">Essa interface tem apenas um método: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , e a assinatura é:</span><span class="sxs-lookup"><span data-stu-id="5dd54-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="5dd54-174">método Hello usa quatro parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5dd54-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="5dd54-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-175">**linkedServices**.</span></span> <span data-ttu-id="5dd54-176">Esta propriedade é uma lista enumerável de serviços de repositório de dados vinculado referenciado por conjuntos de dados de entrada/saída para a atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="5dd54-177">**conjuntos de dados**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-177">**datasets**.</span></span> <span data-ttu-id="5dd54-178">Esta propriedade é uma lista enumerável de conjuntos de dados de entrada/saída para a atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="5dd54-179">Você pode usar este locais de saudação do parâmetro tooget e esquemas definidos pelos conjuntos de dados de entrada e saídos.</span><span class="sxs-lookup"><span data-stu-id="5dd54-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="5dd54-180">**atividade**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-180">**activity**.</span></span> <span data-ttu-id="5dd54-181">Esta propriedade representa a atividade atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-181">This property represents hello current activity.</span></span> <span data-ttu-id="5dd54-182">Ele pode ser usado tooaccess propriedades estendidas associadas com a atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="5dd54-183">Consulte [Acessar propriedades estendidas](#access-extended-properties) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="5dd54-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="5dd54-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-184">**logger**.</span></span> <span data-ttu-id="5dd54-185">Esse objeto permite que você escreva essa superfície de comentários de depuração no log de usuário Olá para o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="5dd54-186">método Hello retorna um dicionário que pode ser atividades personalizadas toochain usados juntos em um futuro hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="5dd54-187">Este recurso ainda não foi implementado, isso retornará um dicionário vazio do método hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="5dd54-188">Procedimento</span><span class="sxs-lookup"><span data-stu-id="5dd54-188">Procedure</span></span>
1. <span data-ttu-id="5dd54-189">Crie um projeto de **Biblioteca de Classes do .NET** .</span><span class="sxs-lookup"><span data-stu-id="5dd54-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="5dd54-190">Inicialize o <b>Visual Studio 2017</b> ou o <b>Visual Studio 2015</b> ou o <b>Visual Studio 2013</b> ou o <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="5dd54-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="5dd54-191">Clique em <b>arquivo</b>, ponto muito<b>novo</b>e clique em <b>projeto</b>.</span><span class="sxs-lookup"><span data-stu-id="5dd54-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="5dd54-192">Expanda <b>Modelos</b> e selecione <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="5dd54-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="5dd54-193">Neste passo a passo, você pode usar c#, mas você pode usar qualquer atividade personalizada do .NET idioma toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="5dd54-194">Selecione <b>biblioteca de classes</b> da lista de saudação de tipos de projeto em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="5dd54-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="5dd54-195">No VS 2017, escolha <b>Biblioteca de Classes (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="5dd54-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="5dd54-196">Digite <b>MyDotNetActivity</b> para Olá <b>nome</b>.</span><span class="sxs-lookup"><span data-stu-id="5dd54-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="5dd54-197">Selecione <b>C:\ADFGetStarted</b> para Olá <b>local</b>.</span><span class="sxs-lookup"><span data-stu-id="5dd54-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="5dd54-198">Clique em <b>Okey</b> toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="5dd54-199">
2.Clique em **ferramentas**, ponto muito**NuGet Package Manager**e clique em **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="5dd54-200">3.</span><span class="sxs-lookup"><span data-stu-id="5dd54-200">3.</span></span> <span data-ttu-id="5dd54-201">No hello Package Manager Console, execute Olá após o comando tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="5dd54-202">Saudação de importação **armazenamento do Azure** pacote do NuGet no projeto toohello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="5dd54-203">Iniciador do serviço de fábrica de dados requer a versão de hello 4.3 do windowsazure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="5dd54-204">Se você adicionar uma referência tooa versão posterior do assembly de armazenamento do Azure no seu projeto de atividade personalizada, você vê um erro quando hello atividade é executada.</span><span class="sxs-lookup"><span data-stu-id="5dd54-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="5dd54-205">Erro de saudação tooresolve, consulte [Appdomain isolamento](#appdomain-isolation) seção.</span><span class="sxs-lookup"><span data-stu-id="5dd54-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="5dd54-206">Adicione o seguinte Olá **usando** instruções toohello fonte arquivo hello projeto.</span><span class="sxs-lookup"><span data-stu-id="5dd54-206">Add hello following **using** statements toohello source file in hello project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="5dd54-207">Alterar o nome de saudação do hello **namespace** muito**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="5dd54-208">Alterar o nome de saudação da classe Olá muito**MyDotNetActivity** e ele derivam Olá **IDotNetActivity** interface conforme mostrado no trecho de código a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="5dd54-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="5dd54-209">Saudação de implementar (Adicionar) **Execute** método hello **IDotNetActivity** interface toohello **MyDotNetActivity** Olá cópia e de classe, método de toohello de código de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5dd54-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="5dd54-210">Olá exemplo a seguir conta Olá número de ocorrências do termo de pesquisa da saudação ("Microsoft") em cada blob associado a uma fatia de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="5dd54-211">Adicione Olá métodos auxiliares a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-211">Add hello following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="5dd54-212">Olá GetFolderPath método retorna Olá caminho toohello pasta que Olá dataset aponta tooand Olá GetFileName retorna Olá nome do método de saudação/arquivo de blob que Olá pontos de conjunto de dados para.</span><span class="sxs-lookup"><span data-stu-id="5dd54-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="5dd54-213">Se você havefolderPath define usando variáveis como {Year}, {Month} retorna {Day} etc., método hello Olá cadeia de caracteres que é sem substituí-los com valores de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5dd54-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="5dd54-214">Confira a seção [Acessar propriedades estendidas](#access-extended-properties) para obter detalhes sobre como acessar SliceStart, SliceEnd, etc.</span><span class="sxs-lookup"><span data-stu-id="5dd54-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="5dd54-215">Olá método Calculate calcula o número de saudação de instâncias da palavra-chave Microsoft nos arquivos de entrada hello (blobs na pasta Olá).</span><span class="sxs-lookup"><span data-stu-id="5dd54-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="5dd54-216">termo de pesquisa da saudação ("Microsoft") é embutido em código hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="5dd54-217">Compile o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-217">Compile hello project.</span></span> <span data-ttu-id="5dd54-218">Clique em **criar** de saudação menu e clique em **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5dd54-219">Conjunto 4.5.2 versão do .NET Framework, como o framework de destino de saudação do seu projeto: clique com botão direito hello e, em seguida, clique em **propriedades** tooset framework de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="5dd54-220">O Data Factory não oferece suporte a atividades personalizadas compiladas em versões do .NET Framework posteriores a 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="5dd54-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="5dd54-221">Iniciar **Windows Explorer**e navegue muito**bin\debug** ou **bin\release** pasta dependendo do tipo de saudação da compilação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="5dd54-222">Criar um arquivo zip **MyDotNetActivity.zip** que contém todos os binários de saudação em Olá <project folder>pasta \bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="5dd54-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="5dd54-223">Incluir Olá **MyDotNetActivity.pdb** arquivos de forma que você obter detalhes adicionais, como o número de linha no código-fonte Olá que causou o problema de saudação se houve uma falha.</span><span class="sxs-lookup"><span data-stu-id="5dd54-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="5dd54-224">Todos Olá arquivos contidos no arquivo zip Olá para atividade de saudação personalizada deve estar no hello **nível superior** com nenhuma subpastas.</span><span class="sxs-lookup"><span data-stu-id="5dd54-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![Arquivos de saída binários](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="5dd54-226">Crie um contêiner de blob chamado **customactivitycontainer** se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="5dd54-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="5dd54-227">Carregar MyDotNetActivity.zip como customactivitycontainer de toohello um blob em um **geral** armazenamento de BLOBs do Azure (armazenamento de Blob não hot/cool) que é referenciado por AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="5dd54-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="5dd54-228">Se você adiciona essa solução de tooa de projeto de atividade .NET no Visual Studio que contém um projeto de fábrica de dados e adicionar um projeto de atividade de too.NET de referência de projeto de aplicativo hello fábrica de dados, não é necessário tooperform Olá duas últimas etapas de criação manual arquivo zip de saudação e carregando-o armazenamento de BLOBs do Azure para fins gerais toohello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="5dd54-229">Quando você publica entidades da fábrica de dados usando o Visual Studio, essas etapas são executadas automaticamente pelo processo de publicação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="5dd54-230">Para obter mais informações, consulte a seção [projeto de Data Factory no Visual Studio](#data-factory-project-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="5dd54-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="5dd54-231">Criar um pipeline com atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="5dd54-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="5dd54-232">Você criar uma atividade personalizada e carregar o arquivo zip de saudação com contêiner de blob tooa binários em uma **geral** conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="5dd54-233">Nesta seção, você pode criar uma fábrica de dados do Azure com um pipeline que usa a atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="5dd54-234">conjunto de dados de entrada de Hello atividade personalizado Olá representa blobs (arquivos) na pasta de customactivityinput de saudação do contêiner adftutorial no armazenamento de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="5dd54-235">Olá o conjunto de dados de saída para a atividade de saudação representa blobs de saída na pasta de customactivityoutput de saudação do contêiner adftutorial no armazenamento de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="5dd54-236">Criar **arquivo.txt** arquivo com hello seguinte conteúdo e carregá-lo muito**customactivityinput** pasta da saudação **adftutorial** contêiner.</span><span class="sxs-lookup"><span data-stu-id="5dd54-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="5dd54-237">Crie contêiner de adftutorial Olá se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="5dd54-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="5dd54-238">pasta entrada Hello corresponde tooa fatia na fábrica de dados do Azure, mesmo se a pasta de saudação tem dois ou mais arquivos.</span><span class="sxs-lookup"><span data-stu-id="5dd54-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="5dd54-239">Quando cada fatia é processada pelo pipeline hello, atividade personalizada Olá itera em todos os blobs de saudação na pasta de entrada hello essa fatia.</span><span class="sxs-lookup"><span data-stu-id="5dd54-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="5dd54-240">Você verá um arquivo na pasta de adftutorial\customactivityoutput Olá de saída com uma ou mais linhas (mesmo que o número de blobs na pasta de entrada hello):</span><span class="sxs-lookup"><span data-stu-id="5dd54-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="5dd54-241">Aqui estão as etapas Olá que executar nesta seção:</span><span class="sxs-lookup"><span data-stu-id="5dd54-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="5dd54-242">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="5dd54-243">Criar **serviços vinculados** para pool de lote do Azure Olá de VMs em qual hello atividade personalizada é executado e Olá armazenamento do Azure que contém Olá blobs de entrada/saída.</span><span class="sxs-lookup"><span data-stu-id="5dd54-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="5dd54-244">Criar a entrada e saída **conjuntos de dados** que representam a entrada e saída da atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="5dd54-245">Criar um **pipeline** que usa a atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="5dd54-246">Criar hello **arquivo.txt** e carregue-o contêiner de blob tooa se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="5dd54-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="5dd54-247">Consulte as instruções em Olá anterior de seção.</span><span class="sxs-lookup"><span data-stu-id="5dd54-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="5dd54-248">Etapa 1: Criar a fábrica de dados Olá</span><span class="sxs-lookup"><span data-stu-id="5dd54-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="5dd54-249">Após o logon toohello portal do Azure, Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="5dd54-250">Clique em **novo** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="5dd54-251">Clique em **dados + análise** em Olá **novo** folha.</span><span class="sxs-lookup"><span data-stu-id="5dd54-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="5dd54-252">Clique em **Data Factory** em Olá **análises de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="5dd54-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Novo menu do Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="5dd54-254">Em Olá **nova fábrica de dados** folha, digite **CustomActivityFactory** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="5dd54-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="5dd54-255">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5dd54-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="5dd54-256">Se você receber o erro Olá: **"CustomActivityFactory" nome da fábrica de dados não está disponível**, alterar nome Olá Olá da fábrica de dados (por exemplo, **yournameCustomActivityFactory**) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="5dd54-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Nova folha do Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="5dd54-258">Clique em **NOME DO GRUPO DE RECURSOS**para selecionar um grupo de recursos existente ou criar um.</span><span class="sxs-lookup"><span data-stu-id="5dd54-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="5dd54-259">Verificar se você está usando Olá correto **assinatura** e **região** onde você deseja Olá toobe de fábrica de dados criado.</span><span class="sxs-lookup"><span data-stu-id="5dd54-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="5dd54-260">Clique em **criar** em Olá **nova fábrica de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="5dd54-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="5dd54-261">Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="5dd54-262">Depois de fábrica de dados Olá tiver sido criada com êxito, você verá a folha de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Folha Data Factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="5dd54-264">Etapa 2: Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="5dd54-264">Step 2: Create linked services</span></span>
<span data-ttu-id="5dd54-265">Serviços vinculados vincular armazenamentos de dados ou de computação serviços tooan data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="5dd54-266">Nesta etapa, você pode vincular sua conta de armazenamento do Azure e a fábrica de dados de tooyour de conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="5dd54-267">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd54-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="5dd54-268">Clique em Olá **autor e implantar** bloco Olá **DATA FACTORY** folha para **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="5dd54-269">Você verá Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="5dd54-270">Clique em **novo repositório de dados** Olá barra de comandos e escolha **armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="5dd54-271">Você deve ver Olá script JSON para a criação de um armazenamento do Azure vinculada serviço no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![Novo armazenamento de dados – Armazenamento do Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="5dd54-273">Substituir `<accountname>` com o nome da sua conta de armazenamento do Azure e `<accountkey>` com a chave de acesso do hello conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="5dd54-274">toolearn como tooget seu armazenamento acessar chave, consulte [exibir, copiar e regenerar as contas de armazenamento de chaves de acesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5dd54-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Serviço vinculado do Armazenamento do Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="5dd54-276">Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="5dd54-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="5dd54-277">Crie o serviço vinculado do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd54-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="5dd54-278">No hello Editor da fábrica de dados, clique em **... Mais** na barra de comandos de saudação, clique em **nova computação**e, em seguida, selecione **do Azure Batch** menu hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![Nova computação – Lote do Azure](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="5dd54-280">Verifique Olá alterações toohello JSON script a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="5dd54-281">Especifique o nome da conta de lote do Azure para Olá **accountName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="5dd54-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="5dd54-282">Olá **URL** de saudação **folha de conta de lote do Azure** está em Olá formato a seguir: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5dd54-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="5dd54-283">Para Olá **batchUri** propriedade Olá JSON, você precisa tooremove `accountname.` de Olá Olá URL e use `accountname` para Olá `accountName` propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="5dd54-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="5dd54-284">Especifique a chave de conta de lote do Azure Olá para hello **accessKey** propriedade.</span><span class="sxs-lookup"><span data-stu-id="5dd54-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="5dd54-285">Especifique o nome de saudação de pool de saudação criado como parte dos pré-requisitos para hello **poolName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="5dd54-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="5dd54-286">Você também pode especificar a ID de saudação do pool de saudação em vez do nome de saudação do pool de saudação de.</span><span class="sxs-lookup"><span data-stu-id="5dd54-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="5dd54-287">Especifique o URI do lote do Azure para Olá **batchUri** propriedade.</span><span class="sxs-lookup"><span data-stu-id="5dd54-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="5dd54-288">Exemplo: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5dd54-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="5dd54-289">Especifique a saudação **AzureStorageLinkedService** para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="5dd54-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="5dd54-290">Para Olá **poolName** propriedade, você também pode especificar a ID de saudação do pool de saudação em vez do nome de saudação do pool de saudação de.</span><span class="sxs-lookup"><span data-stu-id="5dd54-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="5dd54-291">Olá serviço da fábrica de dados não dá suporte uma opção sob demanda para o lote do Azure como faz para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="5dd54-292">Você só pode usar seu próprio pool do Azure Batch em um Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5dd54-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="5dd54-293">Etapa 3: Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="5dd54-293">Step 3: Create datasets</span></span>
<span data-ttu-id="5dd54-294">Nesta etapa, você cria conjuntos de dados toorepresent entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="5dd54-295">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="5dd54-295">Create input dataset</span></span>
1. <span data-ttu-id="5dd54-296">Em Olá **Editor** para Olá fábrica de dados, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e, em seguida, selecione **armazenamento de BLOBs do Azure** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="5dd54-297">Substitua Olá JSON no painel direito Olá Olá trecho JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="5dd54-298">Você cria um pipeline posteriormente neste passo a passo com hora de início: 2016-11-16T00:00:00Z e final: 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="5dd54-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="5dd54-299">São dados tooproduce agendado por hora, portanto, há cinco fatias de entrada/saída (entre **00**: 00:00 -> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="5dd54-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="5dd54-300">Olá **frequência** e **intervalo** para o conjunto de dados de entrada hello está definido muito**hora** e **1**, que significa que Olá entrada fatia está disponível por hora.</span><span class="sxs-lookup"><span data-stu-id="5dd54-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="5dd54-301">Neste exemplo, é Olá mesmo arquivo (arquivo. txt) em intputfolder hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="5dd54-302">Aqui estão os horários de início de saudação de cada fatia, que é representado pela variável de sistema SliceStart no hello acima trecho JSON.</span><span class="sxs-lookup"><span data-stu-id="5dd54-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="5dd54-303">Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="5dd54-304">Confirme que você vê Olá **tabela CRIADA com êxito** mensagem na barra de título de saudação da saudação Editor.</span><span class="sxs-lookup"><span data-stu-id="5dd54-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="5dd54-305">Criar um conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="5dd54-305">Create an output dataset</span></span>
1. <span data-ttu-id="5dd54-306">Em Olá **editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e, em seguida, selecione **armazenamento de BLOBs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="5dd54-307">Substitua script JSON de saudação no painel direito Olá Olá script JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="5dd54-308">Local de saída é **adftutorial/customactivityoutput/** e o nome do arquivo de saída é AAAA-MM-dd-HH.txt onde AAAA-MM-dd-HH é ano hello, mês, data e hora da fatia Olá sendo produzida.</span><span class="sxs-lookup"><span data-stu-id="5dd54-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="5dd54-309">Consulte a [Referência do Desenvolvedor][adf-developer-reference] para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5dd54-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="5dd54-310">Um blob/arquivo de saída é gerado para cada fatia de entrada.</span><span class="sxs-lookup"><span data-stu-id="5dd54-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="5dd54-311">Aqui está como um arquivo de saída é chamado para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="5dd54-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="5dd54-312">Todos os arquivos de saída de hello são gerados em uma pasta de saída: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="5dd54-313">Fatia</span><span class="sxs-lookup"><span data-stu-id="5dd54-313">Slice</span></span> | <span data-ttu-id="5dd54-314">Hora de início</span><span class="sxs-lookup"><span data-stu-id="5dd54-314">Start time</span></span> | <span data-ttu-id="5dd54-315">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="5dd54-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="5dd54-316">1</span><span class="sxs-lookup"><span data-stu-id="5dd54-316">1</span></span> |<span data-ttu-id="5dd54-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="5dd54-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="5dd54-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="5dd54-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="5dd54-319">2</span><span class="sxs-lookup"><span data-stu-id="5dd54-319">2</span></span> |<span data-ttu-id="5dd54-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="5dd54-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="5dd54-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="5dd54-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="5dd54-322">3</span><span class="sxs-lookup"><span data-stu-id="5dd54-322">3</span></span> |<span data-ttu-id="5dd54-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="5dd54-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="5dd54-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="5dd54-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="5dd54-325">4</span><span class="sxs-lookup"><span data-stu-id="5dd54-325">4</span></span> |<span data-ttu-id="5dd54-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="5dd54-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="5dd54-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="5dd54-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="5dd54-328">5</span><span class="sxs-lookup"><span data-stu-id="5dd54-328">5</span></span> |<span data-ttu-id="5dd54-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="5dd54-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="5dd54-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="5dd54-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="5dd54-331">Lembre-se de que todos os arquivos de saudação em uma pasta de entrada são parte de uma fatia com horários de início da saudação mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="5dd54-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="5dd54-332">Quando essa fatia é processada, a atividade personalizada Olá verifica cada arquivo e produz uma linha no arquivo de saída de hello com número de saudação de ocorrências do termo de pesquisa ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="5dd54-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="5dd54-333">Se houver três arquivos na inputfolder hello, há três linhas no arquivo de saída de saudação de cada fatia por hora: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span><span class="sxs-lookup"><span data-stu-id="5dd54-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="5dd54-334">Olá toodeploy **OutputDataset**, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="5dd54-335">Criar e executar um pipeline que usa a atividade personalizada Olá</span><span class="sxs-lookup"><span data-stu-id="5dd54-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="5dd54-336">No hello Editor da fábrica de dados, clique em **... Mais**e, em seguida, selecione **novo pipeline** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="5dd54-337">Substitua Olá JSON no painel direito Olá Olá script JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="5dd54-338">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-338">Note hello following points:</span></span>

   * <span data-ttu-id="5dd54-339">**Simultaneidade** está definido muito**2** para que duas fatias são processadas em paralelo por 2 VMs no pool de lote do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="5dd54-340">Há uma atividade na seção de atividades de saudação e é do tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="5dd54-341">**AssemblyName** é definir o nome toohello Olá DLL: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="5dd54-342">**Ponto de entrada** está definido muito**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="5dd54-343">**PackageLinkedService** está definido muito**AzureStorageLinkedService** que aponte toohello armazenamento de blob que contém o arquivo de zip hello atividade personalizado.</span><span class="sxs-lookup"><span data-stu-id="5dd54-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="5dd54-344">Se você estiver usando diferentes contas de armazenamento do Azure para arquivos de entrada/saída e hello arquivo zip de atividade personalizada, você criar outro serviço vinculado do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="5dd54-345">Este artigo pressupõe que você está usando Olá a mesma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="5dd54-346">**PackageFile** está definido muito**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="5dd54-347">Formato de saudação: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="5dd54-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="5dd54-348">atividades personalizadas Olá **InputDataset** como entrada e **OutputDataset** como saída.</span><span class="sxs-lookup"><span data-stu-id="5dd54-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="5dd54-349">propriedade linkedServiceName Hello atividade personalizada Olá pontos toohello **AzureBatchLinkedService**, que informa ao Azure Data Factory dessa atividade personalizada Olá precisa toorun em VMs do lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="5dd54-350">**isPaused** propriedade for definida muito**false** por padrão.</span><span class="sxs-lookup"><span data-stu-id="5dd54-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="5dd54-351">Olá pipeline é executado imediatamente neste exemplo como fatias Olá começam em Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="5dd54-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="5dd54-352">Você pode configurar o pipeline de saudação essa propriedade tootrue toopause e defina-a como toorestart toofalse back.</span><span class="sxs-lookup"><span data-stu-id="5dd54-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="5dd54-353">Olá **iniciar** tempo e **final** vezes são **cinco** horas separadas e fatias são produzidas por hora, para cinco fatias são produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="5dd54-354">pipeline de saudação toodeploy, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="5dd54-355">Pipeline de saudação do monitor</span><span class="sxs-lookup"><span data-stu-id="5dd54-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="5dd54-356">Na folha da fábrica de dados Olá no hello portal do Azure, clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Bloco do diagrama](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="5dd54-358">Na exibição de diagrama de Olá, agora clique Olá OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="5dd54-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Exibição de diagrama](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="5dd54-360">Você deve ver que cinco fatias de saída Olá estão em estado pronto do hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="5dd54-361">Se não estiverem no estado pronto do hello, que ainda não foram produzidas ainda.</span><span class="sxs-lookup"><span data-stu-id="5dd54-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Fatias de saída](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="5dd54-363">Verifique se que arquivos de saída de hello são gerados no armazenamento de blob de saudação em Olá **adftutorial** contêiner.</span><span class="sxs-lookup"><span data-stu-id="5dd54-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![saída de atividade personalizada][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="5dd54-365">Se você abrir o arquivo de saída de hello, você deve ver Olá saída semelhante toohello saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="5dd54-366">Saudação de uso [portal do Azure] [ azure-preview-portal] ou toomonitor de cmdlets do PowerShell do Azure sua fábrica de dados, pipelines e conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="5dd54-367">Você pode ver as mensagens de saudação **ActivityLogger** no código de saudação para a atividade personalizada Olá nos logs de saudação (especificamente usuário-0.log) que você pode baixar do portal de saudação ou usando cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5dd54-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![baixar logs de atividade personalizada][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="5dd54-369">Consulte [Monitorar e Gerenciar Pipelines](data-factory-monitor-manage-pipelines.md) para obter etapas detalhadas do monitoramento de conjuntos de dados e pipelines.</span><span class="sxs-lookup"><span data-stu-id="5dd54-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="5dd54-370">Projeto de Data Factory no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5dd54-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="5dd54-371">Você pode criar e publicar entidades de Data Factory usando o Visual Studio, em vez de usar o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="5dd54-372">Para obter informações detalhadas sobre a criação e publicação de entidades da fábrica de dados usando o Visual Studio, consulte [criar seu primeiro pipeline usando o Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) e [copiar dados de Blob do Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="5dd54-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="5dd54-373">Olá etapas adicionais a seguir se você estiver criando o projeto de fábrica de dados no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5dd54-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="5dd54-374">Adicione Olá Data Factory projeto toohello solução do Visual Studio que contém o projeto de atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="5dd54-375">Adicione um projeto de atividade do .NET de toohello Referência de projeto de fábrica de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="5dd54-376">Clique com botão direito fábrica de dados, aponte muito**adicionar**e, em seguida, clique em **referência**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="5dd54-377">Em Olá **adicionar referência** caixa de diálogo, selecione Olá **MyDotNetActivity** do projeto e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="5dd54-378">Criar e publicar Olá solução.</span><span class="sxs-lookup"><span data-stu-id="5dd54-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5dd54-379">Quando você publica entidades da fábrica de dados, um arquivo zip é criado automaticamente para você e é o contêiner de blob carregado toohello: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="5dd54-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="5dd54-380">Se o contêiner de blob Olá não existir, ela é criada automaticamente muito.</span><span class="sxs-lookup"><span data-stu-id="5dd54-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="5dd54-381">Integração de Data Factory e Lote</span><span class="sxs-lookup"><span data-stu-id="5dd54-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="5dd54-382">Olá serviço da fábrica de dados cria um trabalho em lote do Azure com o nome da saudação: **poolname adf: trabalho xxx**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="5dd54-383">Clique em **trabalhos** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-383">Click **Jobs** from hello left menu.</span></span> 

![Trabalhos de Azure Data Factory - Lote](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="5dd54-385">Uma tarefa é criada para cada execução de atividade da fatia.</span><span class="sxs-lookup"><span data-stu-id="5dd54-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="5dd54-386">Se houver cinco toobe pronto fatias processadas, cinco tarefas são criadas no trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dd54-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="5dd54-387">Se houver vários nós de computação no pool do lote de saudação, duas ou mais fatias podem ser executados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="5dd54-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="5dd54-388">Se o conjunto de nós de computação de máximo de tarefas por Olá muito > 1, você também pode ter mais de uma fatia em execução no hello computação mesmo.</span><span class="sxs-lookup"><span data-stu-id="5dd54-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Tarefas do trabalho de Azure Data Factory - Lote](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="5dd54-390">Olá diagrama a seguir ilustra o relacionamento de saudação entre tarefas do Azure Data Factory e lote.</span><span class="sxs-lookup"><span data-stu-id="5dd54-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory e lote](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="5dd54-392">Falhas na solução de problemas</span><span class="sxs-lookup"><span data-stu-id="5dd54-392">Troubleshoot failures</span></span>
<span data-ttu-id="5dd54-393">A solução de problemas consiste em algumas técnicas básicas:</span><span class="sxs-lookup"><span data-stu-id="5dd54-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="5dd54-394">Se você vir Olá erro a seguir, você pode estar usando um armazenamento de blob acesso/Cool em vez de usar um armazenamento de BLOBs do Azure para fins gerais.</span><span class="sxs-lookup"><span data-stu-id="5dd54-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="5dd54-395">Carregar Olá zip arquivo tooa **conta de armazenamento do Azure para fins gerais**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="5dd54-396">Se você vir Olá erro a seguir, confirme que nome de saudação de classe Olá Olá CS arquivo corresponde ao Olá nome especificado para Olá **EntryPoint** propriedades em JSON de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="5dd54-397">Passo a passo Olá, nome da classe de saudação é: MyDotNetActivity e Olá EntryPoint no hello JSON é: MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="5dd54-398">Se Olá correspondam, confirme se todos os binários de saudação estão em Olá **pasta raiz** do arquivo zip de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="5dd54-399">Ou seja, quando você abrir o arquivo zip de saudação, você deve ver todos os arquivos de saudação na pasta raiz de hello, mas não em quaisquer subpastas.</span><span class="sxs-lookup"><span data-stu-id="5dd54-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="5dd54-400">Se a fatia de entrada hello não está definida muito**pronto**, confirme se a estrutura de pasta de entrada hello está correta e **arquivo. txt** existe em pastas de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="5dd54-401">Em Olá **Execute** método de sua atividade personalizada, use Olá **IActivityLogger** informações toolog do objeto que ajuda você a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="5dd54-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="5dd54-402">mensagens de saudação conectada aparecem nos arquivos de log de usuário hello (um ou mais arquivos nomeados: usuário 0.log, 1.log de usuário, usuário 2.log, etc.).</span><span class="sxs-lookup"><span data-stu-id="5dd54-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="5dd54-403">Em Olá **OutputDataset** folha, clique em Olá fatia toosee Olá **FATIA de dados** folha para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="5dd54-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="5dd54-404">Você vê as **execuções de atividade** para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="5dd54-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="5dd54-405">Você deve ver uma atividade executar fatia hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="5dd54-406">Se você clicar em executar na barra de comandos hello, você pode iniciar outra atividade executada para Olá mesma fatia.</span><span class="sxs-lookup"><span data-stu-id="5dd54-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="5dd54-407">Quando você clica em execução da atividade hello, você vê Olá **detalhes de execução da atividade** folha com uma lista de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="5dd54-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="5dd54-408">Você ver as mensagens registradas no arquivo de user_0.log hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="5dd54-409">Quando ocorre um erro, você verá três execuções de atividade porque a contagem de repetição de saudação é definida too3 Olá pipeline/atividade JSON.</span><span class="sxs-lookup"><span data-stu-id="5dd54-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="5dd54-410">Quando você clica em execução da atividade Olá, você ver arquivos de log de saudação que você pode examinar o erro de saudação tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="5dd54-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="5dd54-411">Na lista de saudação de arquivos de log, clique em Olá **0.log usuário**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="5dd54-412">No painel direito da saudação são resultados de saudação do uso Olá **IActivityLogger.Write** método.</span><span class="sxs-lookup"><span data-stu-id="5dd54-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="5dd54-413">Se não ver todas as mensagens, verifique se você terá mais arquivos de log chamados: user_1.log, user_2.log, etc. Caso contrário, o código de saudação pode ter falhado depois Olá registrado última mensagem.</span><span class="sxs-lookup"><span data-stu-id="5dd54-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="5dd54-414">Verifique **system-0.log** para quaisquer mensagens de erro e exceções do sistema.</span><span class="sxs-lookup"><span data-stu-id="5dd54-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="5dd54-415">Incluir Olá **PDB** no arquivo zip de saudação do arquivo para que os detalhes do erro Olá contêm informações como **pilha de chamadas** quando ocorre um erro.</span><span class="sxs-lookup"><span data-stu-id="5dd54-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="5dd54-416">Todos Olá arquivos contidos no arquivo zip Olá para atividade de saudação personalizada deve estar no hello **nível superior** com nenhuma subpastas.</span><span class="sxs-lookup"><span data-stu-id="5dd54-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="5dd54-417">Certifique-se de que Olá **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip), e **packageLinkedService** (deve apontar toohello **geral**armazenamento de BLOBs do Azure que contém o arquivo zip de saudação) são definidos valores toocorrect.</span><span class="sxs-lookup"><span data-stu-id="5dd54-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="5dd54-418">Se você fixa uma fatia de saudação tooreprocess erro e quiser, clique com botão direito fatia Olá Olá **OutputDataset** folha e clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="5dd54-419">Se você vir Olá erro a seguir, você está usando o pacote do armazenamento do Azure Olá de versão > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="5dd54-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="5dd54-420">Iniciador do serviço de fábrica de dados requer a versão de hello 4.3 do windowsazure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="5dd54-421">Consulte [Appdomain isolamento](#appdomain-isolation) seção para uma solução alternativa se você precisar usar Olá versão posterior do assembly de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="5dd54-422">Se você pode usar a versão de hello 4.3.0 do pacote do armazenamento do Azure, remova Olá referência tooAzure armazenamento pacote existente de versão > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="5dd54-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="5dd54-423">Em seguida, execute Olá após o comando NuGet Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="5dd54-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="5dd54-424">Compile o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-424">Build hello project.</span></span> <span data-ttu-id="5dd54-425">Exclua Azure.Storage assembly de versão > 4.3.0 Olá bin\Debug pasta.</span><span class="sxs-lookup"><span data-stu-id="5dd54-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="5dd54-426">Crie um arquivo zip com binários e o arquivo PDB hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="5dd54-427">Substitua o arquivo zip da antiga Olá por no contêiner de blob da saudação (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="5dd54-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="5dd54-428">Olá execute fatias com falha (com o botão direito fatia e clique em Executar).</span><span class="sxs-lookup"><span data-stu-id="5dd54-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="5dd54-429">atividade personalizada Olá não usa Olá **App. config** arquivo do seu pacote.</span><span class="sxs-lookup"><span data-stu-id="5dd54-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="5dd54-430">Portanto, se seu código lê qualquer cadeia de caracteres de conexão do arquivo de configuração hello, ele não funciona em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5dd54-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="5dd54-431">Olá prática recomendada ao usar o lote do Azure é toohold qualquer segredos em um **Azure KeyVault**, use uma saudação tooprotect principal de serviço com base em certificado **keyvault**e distribuir certificados Olá tooAzure pool do lote.</span><span class="sxs-lookup"><span data-stu-id="5dd54-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="5dd54-432">Hello atividade personalizada do .NET pode acessar segredos de saudação KeyVault em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5dd54-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="5dd54-433">Essa solução é uma solução genérica e pode ser dimensionado tooany tipo de segredo, não apenas a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="5dd54-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="5dd54-434">Há uma solução mais fácil (mas não é uma prática recomendada): você pode criar um **serviço vinculado do SQL Azure** com configurações de cadeia de caracteres de conexão, criar um conjunto de dados que usa Olá serviço vinculado e cadeia Olá conjunto de dados como um conjunto de dados de entrada fictício toohello atividade personalizada de .NET.</span><span class="sxs-lookup"><span data-stu-id="5dd54-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="5dd54-435">Você pode então Olá acesso vinculado cadeia de caracteres de conexão do serviço no código do hello atividade personalizado.</span><span class="sxs-lookup"><span data-stu-id="5dd54-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="5dd54-436">Atualize a atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="5dd54-436">Update custom activity</span></span>
<span data-ttu-id="5dd54-437">Se você atualizar o código de hello atividade personalizado hello, compile-o e carregue o arquivo hello. zip que contém o novo armazenamento de blob toohello binários.</span><span class="sxs-lookup"><span data-stu-id="5dd54-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="5dd54-438">Isolamento de Appdomain</span><span class="sxs-lookup"><span data-stu-id="5dd54-438">Appdomain isolation</span></span>
<span data-ttu-id="5dd54-439">Consulte [entre AppDomain exemplo](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) que mostra como toocreate uma atividade personalizada que não é restrita versões tooassembly usadas pelo iniciador da fábrica de dados de saudação (exemplo: v 4.3.0 do windowsazure v6.0.x newtonsoft. JSON, etc.).</span><span class="sxs-lookup"><span data-stu-id="5dd54-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="5dd54-440">Acessar propriedades estendidas</span><span class="sxs-lookup"><span data-stu-id="5dd54-440">Access extended properties</span></span>
<span data-ttu-id="5dd54-441">Você pode declarar propriedades estendidas na atividade de saudação JSON conforme Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="5dd54-442">Exemplo hello, há duas propriedades estendidas: **SliceStart** e **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="5dd54-443">valor Olá SliceStart baseia-se a variável de sistema SliceStart hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="5dd54-444">Consulte [Variáveis de Sistema](data-factory-functions-variables.md) para obter uma lista das variáveis de sistema com suporte.</span><span class="sxs-lookup"><span data-stu-id="5dd54-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="5dd54-445">valor Olá DataFactoryName é tooCustomActivityFactory embutida.</span><span class="sxs-lookup"><span data-stu-id="5dd54-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="5dd54-446">tooaccess essas propriedades estendidas de em Olá **Execute** método, use código semelhante toohello, código a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="5dd54-447">Dimensionamento automático do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd54-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="5dd54-448">Você também pode criar um pool de Lotes do Azure com o recurso **autoscale** .</span><span class="sxs-lookup"><span data-stu-id="5dd54-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="5dd54-449">Por exemplo, você pode criar um pool de lote do azure com 0 VMs dedicadas e uma fórmula de dimensionamento automático com base no número de saudação de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="5dd54-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="5dd54-450">fórmula de exemplo Hello aqui alcança Olá comportamento a seguir: quando o pool de saudação inicialmente é criado, ele começa com 1 VM.</span><span class="sxs-lookup"><span data-stu-id="5dd54-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="5dd54-451">Métrica de $PendingTasks define o número de saudação de tarefas em execução + ativo (na fila) estado.</span><span class="sxs-lookup"><span data-stu-id="5dd54-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="5dd54-452">fórmula de saudação localiza Olá média de tarefas pendentes no hello Últimos 180 segundos e define TargetDedicated adequadamente.</span><span class="sxs-lookup"><span data-stu-id="5dd54-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="5dd54-453">Isso garante que TargetDedicated nunca ultrapasse 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="5dd54-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="5dd54-454">Assim, como novas tarefas forem enviadas, pool cresce automaticamente e como tarefas concluídas, as VMs se tornam livre uma e hello autoscaling reduz as VMs.</span><span class="sxs-lookup"><span data-stu-id="5dd54-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="5dd54-455">startingNumberOfVMs e maxNumberofVMs podem ser ajustadas tooyour necessidades.</span><span class="sxs-lookup"><span data-stu-id="5dd54-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="5dd54-456">Fórmula de dimensionamento automático:</span><span class="sxs-lookup"><span data-stu-id="5dd54-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="5dd54-457">Consulte [Dimensionar automaticamente os nós de computação em um pool de Lotes do Azure](../batch/batch-automatic-scaling.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5dd54-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="5dd54-458">Se estiver usando o pool de saudação padrão Olá [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Olá serviço de lote pode levar 15 a 30 minutos tooprepare Olá VM antes de executar a atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="5dd54-459">Se o pool de saudação está usando um autoScaleEvaluationInterval diferente, Olá serviço de lote pode levar autoScaleEvaluationInterval + 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="5dd54-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="5dd54-460">Use o serviço de computação do HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd54-460">Use HDInsight compute service</span></span>
<span data-ttu-id="5dd54-461">Olá explicação passo a passo, você usou a atividade personalizada do lote do Azure computação toorun Olá.</span><span class="sxs-lookup"><span data-stu-id="5dd54-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="5dd54-462">Você pode também usar seu próprio cluster HDInsight baseados em Windows ou fábrica de dados criar uma cluster baseado no Windows HDInsight sob demanda e ter atividade personalizada Olá executados no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="5dd54-463">Aqui estão as etapas de alto nível Olá para usar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5dd54-464">atividades personalizadas de .NET Olá executadas somente em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="5dd54-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5dd54-465">Uma alternativa para essa limitação é toouse Olá mapa reduzir atividade toorun Java código personalizado em um cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="5dd54-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5dd54-466">Outra opção é toouse um pool de lote do Azure de atividades personalizadas de toorun de VMs em vez de usar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="5dd54-467">Criar um serviço vinculado do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="5dd54-468">Serviço em vez de vinculado do HDInsight de uso **AzureBatchLinkedService** em Olá JSON de pipeline.</span><span class="sxs-lookup"><span data-stu-id="5dd54-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="5dd54-469">Se você quiser tootest com hello passo a passo, alteração **iniciar** e **final** horas para o pipeline de hello, de modo que você pode testar o cenário de saudação com hello serviço HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="5dd54-470">Criar o serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dd54-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="5dd54-471">Olá serviço fábrica de dados do Azure oferece suporte à criação de um cluster sob demanda e use-a como dados de saída tooprocess tooproduce de entrada.</span><span class="sxs-lookup"><span data-stu-id="5dd54-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="5dd54-472">Você também pode usar seu próprio cluster tooperform Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="5dd54-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="5dd54-473">Quando você usa o cluster HDInsight sob demanda, um cluster é criado para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="5dd54-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="5dd54-474">Por outro lado, se você usar seu próprio cluster HDInsight, cluster hello está pronto tooprocess Olá fatia imediatamente.</span><span class="sxs-lookup"><span data-stu-id="5dd54-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="5dd54-475">Portanto, quando você usa um cluster sob demanda, você não verá os dados de saída de hello mais rápido quando você usa seu próprio cluster.</span><span class="sxs-lookup"><span data-stu-id="5dd54-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5dd54-476">Em tempo de execução, uma instância de uma atividade de .NET é executado somente em um nó de trabalho no cluster do HDInsight Olá; ele não pode ser dimensionado toorun em vários nós.</span><span class="sxs-lookup"><span data-stu-id="5dd54-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="5dd54-477">Várias instâncias de atividade .NET podem ser executados em paralelo em diferentes nós de cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="5dd54-478">toouse um cluster do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="5dd54-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="5dd54-479">Em Olá **portal do Azure**, clique em **criar e implantar** na home page do hello fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="5dd54-480">No hello Editor da fábrica de dados, clique em **nova computação** do comando Olá barra e selecione **cluster HDInsight sob demanda** menu hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="5dd54-481">Verifique Olá alterações toohello JSON script a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="5dd54-482">Para Olá **clusterSize** propriedade, especificar o tamanho de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="5dd54-483">Para Olá **timeToLive** propriedade, especifique quanto tempo Prezado cliente pode ficar ocioso antes de ser excluído.</span><span class="sxs-lookup"><span data-stu-id="5dd54-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="5dd54-484">Para Olá **versão** propriedade, especificar a versão do HDInsight Olá deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="5dd54-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="5dd54-485">Se você excluir essa propriedade, a versão mais recente da saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="5dd54-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="5dd54-486">Para Olá **linkedServiceName**, especifique **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="5dd54-487">atividades personalizadas de .NET Olá executadas somente em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="5dd54-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5dd54-488">Uma alternativa para essa limitação é toouse Olá mapa reduzir atividade toorun Java código personalizado em um cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="5dd54-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5dd54-489">Outra opção é toouse um pool de lote do Azure de atividades personalizadas de toorun de VMs em vez de usar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="5dd54-490">Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="5dd54-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="5dd54-491">toouse seu próprio cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5dd54-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="5dd54-492">Em Olá **portal do Azure**, clique em **criar e implantar** na home page do hello fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd54-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="5dd54-493">Em Olá **Editor da fábrica de dados**, clique em **nova computação** do comando Olá barra e selecione **cluster HDInsight** menu hello.</span><span class="sxs-lookup"><span data-stu-id="5dd54-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="5dd54-494">Verifique Olá alterações toohello JSON script a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd54-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="5dd54-495">Para Olá **clusterUri** propriedade, digite a URL de saudação para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dd54-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="5dd54-496">Por exemplo: https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="5dd54-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="5dd54-497">Para Olá **UserName** propriedade, digite nome de usuário Olá quem tem acesso toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5dd54-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="5dd54-498">Para Olá **senha** propriedade, digite a senha de saudação do usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dd54-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="5dd54-499">Para Olá **LinkedServiceName** propriedade, digite **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5dd54-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="5dd54-500">Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="5dd54-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="5dd54-501">Consulte os [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5dd54-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="5dd54-502">Em Olá **JSON de pipeline**, use HDInsight (sob demanda ou seu próprio) serviço vinculado:</span><span class="sxs-lookup"><span data-stu-id="5dd54-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="5dd54-503">Criar uma atividade personalizada usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="5dd54-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="5dd54-504">Olá passo a passo neste artigo, você pode criar uma fábrica de dados com um pipeline que usa a atividade personalizada hello usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd54-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="5dd54-505">saudação de código a seguir mostra como toocreate Olá fábrica de dados usando o SDK do .NET em vez disso.</span><span class="sxs-lookup"><span data-stu-id="5dd54-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="5dd54-506">Você pode encontrar mais detalhes sobre como usar o SDK tooprogrammatically criar pipelines no hello [criar um pipeline com atividade de cópia usando API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5dd54-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="5dd54-507">Depurar atividade personalizada no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5dd54-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="5dd54-508">Olá [do Azure Data Factory - ambiente local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) exemplo no GitHub inclui uma ferramenta que permite a você toodebug atividades personalizadas de .NET dentro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5dd54-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="5dd54-509">Exemplo de atividades personalizadas no GitHub</span><span class="sxs-lookup"><span data-stu-id="5dd54-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="5dd54-510">Amostra</span><span class="sxs-lookup"><span data-stu-id="5dd54-510">Sample</span></span> | <span data-ttu-id="5dd54-511">Qual atividade personalizada realiza</span><span class="sxs-lookup"><span data-stu-id="5dd54-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="5dd54-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="5dd54-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="5dd54-513">Baixa os dados de um armazenamento de Blob usando c# atividade personalizada na fábrica de dados de tooAzure do ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="5dd54-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="5dd54-514">Exemplo de análise de opinião no Twitter</span><span class="sxs-lookup"><span data-stu-id="5dd54-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="5dd54-515">Invoca um modelo ML do Azure e faz análise de opinião, contagem de pontos, previsão, etc.</span><span class="sxs-lookup"><span data-stu-id="5dd54-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="5dd54-516">[Executar Script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="5dd54-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="5dd54-517">Invoca o script de R executando o RScript.exe no seu cluster do HDInsight que já tem o R instalado nele.</span><span class="sxs-lookup"><span data-stu-id="5dd54-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="5dd54-518">Atividade cruzada do .NET no AppDomain</span><span class="sxs-lookup"><span data-stu-id="5dd54-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="5dd54-519">Usa versões de assembly diferente daquelas usadas pelo iniciador da fábrica de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="5dd54-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="5dd54-520">Reprocessar um modelo no Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="5dd54-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="5dd54-521">Reprocessar um modelo no Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5dd54-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
