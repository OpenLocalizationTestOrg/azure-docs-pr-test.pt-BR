---
title: "Opções de cluster de HPC Pack aaaLinux na nuvem Olá | Microsoft Docs"
description: "Saiba mais sobre opções com Microsoft HPC Pack toocreate e gerenciar um Linux computação de alto desempenho cluster (HPC) em Olá nuvem do Azure"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="62593-103">As opções com HPC Pack toocreate e gerenciar um cluster HPC no Azure para cargas de trabalho do Linux</span><span class="sxs-lookup"><span data-stu-id="62593-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="62593-104">Este artigo se concentra em cargas de trabalho de opções toouse HPC Pack toorun Linux.</span><span class="sxs-lookup"><span data-stu-id="62593-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="62593-105">Também há opções para executar [cargas de trabalho de HPC do Windows com o HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62593-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="62593-106">Executar um cluster HPC Pack em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="62593-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="62593-107">Modelos do Azure</span><span class="sxs-lookup"><span data-stu-id="62593-107">Azure templates</span></span>
* <span data-ttu-id="62593-108">(GitHub) [Modelos de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="62593-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="62593-109">(Marketplace) [Cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="62593-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="62593-110">(Início rápido) [Criar um cluster HPC Pack com nós de computação do Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="62593-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="62593-111">Script de implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="62593-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="62593-112">Criar um cluster de HPC Linux com hello script de implantação IaaS do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="62593-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="62593-113">Tutoriais</span><span class="sxs-lookup"><span data-stu-id="62593-113">Tutorials</span></span>
* [<span data-ttu-id="62593-114">Tutorial: introdução a nós de computação Linux em um cluster de HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="62593-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="62593-115">Tutorial: executar o NAMD com o Microsoft HPC Pack em nós de computação Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="62593-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="62593-116">Tutorial: executar OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="62593-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="62593-117">Tutorial: executar o STAR-CCM+ com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="62593-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="62593-118">Gerenciamento de clusters</span><span class="sxs-lookup"><span data-stu-id="62593-118">Cluster management</span></span>
* [<span data-ttu-id="62593-119">Enviar o cluster de HPC Pack tooan trabalhos no Azure</span><span class="sxs-lookup"><span data-stu-id="62593-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="62593-120">Gerenciamento de trabalho no HPC Pack</span><span class="sxs-lookup"><span data-stu-id="62593-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="62593-121">Criar clusters de RDMA para cargas de trabalho MPI</span><span class="sxs-lookup"><span data-stu-id="62593-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="62593-122">Tutorial: executar OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="62593-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="62593-123">Configurar um aplicativo de MPI toorun Linux RDMA cluster</span><span class="sxs-lookup"><span data-stu-id="62593-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

