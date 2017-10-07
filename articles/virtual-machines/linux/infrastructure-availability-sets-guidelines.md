---
title: Define aaaAvailability para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para a implantação de conjuntos de disponibilidade nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 24f1d91c-8cc0-4251-bb67-ac4c4c37e8cd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78e4da5c8fd9eb186cafacb46454444b73a9439c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-linux-vms"></a>Diretrizes de conjuntos de disponibilidade do Azure para VMs Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo enfoca a compreensão Olá necessárias etapas de planejamento para conjuntos de disponibilidade tooensure seus aplicativos permanecem acessíveis durante eventos planejados ou não planejados.

## <a name="implementation-guidelines-for-availability-sets"></a>Diretrizes de implementação para conjuntos de disponibilidade
Decisões:

* Quantos conjuntos de disponibilidade você precisa para Olá várias camadas e funções em sua infraestrutura de aplicativo?

Tarefas:

* Defina o número de saudação de VMs em cada camada de aplicativo que você precisa.
* Determine se você precisa que o número de saudação do tooadjust de toobe domínios de falha ou atualização usado para o seu aplicativo.
* Definir conjuntos de disponibilidade Olá necessárias usando a convenção de nomenclatura e quais máquinas virtuais residem neles. Uma VM pode residir apenas em um conjunto de disponibilidade. 

## <a name="availability-sets"></a>Conjuntos de disponibilidade
No Azure, máquinas virtuais (VMs) pode ser colocadas em um agrupamento lógico de tooa chamado de um conjunto de disponibilidade. Quando você criar máquinas virtuais dentro de um conjunto de disponibilidade, Olá plataforma Windows Azure distribui o posicionamento de saudação dessas VMs por Olá infra-estrutura subjacente. Deve haver um hardware subjacente ou um evento de manutenção planejada toohello plataforma Windows Azure / falhas de infraestrutura, use Olá conjuntos de disponibilidade garante que pelo menos uma VM permanece em execução.

Como prática recomendada, os aplicativos não devem residir em uma única VM. Um conjunto de disponibilidade que contém uma única VM não obter proteção contra eventos planejados ou não planejados em Olá plataforma Windows Azure. Olá [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines) requer dois ou mais VMs dentro de uma disponibilidade conjunto tooallow Olá distribuição de VMs em Olá infra-estrutura subjacente. Se você estiver usando [armazenamento Premium do Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Olá SLA do Azure se aplica a tooa única VM.

a infraestrutura subjacente Olá no Azure é dividida em clusters de hardware toomultiple. Cada cluster de hardware pode dar suporte a uma variedade de tamanhos de VM. Um conjunto de disponibilidade só pode ser hospedado em um único cluster de hardware em qualquer ponto no tempo. Portanto, os tamanhos de intervalo de VM Olá que podem existir em um único conjunto de disponibilidade é limitado toohello tamanhos de intervalo de VM suportados por cluster de hardware de saudação. cluster de hardware de saudação para conjunto de disponibilidade de saudação é selecionado quando hello primeira VM no conjunto de disponibilidade de saudação é implantado ou iniciando Olá primeira VM em um conjunto de disponibilidade, onde todas as máquinas virtuais estão em estado de parado-desalocado hello. Olá CLI comando a seguir pode ser usado toodetermine Olá intervalo da VM tamanhos disponíveis para um conjunto de disponibilidade: "az vm lista-tamanhos – local \<cadeia de caracteres\>"

Cada cluster de hardware é dividido em domínios de atualização toomultiple e domínios de falha. Esses domínios são definidos pelos hosts que compartilham um ciclo de atualização comum ou uma infraestrutura física semelhante, como energia e rede. Azure distribui automaticamente suas VMs em um conjunto de disponibilidade de toomaintain de domínios e tolerância a falhas de disponibilidade. Dependendo do tamanho de saudação do seu aplicativo e o número de saudação de VMs em um conjunto de disponibilidade, você pode ajustar o número de saudação de domínios que você deseja toouse. Você pode ler mais sobre [gerenciamento de disponibilidade e o uso dos domínios de atualização e de falha](manage-availability.md).

Ao projetar sua infraestrutura de aplicativo, planeje Olá toouse de camadas de aplicativo. Máquinas virtuais do grupo que servem Olá mesmo finalidade em conjuntos de tooavailability, como um conjunto de disponibilidade para suas VMs front-end executando o nginx ou Apache. Crie um conjunto de disponibilidade separado para suas VMs de back-end executando o MongoDB ou MySQL. meta de saudação é tooensure que cada componente do aplicativo é protegido por um conjunto de disponibilidade e pelo menos uma vez instância sempre permanece em execução.

Balanceadores de carga podem ser utilizados na frente de cada toowork de camada de aplicativo junto com um conjunto de disponibilidade e certifique-se de que o tráfego sempre pode ser roteada tooa instância em execução. Sem um balanceador de carga, suas VMs podem continuar em execução durante manutenções planejadas e não planejadas, mas seu usuário final pode não ser capaz de tooresolve-los se hello VM primário está indisponível.

Projete o aplicativo para alta disponibilidade na camada de armazenamento. prática recomendada Olá é muito[usar discos gerenciados para as VMs em um conjunto de disponibilidade](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Se você estiver usando discos não gerenciados, é altamente recomendável muito[converter VMs no conjunto de disponibilidade toouse gerenciados discos](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

