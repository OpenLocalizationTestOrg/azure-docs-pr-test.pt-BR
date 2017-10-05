---
title: Processar conjuntos de dados em larga escala usando o Data Factory e o Lote | Microsoft Docs
description: Descreve como processar grandes volumes de dados em um pipeline do Data Factory do Azure usando o recurso de processamento paralelo do Lote do Azure.
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
ms.openlocfilehash: 9defbf7a6a515740fa3b3cb1c67a2f5f9d9baa01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="f2fc0-103">Processar conjuntos de dados em larga escala usando o Data Factory e o Lote</span><span class="sxs-lookup"><span data-stu-id="f2fc0-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="f2fc0-104">Este artigo descreve uma arquitetura de um exemplo de solução que move e processa os conjuntos de dados em larga escala de maneira automática e agendada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="f2fc0-105">Ele também fornece um passo a passo completo para implementar a solução usando Azure Data Factory e o Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="f2fc0-106">Este artigo é maior que nossos artigos comuns porque contém um passo a passo de um exemplo de solução inteira.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="f2fc0-107">Se não tiver experiência com o Lote e o Data Factory, você pode aprender mais sobre esses serviços e como eles funcionam juntos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="f2fc0-108">Se já tem algum conhecimento sobre os serviços e estiver projetando/arquitetando uma solução, você pode se concentrar apenas na [seção de arquitetura](#architecture-of-sample-solution) do artigo e, se estiver desenvolvendo um protótipo ou uma solução, também pode querer testar nossas instruções no [passo a passo](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="f2fc0-109">Seus comentários sobre esse conteúdo e como usá-lo são bem-vindos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="f2fc0-110">Em primeiro lugar, vamos observar como os serviços Data Factory e Lote podem ajudar com o processamento de conjuntos de dados grandes na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="f2fc0-111">Por que usar o Lote do Azure?</span><span class="sxs-lookup"><span data-stu-id="f2fc0-111">Why Azure Batch?</span></span>
<span data-ttu-id="f2fc0-112">O Lote do Azure o habilita a executar aplicativos paralelos em larga escala e de HPC (computação de alto desempenho) na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="f2fc0-113">É um serviço de plataforma que agenda o trabalho de computação intensiva para executar em uma coleção gerenciada de máquinas virtuais e que pode dimensionar automaticamente os recursos de computação para atender às necessidades dos trabalhos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="f2fc0-114">Com o serviço em Lotes, você define os recursos de computação do Azure para executar os aplicativos em paralelo e em escala.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="f2fc0-115">Você pode executar trabalhos sob demanda ou agendados e não precisa criar, configurar e gerenciar manualmente um cluster HPC, máquinas virtuais individuais, redes virtuais ou uma infraestrutura complexa de agendamento de trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="f2fc0-116">Se não estiver familiarizado com o Lote do Azure, veja os artigos a seguir, pois eles ajudam a entender a arquitetura/implementação da solução descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="f2fc0-117">Noções básicas de Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="f2fc0-118">Visão geral do recurso de Lote</span><span class="sxs-lookup"><span data-stu-id="f2fc0-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="f2fc0-119">(opcional) Para saber mais sobre o Lote do Azure, confira o [Caminho de aprendizagem do Lote do Azure](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="f2fc0-120">Por que usar o Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="f2fc0-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="f2fc0-121">O Data Factory é um serviço de integração de dados baseado em nuvem que automatiza a movimentação e a transformação dos dados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="f2fc0-122">Com o serviço Data Factory, você pode criar pipelines de dados gerenciados que movem dados de repositórios de dados locais e na nuvem para um repositório de dados centralizado (por exemplo: Armazenamento de Blobs do Azure), bem como processar/transformar dados usando serviços como o Azure HDInsight e o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="f2fc0-123">Também é possível agendar pipelines de dados para execução de maneira agendada (de hora em hora, diariamente, semanalmente etc.), além de monitorá-los e gerenciá-los rapidamente a fim de identificar problemas e tomar providências.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="f2fc0-124">Se não estiver familiarizado com o Azure Data Factory, veja os artigos a seguir, pois eles ajudam a entender a arquitetura/implementação da solução descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="f2fc0-125">Introdução ao Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f2fc0-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="f2fc0-126">Criar seu primeiro pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="f2fc0-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="f2fc0-127">(opcional) Para saber mais sobre o Azure Data Factory, confira o [Caminho de aprendizagem do Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="f2fc0-128">Data Factory e Lote juntos</span><span class="sxs-lookup"><span data-stu-id="f2fc0-128">Data Factory and Batch together</span></span>
<span data-ttu-id="f2fc0-129">O Data Factory inclui atividades internas como Atividade de Cópia para copiar/mover dados de um repositório de dados de origem para um repositório de dados de destino, bem como a Atividade Hive para processar dados usando clusters Hadoop (HDInsight) no Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="f2fc0-130">Confira [Atividades de transformação de dados](data-factory-data-transformation-activities.md) para obter uma lista de atividades de transformação permitidas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="f2fc0-131">Ele também permite criar atividades do .NET personalizadas para mover ou processar dados com sua própria lógica e executar essas atividades em um cluster do Azure HDInsight ou em um pool de VMs do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="f2fc0-132">Ao usar o Lote do Azure, é possível configurar o pool para dimensionar automaticamente (adicionar ou remover VMs com base na carga de trabalho) com base em uma fórmula que você fornece.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="f2fc0-133">Arquitetura do exemplo de solução</span><span class="sxs-lookup"><span data-stu-id="f2fc0-133">Architecture of sample solution</span></span>
<span data-ttu-id="f2fc0-134">Embora a arquitetura descrita neste artigo seja para uma solução simples, ela é relevante para cenários complexos, como modelagem de risco por serviços financeiros, processamento e renderização de imagem, e análise genômica.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="f2fc0-135">O diagrama ilustra 1) como o Data Factory orquestra movimentação e processamento de dados e 2) como o Lote do Azure processa os dados de forma paralela.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="f2fc0-136">Baixe e imprima o diagrama para consulta fácil (27,94 x 43,18 cm</span><span class="sxs-lookup"><span data-stu-id="f2fc0-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="f2fc0-137">ou tamanho A3): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686) (HPC e orquestração de dados usando o Azure Batch e o Data Factory).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="f2fc0-138">[![Diagrama de processamento de dados em larga escala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="f2fc0-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="f2fc0-139">A lista a seguir fornece as etapas básicas do processo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="f2fc0-140">A solução inclui código e explicações para criar a solução de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="f2fc0-141">**Configure o Lote do Azure com um pool de nós de computação (VMs)**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="f2fc0-142">Você pode especificar o número de nós e o tamanho de cada nó.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="f2fc0-143">**Crie uma instância do Azure Data Factory** que está configurada com entidades que representam o armazenamento de blobs do Azure, serviço de computação do Lote do Azure, dados de entrada/saída e um fluxo de trabalho/pipeline com atividades que movem e transformam dados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="f2fc0-144">**Crie uma atividade .NET personalizada no pipeline do Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="f2fc0-145">A atividade é seu código de usuário que é executado no pool do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="f2fc0-146">**Armazene grandes quantidades de dados de entrada como blobs no armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="f2fc0-147">Os dados são divididos em fatias lógicas (geralmente, por hora).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="f2fc0-148">**O Data Factory copia os dados que são processados em paralelo** para a localização secundária.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="f2fc0-149">**O Data Factory executa a atividade personalizada usando o pool alocado pelo Lote**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="f2fc0-150">O Data Factory pode executar atividades simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="f2fc0-151">Cada atividade processa uma fatia de dados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="f2fc0-152">Os resultados são armazenados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="f2fc0-153">**O Data Factory move os resultados finais para um terceiro local**para distribuição por meio de um aplicativo ou para processamento adicional por outras ferramentas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="f2fc0-154">Implementação da solução de exemplo</span><span class="sxs-lookup"><span data-stu-id="f2fc0-154">Implementation of sample solution</span></span>
<span data-ttu-id="f2fc0-155">A solução de exemplo é intencionalmente simples e serve para mostrar como usar o Data Factory e o Lote juntos no processamento de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="f2fc0-156">A solução conta apenas com o número de ocorrências de um termo de pesquisa ("Microsoft") em arquivos de entrada organizados em uma série temporal.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="f2fc0-157">Ele produz a contagem para arquivos de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-157">It outputs the count to output files.</span></span>

<span data-ttu-id="f2fc0-158">**Tempo**: se você estiver familiarizado com as noções básicas do Azure, Data Factory e Batch e tiver atendido aos pré-requisitos listados abaixo, estimamos que essa solução levará de 1 a 2 horas para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f2fc0-159">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f2fc0-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="f2fc0-160">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-160">Azure subscription</span></span>
<span data-ttu-id="f2fc0-161">Se você não tiver uma assinatura do Azure, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f2fc0-162">Veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="f2fc0-163">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-163">Azure storage account</span></span>
<span data-ttu-id="f2fc0-164">Você usará uma conta de armazenamento do Azure para armazenar os dados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="f2fc0-165">Se você não tiver uma conta de armazenamento do Azure, consulte o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="f2fc0-166">A solução de exemplo usa o armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="f2fc0-167">Conta do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-167">Azure Batch account</span></span>
<span data-ttu-id="f2fc0-168">Crie uma conta do Azure Batch usando o [Portal do Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="f2fc0-169">Consulte [Criar e gerenciar uma conta do Lote do Azure](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="f2fc0-170">Anote a chave e o nome da conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="f2fc0-171">Você também pode usar o cmdlet [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) para criar uma conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="f2fc0-172">Consulte [Introdução aos cmdlets do PowerShell do Lote do Azure](../batch/batch-powershell-cmdlets-get-started.md) para obter instruções detalhadas sobre como usar esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="f2fc0-173">A solução de exemplo usa Azure Batch (indiretamente por meio de um pipeline do Azure Data Factory) para processar dados de forma paralela em um pool de nós de computação (uma coleção gerenciada de máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="f2fc0-174">Pool de VMs (máquinas virtuais) do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="f2fc0-175">Crie um **pool de Lote do Azure** com pelo menos dois nós de computação.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="f2fc0-176">No [Portal do Azure](https://portal.azure.com), clique em **Procurar** no menu à esquerda e clique em **Contas do Batch**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="f2fc0-177">Selecione sua a conta do Lote do Azure para abrir a folha **Conta do Batch** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="f2fc0-178">Clique no bloco **Pools** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="f2fc0-179">Na folha **Pools** , clique no botão Adicionar na barra de ferramentas para adicionar um pool.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="f2fc0-180">Insira uma ID para o pool (**ID do Pool**).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="f2fc0-181">Observe a **ID do pool**; você precisa dela ao criar a solução Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="f2fc0-182">Especifique **Windows Server 2012 R2** para a configuração da família do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="f2fc0-183">Selecione um **camada de preços de nó**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="f2fc0-184">Digite **2** como valor para a configuração **Destino Dedicado**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="f2fc0-185">Digite **2** como valor para a configuração **Máximo de tarefas por nó**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="f2fc0-186">Clique em **OK** para criar o pool.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="f2fc0-187">Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-187">Azure Storage Explorer</span></span>
<span data-ttu-id="f2fc0-188">[Azure Storage Explorer 6 (ferramenta)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (da ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="f2fc0-189">Você usa essas ferramentas para inspecionar e alterar os dados em seus projetos do Azure Storage, incluindo os logs dos aplicativos hospedados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="f2fc0-190">Crie um contêiner chamado **mycontainer** com acesso privado (sem acesso anônimo)</span><span class="sxs-lookup"><span data-stu-id="f2fc0-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="f2fc0-191">Se você estiver usando **CloudXplorer**, crie pastas e subpastas com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="f2fc0-192">`Inputfolder` e `outputfolder` são pastas de nível superior no `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="f2fc0-193">A `inputfolder` contém subpastas com carimbos de data/hora (AAAA-MM-DD-HH).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-193">The `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="f2fc0-194">Se você estiver usando o **Gerenciador de Armazenamento do Azure**, na próxima etapa, precisará carregar arquivos com os nomes `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-194">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="f2fc0-195">Essa etapa cria as pastas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-195">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="f2fc0-196">Crie um arquivo de texto **file.txt** no computador com o conteúdo com a palavra-chave **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-196">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="f2fc0-197">Por exemplo: "testar a atividade personalizada Microsoft testar atividade personalizada Microsoft".</span><span class="sxs-lookup"><span data-stu-id="f2fc0-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="f2fc0-198">Carregue o arquivo para as seguintes pastas de entrada no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-198">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="f2fc0-199">Se você estiver usando o **Azure Storage Explorer**, carregue o arquivo **file.txt** para **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-199">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="f2fc0-200">Clique em **Copiar** na barra de ferramentas para criar uma cópia do blob.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-200">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="f2fc0-201">Na caixa de diálogo **Copiar Blob**, altere o **nome do blob de destino** para `inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-201">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="f2fc0-202">Repita essa etapa para criar `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-202">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="f2fc0-203">Essa ação cria as pastas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-203">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="f2fc0-204">Crie outro contêiner chamado `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="f2fc0-205">Você carrega o arquivo zip da atividade personalizada para esse contêiner.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-205">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="f2fc0-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2fc0-206">Visual Studio</span></span>
<span data-ttu-id="f2fc0-207">Microsoft Visual Studio 2012 ou posterior para criar a atividade personalizada do Lote a ser usada na solução de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-207">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="f2fc0-208">Etapas de alto nível para criar a solução</span><span class="sxs-lookup"><span data-stu-id="f2fc0-208">High-level steps to create the solution</span></span>
1. <span data-ttu-id="f2fc0-209">Crie uma atividade personalizada que contenha a lógica de processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-209">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="f2fc0-210">Crie um Azure Data Factory que usa a atividade personalizada:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-210">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="f2fc0-211">Criar a atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="f2fc0-211">Create the custom activity</span></span>
<span data-ttu-id="f2fc0-212">A atividade personalizada do Data Factory é o cerne desta solução de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-212">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="f2fc0-213">A solução de exemplo usa o Lote do Azure para executar a atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-213">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="f2fc0-214">Consulte [Usar atividades personalizadas em um pipeline do Azure Data Factory](data-factory-use-custom-activities.md) para obter as informações básicas para desenvolver atividades personalizadas e usá-las em pipelines do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="f2fc0-215">Para criar uma atividade personalizada do .NET que possa ser usada em um pipeline do Azure Data Factory, você precisa criar um projeto da **Biblioteca de Classes do .NET** com uma classe que implemente a interface **IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-215">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="f2fc0-216">Essa interface tem apenas um método: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="f2fc0-217">Veja a assinatura desse método:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-217">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="f2fc0-218">O método tem alguns componentes principais que você precisa entender.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-218">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="f2fc0-219">O método utiliza quatro parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-219">The method takes four parameters:</span></span>

  1. <span data-ttu-id="f2fc0-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-220">**linkedServices**.</span></span> <span data-ttu-id="f2fc0-221">Uma lista enumerável de serviços vinculados que vinculam fontes de dados de entrada/saída (por exemplo: armazenamento de blobs do Azure) no data factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="f2fc0-222">Neste exemplo, há apenas um serviço vinculado do tipo armazenamento do Azure usado para entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="f2fc0-223">**conjuntos de dados**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-223">**datasets**.</span></span> <span data-ttu-id="f2fc0-224">É uma lista enumerável de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="f2fc0-225">Você pode usar esse parâmetro para obter os locais e esquemas definidos por conjuntos de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-225">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="f2fc0-226">**atividade**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-226">**activity**.</span></span> <span data-ttu-id="f2fc0-227">Esse parâmetro representa a entidade de computação atual, nesse caso, um serviço de Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-227">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="f2fc0-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-228">**logger**.</span></span> <span data-ttu-id="f2fc0-229">O logger permite que você escreva comentários de depuração que são exibidos como o log do “usuário" no pipeline.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-229">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="f2fc0-230">O método retorna um dicionário que pode ser usado para unir atividades personalizadas no futuro.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-230">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="f2fc0-231">Este recurso ainda não está implementado, portanto, retorne um dicionário vazio do método.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-231">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="f2fc0-232">Procedimento: criar a atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="f2fc0-232">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="f2fc0-233">Crie um projeto de Biblioteca de Classes .NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="f2fc0-234">Inicie o **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="f2fc0-235">Clique em **Arquivo**, aponte para **Novo** e clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-235">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="f2fc0-236">Expanda **Modelos** e selecione **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="f2fc0-237">Neste passo a passo, você pode usar C\#, mas pode usar qualquer linguagem .NET para desenvolver a atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-237">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="f2fc0-238">Selecione **Biblioteca de Classes** na lista de tipos de projeto à direita.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-238">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="f2fc0-239">Insira **MyDotNetActivity** for the **Nome**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-239">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="f2fc0-240">Selecione **C:\\ADF** para a **Localização**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-240">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="f2fc0-241">Crie a pasta **ADF** se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-241">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="f2fc0-242">Clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-242">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="f2fc0-243">Clique em **Ferramentas**, aponte para **Gerenciador de Pacotes NuGet** e clique em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-243">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="f2fc0-244">No **Console do Gerenciador de Pacotes**, execute o comando a seguir para importar **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-244">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="f2fc0-245">Importe o pacote NuGet do **Armazenamento do Azure** para o projeto.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-245">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="f2fc0-246">Você precisa desse pacote porque usa a API de Armazenamento de Blobs neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-246">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="f2fc0-247">Adicione as diretivas **using** a seguir ao arquivo de origem no projeto.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-247">Add the following **using** directives to the source file in the project.</span></span>

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
6. <span data-ttu-id="f2fc0-248">Altere o nome do **namespace** para **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-248">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="f2fc0-249">Altere o nome da classe para **MyDotNetActivity** e derive-a da interface **IDotNetActivity**, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-249">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="f2fc0-250">Implemente (Adicione) o método **Execute** da interface **IDotNetActivity** à classe **MyDotNetActivity** e copie o seguinte código de exemplo para o método.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-250">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="f2fc0-251">Consulte a seção [Método Execute](#execute-method) para obter uma explicação para a lógica usada nesse método.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-251">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
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
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="f2fc0-252">Adicione os seguintes métodos auxiliares à classe.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-252">Add the following helper methods to the class.</span></span> <span data-ttu-id="f2fc0-253">Esses métodos são invocados pelo método **Execute** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-253">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="f2fc0-254">Mais importante, o método **Calculate** isola o código que itera através de cada blob.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-254">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
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
    /// Gets the fileName value from the input/output dataset.
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
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
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
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="f2fc0-255">O método **GetFolderPath** retorna o caminho para a pasta indicada pelo conjunto de dados e o método **GetFileName** retorna o nome do blob/arquivo para o qual o conjunto de dados aponta.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-255">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="f2fc0-256">O método **Calculate** calcula o número de instâncias da palavra-chave **Microsoft** nos arquivos de entrada (blobs na pasta).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-256">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="f2fc0-257">O termo de pesquisa ("Microsoft") é embutido no código.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-257">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="f2fc0-258">Compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-258">Compile the project.</span></span> <span data-ttu-id="f2fc0-259">Clique em **Compilar** no menu e clique em **Compilar Solução**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-259">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="f2fc0-260">Inicie o **Windows Explorer** e navegue até a pasta **bin\\debug** ou **bin\\release** dependendo do tipo da compilação.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-260">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="f2fc0-261">Crie um arquivo zip **MyDotNetActivity.zip** que contém todos os binários na pasta **\\bin\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-261">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="f2fc0-262">Inclua o arquivo MyDotNetActivity.**pdb** para obter detalhes adicionais, como número de linha no código fonte que causou o problema quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-262">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="f2fc0-263">Carregue **MyDotNetActivity.zip** como um blob no contêiner de blobs `customactivitycontainer`, no armazenamento de blobs do Azure utilizado pelo serviço vinculado **StorageLinkedService** no **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-263">Upload **MyDotNetActivity.zip** as a blob to the blob container: `customactivitycontainer` in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="f2fc0-264">Crie o contêiner de blobs `customactivitycontainer` se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-264">Create the blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="f2fc0-265">Método Execute</span><span class="sxs-lookup"><span data-stu-id="f2fc0-265">Execute method</span></span>
<span data-ttu-id="f2fc0-266">Esta seção fornece mais detalhes e observações sobre o código no método Execute.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-266">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="f2fc0-267">Os membros para iteração pela coleção de entrada são encontrados no namespace [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-267">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="f2fc0-268">A iteração através da coleção de blobs requer o uso da classe **BlobContinuationToken** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-268">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="f2fc0-269">Em essência, você deve usar um loop do-while com o token, como o mecanismo para saída do loop.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-269">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="f2fc0-270">Para obter mais informações, consulte o artigo sobre [Como usar o armazenamento de blobs do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-270">For more information, see [How to use Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f2fc0-271">Um loop básico é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
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
   <span data-ttu-id="f2fc0-272">Consulte a documentação do método [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-272">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="f2fc0-273">O código para trabalhar com o conjunto de blobs logicamente fica dentro do loop do-while.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-273">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="f2fc0-274">No método **Execute**, o loop do-while passa a lista de blobs para um método chamado **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-274">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="f2fc0-275">O método retorna uma variável de cadeia de caracteres chamada **output** , que é o resultado da iteração nos blobs do segmento.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-275">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="f2fc0-276">Ele retorna o número de ocorrências do termo de pesquisa (**Microsoft**) no blob passado para o método **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-276">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="f2fc0-277">Quando o método **Calculate** tiver feito o trabalho, ele deverá ser gravado em um novo blob.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-277">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="f2fc0-278">Para cada conjunto de blobs processado, um novo blob pode ser gravado nos resultados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-278">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="f2fc0-279">Para gravar um novo blob, primeiro localize o conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-279">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="f2fc0-280">O código também chama um método auxiliar: **GetFolderPath** para recuperar o caminho da pasta (o nome do contêiner de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-280">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="f2fc0-281">O **GetFolderPath** converte o objeto DataSet em um AzureBlobDataSet, que tem uma propriedade chamada FolderPath.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-281">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="f2fc0-282">O código chama o método **GetFileName** para recuperar o nome do arquivo (nome do blob).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-282">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="f2fc0-283">O código é semelhante ao código acima para obter o caminho da pasta.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-283">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="f2fc0-284">O nome do arquivo é gravado, ao criar um objeto URI.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-284">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="f2fc0-285">O construtor de URI usa a propriedade **BlobEndpoint** propriedade para retornar o nome do contêiner.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-285">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="f2fc0-286">O nome do arquivo e caminho da pasta são adicionados para construir o URI do blob de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-286">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="f2fc0-287">O nome do arquivo foi escrito e agora você pode gravar a cadeia de caracteres de saída do método **Calculate** em um novo blob:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-287">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="f2fc0-288">Criar o data factory</span><span class="sxs-lookup"><span data-stu-id="f2fc0-288">Create the data factory</span></span>
<span data-ttu-id="f2fc0-289">Na seção [Criar atividade personalizada](#create-the-custom-activity) , você criou uma atividade personalizada e carregou o arquivo zip com binários e o arquivo PDB em um contêiner de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-289">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="f2fc0-290">Nesta seção, você cria um Azure **data factory** com um **pipeline** que usa **atividade personalizada**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-290">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="f2fc0-291">O conjunto de dados de entrada da atividade personalizada representa os blobs (arquivos) na pasta de entrada (`mycontainer\\inputfolder`) no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-291">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="f2fc0-292">O conjunto de dados de saída da atividade representa os blobs de saída na pasta de saída (`mycontainer\\outputfolder`) no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-292">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="f2fc0-293">Solte um ou mais arquivos nas pastas de entrada:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-293">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="f2fc0-294">Por exemplo, solte um arquivo (file.txt) com o seguinte conteúdo em cada uma das pastas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-294">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="f2fc0-295">A pasta de entrada corresponde a uma fatia no Azure Data Factory, mesmo que a pasta tenha dois ou mais arquivos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-295">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="f2fc0-296">Quando cada fatia é processada pelo pipeline, a atividade personalizada itera em todos os blobs na pasta de entrada dessa fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-296">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="f2fc0-297">Você vê cinco arquivos de saída com o mesmo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-297">You see five output files with the same content.</span></span> <span data-ttu-id="f2fc0-298">Por exemplo, o arquivo de saída do processamento do arquivo na pasta 2015-11-16-00 tem o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-298">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="f2fc0-299">Se você soltar vários arquivos (file.txt, file2.txt, file3.txt) com o mesmo conteúdo na pasta de entrada, verá o seguinte conteúdo no arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="f2fc0-300">Cada pasta (2015-11-16-00, etc.) corresponde a uma fatia neste exemplo, mesmo que a pasta tenha vários arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-300">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="f2fc0-301">O arquivo de saída tem três linhas agora, uma para cada arquivo de entrada (blob) na pasta associada à fatia (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-301">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="f2fc0-302">Uma tarefa é criada para cada execução de atividade.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-302">A task is created for each activity run.</span></span> <span data-ttu-id="f2fc0-303">Neste exemplo, há apenas uma atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-303">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="f2fc0-304">Quando uma fatia é processada pelo pipeline, a atividade personalizada é executada no Lote do Azure para processar a fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-304">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="f2fc0-305">Uma vez que há cinco intervalos (cada fatia pode ter vários blobs ou arquivos), há cinco tarefas criadas no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="f2fc0-306">Quando uma tarefa é executada em lote, é, na verdade, a atividade personalizada que está sendo executada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-306">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="f2fc0-307">A apresentação passo a passo a seguir dá os detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-307">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="f2fc0-308">Etapa 1: Criar o data factory</span><span class="sxs-lookup"><span data-stu-id="f2fc0-308">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="f2fc0-309">Depois de fazer logon no [Portal do Azure](https://portal.azure.com/), execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-309">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="f2fc0-310">Clique em **NOVO** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-310">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="f2fc0-311">Clique em **Dados + Análise** na folha **Novo**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-311">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="f2fc0-312">Clique em **Data Factory** na folha **Análise de dados**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-312">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="f2fc0-313">Na folha **Novo data factory**, insira **CustomActivityFactory** para o Nome.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-313">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="f2fc0-314">O nome da data factory do Azure deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-314">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="f2fc0-315">Se você receber o erro: **O nome de data factory “CustomActivityFactory” não está disponível**, altere o nome (por exemplo, **yournameCustomActivityFactory**) e tente criá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-315">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="f2fc0-316">Clique em **NOME DO GRUPO DE RECURSOS**para selecionar um grupo de recursos existente ou criar um.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="f2fc0-317">Depois de selecionar o grupo de recursos, verifique se que você está usando a assinatura correta e a região na qual deseja que o data factory seja criado.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-317">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="f2fc0-318">Clique em **Criar** na folha **Novo data factory**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-318">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="f2fc0-319">Você vê o data factory sendo criado no **Painel** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-319">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="f2fc0-320">Após o data factory ter sido criado com êxito, você verá a página do data factory, que exibe seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-320">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="f2fc0-321">Etapa 2: Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="f2fc0-321">Step 2: Create linked services</span></span>
<span data-ttu-id="f2fc0-322">Serviços vinculados vinculam armazenamentos de dados ou serviços de computação para uma data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-322">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="f2fc0-323">Nesta etapa, você vincula a conta do **Azure Storage** e a conta do **Azure Batch** ao data factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-323">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="f2fc0-324">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="f2fc0-325">Clique no bloco **Criar e implantar** na folha **DATA FACTORY** para **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-325">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="f2fc0-326">Você vê o Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-326">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="f2fc0-327">Clique em **Novo armazenamento de dados** na barra de comandos e escolha **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-327">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="f2fc0-328">Você deve ver o script JSON para criar um serviço de armazenamento vinculado do Azure no editor.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-328">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="f2fc0-329">Substitua o **nome da conta** pelo nome da conta do Armazenamento do Azure e a **chave de conta** pela chave de acesso da sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-329">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="f2fc0-330">Para saber como obter sua chave de acesso de armazenamento, confira [Exibir, copiar e regenerar chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-330">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="f2fc0-331">Clique em **Implantar** na barra de comandos para implantar o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-331">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="f2fc0-332">Crie o serviço vinculado do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="f2fc0-333">Nesta etapa, você cria um serviço vinculado para a sua conta do **Azure Batch** que é usado para executar a atividade personalizada do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-333">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="f2fc0-334">Clique em **Novo computador** na barra de comandos e escolha **Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-334">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="f2fc0-335">Você deve ver o script JSON para criar um serviço vinculado do Lote do Azure no editor.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-335">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="f2fc0-336">No script JSON:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-336">In the JSON script:</span></span>

   1. <span data-ttu-id="f2fc0-337">Substitua **nome da conta** pelo nome da sua conta do Lote do Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-337">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="f2fc0-338">Substitua **chave de acesso** pela chave de acesso da conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-338">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="f2fc0-339">Insira a ID do pool para a propriedade **poolName****.**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-339">Enter the ID of the pool for the **poolName** property**.**</span></span> <span data-ttu-id="f2fc0-340">Para essa propriedade, você pode especificar o nome do pool ou o ID do pool.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="f2fc0-341">Digite o URI do lote para a propriedade JSON **batchUri** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-341">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="f2fc0-342">A **URL** da **folha da conta do Azure Batch** está no seguinte formato: \<accountname\>.\<region\>.batch.azure.com. Para a propriedade **batchUri** em JSON, você precisará **remover "accountname."**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-342">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com. For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="f2fc0-343">da URL.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-343">from the URL.</span></span> <span data-ttu-id="f2fc0-344">Exemplo: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="f2fc0-345">Para a propriedade **poolName** , você também pode especificar a ID do pool em vez do nome do pool.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f2fc0-346">O serviço de Data Factory não suporta uma opção sob demanda para o Azure Batch como o faz para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="f2fc0-347">Você só pode usar seu próprio pool do Azure Batch em um Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="f2fc0-348">Especifique **StorageLinkedService** for the **linkedServiceName** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="f2fc0-349">Você criou esse serviço vinculado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="f2fc0-350">Esse armazenamento é usado como uma área de preparação para arquivos e logs.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="f2fc0-351">Clique em **Implantar** na barra de comandos para implantar o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="f2fc0-352">Etapa 3: Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="f2fc0-352">Step 3: Create datasets</span></span>
<span data-ttu-id="f2fc0-353">Nesta etapa, você cria conjuntos de dados para representar a entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="f2fc0-354">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="f2fc0-354">Create input dataset</span></span>
1. <span data-ttu-id="f2fc0-355">No **Editor** do Data Factory, clique no botão **Novo conjunto de dados** na barra de ferramentas e clique em **Armazenamento de Blobs do Azure** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="f2fc0-356">Substitua o JSON no painel direito pelo trecho de código JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="f2fc0-357">Você cria um pipeline posteriormente neste passo a passo com hora de início: 2015-11-16T00:00:00Z e final: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="f2fc0-358">Ele é agendado para gerar dados **de hora em hora**, então há cinco fatias de entrada/saída (**00**:00:00 –\> **05**:00:00).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="f2fc0-359">A **frequência** e o **intervalo** do conjunto de dados de entrada são definidos como **Hora** e **1**, o que significa que a fatia de entrada está disponível por hora.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="f2fc0-360">Aqui estão as horas de início de cada fatia, representado pela variável de sistema **SliceStart** no trecho de código JSON acima.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="f2fc0-361">**Fatia**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-361">**Slice**</span></span> | <span data-ttu-id="f2fc0-362">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="f2fc0-363">1</span><span class="sxs-lookup"><span data-stu-id="f2fc0-363">1</span></span>         | <span data-ttu-id="f2fc0-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="f2fc0-365">2</span><span class="sxs-lookup"><span data-stu-id="f2fc0-365">2</span></span>         | <span data-ttu-id="f2fc0-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="f2fc0-367">3</span><span class="sxs-lookup"><span data-stu-id="f2fc0-367">3</span></span>         | <span data-ttu-id="f2fc0-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="f2fc0-369">4</span><span class="sxs-lookup"><span data-stu-id="f2fc0-369">4</span></span>         | <span data-ttu-id="f2fc0-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="f2fc0-371">5</span><span class="sxs-lookup"><span data-stu-id="f2fc0-371">5</span></span>         | <span data-ttu-id="f2fc0-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="f2fc0-373">O **folderPath** é calculado usando a parte de ano, mês, dia e hora da hora de início da fatia (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="f2fc0-374">Portanto, é assim que uma pasta de entrada é mapeada para uma fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="f2fc0-375">**Fatia**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-375">**Slice**</span></span> | <span data-ttu-id="f2fc0-376">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-376">**Start time**</span></span>          | <span data-ttu-id="f2fc0-377">**Pasta de entrada**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="f2fc0-378">1</span><span class="sxs-lookup"><span data-stu-id="f2fc0-378">1</span></span>         | <span data-ttu-id="f2fc0-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="f2fc0-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="f2fc0-381">2</span><span class="sxs-lookup"><span data-stu-id="f2fc0-381">2</span></span>         | <span data-ttu-id="f2fc0-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="f2fc0-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="f2fc0-384">3</span><span class="sxs-lookup"><span data-stu-id="f2fc0-384">3</span></span>         | <span data-ttu-id="f2fc0-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="f2fc0-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="f2fc0-387">4</span><span class="sxs-lookup"><span data-stu-id="f2fc0-387">4</span></span>         | <span data-ttu-id="f2fc0-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="f2fc0-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="f2fc0-390">5</span><span class="sxs-lookup"><span data-stu-id="f2fc0-390">5</span></span>         | <span data-ttu-id="f2fc0-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="f2fc0-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="f2fc0-393">Clique em **Implantar** na barra de ferramentas para criar e implantar a tabela **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="f2fc0-394">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="f2fc0-394">Create output dataset</span></span>
<span data-ttu-id="f2fc0-395">Nesta etapa, você cria outro conjunto de dados do tipo AzureBlob para representar os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="f2fc0-396">No **Editor** do Data Factory, clique no botão **Novo conjunto de dados** na barra de ferramentas e clique em **Armazenamento de Blobs do Azure** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="f2fc0-397">Substitua o JSON no painel direito pelo trecho de código JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="f2fc0-398">Um blob/arquivo de saída é gerado para cada fatia de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="f2fc0-399">Aqui está como um arquivo de saída é chamado para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="f2fc0-400">Todos os arquivos de saída são gerados em uma pasta de saída: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-400">All the output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="f2fc0-401">**Fatia**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-401">**Slice**</span></span> | <span data-ttu-id="f2fc0-402">**Hora de início**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-402">**Start time**</span></span>          | <span data-ttu-id="f2fc0-403">**Arquivo de saída**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="f2fc0-404">1</span><span class="sxs-lookup"><span data-stu-id="f2fc0-404">1</span></span>         | <span data-ttu-id="f2fc0-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="f2fc0-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="f2fc0-407">2</span><span class="sxs-lookup"><span data-stu-id="f2fc0-407">2</span></span>         | <span data-ttu-id="f2fc0-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="f2fc0-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="f2fc0-410">3</span><span class="sxs-lookup"><span data-stu-id="f2fc0-410">3</span></span>         | <span data-ttu-id="f2fc0-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="f2fc0-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="f2fc0-413">4</span><span class="sxs-lookup"><span data-stu-id="f2fc0-413">4</span></span>         | <span data-ttu-id="f2fc0-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="f2fc0-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="f2fc0-416">5</span><span class="sxs-lookup"><span data-stu-id="f2fc0-416">5</span></span>         | <span data-ttu-id="f2fc0-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="f2fc0-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="f2fc0-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="f2fc0-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="f2fc0-419">Lembre-se de que todos os arquivos em uma pasta de entrada (por exemplo, 2015-11-16-00) fazem parte de uma fatia com as horas de início mencionadas acima: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="f2fc0-420">Quando essa fatia é processada, a atividade personalizada examina cada arquivo e produz uma linha no arquivo de saída com o número de ocorrências do termo de pesquisa ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="f2fc0-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="f2fc0-421">Se houver três arquivos na pasta 2015-11-16-00, haverá três linhas no arquivo de saída: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="f2fc0-422">Clique em **Implantar** na barra de ferramentas para criar e implantar **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="f2fc0-423">Etapa 4: criar e executar o pipeline com atividade personalizada</span><span class="sxs-lookup"><span data-stu-id="f2fc0-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="f2fc0-424">Nesta etapa, você cria um pipeline com uma atividade, a atividade personalizada criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2fc0-425">Se você ainda não tiver carregado o **file.txt** para as pastas de entrada no contêiner de blob, faça isso antes de criar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="f2fc0-426">A propriedade **isPaused** é definida como false no JSON do pipeline, de modo que o pipeline é executado imediatamente, já que a data **inicial** está no passado.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="f2fc0-427">No Editor Data Factory, clique em **Novo pipeline** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="f2fc0-428">Se você não vir o comando, clique em **... (Reticências)** para vê-lo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="f2fc0-429">Substitua o JSON no painel direito pelo script JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-429">Replace the JSON in the right pane with the following JSON script:</span></span>

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
   <span data-ttu-id="f2fc0-430">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-430">Note the following points:</span></span>

   * <span data-ttu-id="f2fc0-431">Há apenas uma atividade no pipeline, e ela é do tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="f2fc0-432">**AssemblyName** é definido para o nome da DLL: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="f2fc0-433">**EntryPoint** é definido como **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="f2fc0-434">Ele é basicamente \<namespace\>.\<classname\> em seu código.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="f2fc0-435">**PackageLinkedService** é definido como **StorageLinkedService**, que aponta para o armazenamento de blobs que contém o arquivo zip da atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="f2fc0-436">Se você estiver usando contas do Azure Storage diferentes para arquivos de entrada/saída e o arquivo zip da atividade personalizada, precisa de criar outro serviço vinculado do Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="f2fc0-437">Este artigo pressupõe que você está usando a mesma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="f2fc0-438">**PackageFile** é definido como **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="f2fc0-439">Ele está no formato: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="f2fc0-440">A atividade personalizada usa **InputDataset** como entrada e **OutputDataset** como saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="f2fc0-441">A propriedade **linkedServiceName** da atividade personalizada aponta para o **AzureBatchLinkedService**, que informa ao Azure Data Factory que a atividade personalizada precisa ser executada em um cluster do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="f2fc0-442">A configuração **simultaneidade** é importante.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="f2fc0-443">Se você usar o valor padrão, que é 1, mesmo que tenha dois ou mais nós de computação no pool de Lote do Azure, as fatias serão processadas uma após a outra.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="f2fc0-444">Portanto, você não está aproveitando a capacidade de processamento paralelo de Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="f2fc0-445">Se você definir **simultaneidade** para um valor mais alto, digamos 2, isso significará que duas fatias (correspondendo a duas tarefas no Azure Batch) poderão ser processadas ao mesmo tempo, nesse caso, ambas as VMs no pool do Azure Batch serão utilizadas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="f2fc0-446">Portanto, defina a propriedade de simultaneidade adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="f2fc0-447">Apenas uma tarefa (fatia) é executada em uma VM a qualquer momento por padrão.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="f2fc0-448">Isso ocorre porque, por padrão, o **Máximo de tarefas por VM** é definido como 1 para um pool do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="f2fc0-449">Como parte dos pré-requisitos, você criou um pool com essa propriedade definida para 2, de modo que as fatias do Data Factory podem ser executadas em uma VM ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="f2fc0-450">**isPaused** está definida para falso por padrão.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="f2fc0-451">O pipeline é executado imediatamente neste exemplo porque a fatias começam no passado.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="f2fc0-452">Você pode definir essa propriedade como verdadeira para pausar o pipeline e defini-lo novamente como falsa para reiniciar.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="f2fc0-453">As horas de **início** e **fim** são distantes cinco horas e as fatias são produzidas por hora, portanto, são produzidas cinco fatias pelo pipeline.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="f2fc0-454">Clique em **Implantar** na barra de comandos para implantar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="f2fc0-455">Etapa 5: testar o pipeline</span><span class="sxs-lookup"><span data-stu-id="f2fc0-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="f2fc0-456">Nesta etapa, você testa o pipeline soltando arquivos nas pastas de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="f2fc0-457">Vamos começar testando o pipeline com um arquivo por uma pasta de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="f2fc0-458">Na folha Data Factory do portal do Azure, clique em **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="f2fc0-459">Na exibição de diagrama, clique duas vezes no conjunto de dados de entrada: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="f2fc0-460">Você deve ver a folha **InputDataset** com todas as cinco fatias prontas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="f2fc0-461">Observe a **HORA DE INÍCIO DA FATIA** e a **HORA DE TÉRMINO DA FATIA** de cada fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="f2fc0-462">Na **Exibição de Diagrama**, clique em **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="f2fc0-463">Você deve ver que as cinco fatias de saída estarão no estado Pronto, se já tiverem sido produzidas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="f2fc0-464">Use o Portal do Azure para exibir as **tarefas** associadas às **fatias** e veja em qual VM cada fatia foi executada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="f2fc0-465">Confira a seção [Integração de Data Factory e Lote](#data-factory-and-batch-integration) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="f2fc0-466">Você deverá ver os arquivos de saída na `outputfolder` do `mycontainer` no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-466">You should see the output files in the `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="f2fc0-467">Você deve ver cinco arquivos de saída, um para cada fatia de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="f2fc0-468">Cada arquivo de saída deve ter conteúdo semelhante à seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="f2fc0-469">O diagrama a seguir ilustra como as fatias do Data Factory são mapeadas para tarefas em Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="f2fc0-470">Neste exemplo, uma fatia tem apenas uma execução.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="f2fc0-471">Agora, vamos tentar com vários arquivos em uma pasta.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="f2fc0-472">Crie arquivos: **file2.txt**, **file3.txt**, **file4.txt** e **file5.txt** com o mesmo conteúdo que o file.txt na pasta: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="f2fc0-473">Na pasta de saída, **exclua** o arquivo de saída: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="f2fc0-474">Agora, na folha **OutputDataset**, clique com o botão direito do mouse na fatia com **HORA DE INÍCIO DA FATIA** definida como **11/16/2015 01:00:00 AM (16/11/2015 01:00:00)** e clique em **Executar** para executar/processar novamente a fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="f2fc0-475">Agora, a fatia tem cinco arquivos em vez de um.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-475">Now, the slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="f2fc0-476">Depois que a fatia for executada e seu status for **Pronto**, verifique se no conteúdo do arquivo de saída existe esta fatia (**2015-11-16-01.txt**) na `outputfolder` do `mycontainer` no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="f2fc0-477">Deve haver uma linha para cada arquivo da fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="f2fc0-478">Se você não tiver excluído o arquivo de saída 2015-11-16-01.txt antes de tentar com arquivos de entrada, uma linha da execução da fatia anterior e cinco linhas da execução da fatia atual serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="f2fc0-479">Por padrão, o conteúdo é anexado ao arquivo de saída, se ele já existir.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="f2fc0-480">Integração de Data Factory e Lote</span><span class="sxs-lookup"><span data-stu-id="f2fc0-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="f2fc0-481">O serviço Data Factory cria um trabalho no Lote do Azure com o nome `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-481">The Data Factory service creates a job in Azure Batch with the name: `adf-poolname:job-xxx`.</span></span>

![Trabalhos de Azure Data Factory - Lote](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="f2fc0-483">Uma tarefa é criada no trabalho para cada execução de atividade de uma fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="f2fc0-484">Se houver 10 fatias prontas para serem processadas, 10 tarefas serão criadas no trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="f2fc0-485">Pode haver mais de uma fatia em execução em paralelo, se você tiver vários nós de computação no pool.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="f2fc0-486">Se o máximo de tarefas por nó de computação for definido como > 1, pode haver mais de uma fatia em execução na mesma computação.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="f2fc0-487">Neste exemplo, há cinco fatias, então cinco tarefas no Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="f2fc0-488">Com a **simultaneidade** definida como **5** no JSON do pipeline no Azure Data Factory e **Máximo de tarefas por VM** definido como **2** no pool do Azure Batch com **2** VMs, as tarefas são executadas rapidamente (verifique os horários de início e de término das tarefas).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="f2fc0-489">Use o portal para exibir o trabalho do Lote e suas tarefas associadas às **fatias** e veja em qual VM cada fatia foi executada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Tarefas do trabalho de Azure Data Factory - Lote](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="f2fc0-491">Depurar o pipeline</span><span class="sxs-lookup"><span data-stu-id="f2fc0-491">Debug the pipeline</span></span>
<span data-ttu-id="f2fc0-492">A depuração consiste em algumas técnicas básicas:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="f2fc0-493">Se a fatia de entrada não estiver definida como **Pronto**, confirme se a estrutura da pasta de entrada está correta e se file.txt existe nas pastas de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="f2fc0-494">No método **Execute** da atividade personalizada, use o objeto **IActivityLogger** para registrar informações que o ajudam a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="f2fc0-495">As mensagens registradas aparecerão no arquivo user\_0.log.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="f2fc0-496">Na folha **OutputDataset**, clique na fatia para ver a folha **FATIA DE DADOS** dessa fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="f2fc0-497">Você vê as **execuções de atividade** para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="f2fc0-498">Você deverá ver uma execução de atividade para a fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="f2fc0-499">Se você clicar em **Executar** na barra de comandos, poderá iniciar outra execução de atividade para a mesma fatia.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="f2fc0-500">Quando você clicar na execução da atividade, verá a folha **DETALHES DE EXECUÇÃO DA ATIVIDADE** com uma lista de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="f2fc0-501">Você vê mensagens registradas no arquivo **user\_0.log**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="f2fc0-502">Quando ocorrer um erro, você verá três execuções de atividade porque a contagem de repetições é definida como 3 no JSON do pipeline/atividade.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="f2fc0-503">Quando você clicar na execução da atividade, verá os arquivos de log que pode examinar para solucionar o erro.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="f2fc0-504">Na lista de arquivos de log, clique em **user-0.loo**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="f2fc0-505">No painel à direita, estão os resultados do uso do método **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="f2fc0-506">Verifique o system-0.log para quaisquer mensagens de erro e exceções do sistema.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="f2fc0-507">Inclua o arquivo **PDB** no arquivo zip para que os detalhes do erro tenham informações como **pilha de chamadas** quando ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="f2fc0-508">Todos os arquivos no arquivo zip para a atividade personalizada devem estar no **nível superior** sem subpastas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="f2fc0-509">Verifique se **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip) e **packageLinkedService** (devem apontar para o armazenamento de blobs do Azure que contém o arquivo zip) estão definidos com os valores corretos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="f2fc0-510">Se você corrigir um erro e quiser reprocessar a fatia, clique com o botão direito do mouse na fatia na folha **OutputDataset** e clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="f2fc0-511">Você verá um **contêiner** no Armazenamento de blobs do Azure chamado `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="f2fc0-512">Esse contêiner não é automaticamente excluído, mas você pode excluí-lo com segurança depois de concluir o teste da solução.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="f2fc0-513">Da mesma forma, a solução Data Factory cria um **trabalho** do Lote do Azure chamado `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="f2fc0-514">Você pode excluir esse trabalho depois de testar a solução, se desejar.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="f2fc0-515">A atividade personalizada não usa o arquivo **app.config** do seu pacote.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="f2fc0-516">Portanto, se seu código lê as cadeias de conexão do arquivo de configuração, ele não funciona no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="f2fc0-517">A prática recomendada ao usar o Azure Batch é armazenar os segredos em um **Azure KeyVault**, usar uma entidade de serviço com base em certificados para proteger o keyvault e distribuir o certificado para o pool do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="f2fc0-518">A atividade personalizada do .NET pode então acessar segredos no KeyVault no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="f2fc0-519">Essa é uma solução genérica e pode ser dimensionada para qualquer tipo de segredo, não apenas a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="f2fc0-520">Há uma solução alternativa mais fácil (mas não é uma prática recomendada): você pode criar um **serviço vinculado do SQL Azure** com configurações da cadeia de conexão, criar um conjunto de dados que usa o serviço vinculado e encadear o conjunto de dados como um conjunto de dados de entrada fictício para a atividade personalizada do .NET.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="f2fc0-521">Você pode então acessar a cadeia de conexão do serviço vinculado no código de atividade personalizada e isso deve funcionar bem no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="f2fc0-522">Estender o exemplo</span><span class="sxs-lookup"><span data-stu-id="f2fc0-522">Extend the sample</span></span>
<span data-ttu-id="f2fc0-523">Você pode estender este exemplo para saber mais sobre os recursos de Data Factory do Azure e Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="f2fc0-524">Por exemplo, para processar fatias em um intervalo de tempo diferente, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="f2fc0-525">Adicione as seguintes subpastas a `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09. Depois, coloque os arquivos de entrada nessas pastas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-525">Add the following subfolders in the `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="f2fc0-526">Altere a hora de término do pipeline de `2015-11-16T05:00:00Z` para `2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="f2fc0-527">Na **Exibição de Diagrama**, clique duas vezes em **InputDataset** e confirme se as fatias de entrada estão prontas.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="f2fc0-528">Clique duas vezes em **OuptutDataset** para ver o estado das fatias de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="f2fc0-529">Se estiverem no estado Pronto, verifique se os arquivos de saída estão na pasta de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-529">If they are in Ready state, check the output folder for the output files.</span></span>
2. <span data-ttu-id="f2fc0-530">Aumente ou diminua a configuração de **simultaneidade** para entender como ela afeta o desempenho da sua solução, especialmente o processamento que ocorre no Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="f2fc0-531">(Consulte a etapa 4: criar e executar o pipeline para obter mais informações sobre a configuração **simultaneidade** .)</span><span class="sxs-lookup"><span data-stu-id="f2fc0-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="f2fc0-532">Crie um pool com **Máximo de tarefas por VM**maior/menor.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="f2fc0-533">Para usar o novo pool criado, atualize o serviço vinculado do Azure Batch na solução do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="f2fc0-534">(Consulte a etapa 4: criar e executar o pipeline para obter mais informações sobre a configuração **Máximo de tarefas por VM** .)</span><span class="sxs-lookup"><span data-stu-id="f2fc0-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="f2fc0-535">Crie um pool do Lote do Azure com o recurso **dimensionar automaticamente** .</span><span class="sxs-lookup"><span data-stu-id="f2fc0-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="f2fc0-536">O dimensionamento automático de nós de computação em um pool do Lote do Azure é o ajuste dinâmico da potência de processamento usada pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="f2fc0-537">A fórmula de exemplo alcança o seguinte comportamento: quando o pool é inicialmente criado, ele começa com uma VM.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="f2fc0-538">A métrica de $PendingTasks define o número de tarefas em execução + estado ativo (em fila).</span><span class="sxs-lookup"><span data-stu-id="f2fc0-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="f2fc0-539">A fórmula localiza o número médio de tarefas pendentes nos últimos 180 segundos e define TargetDedicated adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="f2fc0-540">Isso garante que TargetDedicated nunca ultrapasse 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="f2fc0-541">Assim, o pool aumenta automaticamente conforme novas tarefas são enviadas e, conforme as tarefas são concluídas, as VMs se liberam uma a uma e são reduzidas pelo dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="f2fc0-542">startingNumberOfVMs e maxNumberofVMs podem ser ajustados às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="f2fc0-543">Fórmula de dimensionamento automático:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="f2fc0-544">Consulte [Dimensionar automaticamente os nós de computação em um pool de Lotes do Azure](../batch/batch-automatic-scaling.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="f2fc0-545">Se o pool estiver usando o padrão [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), o serviço Lote poderá demorar de 15 a 30 minutos para preparar a VM antes de executar a atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="f2fc0-546">Se o pool estiver usando um autoScaleEvaluationInterval diferente, o serviço de lote pode levar autoScaleEvaluationInterval + 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="f2fc0-547">Na solução de exemplo, o método **Execute** invoca o método **Calculate**, que processa uma fatia de dados de entrada para produzir uma fatia de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="f2fc0-548">Você pode escrever seu próprio método para processar dados de entrada e substituir a chamada do método Calculate no método Execute por uma chamada para o seu método.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="f2fc0-549">Próximas etapas: consumir os dados</span><span class="sxs-lookup"><span data-stu-id="f2fc0-549">Next steps: Consume the data</span></span>
<span data-ttu-id="f2fc0-550">Depois de processar dados, é possível consumi-lo com ferramentas online como o **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="f2fc0-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="f2fc0-551">Aqui estão links para ajudá-lo a entender o Power BI e como usá-lo no Azure:</span><span class="sxs-lookup"><span data-stu-id="f2fc0-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="f2fc0-552">Explorar um conjunto de dados no Power BI</span><span class="sxs-lookup"><span data-stu-id="f2fc0-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="f2fc0-553">Introdução ao Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="f2fc0-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="f2fc0-554">Atualizar dados no Power BI</span><span class="sxs-lookup"><span data-stu-id="f2fc0-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="f2fc0-555">Azure e Power BI - visão geral básica</span><span class="sxs-lookup"><span data-stu-id="f2fc0-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="f2fc0-556">Referências</span><span class="sxs-lookup"><span data-stu-id="f2fc0-556">References</span></span>
* [<span data-ttu-id="f2fc0-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f2fc0-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="f2fc0-558">Introdução ao serviço do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f2fc0-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="f2fc0-559">Introdução ao Data Factory do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="f2fc0-560">Usar atividades personalizadas em um pipeline do Data Factory do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="f2fc0-561">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="f2fc0-562">Noções básicas de Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="f2fc0-563">Visão geral dos recursos do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="f2fc0-564">Criar e gerenciar uma conta do Azure Batch no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="f2fc0-565">Introdução ao .NET da Biblioteca de Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="f2fc0-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
