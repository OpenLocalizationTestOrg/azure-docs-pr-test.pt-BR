---
title: "aaaUsing toomanage de controle de acesso baseado em função do Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooapply e usar baseado em função de controle de acesso (RBAC) toomanage suas implantações do Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Use o controle de acesso baseado em função toomanage do Azure Site Recovery implantações

O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Azure. Usando o RBAC, você pode separar responsabilidades dentro de sua equipe e conceder apenas toousers de permissões de acesso específico como trabalhos específicos necessários tooperform.

O Azure Site Recovery fornece funções internas 3 toocontrol operações de gerenciamento de recuperação de Site. Saiba mais sobre as [funções internas do RBAC do Azure](../active-directory/role-based-access-built-in-roles.md)

* [O colaborador de recuperação de site](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -essa função tem todas as operações de recuperação de Site do Azure toomanage necessário de permissões em um cofre de serviços de recuperação. Ou um usuário com essa função, no entanto, não é possível criar ou excluir um cofre de serviços de recuperação atribuir tooother os usuários com direitos de acesso. Essa função é ideal para os administradores de recuperação de desastres que podem habilitar e gerenciar a recuperação de desastres para aplicativos ou organizações inteiras, como Olá caso.
* [Operador de recuperação de site](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -essa função tem permissões tooexecute e o Gerenciador de Failover e Failback as operações. Um usuário com essa função não pode habilitar ou desabilitar a replicação, criar ou excluir cofres, registrar nova infraestrutura ou atribuir tooother os usuários com direitos de acesso. Essa função é ideal para um operador de recuperação de desastre que pode executar failover em máquinas virtuais ou aplicativos quando instruído por administradores de TI ou proprietários do aplicativo em uma situação de desastre real ou simulada, como em uma simulação de recuperação de desastre. POST resolução de desastre hello, operador Olá DR pode proteger novamente e failback Olá máquinas virtuais.
* [Leitor de recuperação de site](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -essa função tem permissões tooview todas as operações de gerenciamento de recuperação de Site. Essa função é ideal para um executivo de monitoramento de TI que pode monitorar o estado atual de saudação de proteção e gerar tíquetes de suporte, se necessário.

Se você estiver procurando toodefine suas próprias funções para controlar ainda mais, consulte como muito[criar funções personalizadas](../active-directory/role-based-access-control-custom-roles.md) no Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Permissões necessárias tooEnable replicação para novas máquinas virtuais
Quando uma nova máquina Virtual é replicada tooAzure usando o Azure Site Recovery, níveis de acesso do usuário Olá associado são validada tooensure que Olá usuário Olá exigiu permissões toouse Olá recursos do Azure fornecidos tooSite recuperação.

replicação tooenable para uma nova máquina virtual, um usuário deve ter:
* Permissão toocreate uma máquina virtual no grupo de recursos selecionado Olá
* Permissão toocreate uma máquina virtual na rede virtual selecionada de saudação
* Permissão toowrite toohello selecionado conta de armazenamento

Um usuário precisa Olá replicação toocomplete de permissões de uma nova máquina virtual a seguir.

> [!IMPORTANT]
>Certifique-se de que as permissões relevantes são adicionadas por modelo de implantação de saudação (Gerenciador de recursos / clássico) usado para a implantação de recursos.

| **Tipo de recurso** | **Modelo de implantação** | **Permissão** |
| --- | --- | --- |
| Computação | Gerenciador de Recursos | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Clássico | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Rede | Gerenciador de Recursos | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Clássico | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Armazenamento | Gerenciador de Recursos | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Clássico | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Grupo de recursos | Gerenciador de Recursos | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Considere o uso de saudação 'Colaborador da máquina Virtual' e 'Clássico Colaborador de máquina Virtual' [funções internas](../active-directory/role-based-access-built-in-roles.md) para implantação do Gerenciador de recursos e clássico modelos respectivamente.

## <a name="next-steps"></a>Próximas etapas
* [Controle de acesso baseado em função](../active-directory/role-based-access-control-configure.md): Introdução ao RBAC em Olá portal do Azure.
* Saiba como toomanage acessar com:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Solução de problemas de Controle de Acesso Baseado em Função](../active-directory/role-based-access-control-troubleshooting.md): obtenha sugestões para corrigir problemas comuns.
