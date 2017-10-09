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
# <a name="high-performance-compute-vm-sizes"></a>Tamanhos de VM de computação de alto desempenho

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Instâncias compatíveis com RDMA
Uma interface de rede para conectividade de acesso (RDMA) de memória direta remota de recurso de um subconjunto de instâncias de computação intensiva hello (H16r, H16mr, A8 e A9). Além disso, esta interface é tamanhos de VM toohello padrão da rede do Azure interface tooother disponíveis. 
  
Essa interface permite Olá compatíveis com RDMA instâncias toocommunicate em uma rede InfiniBand, operando em taxas FDR para máquinas virtuais H16r e H16mr e taxas QDR para máquinas virtuais A8 e A9. Esses recursos RDMA podem melhorar a escalabilidade de saudação e o desempenho de aplicativos de Interface MPI (Message Passing).

Estes são os requisitos para máquinas virtuais do Windows compatíveis com RDMA tooaccess Olá rede RDMA do Azure: 

* **Sistema operacional**
  
  Windows Server 2012 R2, Windows Server 2012
  
  > [!NOTE]
  > Atualmente, o Windows Server 2016 não dá suporte à conectividade RDMA no Azure.
  >

* **Conjunto de disponibilidade ou serviço de nuvem** – implantar VMs de saudação compatíveis com RDMA na Olá mesmo conjunto (quando você usa o modelo de implantação do Azure Resource Manager Olá) de disponibilidade ou Olá mesmo serviço de nuvem (quando você usa o modelo de implantação clássico Olá). Se você usar o lote do Azure, Olá VMs compatíveis com RDMA deve estar no hello mesmo pool.

* **MPI** – Microsoft MPI (MS-MPI) 2012 R2 ou posterior, Intel MPI Library 5.x

  Implementações de MPI com suporte usam toocommunicate de interface direta da rede Microsoft hello entre instâncias. 

* **Espaço de endereço de rede RDMA** -rede RDMA Olá no Azure reserva Olá endereço espaço 172.16.0.0/16. toorun aplicativos de MPI em instâncias implantadas em uma rede virtual do Azure, certifique-se de que espaço de endereço de rede virtual Olá não se sobreponha a rede RDMA hello.

* **Extensão HpcVmDrivers VM** -em VMs compatíveis com RDMA, você deve adicionar Olá HpcVmDrivers extensão tooinstall rede drivers de dispositivo Windows para a conectividade RDMA. (Em certas implantações de instâncias A8 e A9, Olá extensão HpcVmDrivers é adicionada automaticamente.) tooadd Olá VM extensão tooa VM, você pode usar [Azure PowerShell](/powershell/azure/overview) cmdlets. 

  
  Olá instala hello mais recente extensão HpcVMDrivers de versão 1.1 em uma VM compatíveis com RDMA existente chamada de comando a seguir *myVM* implantada no grupo de recursos de saudação chamado *myResourceGroup* em Olá  *Oeste dos EUA* região:

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Para obter mais informações, consulte [Recursos e extensões da máquina virtual](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Você também pode trabalhar com extensões para as VMs implantadas em Olá [modelo de implantação clássico](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>Usando o HPC Pack

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), solução gratuita da Microsoft HPC cluster e o trabalho de gerenciamento, é uma opção para toocreate um cluster de computação em aplicativos de MPI baseados no Windows Azure toorun e outras cargas de trabalho do HPC. HPC Pack 2012 R2 e versões posteriores incluem um ambiente de tempo de execução para MS-MPI que usa a rede de RDMA do Azure hello quando implantado em VMs compatíveis com RDMA.




## <a name="other-sizes"></a>Outros tamanhos
- [Propósito geral](sizes-general.md)
- [Computação otimizada](sizes-compute.md)
- [Memória otimizada](../virtual-machines-windows-sizes-memory.md)
- [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md)
- [GPU otimizada](sizes-gpu.md)

## <a name="next-steps"></a>Próximas etapas

- Para instâncias de computação intensiva listas de verificação toouse Olá com o HPC Pack no Windows Server, consulte [configurar um cluster do Windows RDMA com aplicativos de MPI do HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- instâncias de computação intensiva toouse ao executar aplicativos MPI com o lote do Azure, consulte [Use a instância várias tarefas toorun passando Interface aplicativos MPI (Message) em lote do Azure](../../batch/batch-mpi.md).

- Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.




