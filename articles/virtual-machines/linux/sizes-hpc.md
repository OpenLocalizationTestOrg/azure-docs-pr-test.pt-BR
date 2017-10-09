---
title: tamanhos de VM do Linux do aaaAzure - HPC | Microsoft Docs
description: "Lista tamanhos diferentes de saudação disponíveis para máquinas virtuais no Azure de computação de alto e desempenho do Linux."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="8eaff-103">Tamanhos de VM Linux de computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="8eaff-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="8eaff-104">Instâncias compatíveis com RDMA</span><span class="sxs-lookup"><span data-stu-id="8eaff-104">RDMA-capable instances</span></span>
<span data-ttu-id="8eaff-105">Uma interface de rede para conectividade de acesso (RDMA) de memória direta remota de recurso de um subconjunto de instâncias de computação intensiva hello (H16r, H16mr, A8 e A9).</span><span class="sxs-lookup"><span data-stu-id="8eaff-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="8eaff-106">Além disso, esta interface é tamanhos de VM toohello padrão da rede do Azure interface tooother disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8eaff-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="8eaff-107">Essa interface permite Olá compatíveis com RDMA instâncias toocommunicate em uma rede InfiniBand, operando em taxas FDR para máquinas virtuais H16r e H16mr e taxas QDR para máquinas virtuais A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="8eaff-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="8eaff-108">Esses recursos RDMA podem melhorar a escalabilidade de saudação e o desempenho de aplicativos de Interface MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="8eaff-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="8eaff-109">Estes são os requisitos para máquinas virtuais de Linux compatíveis com RDMA tooaccess Olá rede RDMA do Azure:</span><span class="sxs-lookup"><span data-stu-id="8eaff-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="8eaff-110">**Distribuições** - você deve implantar as VMs de compatíveis com RDMA SUSE Linux Enterprise Server (SLES) ou imagens de Software não autorizado Wave (anteriormente conhecida como OpenLogic) com base em CentOS HPC em hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8eaff-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="8eaff-111">Olá Marketplace imagens suporte conectividade RDMA a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eaff-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="8eaff-112">SLES 12 SP1 para HPC ou SLES 12 SP1 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="8eaff-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="8eaff-113">HPC 7.3, 7.1, 6.8 ou 6.5 baseado em CentOS</span><span class="sxs-lookup"><span data-stu-id="8eaff-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="8eaff-114">Para VMs da série H, recomendamos o SLES 12 SP1 para imagem do HPC ou imagem do HPC 7.1 baseado em CentOS.</span><span class="sxs-lookup"><span data-stu-id="8eaff-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="8eaff-115">Em imagens de HPC com base em CentOS hello, atualizações de kernel estão desabilitadas no hello **yum** arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="8eaff-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="8eaff-116">Isso ocorre porque hello drivers Linux RDMA são distribuídos como um pacote RPM e atualizações de driver podem não funcionar se kernel Olá for atualizada.</span><span class="sxs-lookup"><span data-stu-id="8eaff-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="8eaff-117">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="8eaff-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="8eaff-118">Dependendo da imagem do Marketplace Olá escolher, instalação de licenciamento, separada, ou a configuração da Intel MPI ser necessário, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8eaff-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="8eaff-119">**SLES 12 SP1 para imagem HPC** -Intel MPI pacotes são distribuídos em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8eaff-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="8eaff-120">Instale executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eaff-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="8eaff-121">**Imagens do HPC baseado em CentOS** – O Intel MPI 5.1 já está instalado.</span><span class="sxs-lookup"><span data-stu-id="8eaff-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="8eaff-122">Configurações adicionais do sistema é necessário toorun de trabalhos MPI em máquinas virtuais em cluster.</span><span class="sxs-lookup"><span data-stu-id="8eaff-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="8eaff-123">Por exemplo, em um cluster de máquinas virtuais, você precisa tooestablish confiança entre Olá nós de computação.</span><span class="sxs-lookup"><span data-stu-id="8eaff-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="8eaff-124">Para as configurações típicas, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8eaff-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="8eaff-125">Considerações de topologia de rede</span><span class="sxs-lookup"><span data-stu-id="8eaff-125">Network topology considerations</span></span>
* <span data-ttu-id="8eaff-126">Em VMs Linux habilitadas para RDMA no Azure, Eth1 é reservado para o tráfego de rede RDMA.</span><span class="sxs-lookup"><span data-stu-id="8eaff-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="8eaff-127">Não altere as configurações de Eth1 ou todas as informações no arquivo de configuração de saudação referindo-se a rede toothis.</span><span class="sxs-lookup"><span data-stu-id="8eaff-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="8eaff-128">Eth0 é reservado para o tráfego de rede regular do Azure.</span><span class="sxs-lookup"><span data-stu-id="8eaff-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="8eaff-129">IP sobre InfiniBand (IB) não tem suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="8eaff-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="8eaff-130">Apenas RDMA sobre IB é compatível.</span><span class="sxs-lookup"><span data-stu-id="8eaff-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="8eaff-131">Usando o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="8eaff-131">Using HPC Pack</span></span>
<span data-ttu-id="8eaff-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), solução gratuita da Microsoft HPC cluster e o trabalho de gerenciamento, é uma opção para que instâncias de computação intensiva Olá toouse com Linux.</span><span class="sxs-lookup"><span data-stu-id="8eaff-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="8eaff-133">versões mais recentes de saudação do HPC Pack oferecem suporte a várias distribuições do Linux toorun em computação nós implantados em máquinas virtuais do Azure, gerenciado por um nó principal do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8eaff-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="8eaff-134">Conosco de computação compatíveis com RDMA Linux executando Intel MPI, HPC Pack pode agendar e executar aplicativos MPI Linux essa rede RDMA de saudação de acesso.</span><span class="sxs-lookup"><span data-stu-id="8eaff-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="8eaff-135">Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8eaff-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="8eaff-136">Outros tamanhos</span><span class="sxs-lookup"><span data-stu-id="8eaff-136">Other sizes</span></span>
- [<span data-ttu-id="8eaff-137">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="8eaff-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="8eaff-138">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="8eaff-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="8eaff-139">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="8eaff-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="8eaff-140">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="8eaff-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="8eaff-141">GPU</span><span class="sxs-lookup"><span data-stu-id="8eaff-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="8eaff-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8eaff-142">Next steps</span></span>

- <span data-ttu-id="8eaff-143">tooget iniciado Implantando e usando tamanhos de computação intensiva com o RDMA no Linux, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8eaff-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="8eaff-144">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8eaff-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




