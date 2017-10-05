---
title: "Tamanhos de VM Linux do Azure — HPC | Microsoft Docs"
description: "Lista os diferentes tamanhos disponíveis para máquinas virtuais de computação de alto desempenho Linux no Azure."
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
ms.openlocfilehash: b7a3844ce86b4efac8a4fc3c2540e7b6460873a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="fd8d7-103">Tamanhos de VM Linux de computação de alto desempenho</span><span class="sxs-lookup"><span data-stu-id="fd8d7-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="fd8d7-104">Instâncias compatíveis com RDMA</span><span class="sxs-lookup"><span data-stu-id="fd8d7-104">RDMA-capable instances</span></span>
<span data-ttu-id="fd8d7-105">Um subconjunto das instâncias de computação intensiva (H16r, H16mr, A8 e A9) apresenta um adaptador de rede para conectividade RDMA (acesso remoto direto à memória).</span><span class="sxs-lookup"><span data-stu-id="fd8d7-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="fd8d7-106">Essa interface é além do adaptador de rede do Azure padrão disponível para outros tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="fd8d7-107">Essa interface permite que instâncias compatíveis com RDMA se comuniquem em uma rede InfiniBand, operando em taxas FDR para máquinas virtuais H16r e H16mr e taxas QDR para máquinas virtuais A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="fd8d7-108">Esses recursos RDMA podem melhorar a escalabilidade e o desempenho de aplicativos MPI (Interface de Transmissão de Mensagens).</span><span class="sxs-lookup"><span data-stu-id="fd8d7-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="fd8d7-109">Estes são os requisitos para VMs Linux compatíveis com RDMA acessarem a rede RDMA do Azure:</span><span class="sxs-lookup"><span data-stu-id="fd8d7-109">Following are requirements for RDMA-capable Linux VMs to access the Azure RDMA network:</span></span>
 
* <span data-ttu-id="fd8d7-110">**Distribuições** – Você deve implantar as VMs de imagens HPC com base em Rogue Wave Software (anteriormente OpenLogic) CentOS ou SLES (SUSE Linux Enterprise Server) compatíveis com RDMA no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="fd8d7-111">As seguintes imagens do Marketplace dão suporte à conectividade RDMA:</span><span class="sxs-lookup"><span data-stu-id="fd8d7-111">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="fd8d7-112">SLES 12 SP1 para HPC ou SLES 12 SP1 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="fd8d7-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="fd8d7-113">HPC 7.3, 7.1, 6.8 ou 6.5 baseado em CentOS</span><span class="sxs-lookup"><span data-stu-id="fd8d7-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="fd8d7-114">Para VMs da série H, recomendamos o SLES 12 SP1 para imagem do HPC ou imagem do HPC 7.1 baseado em CentOS.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="fd8d7-115">Nas imagens do HPC baseado em CentOS, as atualizações de kernel estão desabilitadas no arquivo de configuração **yum** .</span><span class="sxs-lookup"><span data-stu-id="fd8d7-115">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="fd8d7-116">Isso ocorre porque os drivers RDMA do Linux são distribuídos como um pacote RPM, e as atualizações de driver poderão não funcionar caso o kernel seja atualizado.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-116">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="fd8d7-117">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="fd8d7-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="fd8d7-118">Dependendo da imagem do Marketplace escolhida, podem ser necessários licenciamento, instalação ou configuração separada do Intel MPI, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="fd8d7-118">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="fd8d7-119">**SLES 12 SP1 para imagem HPC** – pacotes Intel MPI são distribuídos na VM.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="fd8d7-120">Instale o executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="fd8d7-120">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="fd8d7-121">**Imagens do HPC baseado em CentOS** – O Intel MPI 5.1 já está instalado.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="fd8d7-122">Configurações adicionais do sistema são necessárias para executar trabalhos MPI em máquinas virtuais clusterizadas.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-122">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="fd8d7-123">Por exemplo, em um cluster de máquinas virtuais, você precisa estabelecer confiança entre os nós de computação.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-123">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="fd8d7-124">Para configurações típicas, consulte [Configurar um cluster de RDMA do Linux para executar aplicativos MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="fd8d7-124">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="fd8d7-125">Considerações de topologia de rede</span><span class="sxs-lookup"><span data-stu-id="fd8d7-125">Network topology considerations</span></span>
* <span data-ttu-id="fd8d7-126">Em VMs Linux habilitadas para RDMA no Azure, Eth1 é reservado para o tráfego de rede RDMA.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="fd8d7-127">Não altere as configurações de Eth1 ou as informações no arquivo de configuração que se refere a essa rede.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-127">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="fd8d7-128">Eth0 é reservado para o tráfego de rede regular do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="fd8d7-129">IP sobre InfiniBand (IB) não tem suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="fd8d7-130">Apenas RDMA sobre IB é compatível.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="fd8d7-131">Usando o HPC Pack</span><span class="sxs-lookup"><span data-stu-id="fd8d7-131">Using HPC Pack</span></span>
<span data-ttu-id="fd8d7-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), a solução de gerenciamento de trabalho e cluster HPC gratuita da Microsoft, é uma opção para usar as instâncias de computação intensiva com o Linux.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="fd8d7-133">As últimas versões do HPC Pack dão suporte a várias distribuições Linux para execução em nós de computação implantados nas VMs do Azure, gerenciados por um nó de cabeçalho do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-133">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="fd8d7-134">Com os nós de computação Linux compatíveis com RDMA executando o Intel MPI, o HPC Pack pode agendar e executar os aplicativos Linux MPI que acessam a rede RDMA.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="fd8d7-135">Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fd8d7-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="fd8d7-136">Outros tamanhos</span><span class="sxs-lookup"><span data-stu-id="fd8d7-136">Other sizes</span></span>
- [<span data-ttu-id="fd8d7-137">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="fd8d7-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="fd8d7-138">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="fd8d7-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="fd8d7-139">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="fd8d7-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="fd8d7-140">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="fd8d7-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="fd8d7-141">GPU</span><span class="sxs-lookup"><span data-stu-id="fd8d7-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="fd8d7-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd8d7-142">Next steps</span></span>

- <span data-ttu-id="fd8d7-143">Para se familiarizar com a implantação e o uso dos tamanhos de computação intensiva com o RDMA no Linux, veja [Configurar um cluster de RDMA do Linux para executar aplicativos MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fd8d7-143">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="fd8d7-144">Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd8d7-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




