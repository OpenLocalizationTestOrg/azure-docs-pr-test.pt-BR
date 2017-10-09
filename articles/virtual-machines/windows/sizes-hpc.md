---
title: tamanhos de VM do Windows aaaAzure - HPC | Microsoft Docs
description: "Lista tamanhos diferentes de saudação disponíveis para máquinas virtuais no Azure de computação de alto e desempenho do Windows."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="0fc25-103">Tamanhos de VM de computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="0fc25-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="0fc25-104">Instâncias compatíveis com RDMA</span><span class="sxs-lookup"><span data-stu-id="0fc25-104">RDMA-capable instances</span></span>
<span data-ttu-id="0fc25-105">Uma interface de rede para conectividade de acesso (RDMA) de memória direta remota de recurso de um subconjunto de instâncias de computação intensiva hello (H16r, H16mr, A8 e A9).</span><span class="sxs-lookup"><span data-stu-id="0fc25-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="0fc25-106">Além disso, esta interface é tamanhos de VM toohello padrão da rede do Azure interface tooother disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0fc25-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="0fc25-107">Essa interface permite Olá compatíveis com RDMA instâncias toocommunicate em uma rede InfiniBand, operando em taxas FDR para máquinas virtuais H16r e H16mr e taxas QDR para máquinas virtuais A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="0fc25-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="0fc25-108">Esses recursos RDMA podem melhorar a escalabilidade de saudação e o desempenho de aplicativos de Interface MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="0fc25-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="0fc25-109">Estes são os requisitos para máquinas virtuais do Windows compatíveis com RDMA tooaccess Olá rede RDMA do Azure:</span><span class="sxs-lookup"><span data-stu-id="0fc25-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="0fc25-110">**Sistema operacional**</span><span class="sxs-lookup"><span data-stu-id="0fc25-110">**Operating system**</span></span>
  
  <span data-ttu-id="0fc25-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0fc25-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0fc25-112">Atualmente, o Windows Server 2016 não dá suporte à conectividade RDMA no Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc25-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="0fc25-113">**Conjunto de disponibilidade ou serviço de nuvem** – implantar VMs de saudação compatíveis com RDMA na Olá mesmo conjunto (quando você usa o modelo de implantação do Azure Resource Manager Olá) de disponibilidade ou Olá mesmo serviço de nuvem (quando você usa o modelo de implantação clássico Olá).</span><span class="sxs-lookup"><span data-stu-id="0fc25-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="0fc25-114">Se você usar o lote do Azure, Olá VMs compatíveis com RDMA deve estar no hello mesmo pool.</span><span class="sxs-lookup"><span data-stu-id="0fc25-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="0fc25-115">**MPI** – Microsoft MPI (MS-MPI) 2012 R2 ou posterior, Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="0fc25-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="0fc25-116">Implementações de MPI com suporte usam toocommunicate de interface direta da rede Microsoft hello entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="0fc25-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="0fc25-117">**Espaço de endereço de rede RDMA** -rede RDMA Olá no Azure reserva Olá endereço espaço 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="0fc25-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="0fc25-118">toorun aplicativos de MPI em instâncias implantadas em uma rede virtual do Azure, certifique-se de que espaço de endereço de rede virtual Olá não se sobreponha a rede RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="0fc25-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="0fc25-119">**Extensão HpcVmDrivers VM** -em VMs compatíveis com RDMA, você deve adicionar Olá HpcVmDrivers extensão tooinstall rede drivers de dispositivo Windows para a conectividade RDMA.</span><span class="sxs-lookup"><span data-stu-id="0fc25-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="0fc25-120">(Em certas implantações de instâncias A8 e A9, Olá extensão HpcVmDrivers é adicionada automaticamente.) tooadd Olá VM extensão tooa VM, você pode usar [Azure PowerShell](/powershell/azure/overview) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0fc25-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="0fc25-121">Olá instala hello mais recente extensão HpcVMDrivers de versão 1.1 em uma VM compatíveis com RDMA existente chamada de comando a seguir *myVM* implantada no grupo de recursos de saudação chamado *myResourceGroup* em Olá  *Oeste dos EUA* região:</span><span class="sxs-lookup"><span data-stu-id="0fc25-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="0fc25-122">Para obter mais informações, consulte [Recursos e extensões da máquina virtual](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0fc25-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0fc25-123">Você também pode trabalhar com extensões para as VMs implantadas em Olá [modelo de implantação clássico](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="0fc25-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="0fc25-124">Usando o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0fc25-124">Using HPC Pack</span></span>

<span data-ttu-id="0fc25-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), solução gratuita da Microsoft HPC cluster e o trabalho de gerenciamento, é uma opção para toocreate um cluster de computação em aplicativos de MPI baseados no Windows Azure toorun e outras cargas de trabalho do HPC.</span><span class="sxs-lookup"><span data-stu-id="0fc25-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="0fc25-126">HPC Pack 2012 R2 e versões posteriores incluem um ambiente de tempo de execução para MS-MPI que usa a rede de RDMA do Azure hello quando implantado em VMs compatíveis com RDMA.</span><span class="sxs-lookup"><span data-stu-id="0fc25-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="0fc25-127">Outros tamanhos</span><span class="sxs-lookup"><span data-stu-id="0fc25-127">Other sizes</span></span>
- [<span data-ttu-id="0fc25-128">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="0fc25-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="0fc25-129">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="0fc25-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="0fc25-130">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="0fc25-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="0fc25-131">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="0fc25-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="0fc25-132">GPU otimizada</span><span class="sxs-lookup"><span data-stu-id="0fc25-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="0fc25-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fc25-133">Next steps</span></span>

- <span data-ttu-id="0fc25-134">Para instâncias de computação intensiva listas de verificação toouse Olá com o HPC Pack no Windows Server, consulte [configurar um cluster do Windows RDMA com aplicativos de MPI do HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0fc25-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="0fc25-135">instâncias de computação intensiva toouse ao executar aplicativos MPI com o lote do Azure, consulte [Use a instância várias tarefas toorun passando Interface aplicativos MPI (Message) em lote do Azure](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="0fc25-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="0fc25-136">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc25-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




