---
title: "Configuração de drivers da série N do Azure para Windows | Microsoft Docs"
description: "Como configurar drivers NVIDIA GPU para VMs da série N que executam o Windows no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b480d10df777a2757c073ff77e1845d33d63163a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="19f8a-103">Configurar drivers GPU para VMs da série N executando o Windows Server</span><span class="sxs-lookup"><span data-stu-id="19f8a-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="19f8a-104">Para aproveitar os recursos de GPU das VMs série N do Azure que estão executando o Windows Server 2016 ou o Windows Server 2012 R2, instale os drivers gráficos NVIDIA com suporte.</span><span class="sxs-lookup"><span data-stu-id="19f8a-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="19f8a-105">Este artigo apresenta etapas de instalação do driver depois que você implanta uma VM da série N.</span><span class="sxs-lookup"><span data-stu-id="19f8a-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="19f8a-106">Também há informações de instalação de driver disponíveis para [VMs Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19f8a-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="19f8a-107">Para especificações básicas, capacidades de armazenamento e detalhes de disco, consulte [tamanhos de VM Windows da GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19f8a-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="19f8a-108">Instalação do driver</span><span class="sxs-lookup"><span data-stu-id="19f8a-108">Driver installation</span></span>

1. <span data-ttu-id="19f8a-109">Conecte-se pela Área de Trabalho Remota a cada VM da série N.</span><span class="sxs-lookup"><span data-stu-id="19f8a-109">Connect by Remote Desktop to each N-series VM.</span></span>

2. <span data-ttu-id="19f8a-110">Baixe, extraia e instale o driver com suporte para o sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="19f8a-110">Download, extract, and install the supported driver for your Windows operating system.</span></span>

<span data-ttu-id="19f8a-111">Em VMs NV do Azure, uma reinicialização é necessária após a instalação de drivers.</span><span class="sxs-lookup"><span data-stu-id="19f8a-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="19f8a-112">Em VMs NC, uma reinicialização não é necessária.</span><span class="sxs-lookup"><span data-stu-id="19f8a-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="19f8a-113">Verificar a instalação de drivers</span><span class="sxs-lookup"><span data-stu-id="19f8a-113">Verify driver installation</span></span>

<span data-ttu-id="19f8a-114">É possível verificar a instalação de drivers no Gerenciador de Dispositivos.</span><span class="sxs-lookup"><span data-stu-id="19f8a-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="19f8a-115">O exemplo a seguir mostra uma configuração bem-sucedida da placa Tesla K80 em uma VM NC do Azure.</span><span class="sxs-lookup"><span data-stu-id="19f8a-115">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span></span>

![Propriedades do driver GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="19f8a-117">Para consultar o estado do dispositivo GPU, execute o utilitário de linha de comando [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o driver.</span><span class="sxs-lookup"><span data-stu-id="19f8a-117">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span>

1. <span data-ttu-id="19f8a-118">Abra um prompt de comando e mude para o diretório **C:\Program Files\NVIDIA Corporation\NVSMI**.</span><span class="sxs-lookup"><span data-stu-id="19f8a-118">Open a command prompt and change to the **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="19f8a-119">Execute **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="19f8a-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="19f8a-120">Se o driver estiver instalado, você verá um resultado semelhante ao mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="19f8a-120">If the driver is installed you will see output similar to below.</span></span> <span data-ttu-id="19f8a-121">Observe que **GPU-Util** mostrará **0%**, a menos que você esteja executando uma carga de trabalho da GPU na VM.</span><span class="sxs-lookup"><span data-stu-id="19f8a-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on the VM.</span></span>

![Status do dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="19f8a-123">Rede RDMA para VMs NC24r</span><span class="sxs-lookup"><span data-stu-id="19f8a-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="19f8a-124">A conectividade de rede RDMA pode ser habilitada em VMs NC24r implantadas no mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="19f8a-124">RDMA network connectivity can be enabled on NC24r VMs deployed in the same availability set.</span></span> <span data-ttu-id="19f8a-125">A extensão HpcVmDrivers deve ser adicionada para instalar drivers de dispositivo de rede do Windows que habilitam a conectividade RDMA.</span><span class="sxs-lookup"><span data-stu-id="19f8a-125">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="19f8a-126">Para adicionar a extensão de VM a uma VM NC24r, use cmdlets do [Azure PowerShell](/powershell/azure/overview) para o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="19f8a-126">To add the VM extension to an NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="19f8a-127">Atualmente, apenas o Windows Server 2012 R2 dá suporte à rede RDMA em VMs NC24r.</span><span class="sxs-lookup"><span data-stu-id="19f8a-127">Currently, only Windows Server 2012 R2 supports the RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="19f8a-128">Para instalar a última extensão HpcVMDrivers versão 1.1 em uma VM compatível com RDMA existente chamada myVM na região Oeste dos EUA:</span><span class="sxs-lookup"><span data-stu-id="19f8a-128">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="19f8a-129">Para obter mais informações, consulte [Recursos e extensões da máquina virtual para Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19f8a-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="19f8a-130">A rede RDMA dá suporte ao tráfego da Interface de transmissão de mensagens (MPI) para aplicativos executados com [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="19f8a-130">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="19f8a-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19f8a-131">Next steps</span></span>

* <span data-ttu-id="19f8a-132">Para obter mais informações sobre as GPUs NVIDIA nas VMs da série N, consulte:</span><span class="sxs-lookup"><span data-stu-id="19f8a-132">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="19f8a-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para VMs NC do Azure)</span><span class="sxs-lookup"><span data-stu-id="19f8a-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="19f8a-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para VMs NV do Azure)</span><span class="sxs-lookup"><span data-stu-id="19f8a-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="19f8a-135">Os desenvolvedores que criam aplicativos com aceleração de GPU para GPUs NVIDIA Tesla também podem baixar e instalar o CUDA Toolkit 8 para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="19f8a-135">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="19f8a-136">Para obter mais informações, consulte o [Guia de instalação do CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="19f8a-136">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


