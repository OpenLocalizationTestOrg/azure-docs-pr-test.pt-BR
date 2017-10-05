---
title: "Opções de cluster do Windows HPC Pack na nuvem | Microsoft Docs"
description: "Saiba mais sobre as opções do Microsoft HPC Pack para criar e gerenciar um cluster HPC (computação de alto desempenho) do Windows na nuvem do Azure"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 96a5520d8440af7d8a880c2675a5d4eb4121e9ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="662e2-103">Opções com o HPC Pack para criar e gerenciar um cluster HPC do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-103">Options with HPC Pack to create and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="662e2-104">Este artigo se concentra nas opções para criar clusters HPC Pack para executar cargas de trabalho do Windows.</span><span class="sxs-lookup"><span data-stu-id="662e2-104">This article focuses on options to create HPC Pack clusters to run Windows workloads.</span></span> <span data-ttu-id="662e2-105">Também há opções para a criação de clusters HPC Pack para executar [cargas de trabalho HPC do Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="662e2-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="662e2-106">Executar um cluster HPC Pack em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="662e2-107">Modelos do Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-107">Azure templates</span></span>
* <span data-ttu-id="662e2-108">(GitHub) [Modelos de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="662e2-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="662e2-109">(Marketplace) [Cluster HPC Pack para cargas de trabalho do Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="662e2-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="662e2-110">(Marketplace) [Cluster HPC Pack para cargas de trabalho do Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="662e2-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="662e2-111">(Guia de início rápido) [Criar um cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="662e2-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="662e2-112">(Guia de início rápido) [Criar um cluster HPC com uma imagem personalizada de nó de computação](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="662e2-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="662e2-113">Imagens de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-113">Azure VM images</span></span>
* [<span data-ttu-id="662e2-114">Nó principal do HPC Pack 2016 no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="662e2-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="662e2-115">Nó de computação do HPC Pack 2016 no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="662e2-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="662e2-116">Nó principal do HPC Pack 2016 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="662e2-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="662e2-117">Nó de computação do HPC Pack 2016 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="662e2-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="662e2-118">Nó principal do HPC Pack 2012 R2 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="662e2-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="662e2-119">Nó de computação do HPC Pack 2012 R2 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="662e2-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="662e2-120">Nó de computação do HPC Pack com Excel no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="662e2-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="662e2-121">Script de implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="662e2-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="662e2-122">Criar um cluster HPC com o script de implantação de IaaS do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="662e2-122">Create an HPC cluster with the HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="662e2-123">Tutoriais</span><span class="sxs-lookup"><span data-stu-id="662e2-123">Tutorials</span></span>
* [<span data-ttu-id="662e2-124">Tutorial: Implantar um cluster HPC Pack 2016 no Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="662e2-125">Tutorial: Introdução a um cluster de HPC Pack no Azure para executar cargas de trabalho do Excel e SOA</span><span class="sxs-lookup"><span data-stu-id="662e2-125">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a><span data-ttu-id="662e2-126">Implantação manual com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-126">Manual deployment with the Azure portal</span></span>
* [<span data-ttu-id="662e2-127">Configurar o nó de cabeçalho de um cluster HPC Pack em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-127">Set up the head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="662e2-128">Gerenciamento de clusters</span><span class="sxs-lookup"><span data-stu-id="662e2-128">Cluster management</span></span>
* [<span data-ttu-id="662e2-129">Gerenciar nós de computação em um cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="662e2-130">Aumentar ou reduzir os recursos de computação do Azure em um cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="662e2-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="662e2-131">Enviar trabalhos para um cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-131">Submit jobs to an HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="662e2-132">Gerenciamento de trabalho no HPC Pack</span><span class="sxs-lookup"><span data-stu-id="662e2-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="662e2-133">Gerenciar um cluster HPC Pack no Azure usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="662e2-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a><span data-ttu-id="662e2-134">Adicionar nós de função de trabalho a um cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="662e2-134">Add worker role nodes to an HPC Pack cluster</span></span>
* [<span data-ttu-id="662e2-135">Aumento para instâncias de trabalho do Azure com o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="662e2-135">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="662e2-136">Tutorial: Configurar um cluster híbrido com o HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="662e2-137">Adicionar nós de “disparo contínuo” do Azure a um nó de cabeçalho do HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-137">Add Azure "burst" nodes to an HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="662e2-138">Integrar ao lote do Azure</span><span class="sxs-lookup"><span data-stu-id="662e2-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="662e2-139">Aumento para o lote do Azure com o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="662e2-139">Burst to Azure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="662e2-140">Criar clusters de RDMA para cargas de trabalho MPI</span><span class="sxs-lookup"><span data-stu-id="662e2-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="662e2-141">Configurar um cluster de RDMA do Windows com o HPC Pack para executar aplicativos MPI</span><span class="sxs-lookup"><span data-stu-id="662e2-141">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

