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
# <a name="high-performance-compute-linux-vm-sizes"></a>Tamanhos de VM Linux de computação de alto desempenho

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Instâncias compatíveis com RDMA
Uma interface de rede para conectividade de acesso (RDMA) de memória direta remota de recurso de um subconjunto de instâncias de computação intensiva hello (H16r, H16mr, A8 e A9). Além disso, esta interface é tamanhos de VM toohello padrão da rede do Azure interface tooother disponíveis. 
  
Essa interface permite Olá compatíveis com RDMA instâncias toocommunicate em uma rede InfiniBand, operando em taxas FDR para máquinas virtuais H16r e H16mr e taxas QDR para máquinas virtuais A8 e A9. Esses recursos RDMA podem melhorar a escalabilidade de saudação e o desempenho de aplicativos de Interface MPI (Message Passing).

Estes são os requisitos para máquinas virtuais de Linux compatíveis com RDMA tooaccess Olá rede RDMA do Azure:
 
* **Distribuições** - você deve implantar as VMs de compatíveis com RDMA SUSE Linux Enterprise Server (SLES) ou imagens de Software não autorizado Wave (anteriormente conhecida como OpenLogic) com base em CentOS HPC em hello Azure Marketplace. Olá Marketplace imagens suporte conectividade RDMA a seguir:
  
    * SLES 12 SP1 para HPC ou SLES 12 SP1 para HPC (Premium)
    
    * HPC 7.3, 7.1, 6.8 ou 6.5 baseado em CentOS  
 
        > [!NOTE]
        > Para VMs da série H, recomendamos o SLES 12 SP1 para imagem do HPC ou imagem do HPC 7.1 baseado em CentOS.
        >
        > Em imagens de HPC com base em CentOS hello, atualizações de kernel estão desabilitadas no hello **yum** arquivo de configuração. Isso ocorre porque hello drivers Linux RDMA são distribuídos como um pacote RPM e atualizações de driver podem não funcionar se kernel Olá for atualizada.
        > 
        > 
* **MPI** - Intel MPI Library 5.x
  
    Dependendo da imagem do Marketplace Olá escolher, instalação de licenciamento, separada, ou a configuração da Intel MPI ser necessário, da seguinte maneira: 
  
  * **SLES 12 SP1 para imagem HPC** -Intel MPI pacotes são distribuídos em Olá VM. Instale executando Olá comando a seguir:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **Imagens do HPC baseado em CentOS** – O Intel MPI 5.1 já está instalado.  
    
    Configurações adicionais do sistema é necessário toorun de trabalhos MPI em máquinas virtuais em cluster. Por exemplo, em um cluster de máquinas virtuais, você precisa tooestablish confiança entre Olá nós de computação. Para as configurações típicas, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>Considerações de topologia de rede
* Em VMs Linux habilitadas para RDMA no Azure, Eth1 é reservado para o tráfego de rede RDMA. Não altere as configurações de Eth1 ou todas as informações no arquivo de configuração de saudação referindo-se a rede toothis. Eth0 é reservado para o tráfego de rede regular do Azure.

* IP sobre InfiniBand (IB) não tem suporte no Azure. Apenas RDMA sobre IB é compatível.

## <a name="using-hpc-pack"></a>Usando o HPC Pack
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), solução gratuita da Microsoft HPC cluster e o trabalho de gerenciamento, é uma opção para que instâncias de computação intensiva Olá toouse com Linux. versões mais recentes de saudação do HPC Pack oferecem suporte a várias distribuições do Linux toorun em computação nós implantados em máquinas virtuais do Azure, gerenciado por um nó principal do Windows Server. Conosco de computação compatíveis com RDMA Linux executando Intel MPI, HPC Pack pode agendar e executar aplicativos MPI Linux essa rede RDMA de saudação de acesso. Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="other-sizes"></a>Outros tamanhos
- [Propósito geral](sizes-general.md)
- [Computação otimizada](sizes-compute.md)
- [Memória otimizada](sizes-memory.md)
- [Armazenamento otimizado](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>Próximas etapas

- tooget iniciado Implantando e usando tamanhos de computação intensiva com o RDMA no Linux, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

- Saiba mais sobre como as [ACUs (unidade de computação do Azure)](acu.md) podem ajudar você a comparar o desempenho de computação entre SKUs do Azure.




