---
title: "conjuntos de dados em grande escala aaaProcess usando a fábrica de dados e lote | Microsoft Docs"
description: "Descreve como tooprocess enormes quantidades de dados em uma fábrica de dados do Azure pipeline usando o recurso de processamento paralelo de lote do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="cdd49-103">Processar conjuntos de dados em larga escala usando o Data Factory e o Lote</span><span class="sxs-lookup"><span data-stu-id="cdd49-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="cdd49-104">Este artigo descreve uma arquitetura de um exemplo de solução que move e processa os conjuntos de dados em larga escala de maneira automática e agendada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="cdd49-105">Ele também fornece uma solução de saudação tooimplement passo a passo de ponta a ponta usando o Azure Data Factory e lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="cdd49-106">Este artigo é maior que nossos artigos comuns porque contém um passo a passo de um exemplo de solução inteira.</span><span class="sxs-lookup"><span data-stu-id="cdd49-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="cdd49-107">Se você for novo tooBatch e fábrica de dados, você pode aprender sobre esses serviços e como eles funcionam juntos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="cdd49-108">Se você souber algo sobre serviços hello e está criando/arquitetura de uma solução, você pode se concentrar apenas em Olá [seção arquitetura](#architecture-of-sample-solution) do artigo hello e se você estiver desenvolvendo um protótipo ou uma solução, você também pode desejar tootry out instruções passo a passo em Olá [passo a passo](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="cdd49-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="cdd49-109">Seus comentários sobre esse conteúdo e como usá-lo são bem-vindos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="cdd49-110">Primeiro, vamos examinar como serviços de fábrica de dados e lote podem ajudar com o processamento de grandes conjuntos de dados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="cdd49-111">Por que usar o Lote do Azure?</span><span class="sxs-lookup"><span data-stu-id="cdd49-111">Why Azure Batch?</span></span>
<span data-ttu-id="cdd49-112">Lote do Azure permite que você toorun em larga escala paralelas e alto desempenho HPC (computação) aplicativos com eficiência na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="cdd49-113">É um serviço de plataforma que agenda o trabalho de computação intensa toorun em uma coleção gerenciada de máquinas virtuais, e pode automaticamente escala de computação necessidades de saudação toomeet recursos de seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="cdd49-114">Com hello serviço de lote, você define tooexecute de recursos de computação do Azure seus aplicativos em paralelo e em escala.</span><span class="sxs-lookup"><span data-stu-id="cdd49-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="cdd49-115">Você pode executar sob demanda ou agendadas trabalhos e você não precisa toomanually criar, configurar e gerenciar um cluster de HPC, máquinas virtuais, redes virtuais ou um trabalho complexo e infraestrutura de agendamento de tarefas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="cdd49-116">Consulte Olá artigos a seguir se você não estiver familiarizado com o lote do Azure como ele ajuda com noções básicas sobre arquitetura de saudação/implementação de solução de saudação descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="cdd49-117">Noções básicas de Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="cdd49-118">Visão geral do recurso de Lote</span><span class="sxs-lookup"><span data-stu-id="cdd49-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="cdd49-119">(opcional) toolearn mais sobre o lote do Azure, consulte Olá [de aprendizado de lote do Azure](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="cdd49-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="cdd49-120">Por que usar o Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="cdd49-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="cdd49-121">Fábrica de dados é um serviço de integração de dados com base em nuvem que orquestra e automatiza a movimentação de saudação e transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="cdd49-122">Usando o serviço da fábrica de dados hello, você pode criar pipelines de dados gerenciados que movem dados de local e na nuvem de armazenamento de dados centralizado de tooa de repositórios de dados (por exemplo: armazenamento de BLOBs do Azure) e o processo/transformar dados usando serviços como o HDInsight do Azure e o Azure Aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="cdd49-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="cdd49-123">Você também pode agendar toorun de pipelines de dados em uma maneira agendada (por hora, diariamente, semanalmente, etc.) e o monitor e gerenciá-los em problemas de tooidentify uma visão e tomar medidas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="cdd49-124">Consulte Olá artigos a seguir se você não estiver familiarizado com o Azure Data Factory porque isso ajuda com noções básicas sobre arquitetura de saudação/implementação de solução de saudação descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="cdd49-125">Introdução ao Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cdd49-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="cdd49-126">Criar seu primeiro pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="cdd49-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="cdd49-127">(opcional) toolearn mais sobre o Azure Data Factory, consulte Olá [de aprendizado para o Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="cdd49-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="cdd49-128">Data Factory e Lote juntos</span><span class="sxs-lookup"><span data-stu-id="cdd49-128">Data Factory and Batch together</span></span>
<span data-ttu-id="cdd49-129">Fábrica de dados inclui atividades internas, como dados de toocopy/movimentação de atividade de cópia de uma fonte de dados de armazenamento tooa repositório de dados de destino e dados de tooprocess de atividade de Hive usando clusters de Hadoop (HDInsight) no Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="cdd49-130">Confira [Atividades de transformação de dados](data-factory-data-transformation-activities.md) para obter uma lista de atividades de transformação permitidas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="cdd49-131">Ele também permite que você toocreate .NET atividades personalizadas toomove ou processam dados com sua própria lógica e executar essas atividades em um cluster Azure HDInsight ou em um pool do Azure Batch de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="cdd49-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="cdd49-132">Quando você usa o lote do Azure, você pode configurar a escala Olá pool tooauto (Adicionar ou remover VMs com base na carga de trabalho Olá) com base em uma fórmula que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="cdd49-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="cdd49-133">Arquitetura do exemplo de solução</span><span class="sxs-lookup"><span data-stu-id="cdd49-133">Architecture of sample solution</span></span>
<span data-ttu-id="cdd49-134">Embora a arquitetura de saudação descrita neste artigo é para uma solução simples, é cenários toocomplex relevantes, como risco de modelagem, serviços financeiros, processamento de imagem e processamento e análise genoma.</span><span class="sxs-lookup"><span data-stu-id="cdd49-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="cdd49-135">diagrama de saudação ilustra 1) como o Data Factory orquestra a movimentação de dados e processamento e 2) como processa o lote do Azure Olá dados de forma paralela.</span><span class="sxs-lookup"><span data-stu-id="cdd49-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="cdd49-136">Download e diagrama de impressão Olá para facilitar a referência (11 x 17 no.</span><span class="sxs-lookup"><span data-stu-id="cdd49-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="cdd49-137">ou tamanho A3): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686) (HPC e orquestração de dados usando o Azure Batch e o Data Factory).</span><span class="sxs-lookup"><span data-stu-id="cdd49-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="cdd49-138">[![Diagrama de processamento de dados em larga escala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="cdd49-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="cdd49-139">Olá lista a seguir fornece etapas básicas de saudação do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="cdd49-140">solução de saudação inclui código e explicações sobre solução de ponta a ponta de saudação toobuild.</span><span class="sxs-lookup"><span data-stu-id="cdd49-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="cdd49-141">**Configure o Lote do Azure com um pool de nós de computação (VMs)**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="cdd49-142">Você pode especificar o número de saudação de nós e o tamanho de cada nó.</span><span class="sxs-lookup"><span data-stu-id="cdd49-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="cdd49-143">**Crie uma instância do Azure Data Factory** que está configurada com entidades que representam o armazenamento de blobs do Azure, serviço de computação do Lote do Azure, dados de entrada/saída e um fluxo de trabalho/pipeline com atividades que movem e transformam dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="cdd49-144">**Criar uma atividade personalizada do .NET no pipeline da fábrica de dados Olá**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="cdd49-145">atividade de saudação é o código do usuário que é executado em Olá pool do lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="cdd49-146">**Armazene grandes quantidades de dados de entrada como blobs no armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="cdd49-147">Os dados são divididos em fatias lógicas (geralmente, por hora).</span><span class="sxs-lookup"><span data-stu-id="cdd49-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="cdd49-148">**Fábrica de dados copia os dados que são processados em paralelo** local secundário toohello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="cdd49-149">**Fábrica de dados é executado usando Olá pool alocada por lote de atividade personalizada do hello**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="cdd49-150">O Data Factory pode executar atividades simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="cdd49-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="cdd49-151">Cada atividade processa uma fatia de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="cdd49-152">Olá resultados são armazenados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="cdd49-153">**Fábrica de dados move terceiro local do hello resultados finais tooa**, para distribuição por meio de um aplicativo ou para processamento adicional por outras ferramentas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="cdd49-154">Implementação da solução de exemplo</span><span class="sxs-lookup"><span data-stu-id="cdd49-154">Implementation of sample solution</span></span>
<span data-ttu-id="cdd49-155">solução de exemplo Hello é intencionalmente simple e é tooshow você como toouse conjuntos de dados de tooprocess juntos de fábrica de dados e lote.</span><span class="sxs-lookup"><span data-stu-id="cdd49-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="cdd49-156">solução de saudação simplesmente conta o número de saudação de ocorrências de um termo de pesquisa ("Microsoft") nos arquivos de entrada, organizados em uma série de tempo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="cdd49-157">Ele produz arquivos de toooutput de contagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="cdd49-158">**Tempo**: se você estiver familiarizado com conceitos básicos do Azure, a fábrica de dados e o lote e tem pré-requisitos concluída Olá listados abaixo, estimamos que esta solução usa toocomplete de 1 a 2 horas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cdd49-159">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cdd49-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="cdd49-160">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-160">Azure subscription</span></span>
<span data-ttu-id="cdd49-161">Se você não tiver uma assinatura do Azure, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cdd49-162">Veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdd49-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="cdd49-163">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-163">Azure storage account</span></span>
<span data-ttu-id="cdd49-164">Você pode usar uma conta de armazenamento do Azure para armazenar dados de saudação neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="cdd49-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="cdd49-165">Se você não tiver uma conta de armazenamento do Azure, consulte o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cdd49-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="cdd49-166">solução de exemplo Hello usa o armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="cdd49-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="cdd49-167">Conta do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-167">Azure Batch account</span></span>
<span data-ttu-id="cdd49-168">Criar uma conta de lote do Azure usando Olá [portal do Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="cdd49-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="cdd49-169">Consulte [Criar e gerenciar uma conta do Lote do Azure](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cdd49-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="cdd49-170">Anote a chave de nome e uma conta de conta de lote do Azure do hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="cdd49-171">Você também pode usar [AzureRmBatchAccount novo](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate uma conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="cdd49-172">Consulte [Introdução aos cmdlets do PowerShell do Lote do Azure](../batch/batch-powershell-cmdlets-get-started.md) para obter instruções detalhadas sobre como usar esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cdd49-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="cdd49-173">solução de exemplo Hello usa dados de tooprocess de lote do Azure (indiretamente por meio de um pipeline da fábrica de dados do Azure) de forma paralela em um pool de nós de computação (uma coleção de máquinas virtuais gerenciada).</span><span class="sxs-lookup"><span data-stu-id="cdd49-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="cdd49-174">Pool de VMs (máquinas virtuais) do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="cdd49-175">Crie um **pool de Lote do Azure** com pelo menos dois nós de computação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="cdd49-176">Em Olá [portal do Azure](https://portal.azure.com), clique em **procurar** no hello menus à esquerda e clique em **contas em lotes**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="cdd49-177">Selecione sua saudação do lote do Azure conta tooopen **conta em lotes** folha.</span><span class="sxs-lookup"><span data-stu-id="cdd49-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="cdd49-178">Clique no bloco **Pools** .</span><span class="sxs-lookup"><span data-stu-id="cdd49-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="cdd49-179">Em Olá **Pools** folha, clique no botão Adicionar na saudação da barra de ferramentas tooadd um pool.</span><span class="sxs-lookup"><span data-stu-id="cdd49-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="cdd49-180">Insira uma ID para o pool de saudação (**ID do Pool**).</span><span class="sxs-lookup"><span data-stu-id="cdd49-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="cdd49-181">Saudação de Observação **ID do pool de saudação**; é necessário ao criar a solução de fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="cdd49-182">Especifique **Windows Server 2012 R2** para configuração da família de sistemas operacionais de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="cdd49-183">Selecione um **camada de preços de nó**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="cdd49-184">Digite **2** como valor para Olá **destino dedicado** configuração.</span><span class="sxs-lookup"><span data-stu-id="cdd49-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="cdd49-185">Digite **2** como valor para Olá **tarefas máxima por nó** configuração.</span><span class="sxs-lookup"><span data-stu-id="cdd49-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="cdd49-186">Clique em **Okey** toocreate pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="cdd49-187">Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-187">Azure Storage Explorer</span></span>
<span data-ttu-id="cdd49-188">[Azure Storage Explorer 6 (ferramenta)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (da ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="cdd49-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="cdd49-189">Você pode usar essas ferramentas para inspecionar e alterar dados de saudação em seus projetos de armazenamento do Azure, incluindo os logs de saudação de seus aplicativos hospedados em nuvem.</span><span class="sxs-lookup"><span data-stu-id="cdd49-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="cdd49-190">Crie um contêiner chamado **mycontainer** com acesso privado (sem acesso anônimo)</span><span class="sxs-lookup"><span data-stu-id="cdd49-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="cdd49-191">Se você estiver usando **CloudXplorer**, criar pastas e subpastas com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="cdd49-192">`Inputfolder` e `outputfolder` são pastas de nível superior no `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="cdd49-193">Olá `inputfolder` tem subpastas com carimbos de data e hora (AAAA-MM-DD-HH).</span><span class="sxs-lookup"><span data-stu-id="cdd49-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="cdd49-194">Se você estiver usando **Azure Storage Explorer**, na próxima etapa de saudação, você precisa de arquivos tooupload com nomes: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="cdd49-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="cdd49-195">Esta etapa cria automaticamente as pastas de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="cdd49-196">Criar um arquivo de texto **arquivo.txt** em seu computador com o conteúdo com a palavra-chave de saudação **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="cdd49-197">Por exemplo: "testar a atividade personalizada Microsoft testar atividade personalizada Microsoft".</span><span class="sxs-lookup"><span data-stu-id="cdd49-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="cdd49-198">Carregar Olá arquivo toohello pastas entradas no armazenamento de BLOBs do Azure, a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdd49-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="cdd49-199">Se você estiver usando **Azure Storage Explorer**, carregue o arquivo hello **arquivo.txt** muito**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="cdd49-200">Clique em **cópia** em Olá barra de ferramentas toocreate uma cópia de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="cdd49-201">Em Olá **cópia Blob** caixa de diálogo, alteração Olá **nome de blob de destino** muito`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="cdd49-202">Repita essa etapa toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="cdd49-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="cdd49-203">Essa ação cria automaticamente as pastas de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="cdd49-204">Crie outro contêiner chamado `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="cdd49-205">Carregar o contêiner do toothis de arquivos zip hello atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="cdd49-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdd49-206">Visual Studio</span></span>
<span data-ttu-id="cdd49-207">Instale o Microsoft Visual Studio 2012 ou posterior toocreate Olá personalizado lote atividade toobe usado em Olá solução da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="cdd49-208">Solução de saudação toocreate etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="cdd49-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="cdd49-209">Crie uma atividade personalizada que contém a lógica de processamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="cdd49-210">Crie uma fábrica de dados do Azure que usa a atividade personalizada hello:</span><span class="sxs-lookup"><span data-stu-id="cdd49-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="cdd49-211">Criar atividade personalizada Olá</span><span class="sxs-lookup"><span data-stu-id="cdd49-211">Create hello custom activity</span></span>
<span data-ttu-id="cdd49-212">Hello atividade personalizada de fábrica de dados é o núcleo de saudação desta solução de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="cdd49-213">solução de exemplo Hello usa uma atividade personalizada do lote do Azure toorun hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="cdd49-214">Consulte [usar atividades personalizadas em um pipeline da fábrica de dados do Azure](data-factory-use-custom-activities.md) para atividades personalizadas do toodevelop Olá informações básicas e use-os no Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="cdd49-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="cdd49-215">toocreate uma atividade personalizada do .NET que podem ser usados em um pipeline da fábrica de dados do Azure, você precisa toocreate um **biblioteca de classes .NET** projeto com uma classe que implementa que **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="cdd49-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="cdd49-216">Essa interface tem apenas um método: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="cdd49-217">Aqui está a assinatura de saudação do método hello:</span><span class="sxs-lookup"><span data-stu-id="cdd49-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="cdd49-218">método Hello tem alguns componentes principais que você precisa toounderstand.</span><span class="sxs-lookup"><span data-stu-id="cdd49-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="cdd49-219">método Hello usa quatro parâmetros:</span><span class="sxs-lookup"><span data-stu-id="cdd49-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="cdd49-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-220">**linkedServices**.</span></span> <span data-ttu-id="cdd49-221">Uma lista enumerável de serviços vinculados que vinculam fontes de dados de entrada/saída (por exemplo: armazenamento de BLOBs do Azure) toohello fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="cdd49-222">Neste exemplo, há apenas um serviço vinculado do tipo armazenamento do Azure usado para entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="cdd49-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="cdd49-223">**conjuntos de dados**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-223">**datasets**.</span></span> <span data-ttu-id="cdd49-224">É uma lista enumerável de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="cdd49-225">Você pode usar este locais de saudação do parâmetro tooget e esquemas definidos pelos conjuntos de dados de entrada e saídos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="cdd49-226">**atividade**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-226">**activity**.</span></span> <span data-ttu-id="cdd49-227">Esse parâmetro representa Olá computação entidade atual - nesse caso, um serviço de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="cdd49-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-228">**logger**.</span></span> <span data-ttu-id="cdd49-229">permite a agente Olá para que escrever comentários de depuração essa superfície como hello "Usuário" fazer logon Olá pipeline.</span><span class="sxs-lookup"><span data-stu-id="cdd49-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="cdd49-230">método Hello retorna um dicionário que pode ser atividades personalizadas toochain usados juntos em um futuro hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="cdd49-231">Este recurso ainda não foi implementado, isso retornará um dicionário vazio do método hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="cdd49-232">Procedimento: Criar atividade personalizada Olá</span><span class="sxs-lookup"><span data-stu-id="cdd49-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="cdd49-233">Crie um projeto de Biblioteca de Classes .NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdd49-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="cdd49-234">Inicie o **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="cdd49-235">Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="cdd49-236">Expanda **Modelos** e selecione **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="cdd49-237">Neste passo a passo, você pode usar C\#, mas você pode usar qualquer atividade personalizada do .NET idioma toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="cdd49-238">Selecione **biblioteca de classes** da lista de saudação de tipos de projeto em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="cdd49-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="cdd49-239">Digite **MyDotNetActivity** para Olá **nome**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="cdd49-240">Selecione **c:\\ADF** para Olá **local**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="cdd49-241">Criar pasta Olá **ADF** se ele não existe.</span><span class="sxs-lookup"><span data-stu-id="cdd49-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="cdd49-242">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="cdd49-243">Clique em **ferramentas**, ponto muito**NuGet Package Manager**e clique em **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="cdd49-244">Em Olá **Package Manager Console**, execute Olá após o comando tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="cdd49-245">Saudação de importação **armazenamento do Azure** pacote do NuGet no projeto toohello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="cdd49-246">Você precisa deste pacote porque você usar a API de armazenamento de Blob Olá neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="cdd49-247">Adicione o seguinte Olá **usando** diretivas toohello fonte arquivo hello projeto.</span><span class="sxs-lookup"><span data-stu-id="cdd49-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="cdd49-248">Alterar o nome de saudação do hello **namespace** muito**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="cdd49-249">Alterar o nome de saudação da classe Olá muito**MyDotNetActivity** e ele derivam Olá **IDotNetActivity** interface conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="cdd49-250">Saudação de implementar (Adicionar) **Execute** método hello **IDotNetActivity** interface toohello **MyDotNetActivity** Olá cópia e de classe, método de toohello de código de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdd49-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="cdd49-251">Consulte Olá [executar método](#execute-method) seção para obter explicação para lógica de saudação usada nesse método.</span><span class="sxs-lookup"><span data-stu-id="cdd49-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. <span data-ttu-id="cdd49-252">Adicione Olá classe do auxiliar métodos toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdd49-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="cdd49-253">Esses métodos são chamados pelo Olá **Execute** método.</span><span class="sxs-lookup"><span data-stu-id="cdd49-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="cdd49-254">Mais importante, Olá **Calculate** método isola código Olá que itera por meio de cada blob.</span><span class="sxs-lookup"><span data-stu-id="cdd49-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    <span data-ttu-id="cdd49-255">Olá **GetFolderPath** método retorna a pasta de toohello de caminho de saudação que Olá dataset pontos tooand Olá **GetFileName** método retorna o nome de Olá Olá/do arquivo de blob que Olá pontos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="cdd49-256">Olá **Calculate** método calcula o número de saudação de instâncias da palavra-chave **Microsoft** nos arquivos de entrada hello (blobs na pasta Olá).</span><span class="sxs-lookup"><span data-stu-id="cdd49-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="cdd49-257">termo de pesquisa da saudação ("Microsoft") é embutido em código hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="cdd49-258">Compile o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-258">Compile hello project.</span></span> <span data-ttu-id="cdd49-259">Clique em **criar** de saudação menu e clique em **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="cdd49-260">Iniciar **Windows Explorer**e navegue muito**bin\\depurar** ou **bin\\versão** pasta dependendo do tipo de saudação da compilação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="cdd49-261">Criar um arquivo zip **MyDotNetActivity.zip** que contém todos os binários de saudação em Olá  **\\bin\\depurar** pasta.</span><span class="sxs-lookup"><span data-stu-id="cdd49-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="cdd49-262">Talvez você queira Olá tooinclude MyDotNetActivity. **pdb** arquivos de forma que você obter detalhes adicionais, como o número da linha no código-fonte Olá que causou o problema de saudação quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="cdd49-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="cdd49-263">Carregar **MyDotNetActivity.zip** como um contêiner de blob do blob toohello: `customactivitycontainer` em hello Azure armazenamento de blob que Olá **StorageLinkedService** serviço em Olá vinculado  **ADFTutorialDataFactory** usa.</span><span class="sxs-lookup"><span data-stu-id="cdd49-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="cdd49-264">Criar contêiner de blob Olá `customactivitycontainer` se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="cdd49-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="cdd49-265">Método Execute</span><span class="sxs-lookup"><span data-stu-id="cdd49-265">Execute method</span></span>
<span data-ttu-id="cdd49-266">Esta seção fornece mais detalhes e observações sobre o código Olá Olá método Execute.</span><span class="sxs-lookup"><span data-stu-id="cdd49-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="cdd49-267">membros de saudação para iteração pela coleção de entrada hello são encontrados em Olá [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span><span class="sxs-lookup"><span data-stu-id="cdd49-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="cdd49-268">Iteração pela coleção de blob Olá requer o uso de saudação **BlobContinuationToken** classe.</span><span class="sxs-lookup"><span data-stu-id="cdd49-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="cdd49-269">Em essência, você deve usar um, faça-durante o loop com token hello como mecanismo de saudação para sair do loop de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="cdd49-270">Para obter mais informações, consulte [como toouse armazenamento de BLOBs no .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="cdd49-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="cdd49-271">Um loop básico é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="cdd49-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="cdd49-272">Consulte a documentação para Olá Olá [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) método para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cdd49-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="cdd49-273">Olá código para trabalhar com o conjunto de saudação de blobs logicamente fica dentro de saudação fazer-loop while.</span><span class="sxs-lookup"><span data-stu-id="cdd49-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="cdd49-274">Em Olá **Execute** método, proceda de saudação-enquanto o loop passa a lista de saudação de blobs método tooa chamado **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="cdd49-275">método Hello retorna uma variável de cadeia de caracteres denominada **saída** que é resultado de saudação de ter iteração de todos os blobs Olá no segmento de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="cdd49-276">Retorna Olá número de ocorrências do termo de pesquisa da saudação (**Microsoft**) no blob Olá passada toohello **Calculate** método.</span><span class="sxs-lookup"><span data-stu-id="cdd49-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="cdd49-277">Uma vez Olá **Calculate** método trabalhou hello, ele deve ser escrito tooa novo blob.</span><span class="sxs-lookup"><span data-stu-id="cdd49-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="cdd49-278">Portanto, para cada conjunto de blobs processados, um novo blob pode ser gravado com resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="cdd49-279">toowrite tooa novo blob, o primeiro conjunto de saída de saudação de localizar.</span><span class="sxs-lookup"><span data-stu-id="cdd49-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="cdd49-280">código de saudação também chama um método auxiliar: **GetFolderPath** caminho da pasta tooretrieve hello (nome do contêiner de armazenamento Olá).</span><span class="sxs-lookup"><span data-stu-id="cdd49-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="cdd49-281">Olá **GetFolderPath** conversões Olá tooan de objeto do conjunto de dados AzureBlobDataSet, que tem uma propriedade denominada FolderPath.</span><span class="sxs-lookup"><span data-stu-id="cdd49-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="cdd49-282">saudação de chamadas de código Olá **GetFileName** método tooretrieve Olá arquivo nome (blob).</span><span class="sxs-lookup"><span data-stu-id="cdd49-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="cdd49-283">código de saudação é semelhante toohello acima caminho da pasta código tooget hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="cdd49-284">nome de saudação do arquivo hello é escrito, criando um objeto URI.</span><span class="sxs-lookup"><span data-stu-id="cdd49-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="cdd49-285">construtor URI Olá usa Olá **BlobEndpoint** nome da propriedade tooreturn Olá contêiner.</span><span class="sxs-lookup"><span data-stu-id="cdd49-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="cdd49-286">nome de arquivo e caminho da pasta de saudação são adicionados tooconstruct o URI do blob de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="cdd49-287">nome de saudação do arquivo hello foi gravado e agora você pode criar a cadeia de caracteres de saída de saudação do hello **Calculate** novo blob tooa do método:</span><span class="sxs-lookup"><span data-stu-id="cdd49-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="cdd49-288">Criar hello fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="cdd49-288">Create hello data factory</span></span>
<span data-ttu-id="cdd49-289">Em Olá [Criar atividade personalizada Olá](#create-the-custom-activity) seção, você criou uma atividade personalizada e arquivo zip de saudação carregado com binários e hello PDB arquivo tooan contêiner de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="cdd49-290">Nesta seção, você cria um Azure **fábrica de dados** com um **pipeline** que usa Olá **atividade personalizada**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="cdd49-291">Olá conjunto de dados de entrada para atividade personalizada Olá representa blobs hello (arquivos) na pasta de entrada hello (`mycontainer\\inputfolder`) no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="cdd49-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="cdd49-292">conjunto de dados de saída Hello atividade Olá representa Olá blobs de saída na pasta de saída de hello (`mycontainer\\outputfolder`) no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="cdd49-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="cdd49-293">Remova um ou mais arquivos em pastas de entrada hello:</span><span class="sxs-lookup"><span data-stu-id="cdd49-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="cdd49-294">Por exemplo, remova um arquivo (arquivo. txt) com hello após o conteúdo em cada uma das pastas de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="cdd49-295">Cada pasta de entrada corresponde tooa fatia na fábrica de dados do Azure, mesmo se a pasta de saudação tem 2 ou mais arquivos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="cdd49-296">Quando cada fatia é processada pelo pipeline hello, atividade personalizada Olá itera em todos os blobs de saudação na pasta de entrada hello essa fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="cdd49-297">Você verá cinco arquivos de saída com hello mesmo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-297">You see five output files with hello same content.</span></span> <span data-ttu-id="cdd49-298">Por exemplo, o arquivo de saída de saudação do processamento de arquivo hello na pasta Olá 2015-11-16-00 tem Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="cdd49-299">Se você remover vários arquivos (arquivo. txt, file2.txt, file3.txt) com hello mesmo conteúdo pasta entrada toohello, consulte Olá conteúdo no arquivo de saída de hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdd49-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="cdd49-300">Cada pasta (2015-11-16-00, etc.) corresponde a fatia tooa neste exemplo, embora pasta Olá tem vários arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="cdd49-301">arquivo de saída Olá tem três linhas agora, uma para cada arquivo de entrada (blob) na pasta Olá associado a fatia de saudação (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="cdd49-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="cdd49-302">Uma tarefa é criada para cada execução de atividade.</span><span class="sxs-lookup"><span data-stu-id="cdd49-302">A task is created for each activity run.</span></span> <span data-ttu-id="cdd49-303">Neste exemplo, há apenas uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="cdd49-304">Quando uma fatia é processada pelo pipeline Olá, atividade personalizada Olá é executado na fatia da saudação tooprocess lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="cdd49-305">Uma vez que há cinco intervalos (cada fatia pode ter vários blobs ou arquivos), há cinco tarefas criadas no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cdd49-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="cdd49-306">Quando uma tarefa é executada em lote, é realmente hello atividade personalizada que está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="cdd49-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="cdd49-307">Olá, seguindo as instruções passo a passo fornece detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="cdd49-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="cdd49-308">Etapa 1: Criar a fábrica de dados Olá</span><span class="sxs-lookup"><span data-stu-id="cdd49-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="cdd49-309">Depois de fazer logon em toohello [portal do Azure](https://portal.azure.com/), Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cdd49-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="cdd49-310">Clique em **novo** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="cdd49-311">Clique em **dados + análise** em Olá **novo** folha.</span><span class="sxs-lookup"><span data-stu-id="cdd49-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="cdd49-312">Clique em **Data Factory** em Olá **análises de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="cdd49-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="cdd49-313">Em Olá **nova fábrica de dados** folha, digite **CustomActivityFactory** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="cdd49-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="cdd49-314">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="cdd49-315">Se você receber o erro Olá: **"CustomActivityFactory" nome da fábrica de dados não está disponível**, alterar nome Olá Olá da fábrica de dados (por exemplo, **yournameCustomActivityFactory**) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="cdd49-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="cdd49-316">Clique em **NOME DO GRUPO DE RECURSOS**para selecionar um grupo de recursos existente ou criar um.</span><span class="sxs-lookup"><span data-stu-id="cdd49-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="cdd49-317">Verifique se que você está usando a assinatura correta hello e região onde você deseja Olá toobe de fábrica de dados criado.</span><span class="sxs-lookup"><span data-stu-id="cdd49-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="cdd49-318">Clique em **criar** em Olá **nova fábrica de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="cdd49-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="cdd49-319">Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="cdd49-320">Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="cdd49-321">Etapa 2: Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="cdd49-321">Step 2: Create linked services</span></span>
<span data-ttu-id="cdd49-322">Serviços vinculados vincular armazenamentos de dados ou de computação serviços tooan data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="cdd49-323">Nesta etapa, você vincular seu **armazenamento do Azure** conta e **do Azure Batch** fábrica de dados de tooyour de conta.</span><span class="sxs-lookup"><span data-stu-id="cdd49-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="cdd49-324">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="cdd49-325">Clique em Olá **autor e implantar** bloco Olá **DATA FACTORY** folha para **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="cdd49-326">Você verá Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="cdd49-327">Clique em **novo repositório de dados** Olá barra de comandos e escolha **armazenamento do Azure.**</span><span class="sxs-lookup"><span data-stu-id="cdd49-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="cdd49-328">Você deve ver Olá script JSON para a criação de um armazenamento do Azure vinculada serviço no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="cdd49-329">Substituir **nome da conta** com nome de saudação da sua conta de armazenamento do Azure e **chave de conta** com a chave de acesso de saudação do Olá conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="cdd49-330">toolearn como tooget seu armazenamento acessar chave, consulte [exibir, copiar e regenerar as contas de armazenamento de chaves de acesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cdd49-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="cdd49-331">Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="cdd49-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="cdd49-332">Crie o serviço vinculado do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="cdd49-333">Nesta etapa, você cria um serviço vinculado para o **do Azure Batch** conta que seja usada toorun Olá fábrica de dados personalizado de atividades.</span><span class="sxs-lookup"><span data-stu-id="cdd49-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="cdd49-334">Clique em **nova computação** Olá barra de comandos e escolha **lote do Azure.**</span><span class="sxs-lookup"><span data-stu-id="cdd49-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="cdd49-335">Você deve ver Olá script JSON para a criação de um lote do Azure vinculado de serviço no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="cdd49-336">No script JSON da saudação:</span><span class="sxs-lookup"><span data-stu-id="cdd49-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="cdd49-337">Substituir **nome da conta** com nome de saudação da sua conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="cdd49-338">Substituir **chave de acesso** com chave de acesso de saudação do hello conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="cdd49-339">Insira a ID de saudação do pool de saudação para hello **poolName** propriedade**.**</span><span class="sxs-lookup"><span data-stu-id="cdd49-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="cdd49-340">Para essa propriedade, você pode especificar o nome do pool ou o ID do pool.</span><span class="sxs-lookup"><span data-stu-id="cdd49-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="cdd49-341">Insira o URI de lote de saudação para Olá **batchUri** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="cdd49-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="cdd49-342">Olá **URL** de saudação **folha de conta de lote do Azure** está em Olá formato a seguir: \<accountname\>.\< região\>. batch.azure.com. Para Olá **batchUri** propriedade no hello JSON, é necessário muito**remover "accountname".**</span><span class="sxs-lookup"><span data-stu-id="cdd49-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="cdd49-343">de URL hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-343">from hello URL.</span></span> <span data-ttu-id="cdd49-344">Exemplo: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="cdd49-345">Para Olá **poolName** propriedade, você também pode especificar a ID de saudação do pool de saudação em vez do nome de saudação do pool de saudação de.</span><span class="sxs-lookup"><span data-stu-id="cdd49-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="cdd49-346">Olá serviço da fábrica de dados não dá suporte uma opção sob demanda para o lote do Azure como faz para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cdd49-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="cdd49-347">Você só pode usar seu próprio pool do Azure Batch em um Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cdd49-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="cdd49-348">Especifique **StorageLinkedService** para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="cdd49-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="cdd49-349">Você criou esse serviço vinculado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="cdd49-350">Esse armazenamento é usado como uma área de preparação para arquivos e logs.</span><span class="sxs-lookup"><span data-stu-id="cdd49-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="cdd49-351">Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="cdd49-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="cdd49-352">Etapa 3: Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="cdd49-352">Step 3: Create datasets</span></span>
<span data-ttu-id="cdd49-353">Nesta etapa, você cria conjuntos de dados toorepresent entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="cdd49-354">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="cdd49-354">Create input dataset</span></span>
1. <span data-ttu-id="cdd49-355">Em Olá **Editor** para Olá fábrica de dados, clique em **novo conjunto de dados** botão na barra de ferramentas hello e clique em **armazenamento de BLOBs do Azure** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="cdd49-356">Substitua Olá JSON no painel direito Olá Olá trecho JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    <span data-ttu-id="cdd49-357">Você cria um pipeline posteriormente neste passo a passo com hora de início: 2015-11-16T00:00:00Z e final: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="cdd49-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="cdd49-358">São dados agendados tooproduce **por hora**, portanto, há 5 intervalos de entrada/saída (entre **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="cdd49-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="cdd49-359">Olá **frequência** e **intervalo** para o conjunto de dados de entrada hello está definido muito**hora** e **1**, que significa que Olá entrada fatia está disponível por hora.</span><span class="sxs-lookup"><span data-stu-id="cdd49-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="cdd49-360">Aqui estão os horários de início de saudação de cada fatia, que são representados por **SliceStart** variável do sistema em Olá acima trecho JSON.</span><span class="sxs-lookup"><span data-stu-id="cdd49-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="cdd49-361">**Fatia**</span><span class="sxs-lookup"><span data-stu-id="cdd49-361">**Slice**</span></span> | <span data-ttu-id="cdd49-362">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="cdd49-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="cdd49-363">1</span><span class="sxs-lookup"><span data-stu-id="cdd49-363">1</span></span>         | <span data-ttu-id="cdd49-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="cdd49-365">2</span><span class="sxs-lookup"><span data-stu-id="cdd49-365">2</span></span>         | <span data-ttu-id="cdd49-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="cdd49-367">3</span><span class="sxs-lookup"><span data-stu-id="cdd49-367">3</span></span>         | <span data-ttu-id="cdd49-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="cdd49-369">4</span><span class="sxs-lookup"><span data-stu-id="cdd49-369">4</span></span>         | <span data-ttu-id="cdd49-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="cdd49-371">5</span><span class="sxs-lookup"><span data-stu-id="cdd49-371">5</span></span>         | <span data-ttu-id="cdd49-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="cdd49-373">Olá **folderPath** é calculado usando a parte de ano, mês, dia e hora Olá Olá fatia da hora de início (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="cdd49-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="cdd49-374">Portanto, aqui está como uma pasta de entrada é mapeada tooa fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="cdd49-375">**Fatia**</span><span class="sxs-lookup"><span data-stu-id="cdd49-375">**Slice**</span></span> | <span data-ttu-id="cdd49-376">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="cdd49-376">**Start time**</span></span>          | <span data-ttu-id="cdd49-377">**Pasta de entrada**</span><span class="sxs-lookup"><span data-stu-id="cdd49-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="cdd49-378">1</span><span class="sxs-lookup"><span data-stu-id="cdd49-378">1</span></span>         | <span data-ttu-id="cdd49-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="cdd49-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="cdd49-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="cdd49-381">2</span><span class="sxs-lookup"><span data-stu-id="cdd49-381">2</span></span>         | <span data-ttu-id="cdd49-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="cdd49-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="cdd49-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="cdd49-384">3</span><span class="sxs-lookup"><span data-stu-id="cdd49-384">3</span></span>         | <span data-ttu-id="cdd49-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="cdd49-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="cdd49-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="cdd49-387">4</span><span class="sxs-lookup"><span data-stu-id="cdd49-387">4</span></span>         | <span data-ttu-id="cdd49-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="cdd49-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="cdd49-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="cdd49-390">5</span><span class="sxs-lookup"><span data-stu-id="cdd49-390">5</span></span>         | <span data-ttu-id="cdd49-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="cdd49-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="cdd49-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="cdd49-393">Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **InputDataset** tabela.</span><span class="sxs-lookup"><span data-stu-id="cdd49-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="cdd49-394">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="cdd49-394">Create output dataset</span></span>
<span data-ttu-id="cdd49-395">Nesta etapa, você deve criar outro conjunto de dados de tipo de dados de saída AzureBlob toorepresent hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="cdd49-396">Em Olá **Editor** para Olá fábrica de dados, clique em **novo conjunto de dados** botão na barra de ferramentas hello e clique em **armazenamento de BLOBs do Azure** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="cdd49-397">Substitua Olá JSON no painel direito Olá Olá trecho JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    <span data-ttu-id="cdd49-398">Um blob/arquivo de saída é gerado para cada fatia de entrada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="cdd49-399">Aqui está como um arquivo de saída é chamado para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="cdd49-400">Todos os arquivos de saída de hello são gerados em uma pasta de saída: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="cdd49-401">**Fatia**</span><span class="sxs-lookup"><span data-stu-id="cdd49-401">**Slice**</span></span> | <span data-ttu-id="cdd49-402">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="cdd49-402">**Start time**</span></span>          | <span data-ttu-id="cdd49-403">**Arquivo de saída**</span><span class="sxs-lookup"><span data-stu-id="cdd49-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="cdd49-404">1</span><span class="sxs-lookup"><span data-stu-id="cdd49-404">1</span></span>         | <span data-ttu-id="cdd49-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="cdd49-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="cdd49-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="cdd49-407">2</span><span class="sxs-lookup"><span data-stu-id="cdd49-407">2</span></span>         | <span data-ttu-id="cdd49-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="cdd49-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="cdd49-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="cdd49-410">3</span><span class="sxs-lookup"><span data-stu-id="cdd49-410">3</span></span>         | <span data-ttu-id="cdd49-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="cdd49-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="cdd49-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="cdd49-413">4</span><span class="sxs-lookup"><span data-stu-id="cdd49-413">4</span></span>         | <span data-ttu-id="cdd49-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="cdd49-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="cdd49-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="cdd49-416">5</span><span class="sxs-lookup"><span data-stu-id="cdd49-416">5</span></span>         | <span data-ttu-id="cdd49-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="cdd49-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="cdd49-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="cdd49-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="cdd49-419">Lembre-se de que todos os arquivos em uma pasta de entrada de hello (por exemplo: 2015-11-16-00) fazem parte de uma fatia com hora de início da saudação: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="cdd49-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="cdd49-420">Quando essa fatia é processada, a atividade personalizada Olá verifica cada arquivo e produz uma linha no arquivo de saída de hello com número de saudação de ocorrências do termo de pesquisa ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="cdd49-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="cdd49-421">Se houver três arquivos na pasta Olá 2015-11-16-00, há três linhas no arquivo de saída de hello: 00.txt 2015-11-16.</span><span class="sxs-lookup"><span data-stu-id="cdd49-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="cdd49-422">Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="cdd49-423">Etapa 4: Criar e executar o pipeline de saudação com atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="cdd49-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="cdd49-424">Nesta etapa, você pode criar um pipeline com uma atividade, atividade personalizada de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cdd49-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdd49-425">Se você ainda não carregou Olá **arquivo.txt** tooinput pastas no contêiner de blob hello, fazer isso antes de criar o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="cdd49-426">Olá **isPaused** propriedade é definida toofalse no pipeline Olá JSON, para o pipeline de saudação seja executada imediatamente como Olá **iniciar** data estiver no hello anterior.</span><span class="sxs-lookup"><span data-stu-id="cdd49-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="cdd49-427">No hello Editor da fábrica de dados, clique em **novo pipeline** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="cdd49-428">Se você não vir o comando hello, clique em **... (Reticências)**  toosee-lo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="cdd49-429">Substitua Olá JSON no painel direito Olá Olá script JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="cdd49-430">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-430">Note hello following points:</span></span>

   * <span data-ttu-id="cdd49-431">Há apenas uma atividade no pipeline hello e que é do tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="cdd49-432">**AssemblyName** é definir o nome toohello Olá DLL: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="cdd49-433">**Ponto de entrada** está definido muito**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="cdd49-434">Ele é basicamente \<namespace\>.\<classname\> em seu código.</span><span class="sxs-lookup"><span data-stu-id="cdd49-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="cdd49-435">**PackageLinkedService** está definido muito**StorageLinkedService** que aponte toohello armazenamento de blob que contém o arquivo de zip hello atividade personalizado.</span><span class="sxs-lookup"><span data-stu-id="cdd49-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="cdd49-436">Se você estiver usando diferentes contas de armazenamento do Azure para arquivos de entrada/saída e o arquivo de zip hello atividade personalizada, você tem toocreate outro armazenamento do Azure serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="cdd49-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="cdd49-437">Este artigo pressupõe que você está usando Olá a mesma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="cdd49-438">**PackageFile** está definido muito**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="cdd49-439">Formato de saudação: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="cdd49-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="cdd49-440">atividades personalizadas Olá **InputDataset** como entrada e **OutputDataset** como saída.</span><span class="sxs-lookup"><span data-stu-id="cdd49-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="cdd49-441">Olá **linkedServiceName** propriedade de atividade personalizada Olá aponta toohello **AzureBatchLinkedService**, que informa ao Azure Data Factory dessa atividade personalizada Olá precisa toorun em lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="cdd49-442">Olá **simultaneidade** configuração é importante.</span><span class="sxs-lookup"><span data-stu-id="cdd49-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="cdd49-443">Se você usar o valor padrão de saudação, que é 1, mesmo se você tiver 2 ou mais nós de computação no pool de lote do Azure hello, fatias de saudação são processadas uma após a outra.</span><span class="sxs-lookup"><span data-stu-id="cdd49-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="cdd49-444">Portanto, você não está aproveitando as vantagens da capacidade de processamento paralelo de saudação do lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="cdd49-445">Se você definir **simultaneidade** tooa maior valor, digamos que 2, isso significa que dois fatias (corresponde tootwo tarefas em lote do Azure) podem ser processadas em Olá a mesma hora, nesse caso, as duas máquinas virtuais de saudação de saudação do Azure Batch pool são utilizados.</span><span class="sxs-lookup"><span data-stu-id="cdd49-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="cdd49-446">Portanto, defina a propriedade de simultaneidade de saudação adequadamente.</span><span class="sxs-lookup"><span data-stu-id="cdd49-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="cdd49-447">Apenas uma tarefa (fatia) é executada em uma VM a qualquer momento por padrão.</span><span class="sxs-lookup"><span data-stu-id="cdd49-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="cdd49-448">Olá razão é que, por padrão, hello **máximo de tarefas por VM** é definir too1 para um pool de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="cdd49-449">Como parte dos pré-requisitos, você criou um pool com too2 de definir essa propriedade, para dois intervalos de fábrica de dados podem ser executados em uma VM em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="cdd49-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="cdd49-450">**isPaused** propriedade está definida toofalse por padrão.</span><span class="sxs-lookup"><span data-stu-id="cdd49-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="cdd49-451">Olá pipeline é executado imediatamente neste exemplo como fatias Olá começam em Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="cdd49-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="cdd49-452">Você pode configurar o pipeline de saudação essa propriedade tootrue toopause e defina-a como toorestart toofalse back.</span><span class="sxs-lookup"><span data-stu-id="cdd49-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="cdd49-453">Olá **iniciar** tempo e **final** vezes são separadas de cinco horas e fatias são produzidas por hora, para cinco fatias são produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="cdd49-454">Clique em **implantar** no pipeline de saudação toodeploy da barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="cdd49-455">Etapa 5: Testar o pipeline de saudação</span><span class="sxs-lookup"><span data-stu-id="cdd49-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="cdd49-456">Nesta etapa, você pode testar pipeline Olá soltando arquivos em pastas de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="cdd49-457">Vamos começar com o pipeline de saudação de teste com um arquivo por uma pasta de entrada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="cdd49-458">Na folha da fábrica de dados Olá no hello portal do Azure, clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="cdd49-459">No modo de exibição de diagrama hello, clique duas vezes no conjunto de dados de entrada: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="cdd49-460">Você deve ver Olá **InputDataset** folha com todas as cinco frações pronta.</span><span class="sxs-lookup"><span data-stu-id="cdd49-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="cdd49-461">Saudação de aviso **hora de início da FATIA** e **hora de término da FATIA** para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="cdd49-462">Em Olá **exibição de diagrama**, agora clique **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="cdd49-463">Você deve ver cinco fatias de saída Olá estão em estado pronto do hello se já foi produzidos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="cdd49-464">Saudação de tooview portal do Azure Use **tarefas** associado Olá **fatias** e ver quais VM cada fatia foi executada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="cdd49-465">Confira a seção [Integração de Data Factory e Lote](#data-factory-and-batch-integration) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cdd49-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="cdd49-466">Você deve ver arquivos de saída de saudação em Olá `outputfolder` de `mycontainer` no seu Azure armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="cdd49-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="cdd49-467">Você deve ver cinco arquivos de saída, um para cada fatia de entrada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="cdd49-468">Cada saudação de saída de arquivo deve ter conteúdo toohello semelhante de saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="cdd49-469">Olá diagrama a seguir ilustra como fatias da fábrica de dados de saudação mapeiam tootasks em lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="cdd49-470">Neste exemplo, uma fatia tem apenas uma execução.</span><span class="sxs-lookup"><span data-stu-id="cdd49-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="cdd49-471">Agora, vamos tentar com vários arquivos em uma pasta.</span><span class="sxs-lookup"><span data-stu-id="cdd49-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="cdd49-472">Criar arquivos: **file2.txt**, **file3.txt**, **file4.txt**, e **file5.txt** com hello mesmo conteúdo como arquivo. txt na pasta hello: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="cdd49-473">Na pasta de saída de hello, **excluir** arquivo de saída de hello: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="cdd49-474">Agora, em Olá **OutputDataset** folha, a fatia de saudação atalho com **hora de início da FATIA** definido muito**16/11/2015 01:00:00 AM**e clique em **executar**fatia Olá toorerun/re-process.</span><span class="sxs-lookup"><span data-stu-id="cdd49-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="cdd49-475">Agora, a fatia Olá tem cinco arquivos em vez de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="cdd49-476">Após a execução de fatia hello e seu status é **pronto**, verificar Olá conteúdo no arquivo de saída Olá para esta fatia (**2015-11-16-01.txt**) no hello `outputfolder` de `mycontainer` em seu armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="cdd49-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="cdd49-477">Deve haver uma linha para cada arquivo de fatia hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="cdd49-478">Se você não tiver excluído 2015 de arquivo de saída Olá-11-16-01.txt antes de tentar com cinco arquivos de entrada, você verá uma linha da fatia anterior de saudação executar e cinco linhas de fatia atual de saudação executar.</span><span class="sxs-lookup"><span data-stu-id="cdd49-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="cdd49-479">Por padrão, o conteúdo de saudação é toooutput acrescentados arquivo se ele já existe.</span><span class="sxs-lookup"><span data-stu-id="cdd49-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="cdd49-480">Integração de Data Factory e Lote</span><span class="sxs-lookup"><span data-stu-id="cdd49-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="cdd49-481">Olá serviço da fábrica de dados cria um trabalho em lote do Azure com o nome da saudação: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Trabalhos de Azure Data Factory - Lote](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="cdd49-483">Uma tarefa no trabalho de saudação é criada para cada execução de atividade de uma fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="cdd49-484">Se houver 10 toobe pronto fatias processadas, 10 tarefas são criadas no trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="cdd49-485">Você pode ter mais de uma fatia em execução em paralelo, se você tiver vários nós de computação no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdd49-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="cdd49-486">Se o máximo de tarefas por hello computação de conjunto de nós é muito > 1, pode haver mais de uma fatia em execução no hello computação mesmo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="cdd49-487">Neste exemplo, há cinco fatias, então cinco tarefas no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cdd49-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="cdd49-488">Com hello **simultaneidade** definido muito**5** em Olá pipeline JSON no Azure Data Factory e **máximo de tarefas por VM** definido muito**2** em lote do Azure pool com **2** VMs, Olá tarefas é executada rápida (Verifique as horas de início e término para tarefas).</span><span class="sxs-lookup"><span data-stu-id="cdd49-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="cdd49-489">Use o trabalho em lotes do hello tooview portal hello e suas tarefas associadas a saudação **fatias** e ver quais VM cada fatia foi executada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Tarefas do trabalho de Azure Data Factory - Lote](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="cdd49-491">Depurar pipeline Olá</span><span class="sxs-lookup"><span data-stu-id="cdd49-491">Debug hello pipeline</span></span>
<span data-ttu-id="cdd49-492">A depuração consiste em algumas técnicas básicas:</span><span class="sxs-lookup"><span data-stu-id="cdd49-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="cdd49-493">Se a fatia de entrada hello não está definida muito**pronto**, confirme se a estrutura de pasta de entrada hello está correta e arquivo. txt existe em pastas de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="cdd49-494">Em Olá **Execute** método de sua atividade personalizada, use Olá **IActivityLogger** informações toolog do objeto que ajuda você a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="cdd49-495">mensagens de saudação conectada aparecem no usuário Olá\_0. arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="cdd49-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="cdd49-496">Em Olá **OutputDataset** folha, clique em Olá fatia toosee Olá **FATIA de dados** folha para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="cdd49-497">Você vê as **execuções de atividade** para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="cdd49-498">Você deve ver uma atividade executar fatia hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="cdd49-499">Se você clicar em **executar** na barra de comandos hello, você pode iniciar outra atividade executada para Olá mesma fatia.</span><span class="sxs-lookup"><span data-stu-id="cdd49-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="cdd49-500">Quando você clica em execução da atividade hello, você vê Olá **detalhes de execução da atividade** folha com uma lista de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="cdd49-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="cdd49-501">Consulte as mensagens registradas no hello **usuário\_0. log** arquivo.</span><span class="sxs-lookup"><span data-stu-id="cdd49-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="cdd49-502">Quando ocorre um erro, você verá três execuções de atividade porque a contagem de repetição de saudação é definida too3 Olá pipeline/atividade JSON.</span><span class="sxs-lookup"><span data-stu-id="cdd49-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="cdd49-503">Quando você clica em execução da atividade Olá, você ver arquivos de log de saudação que você pode examinar o erro de saudação tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="cdd49-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="cdd49-504">Na lista de saudação de arquivos de log, clique em Olá **0.log usuário**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="cdd49-505">No painel direito da saudação são resultados de saudação do uso Olá **IActivityLogger.Write** método.</span><span class="sxs-lookup"><span data-stu-id="cdd49-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="cdd49-506">Verifique o system-0.log para quaisquer mensagens de erro e exceções do sistema.</span><span class="sxs-lookup"><span data-stu-id="cdd49-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="cdd49-507">Incluir Olá **PDB** no arquivo zip de saudação do arquivo para que os detalhes do erro Olá contêm informações como **pilha de chamadas** quando ocorre um erro.</span><span class="sxs-lookup"><span data-stu-id="cdd49-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="cdd49-508">Todos Olá arquivos contidos no arquivo zip Olá para atividade de saudação personalizada deve estar no hello **nível superior** sem subpastas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="cdd49-509">Certifique-se de que Olá **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip), e **packageLinkedService** (deve Azure ponto toohello armazenamento de blob que contém o arquivo zip de saudação) são definidos valores toocorrect.</span><span class="sxs-lookup"><span data-stu-id="cdd49-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="cdd49-510">Se você fixa uma fatia de saudação tooreprocess erro e quiser, clique com botão direito fatia Olá Olá **OutputDataset** folha e clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="cdd49-511">Você verá um **contêiner** no Armazenamento de blobs do Azure chamado `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="cdd49-512">Este contêiner não é excluído automaticamente, mas você poderá excluí-la com segurança depois de concluir a solução de saudação testes.</span><span class="sxs-lookup"><span data-stu-id="cdd49-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="cdd49-513">Da mesma forma, a saudação solução da fábrica de dados cria um lote do Azure **trabalho** denominado: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="cdd49-514">Você pode excluir esse trabalho depois de você testar a solução de saudação se desejar.</span><span class="sxs-lookup"><span data-stu-id="cdd49-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="cdd49-515">atividade personalizada Olá não usa Olá **App. config** arquivo do seu pacote.</span><span class="sxs-lookup"><span data-stu-id="cdd49-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="cdd49-516">Portanto, se seu código lê qualquer cadeia de caracteres de conexão do arquivo de configuração hello, ele não funciona em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cdd49-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="cdd49-517">Olá prática recomendada ao usar o lote do Azure é toohold qualquer segredos em um **KeyVault Azure**, use um keyvault do serviço com base em certificado principal tooprotect hello e distribuir o pool do lote Olá certificado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="cdd49-518">Hello atividade personalizada do .NET pode acessar segredos de saudação KeyVault em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cdd49-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="cdd49-519">Essa solução é um arquivo genérico e pode ser dimensionado tooany tipo de segredo, não apenas a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="cdd49-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="cdd49-520">Há uma solução mais fácil (mas não é uma prática recomendada): você pode criar um **serviço vinculado do SQL Azure** com configurações de cadeia de caracteres de conexão, criar um conjunto de dados que usa Olá serviço vinculado e cadeia Olá conjunto de dados como um conjunto de dados de entrada fictício toohello atividade personalizada de .NET.</span><span class="sxs-lookup"><span data-stu-id="cdd49-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="cdd49-521">Você pode então Olá de acesso vinculadas cadeia de caracteres de conexão do serviço no código do hello atividade personalizada e deve funcionar bem em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cdd49-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="cdd49-522">Estender o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="cdd49-522">Extend hello sample</span></span>
<span data-ttu-id="cdd49-523">Você pode estender esse exemplo toolearn mais sobre os recursos do Azure Data Factory e lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="cdd49-524">Por exemplo, tooprocess fatias em um intervalo de tempo diferentes, Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdd49-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="cdd49-525">Adicionar Olá seguintes subpastas Olá `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 e coloque arquivos de entrada nessas pastas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="cdd49-526">Altere a hora de término Olá para o pipeline de saudação do `2015-11-16T05:00:00Z` muito`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="cdd49-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="cdd49-527">Em Olá **exibição de diagrama**, clique duas vezes em Olá **InputDataset**e confirme que as fatias de entrada hello estão prontas.</span><span class="sxs-lookup"><span data-stu-id="cdd49-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="cdd49-528">Clique duas vezes em **OuptutDataset** toosee estado de saudação de fatias de saída.</span><span class="sxs-lookup"><span data-stu-id="cdd49-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="cdd49-529">Se eles estiverem no estado pronto, verifique Olá a pasta de saída para arquivos de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="cdd49-530">Aumentar ou diminuir Olá **simultaneidade** configuração toounderstand como ele afeta o desempenho de saudação da sua solução, especialmente Olá processamento que ocorre em lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd49-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="cdd49-531">(Consulte a etapa 4: criar e executar o pipeline de saudação para saber mais sobre Olá **simultaneidade** configuração.)</span><span class="sxs-lookup"><span data-stu-id="cdd49-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="cdd49-532">Crie um pool com **Máximo de tarefas por VM**maior/menor.</span><span class="sxs-lookup"><span data-stu-id="cdd49-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="cdd49-533">toouse Olá novo pool é criado, saudação de atualização de serviço vinculado do Azure Batch na solução de fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="cdd49-534">(Consulte a etapa 4: criar e executar o pipeline de saudação para saber mais sobre Olá **máximo de tarefas por VM** configuração.)</span><span class="sxs-lookup"><span data-stu-id="cdd49-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="cdd49-535">Crie um pool do Lote do Azure com o recurso **dimensionar automaticamente** .</span><span class="sxs-lookup"><span data-stu-id="cdd49-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="cdd49-536">Dimensionar automaticamente nós de computação em um pool de lote do Azure é o ajuste dinâmico de saudação de energia usada por seu aplicativo de processamento.</span><span class="sxs-lookup"><span data-stu-id="cdd49-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="cdd49-537">fórmula de exemplo Hello aqui alcança Olá comportamento a seguir: quando o pool de saudação inicialmente é criado, ele começa com 1 VM.</span><span class="sxs-lookup"><span data-stu-id="cdd49-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="cdd49-538">Métrica de $PendingTasks define o número de saudação de tarefas em execução + ativo (na fila) estado.</span><span class="sxs-lookup"><span data-stu-id="cdd49-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="cdd49-539">fórmula de saudação localiza Olá média de tarefas pendentes no hello Últimos 180 segundos e define TargetDedicated adequadamente.</span><span class="sxs-lookup"><span data-stu-id="cdd49-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="cdd49-540">Isso garante que TargetDedicated nunca ultrapasse 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="cdd49-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="cdd49-541">Assim, como novas tarefas forem enviadas, pool cresce automaticamente e como tarefas concluídas, as VMs se tornam livre uma e hello autoscaling reduz as VMs.</span><span class="sxs-lookup"><span data-stu-id="cdd49-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="cdd49-542">startingNumberOfVMs e maxNumberofVMs podem ser ajustadas tooyour necessidades.</span><span class="sxs-lookup"><span data-stu-id="cdd49-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="cdd49-543">Fórmula de dimensionamento automático:</span><span class="sxs-lookup"><span data-stu-id="cdd49-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="cdd49-544">Consulte [Dimensionar automaticamente os nós de computação em um pool de Lotes do Azure](../batch/batch-automatic-scaling.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cdd49-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="cdd49-545">Se estiver usando o pool de saudação padrão Olá [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Olá serviço de lote pode levar 15 a 30 minutos tooprepare Olá VM antes de executar a atividade personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="cdd49-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="cdd49-546">Se o pool de saudação está usando um autoScaleEvaluationInterval diferente, Olá serviço de lote pode levar autoScaleEvaluationInterval + 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="cdd49-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="cdd49-547">Solução de exemplo hello, Olá **Execute** método invoca Olá **Calculate** método que processa uma fatia de dados de entrada tooproduce uma fatia de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="cdd49-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="cdd49-548">Você pode escrever seu próprio método tooprocess dados de entrada e substitua a chamada de método hello Calculate no método de execução de saudação com um método de tooyour de chamada.</span><span class="sxs-lookup"><span data-stu-id="cdd49-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="cdd49-549">Próximas etapas: consumir dados Olá</span><span class="sxs-lookup"><span data-stu-id="cdd49-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="cdd49-550">Depois de processar dados, é possível consumi-lo com ferramentas online como o **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="cdd49-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="cdd49-551">Aqui estão os links toohelp entender o Power BI e como toouse-lo no Azure:</span><span class="sxs-lookup"><span data-stu-id="cdd49-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="cdd49-552">Explorar um conjunto de dados no Power BI</span><span class="sxs-lookup"><span data-stu-id="cdd49-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="cdd49-553">Guia de Introdução com hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="cdd49-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="cdd49-554">Atualizar dados no Power BI</span><span class="sxs-lookup"><span data-stu-id="cdd49-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="cdd49-555">Azure e Power BI - visão geral básica</span><span class="sxs-lookup"><span data-stu-id="cdd49-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="cdd49-556">Referências</span><span class="sxs-lookup"><span data-stu-id="cdd49-556">References</span></span>
* [<span data-ttu-id="cdd49-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cdd49-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="cdd49-558">Introdução tooAzure serviço da fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="cdd49-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="cdd49-559">Introdução ao Data Factory do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="cdd49-560">Usar atividades personalizadas em um pipeline do Data Factory do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="cdd49-561">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="cdd49-562">Noções básicas de Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="cdd49-563">Visão geral dos recursos do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="cdd49-564">Criar e gerenciar conta de lote do Azure no portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="cdd49-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="cdd49-565">Introdução ao .NET da Biblioteca de Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="cdd49-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
