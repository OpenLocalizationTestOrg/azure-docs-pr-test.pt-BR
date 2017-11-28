---
title: "Tamanhos de VM Windows do Azure — HPC | Microsoft Docs"
description: "Lista os diferentes tamanhos disponíveis para máquinas virtuais de computação de alto desempenho Windows no Azure."
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
ms.openlocfilehash: a0596d134e9c26877848f93d72f35bfd2c957570
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="66557-103">Tamanhos de VM de computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="66557-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="66557-104">Instâncias compatíveis com RDMA</span><span class="sxs-lookup"><span data-stu-id="66557-104">RDMA-capable instances</span></span>
<span data-ttu-id="66557-105">Um subconjunto das instâncias de computação intensiva (H16r, H16mr, A8 e A9) apresenta um adaptador de rede para conectividade RDMA (acesso remoto direto à memória).</span><span class="sxs-lookup"><span data-stu-id="66557-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="66557-106">Essa interface é além do adaptador de rede do Azure padrão disponível para outros tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="66557-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="66557-107">Essa interface permite que instâncias compatíveis com RDMA se comuniquem em uma rede InfiniBand, operando em taxas FDR para máquinas virtuais H16r e H16mr e taxas QDR para máquinas virtuais A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="66557-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="66557-108">Esses recursos RDMA podem melhorar a escalabilidade e o desempenho de aplicativos MPI (Interface de Transmissão de Mensagens).</span><span class="sxs-lookup"><span data-stu-id="66557-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="66557-109">Estes são os requisitos para VMs Windows compatíveis com RDMA acessarem a rede RDMA do Azure:</span><span class="sxs-lookup"><span data-stu-id="66557-109">Following are requirements for RDMA-capable Windows VMs to access the Azure RDMA network:</span></span> 

* <span data-ttu-id="66557-110">**Sistema operacional**</span><span class="sxs-lookup"><span data-stu-id="66557-110">**Operating system**</span></span>
  
  <span data-ttu-id="66557-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="66557-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="66557-112">Atualmente, o Windows Server 2016 não dá suporte à conectividade RDMA no Azure.</span><span class="sxs-lookup"><span data-stu-id="66557-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="66557-113">**Conjunto de disponibilidade ou serviço de nuvem** – Implante as VMs compatíveis com RDMA no mesmo conjunto de disponibilidade (se usar o modelo de implantação do Azure Resource Manager) ou no mesmo serviço de nuvem (se usar o modelo de implantação clássica).</span><span class="sxs-lookup"><span data-stu-id="66557-113">**Availability set or cloud service** – Deploy the RDMA-capable VMs in the same availability set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model).</span></span> <span data-ttu-id="66557-114">Se você usar o Lote do Azure, as VMs compatíveis com RDMA deverão estar no mesmo pool.</span><span class="sxs-lookup"><span data-stu-id="66557-114">If you use Azure Batch, the RDMA-capable VMs must be in the same pool.</span></span>

* <span data-ttu-id="66557-115">**MPI** – Microsoft MPI (MS-MPI) 2012 R2 ou posterior, Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="66557-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="66557-116">Implementações de MPI com suporte usam a interface direta da rede Microsoft para comunicação entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="66557-116">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 

* <span data-ttu-id="66557-117">**Espaço de endereço de rede RDMA** - A rede RDMA no Azure reserva o espaço de endereço 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="66557-117">**RDMA network address space** - The RDMA network in Azure reserves the address space 172.16.0.0/16.</span></span> <span data-ttu-id="66557-118">Para executar aplicativos MPI em instâncias implantadas em uma rede virtual do Azure, verifique se o espaço do endereço de rede virtual não se sobrepõe à rede RDMA.</span><span class="sxs-lookup"><span data-stu-id="66557-118">To run MPI applications on instances deployed in an Azure virtual network, make sure that the virtual network address space does not overlap the RDMA network.</span></span>

* <span data-ttu-id="66557-119">**Extensão de VM HpcVmDrivers** – Em VMs compatíveis com RDMA, é necessário adicionar a extensão HpcVmDrivers para instalar drivers de dispositivo de rede do Windows para conectividade RDMA.</span><span class="sxs-lookup"><span data-stu-id="66557-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add the HpcVmDrivers extension to install Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="66557-120">(Em algumas implantações das instâncias A8 e A9, a extensão HpcVmDrivers é adicionada automaticamente.) Para adicionar a extensão de VM a uma VM, use cmdlets do [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66557-120">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) To add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="66557-121">O comando a seguir instala a versão 1.1 mais recente da extensão HpcVMDrivers em uma VM compatível com RDMA existente denominada *myVM* implantada no grupo de recursos chamada *myResourceGroup* na região *Oeste dos EUA*:</span><span class="sxs-lookup"><span data-stu-id="66557-121">The following command installs the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in the resource group named *myResourceGroup* in the *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="66557-122">Para obter mais informações, consulte [Recursos e extensões da máquina virtual](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66557-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="66557-123">Também é possível trabalhar com extensões de VMs implantadas no [modelo de implantação clássico](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="66557-123">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="66557-124">Usando o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="66557-124">Using HPC Pack</span></span>

<span data-ttu-id="66557-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), a solução de gerenciamento de trabalho e cluster HPC gratuita da Microsoft, é uma opção para criar um cluster de cálculo no Azure para executar aplicativos MPI baseados no Windows e outras cargas de trabalho de HPC.</span><span class="sxs-lookup"><span data-stu-id="66557-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="66557-126">O HPC Pack 2012 R2 e versões posteriores incluem um ambiente de tempo de execução para MS-MPI que usa a rede RDMA do Azure quando implantado em VMs compatíveis com RDMA.</span><span class="sxs-lookup"><span data-stu-id="66557-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="66557-127">Outros tamanhos</span><span class="sxs-lookup"><span data-stu-id="66557-127">Other sizes</span></span>
- [<span data-ttu-id="66557-128">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="66557-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="66557-129">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="66557-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="66557-130">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="66557-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="66557-131">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="66557-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="66557-132">GPU otimizada</span><span class="sxs-lookup"><span data-stu-id="66557-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="66557-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66557-133">Next steps</span></span>

- <span data-ttu-id="66557-134">Para obter listas de verificação para usar as instâncias de computação intensiva com o HPC Pack no Windows Server, veja [Configurar um cluster de RDMA do Windows com o HPC Pack para executar aplicativos MPI](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66557-134">For checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="66557-135">Para usar instâncias de computação intensiva para executar aplicativos MPI com o Lote do Azure, consulte [Usar tarefas de várias instâncias para executar aplicativos MPI (Interface de Transmissão de Mensagens) no Lote do Azure](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="66557-135">To use compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="66557-136">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="66557-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




