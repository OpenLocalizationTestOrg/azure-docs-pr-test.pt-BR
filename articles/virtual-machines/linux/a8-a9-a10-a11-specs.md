---
title: "computação intensa aaaAbout VMs com Linux | Microsoft Docs"
description: "Obter informações básicas e considerações para o uso de tamanhos de computação intensa H-series e A8, A9, A10 e A11 Olá para VMs do Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="d8702-103">Sobre as VMs da série H e da série A de computação intensiva para Linux</span><span class="sxs-lookup"><span data-stu-id="d8702-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="d8702-104">Eis aqui as informações de plano de fundo e algumas considerações para usar o hello mais recente do Azure H-series e Olá tamanhos A8, A9, A10 e A11 anteriores, também conhecido como *com computação intensiva* instâncias.</span><span class="sxs-lookup"><span data-stu-id="d8702-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="d8702-105">Este artigo ressalta o uso desses tamanhos para VMs Linux.</span><span class="sxs-lookup"><span data-stu-id="d8702-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="d8702-106">Você também pode usá-los para [VMs Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d8702-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="d8702-107">Para obter as especificações básicas, as capacidades de armazenamento e os detalhes de disco, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d8702-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="d8702-108">Rede RDMA toohello acesso</span><span class="sxs-lookup"><span data-stu-id="d8702-108">Access toohello RDMA network</span></span>
<span data-ttu-id="d8702-109">Você pode criar clusters de VMs Linux compatíveis com RDMA que executem uma saudação distribuições de Linux HPC com suporte e uma vantagem de tootake de implementação MPI com suporte de rede de RDMA do Azure Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8702-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="d8702-110">Consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para opções de implantação e as etapas de configuração de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d8702-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="d8702-111">**Distribuições** - você deve implantar as VMs de compatíveis com RDMA SUSE Linux Enterprise Server (SLES) ou imagens de Software não autorizado Wave (anteriormente conhecida como OpenLogic) com base em CentOS HPC em hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d8702-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="d8702-112">Olá Marketplace imagens suporte conectividade RDMA a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8702-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="d8702-113">SLES 12 SP1 para HPC, SLES 12 SP1 para HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="d8702-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="d8702-114">HPC baseado em CentOS 7.1, HPC baseado em CentOS 6.5</span><span class="sxs-lookup"><span data-stu-id="d8702-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="d8702-115">Para VMs da série H, recomendamos o SLES 12 SP1 para imagem do HPC ou imagem do HPC 7.1 baseado em CentOS.</span><span class="sxs-lookup"><span data-stu-id="d8702-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="d8702-116">Em imagens de HPC com base em CentOS hello, atualizações de kernel estão desabilitadas no hello **yum** arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="d8702-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="d8702-117">Isso ocorre porque hello drivers Linux RDMA são distribuídos como um pacote RPM e atualizações de driver podem não funcionar se kernel Olá for atualizada.</span><span class="sxs-lookup"><span data-stu-id="d8702-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="d8702-118">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="d8702-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="d8702-119">Dependendo da imagem do Marketplace Olá escolher, instalação de licenciamento, separada, ou a configuração da Intel MPI ser necessário, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d8702-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="d8702-120">**SLES 12 SP1 para imagem HPC** -Intel MPI pacotes são distribuídos em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d8702-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="d8702-121">Instale executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8702-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="d8702-122">**Imagens do HPC baseado em CentOS** – O Intel MPI 5.1 já está instalado.</span><span class="sxs-lookup"><span data-stu-id="d8702-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="d8702-123">Configurações adicionais do sistema é necessário toorun de trabalhos MPI em máquinas virtuais em cluster.</span><span class="sxs-lookup"><span data-stu-id="d8702-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="d8702-124">Por exemplo, em um cluster de máquinas virtuais, você precisa tooestablish confiança entre Olá nós de computação.</span><span class="sxs-lookup"><span data-stu-id="d8702-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="d8702-125">Para as configurações típicas, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d8702-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="d8702-126">Considerações para HPC Pack e Linux</span><span class="sxs-lookup"><span data-stu-id="d8702-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="d8702-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), solução gratuita da Microsoft HPC cluster e o trabalho de gerenciamento, fornece uma opção para instâncias de computação intensiva Olá toouse com Linux.</span><span class="sxs-lookup"><span data-stu-id="d8702-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="d8702-128">versões mais recentes de saudação do HPC Pack oferecem suporte a várias distribuições do Linux toorun em computação nós implantados em máquinas virtuais do Azure, gerenciado por um nó principal do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d8702-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="d8702-129">Conosco de computação compatíveis com RDMA Linux executando Intel MPI, HPC Pack pode agendar e executar aplicativos MPI Linux essa rede RDMA de saudação de acesso.</span><span class="sxs-lookup"><span data-stu-id="d8702-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="d8702-130">tooget iniciado, consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d8702-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="d8702-131">Considerações de topologia de rede</span><span class="sxs-lookup"><span data-stu-id="d8702-131">Network topology considerations</span></span>
* <span data-ttu-id="d8702-132">Em VMs Linux habilitadas para RDMA no Azure, Eth1 é reservado para o tráfego de rede RDMA.</span><span class="sxs-lookup"><span data-stu-id="d8702-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="d8702-133">Não altere as configurações de Eth1 ou todas as informações no arquivo de configuração de saudação referindo-se a rede toothis.</span><span class="sxs-lookup"><span data-stu-id="d8702-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="d8702-134">Eth0 é reservado para o tráfego de rede regular do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8702-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="d8702-135">IP sobre InfiniBand (IB) não tem suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="d8702-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="d8702-136">Apenas RDMA sobre IB é compatível.</span><span class="sxs-lookup"><span data-stu-id="d8702-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d8702-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8702-137">Next steps</span></span>
* <span data-ttu-id="d8702-138">Para obter detalhes sobre a disponibilidade e preços de tamanhos de computação intensa hello, consulte [preços das máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="d8702-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="d8702-139">Para obter os detalhes de disco e as capacidades de armazenamento, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d8702-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="d8702-140">tooget iniciado Implantando e usando tamanhos de computação intensiva com o RDMA no Linux, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d8702-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

