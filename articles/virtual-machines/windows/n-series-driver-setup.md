---
title: "instalação de driver aaaAzure N-series para Windows | Microsoft Docs"
description: "Como tooset drivers de GPU NVIDIA para VMs série N executando o Windows Azure"
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
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="1662d-103">Configurar drivers GPU para VMs da série N executando o Windows Server</span><span class="sxs-lookup"><span data-stu-id="1662d-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="1662d-104">tootake as vantagens dos recursos GPU de saudação da série de N Azure VMs que executam o Windows Server 2016 ou Windows Server 2012 R2, instale os drivers gráficos NVIDIA com suporte.</span><span class="sxs-lookup"><span data-stu-id="1662d-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="1662d-105">Este artigo apresenta etapas de instalação do driver depois que você implanta uma VM da série N.</span><span class="sxs-lookup"><span data-stu-id="1662d-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="1662d-106">Também há informações de instalação de driver disponíveis para [VMs Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1662d-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1662d-107">Para especificações básicas, capacidades de armazenamento e detalhes de disco, consulte [tamanhos de VM Windows da GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1662d-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="1662d-108">Instalação do driver</span><span class="sxs-lookup"><span data-stu-id="1662d-108">Driver installation</span></span>

1. <span data-ttu-id="1662d-109">Conecte-se pela área de trabalho remota tooeach N-série VM.</span><span class="sxs-lookup"><span data-stu-id="1662d-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="1662d-110">Baixar, extrair e instalar o driver de saudação com suporte para o sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="1662d-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="1662d-111">Em VMs NV do Azure, uma reinicialização é necessária após a instalação de drivers.</span><span class="sxs-lookup"><span data-stu-id="1662d-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="1662d-112">Em VMs NC, uma reinicialização não é necessária.</span><span class="sxs-lookup"><span data-stu-id="1662d-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="1662d-113">Verificar a instalação de drivers</span><span class="sxs-lookup"><span data-stu-id="1662d-113">Verify driver installation</span></span>

<span data-ttu-id="1662d-114">É possível verificar a instalação de drivers no Gerenciador de Dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1662d-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="1662d-115">Olá exemplo a seguir mostra a configuração bem-sucedida do cartão de saudação Tesla K80 em uma VM do Azure NC.</span><span class="sxs-lookup"><span data-stu-id="1662d-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Propriedades do driver GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="1662d-117">Olá tooquery estado de dispositivo GPU, executar Olá [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o driver de saudação de utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1662d-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="1662d-118">Abra um prompt de comando e altere toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span><span class="sxs-lookup"><span data-stu-id="1662d-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="1662d-119">Execute **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="1662d-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="1662d-120">Se o driver hello está instalado você verá toobelow semelhante de saída.</span><span class="sxs-lookup"><span data-stu-id="1662d-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="1662d-121">Observe que **GPU-Util** mostra **0%** , a menos que está executando atualmente uma carga de trabalho GPU em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="1662d-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![Status do dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="1662d-123">Rede RDMA para VMs NC24r</span><span class="sxs-lookup"><span data-stu-id="1662d-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="1662d-124">Conectividade de rede RDMA pode ser habilitada em NC24r VMs implantadas em Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="1662d-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="1662d-125">Olá extensão HpcVmDrivers deve ser adicionado tooinstall Windows rede drivers de dispositivo que habilitar a conectividade RDMA.</span><span class="sxs-lookup"><span data-stu-id="1662d-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="1662d-126">tooadd Olá VM extensão tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets para o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1662d-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="1662d-127">No momento, somente o Windows Server 2012 R2 oferece suporte à rede RDMA de saudação em VMs NC24r.</span><span class="sxs-lookup"><span data-stu-id="1662d-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="1662d-128">tooinstall hello mais recente versão 1.1 extensão HpcVMDrivers em uma VM compatíveis com RDMA existente denominada myVM em região Oeste dos EUA de saudação:</span><span class="sxs-lookup"><span data-stu-id="1662d-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="1662d-129">Para obter mais informações, consulte [Recursos e extensões da máquina virtual para Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1662d-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="1662d-130">rede RDMA Olá oferece suporte ao tráfego de Interface MPI (Message Passing) para aplicativos em execução com [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou MPI Intel 5. x.</span><span class="sxs-lookup"><span data-stu-id="1662d-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1662d-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1662d-131">Next steps</span></span>

* <span data-ttu-id="1662d-132">Para obter mais informações sobre Olá GPUs NVIDIA Olá VMs da série de N, consulte:</span><span class="sxs-lookup"><span data-stu-id="1662d-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="1662d-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para VMs NC do Azure)</span><span class="sxs-lookup"><span data-stu-id="1662d-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="1662d-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para VMs NV do Azure)</span><span class="sxs-lookup"><span data-stu-id="1662d-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="1662d-135">Os desenvolvedores que criam aplicativos acelerado GPU Olá NVIDIA Tesla GPUs também podem baixar e instalar hello CUDA Toolkit 8 para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="1662d-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="1662d-136">Para obter mais informações, consulte Olá [CUDA guia de instalação](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="1662d-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


