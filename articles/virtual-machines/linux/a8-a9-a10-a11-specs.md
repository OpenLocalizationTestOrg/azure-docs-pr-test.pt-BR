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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Sobre as VMs da série H e da série A de computação intensiva para Linux
Eis aqui as informações de plano de fundo e algumas considerações para usar o hello mais recente do Azure H-series e Olá tamanhos A8, A9, A10 e A11 anteriores, também conhecido como *com computação intensiva* instâncias. Este artigo ressalta o uso desses tamanhos para VMs Linux. Você também pode usá-los para [VMs Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obter as especificações básicas, as capacidades de armazenamento e os detalhes de disco, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Rede RDMA toohello acesso
Você pode criar clusters de VMs Linux compatíveis com RDMA que executem uma saudação distribuições de Linux HPC com suporte e uma vantagem de tootake de implementação MPI com suporte de rede de RDMA do Azure Olá a seguir. Consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para opções de implantação e as etapas de configuração de exemplo.

* **Distribuições** - você deve implantar as VMs de compatíveis com RDMA SUSE Linux Enterprise Server (SLES) ou imagens de Software não autorizado Wave (anteriormente conhecida como OpenLogic) com base em CentOS HPC em hello Azure Marketplace. Olá Marketplace imagens suporte conectividade RDMA a seguir:
  
    * SLES 12 SP1 para HPC, SLES 12 SP1 para HPC (Premium)
    
    * HPC baseado em CentOS 7.1, HPC baseado em CentOS 6.5  
 
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
    
    Configurações adicionais do sistema é necessário toorun de trabalhos MPI em máquinas virtuais em cluster. Por exemplo, em um cluster de máquinas virtuais, você precisa tooestablish confiança entre Olá nós de computação. Para as configurações típicas, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Considerações para HPC Pack e Linux
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), solução gratuita da Microsoft HPC cluster e o trabalho de gerenciamento, fornece uma opção para instâncias de computação intensiva Olá toouse com Linux. versões mais recentes de saudação do HPC Pack oferecem suporte a várias distribuições do Linux toorun em computação nós implantados em máquinas virtuais do Azure, gerenciado por um nó principal do Windows Server. Conosco de computação compatíveis com RDMA Linux executando Intel MPI, HPC Pack pode agendar e executar aplicativos MPI Linux essa rede RDMA de saudação de acesso. tooget iniciado, consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Considerações de topologia de rede
* Em VMs Linux habilitadas para RDMA no Azure, Eth1 é reservado para o tráfego de rede RDMA. Não altere as configurações de Eth1 ou todas as informações no arquivo de configuração de saudação referindo-se a rede toothis. Eth0 é reservado para o tráfego de rede regular do Azure.
* IP sobre InfiniBand (IB) não tem suporte no Azure. Apenas RDMA sobre IB é compatível.



## <a name="next-steps"></a>Próximas etapas
* Para obter detalhes sobre a disponibilidade e preços de tamanhos de computação intensa hello, consulte [preços das máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Para obter os detalhes de disco e as capacidades de armazenamento, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* tooget iniciado Implantando e usando tamanhos de computação intensiva com o RDMA no Linux, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

