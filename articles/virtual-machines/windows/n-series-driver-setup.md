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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Configurar drivers GPU para VMs da série N executando o Windows Server
tootake as vantagens dos recursos GPU de saudação da série de N Azure VMs que executam o Windows Server 2016 ou Windows Server 2012 R2, instale os drivers gráficos NVIDIA com suporte. Este artigo apresenta etapas de instalação do driver depois que você implanta uma VM da série N. Também há informações de instalação de driver disponíveis para [VMs Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para especificações básicas, capacidades de armazenamento e detalhes de disco, consulte [tamanhos de VM Windows da GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Instalação do driver

1. Conecte-se pela área de trabalho remota tooeach N-série VM.

2. Baixar, extrair e instalar o driver de saudação com suporte para o sistema operacional Windows.

Em VMs NV do Azure, uma reinicialização é necessária após a instalação de drivers. Em VMs NC, uma reinicialização não é necessária.

## <a name="verify-driver-installation"></a>Verificar a instalação de drivers

É possível verificar a instalação de drivers no Gerenciador de Dispositivos. Olá exemplo a seguir mostra a configuração bem-sucedida do cartão de saudação Tesla K80 em uma VM do Azure NC.

![Propriedades do driver GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

Olá tooquery estado de dispositivo GPU, executar Olá [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o driver de saudação de utilitário de linha de comando.

1. Abra um prompt de comando e altere toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.

2. Execute **nvidia-smi**. Se o driver hello está instalado você verá toobelow semelhante de saída. Observe que **GPU-Util** mostra **0%** , a menos que está executando atualmente uma carga de trabalho GPU em Olá VM.

![Status do dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>Rede RDMA para VMs NC24r

Conectividade de rede RDMA pode ser habilitada em NC24r VMs implantadas em Olá mesmo conjunto de disponibilidade. Olá extensão HpcVmDrivers deve ser adicionado tooinstall Windows rede drivers de dispositivo que habilitar a conectividade RDMA. tooadd Olá VM extensão tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets para o Gerenciador de recursos do Azure.

> [!NOTE]
> No momento, somente o Windows Server 2012 R2 oferece suporte à rede RDMA de saudação em VMs NC24r.
> 

tooinstall hello mais recente versão 1.1 extensão HpcVMDrivers em uma VM compatíveis com RDMA existente denominada myVM em região Oeste dos EUA de saudação:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Para obter mais informações, consulte [Recursos e extensões da máquina virtual para Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

rede RDMA Olá oferece suporte ao tráfego de Interface MPI (Message Passing) para aplicativos em execução com [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou MPI Intel 5. x. 


## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre Olá GPUs NVIDIA Olá VMs da série de N, consulte:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para VMs NC do Azure)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para VMs NV do Azure)

* Os desenvolvedores que criam aplicativos acelerado GPU Olá NVIDIA Tesla GPUs também podem baixar e instalar hello CUDA Toolkit 8 para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Para obter mais informações, consulte Olá [CUDA guia de instalação](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


