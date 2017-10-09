---
title: aaaMigrate do AWS e outra plataformas tooManaged discos no Azure | Microsoft Docs
description: "Criação de VMs no Azure usando VHDs carregados de outras nuvens, como AWS ou outras plataformas de virtualização, e tirar proveito dos Azure Managed Disks."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Migrar de serviços AWS (Amazon Web) e outras plataformas tooManaged discos no Azure

Você pode carregar arquivos VHD AWS ou local toocreate de tooAzure de soluções VMs que tiram proveito de discos gerenciados virtualização. Discos do Azure gerenciados elimina a necessidade de Olá toomanaging de contas de armazenamento para as VMs de IaaS do Azure. Você tem tooonly especificar tipo de saudação (Premium ou padrão) e o tamanho do disco é necessário e Azure criará e gerenciará disco Olá para você. 

Você pode carregar VHDs especializados e generalizados. 
- **VHD generalizado** – teve todas as informações da sua conta pessoal removidas usando o Sysprep. 
- **Especializado VHD** -mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original. 

> [!IMPORTANT]
> Antes de carregar qualquer tooAzure VHD, você deve seguir [preparar um tooAzure de tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Cenário                                                                                                                         | Documentação                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Você tiver um instâncias AWS EC2 existente que você poderia como toomigrate tooAzure discos gerenciado                                     | [Mover uma máquina virtual de tooAzure serviços AWS (Amazon Web)](aws-to-azure.md)                           |
| Você tem outra plataforma de virtualização que você gostaria que toouse toouse como toocreate uma imagem e de uma VM de várias VMs do Azure. | [Carregar um VHD generalizado e usá-lo toocreate um novas VMs no Azure](upload-generalized-managed.md) |
| Você tem uma VM exclusivamente personalizada que você gostaria que toorecreate no Azure.                                                      | [Carregar um tooAzure especializada do VHD e criar uma nova VM](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Visão geral do Managed Disks

Discos gerenciado do Azure simplifica o gerenciamento de VM, removendo as contas de armazenamento toomanage Olá necessidade. O Managed Disks também fornece melhor confiabilidade de VMs em um conjunto de disponibilidade. Garante que os discos Olá das diferentes VMs em um conjunto de disponibilidade será suficientemente isolados de cada outro tooavoid ponto único de falhas. Coloca automaticamente discos de diferentes VMs em um conjunto de disponibilidade em diferentes unidades de escala de armazenamento (carimbos) que limita o impacto de saudação de falhas de unidade de escala de armazenamento único causado devido a falhas de software e toohardware. Com base em suas necessidades, você pode escolher entre dois tipos de opções de armazenamento: 
 
- Os [Managed Disks Premium](../../storage/common/storage-premium-storage.md) são uma mídia de armazenamento com base em unidade de estado sólido (SSD), que fornece alto desempenho, suporte a disco de baixa latência para máquinas virtuais com cargas de trabalho de E/S intensas. Você pode tirar proveito de velocidade de saudação e o desempenho desses discos por discos Migrando do tooPremium gerenciados.  

- [Discos padrão gerenciado](../../storage/common/storage-standard-storage.md) usar a mídia de armazenamento de disco rígido (HDD) com base e são mais adequados para desenvolvimento/teste e outras cargas de trabalho de acesso incomum que são menos confidencial variabilidade de tooperformance.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planejar a migração de saudação do tooManaged discos

Esta seção Ajuda toomake Olá melhor decisão sobre tipos de VM e disco.


### <a name="location"></a>Local

Escolha um local onde o Azure Managed Disks estão disponíveis. Se você estiver migrando tooPremium gerenciados discos, também Verifique se o armazenamento Premium está disponível na região Olá onde você está planejando toomigrate para. Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis.

### <a name="vm-sizes"></a>Tamanhos de VM

Se você estiver migrando tooPremium gerenciados discos, você tem tooupdate tamanho de saudação do hello VM tooPremium tamanho com capacidade de armazenamento disponível na região Olá onde a VM está localizada. Examine os tamanhos de VM Olá que são compatíveis com um armazenamento Premium. especificações de tamanho de VM do Azure Olá são listadas na [tamanhos das máquinas virtuais](sizes.md).
Examine as características de desempenho de saudação de máquinas virtuais que funcionam com o armazenamento Premium e escolha o tamanho VM mais apropriado hello mais adequada para sua carga de trabalho. Certifique-se de que há largura de banda suficiente disponível no seu tráfego de disco VM toodrive hello.

### <a name="disk-sizes"></a>Tamanhos do disco

**Managed Disks Premium**

Há três tipos de discos gerenciados premium que podem ser usados com a sua VM e cada um tem IOPs e limites de taxa de transferência específicos. Considere esses limites ao escolher Olá tipo de disco Premium para sua VM com base nas necessidades de saudação do seu aplicativo em termos de capacidade, escalabilidade e desempenho e cargas de pico.

| Tipo de discos premium  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Tamanho do disco           | 128 GB            | 512 GB            | 1024 GB (1 TB)    |
| IOPS por disco       | 500               | 2.300              | 5.000              |
| Taxa de transferência por disco | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo |

**Managed Disks Standard**

Há cinco tipos de discos gerenciados Standard que podem ser usados com a sua VM. Cada um deles tem uma capacidade diferente, mas com os mesmos limites de taxa de transferência e IOPS. Escolha o tipo de saudação de discos gerenciados padrão com base nas necessidades de capacidade de saudação do seu aplicativo.

| Tipo de disco Standard  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Tamanho do disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   |
| IOPS por disco       | 500              | 500              | 500              | 500              | 500              |
| Taxa de transferência por disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo |

### <a name="disk-caching-policy"></a>Política de cache de disco 

**Managed Disks Premium**

Por padrão, a política de cache de disco é *somente leitura* para todos os discos de dados Premium, de hello e *leitura-gravação* para o disco do sistema operacional Premium Olá anexado toohello VM. Esta configuração é recomendável tooachieve Olá o desempenho ideal para IOs seu aplicativo. Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo.

### <a name="pricing"></a>Preços

Saudação de revisão [preços para discos gerenciados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Preços de discos gerenciados do Premium são igual a saudação discos de Premium não gerenciado. No entanto, os preços do Standard Managed Disks são diferentes dos preços do Standard Unmanaged Disks.


## <a name="next-steps"></a>Próximas etapas

- Antes de carregar qualquer tooAzure VHD, você deve seguir [preparar um tooAzure de tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
