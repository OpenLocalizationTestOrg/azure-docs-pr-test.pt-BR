---
title: "aaaResources de lote e HPC na nuvem do Azure da saudação | Microsoft Docs"
description: "Lista os recursos técnicos toohelp executar sua paralela em grande escala, lote e cargas de trabalho (HPC) no Azure de computação de alto desempenho."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="5d483-103">Big Compute no Azure: recursos técnicos para computação em lote e de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="5d483-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="5d483-104">Este é um guia tootechnical recursos toohelp que você executar o paralela em grande escala, lote e cargas de trabalho de computação de alto desempenho (HPC) no Azure.</span><span class="sxs-lookup"><span data-stu-id="5d483-104">This is a guide tootechnical resources toohelp you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="5d483-105">Estenda o lote existente ou toohello de cargas de trabalho do HPC nuvem do Azure, ou criar novas soluções de computação intensa usando os serviços de um intervalo do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d483-105">Extend your existing batch or HPC workloads toohello Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="5d483-106">Opções de soluções</span><span class="sxs-lookup"><span data-stu-id="5d483-106">Solutions options</span></span>
<span data-ttu-id="5d483-107">Saiba mais sobre opções de computação intensa no Azure e escolha a abordagem certa Olá para suas necessidades de negócios e a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5d483-107">Learn about Big Compute options in Azure, and choose hello right approach for your workload and business need.</span></span>

* [<span data-ttu-id="5d483-108">Soluções de HPC e Lote</span><span class="sxs-lookup"><span data-stu-id="5d483-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="5d483-109">Vídeo: Computação intensa na nuvem Olá com o Azure e HPC</span><span class="sxs-lookup"><span data-stu-id="5d483-109">Video: Big Compute in hello cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="5d483-110">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="5d483-110">Azure Batch</span></span>
<span data-ttu-id="5d483-111">[Lote](https://azure.microsoft.com/services/batch/) é um serviço de plataforma que torna mais fácil toocloud-habilitar seus aplicativos Linux e Windows e executados trabalhos sem configurar e gerenciar um cluster e o trabalho do Agendador.</span><span class="sxs-lookup"><span data-stu-id="5d483-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy toocloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="5d483-112">Use aplicativos de cliente Olá SDK toointegrate com lote do Azure por meio de vários idiomas, estágio tooAzure de dados e criar pipelines de execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5d483-112">Use hello SDK toointegrate client applications with Azure Batch through various languages, stage data tooAzure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="5d483-113">Documentação</span><span class="sxs-lookup"><span data-stu-id="5d483-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="5d483-114">Referência do [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) e da API [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)</span><span class="sxs-lookup"><span data-stu-id="5d483-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="5d483-115">[Biblioteca do .NET de gerenciamento do lote](https://msdn.microsoft.com/library/mt463120.aspx) </span><span class="sxs-lookup"><span data-stu-id="5d483-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="5d483-116">Tutoriais: Introdução à [Biblioteca de lote do Azure para .NET](batch-dotnet-get-started.md) e para o [cliente Python do Lot](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="5d483-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="5d483-117">Fórum do lote</span><span class="sxs-lookup"><span data-stu-id="5d483-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="5d483-118">Vídeos de lote</span><span class="sxs-lookup"><span data-stu-id="5d483-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="5d483-119">Soluções de cluster HPC</span><span class="sxs-lookup"><span data-stu-id="5d483-119">HPC cluster solutions</span></span>
<span data-ttu-id="5d483-120">Implantar ou estenda sua toorun de tooAzure de cluster Windows ou Linux HPC existente suas cargas de trabalho intensivas de computação.</span><span class="sxs-lookup"><span data-stu-id="5d483-120">Deploy or extend your existing Windows or Linux HPC cluster tooAzure toorun your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="5d483-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="5d483-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="5d483-122">O HPC Pack é a solução de HPC gratuita da Microsoft fundamentada nas tecnologias Microsoft Azure e Windows Server, capaz de executar cargas de trabalho do HPC no Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="5d483-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="5d483-123">Baixe o HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="5d483-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="5d483-124">Baixe a atualização 3 do HPC Pack 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5d483-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="5d483-125">Documentação</span><span class="sxs-lookup"><span data-stu-id="5d483-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="5d483-126">Opções de cluster HPC Pack no Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5d483-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="5d483-127">Intermitência tooAzure instâncias de trabalho com o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="5d483-127">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="5d483-128">Intermitência tooAzure em lotes com o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="5d483-128">Burst tooAzure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="5d483-129">Fóruns do Windows HPC</span><span class="sxs-lookup"><span data-stu-id="5d483-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="5d483-130">Soluções de cluster do Linux e OSS</span><span class="sxs-lookup"><span data-stu-id="5d483-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="5d483-131">Use esses toodeploy modelos do Azure Linux HPC clusters.</span><span class="sxs-lookup"><span data-stu-id="5d483-131">Use these Azure templates toodeploy Linux HPC clusters.</span></span>

* <span data-ttu-id="5d483-132">[Crie um cluster SLURM](https://azure.microsoft.com/documentation/templates/slurm/) e uma [postagem de blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="5d483-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="5d483-133">Crie um cluster de Torque</span><span class="sxs-lookup"><span data-stu-id="5d483-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="5d483-134">Modelos de grade de computação com o PBS Professional</span><span class="sxs-lookup"><span data-stu-id="5d483-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="5d483-135">Armazenamento HPC</span><span class="sxs-lookup"><span data-stu-id="5d483-135">HPC storage</span></span>
* [<span data-ttu-id="5d483-136">Sistemas de arquivos paralelos para o armazenamento HPC no Azure</span><span class="sxs-lookup"><span data-stu-id="5d483-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="5d483-137">Intel Cloud Edition for Software Lustre - Eval</span><span class="sxs-lookup"><span data-stu-id="5d483-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="5d483-138">BeeGFS no modelo do CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="5d483-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="5d483-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="5d483-139">Microsoft MPI</span></span>
<span data-ttu-id="5d483-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) é uma implementação da Microsoft da Message Passing Interface padrão para desenvolver e executar aplicativos paralelos na plataforma do Windows hello de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d483-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of hello Message Passing Interface standard for developing and running parallel applications on hello Windows platform.</span></span>

* [<span data-ttu-id="5d483-141">Baixe o MS-MPI</span><span class="sxs-lookup"><span data-stu-id="5d483-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="5d483-142">Referência do MS-MPI</span><span class="sxs-lookup"><span data-stu-id="5d483-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="5d483-143">Fórum do MPI</span><span class="sxs-lookup"><span data-stu-id="5d483-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="5d483-144">Instâncias com uso computacional intensivo</span><span class="sxs-lookup"><span data-stu-id="5d483-144">Compute-intensive instances</span></span>
<span data-ttu-id="5d483-145">Azure oferece uma [tamanhos de intervalo de VM](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), incluindo [H-série de computação intensa](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instâncias capazes de se conectar rede RDMA tooa back-end, toorun suas cargas de trabalho do Linux e do Windows HPC.</span><span class="sxs-lookup"><span data-stu-id="5d483-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting tooa back-end RDMA network, toorun your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="5d483-146">Configurar um aplicativo de MPI toorun Linux RDMA cluster</span><span class="sxs-lookup"><span data-stu-id="5d483-146">Set up a Linux RDMA cluster toorun MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="5d483-147">Configurar um cluster do Windows RDMA com aplicativos de MPI toorun Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="5d483-147">Set up a Windows RDMA cluster with Microsoft HPC Pack toorun MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="5d483-148">Para cargas de trabalho com uso intensivo de GPU, confira [Tamanhos de NC e NV](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="5d483-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="5d483-149">Exemplos e scripts</span><span class="sxs-lookup"><span data-stu-id="5d483-149">Samples and demos</span></span>
* [<span data-ttu-id="5d483-150">Exemplos de código do C# e Python para o Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="5d483-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="5d483-151">[Lote Shipyard](https://azure.github.io/batch-shipyard/) Kit de ferramentas para facilitar a implantação de estilo de lote Dockerized cargas de trabalho tooAzure em lotes</span><span class="sxs-lookup"><span data-stu-id="5d483-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads tooAzure Batch</span></span>
* <span data-ttu-id="5d483-152">Pacote R [doAzureParallel](http://www.github.com/Azure/doAzureParallel), criado com base no Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="5d483-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="5d483-153">Testar o SUSE Linux Enterprise Server para HPC</span><span class="sxs-lookup"><span data-stu-id="5d483-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="5d483-154">Serviços do Azure relacionados</span><span class="sxs-lookup"><span data-stu-id="5d483-154">Related Azure services</span></span>
* [<span data-ttu-id="5d483-155">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="5d483-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* <span data-ttu-id="5d483-156">
            [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)</span><span class="sxs-lookup"><span data-stu-id="5d483-156">[Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)</span></span>
* [<span data-ttu-id="5d483-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="5d483-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="5d483-158">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5d483-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="5d483-159">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="5d483-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="5d483-160">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="5d483-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="5d483-161">Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="5d483-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="5d483-162">Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="5d483-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="5d483-163">Funções</span><span class="sxs-lookup"><span data-stu-id="5d483-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="5d483-164">Plano gráfico da arquitetura</span><span class="sxs-lookup"><span data-stu-id="5d483-164">Architecture blueprints</span></span>
* <span data-ttu-id="5d483-165">[HPC e orquestração de dados usando o Lote do Azure, o Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) e o [artigo](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="5d483-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="5d483-166">Soluções do setor</span><span class="sxs-lookup"><span data-stu-id="5d483-166">Industry solutions</span></span>
* [<span data-ttu-id="5d483-167">Bancos e mercados de capitais</span><span class="sxs-lookup"><span data-stu-id="5d483-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="5d483-168">Simulações de engenharia</span><span class="sxs-lookup"><span data-stu-id="5d483-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="5d483-169">Relatos de clientes</span><span class="sxs-lookup"><span data-stu-id="5d483-169">Customer stories</span></span>
* [<span data-ttu-id="5d483-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="5d483-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="5d483-171">d3View</span><span class="sxs-lookup"><span data-stu-id="5d483-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="5d483-172">Ludwig Institute of Cancer Research</span><span class="sxs-lookup"><span data-stu-id="5d483-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="5d483-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="5d483-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="5d483-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="5d483-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="5d483-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="5d483-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="5d483-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="5d483-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="5d483-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="5d483-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="5d483-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="5d483-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="5d483-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d483-179">Next steps</span></span>
* <span data-ttu-id="5d483-180">Para lançamentos mais recentes de Olá, consulte Olá [blog da equipe do Microsoft HPC e lote](http://blogs.technet.com/b/windowshpc/) e hello [blog Azure](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="5d483-180">For hello latest announcements, see hello [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and hello [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="5d483-181">Consulte também [o que há de novo no lote](https://azure.microsoft.com/updates/?service=batch) ou assinar toohello [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="5d483-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe toohello [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

