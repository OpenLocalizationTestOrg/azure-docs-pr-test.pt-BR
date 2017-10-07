---
title: "Migrar redes virtuais da rota expressa associada de tooResource clássico Manager: Azure: PowerShell | Microsoft Docs"
description: "Esta página descreve como o toomigrate associado a redes virtuais tooResource Manager depois de mover seu circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>Migrar redes virtuais da rota expressa associada de clássico tooResource Manager

Este artigo explica como o toomigrate rota expressa do Azure associado a redes virtuais do modelo de implantação do hello implantação clássica modelo toohello do Azure Resource Manager depois de mover o circuito de rota expressa. 


## <a name="before-you-begin"></a>Antes de começar
* Verifique se você tem a versão mais recente Olá dos módulos do PowerShell do Azure hello. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.
* Revise as informações de saudação que são fornecidas em [movendo um circuito de rota expressa de tooResource clássico Manager](expressroute-move.md). Certifique-se de que você compreenda plenamente Olá limites e as limitações.
* Verifique se o circuito de saudação é totalmente operacional no modelo de implantação clássico hello.
* Certifique-se de que você tenha um grupo de recursos que foi criado no modelo de implantação do Gerenciador de recursos de saudação.
* Saudação de revisão documentação de migração do recurso a seguir:

    * [Suporte de plataforma de migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [Perguntas frequentes: Plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Confira os erros mais comuns de migração e as mitigações](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Cenários com e sem suporte

* Um circuito de rota expressa pode ser movido do ambiente de Gerenciador de recursos de toohello clássico Olá sem nenhum tempo de inatividade. Você pode mover qualquer circuito de rota expressa de saudação clássico toohello ambiente do Gerenciador de recursos sem tempo de inatividade. Siga as instruções de saudação em [movendo circuitos ExpressRoute de modelo de implantação do hello clássico toohello Gerenciador de recursos usando o PowerShell](expressroute-howto-move-arm.md). Isso é uma rede virtual do pré-requisito toomove recursos toohello conectado.
* Implantações associadas na rede virtual Olá que estão anexado tooan circuito de rota expressa em Olá pode ser a mesma assinatura, gateways e redes virtuais migradas ambiente do Gerenciador de recursos de toohello sem qualquer tempo de inatividade. Você pode seguir Olá etapas descritas posteriormente toomigrate recursos como máquinas virtuais implantadas na rede virtual hello, gateways e redes virtuais. Certifique-se de que as redes virtuais Olá estão configuradas corretamente antes que eles são migrados. 
* Redes virtuais, gateways e implantações associadas na rede virtual de saudação que não estão em Olá mesma assinatura como Olá circuito de rota expressa exigir algumas migração de saudação do toocomplete de tempo de inatividade. a última seção saudação do documento hello descreve Olá etapas toobe seguido toomigrate recursos.
* Uma rede virtual com o Gateway de ExpressRoute e Gateway VPN não pode ser migrada.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Mover um circuito de rota expressa de clássico tooResource Manager
Você deve mover um circuito de rota expressa do hello clássico toohello ambiente do Gerenciador de recursos antes de tentar toomigrate recursos que estão anexados toohello circuito de rota expressa. tooaccomplish tarefas, consulte Olá artigos a seguir:

* Revise as informações de saudação que são fornecidas em [movendo um circuito de rota expressa de tooResource clássico Manager](expressroute-move.md).
* [Mover um circuito de tooResource clássico Manager usando o Azure PowerShell](expressroute-howto-move-arm.md).
* Use o portal de gerenciamento de serviços do Azure hello. Você pode seguir o fluxo de trabalho Olá muito[criar um novo circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e selecione a opção de importar hello. 

Esta operação não envolve tempo de inatividade. Você pode continuar tootransfer dados entre suas instalações e Microsoft enquanto Olá migração está em andamento.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Migrar redes virtuais, gateways e implantações associadas

Olá etapas que você seguir toomigrate dependem se os recursos estão em Olá mesma assinatura, assinaturas diferentes ou ambos.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Migrar redes virtuais, gateways, e as implantações associadas no hello mesma assinatura conforme Olá circuito de rota expressa
Esta seção descreve Olá etapas toobe seguido toomigrate uma rede virtual, gateway e implantações associadas no hello mesma assinatura conforme Olá circuito de rota expressa. Nenhum tempo de inatividade é associado a essa migração. Você pode continuar toouse todos os recursos por meio do processo de migração de saudação. plano de gerenciamento de saudação é bloqueado enquanto Olá migração está em andamento. 

1. Certifique-se de que o circuito de rota expressa Olá foi movido do ambiente de Gerenciador de recursos do hello toohello clássico.
2. Certifique-se de que essa rede virtual Olá foi preparado adequadamente para a migração de saudação.
3. Registre sua assinatura para a migração de recursos. tooregister sua assinatura para a migração de recursos, use Olá trecho do PowerShell a seguir:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Valide, prepare e migre. toomove Olá rede virtual, e use Olá trecho do PowerShell a seguir:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  Você também pode anular migração executando Olá cmdlet do PowerShell a seguir:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Próximas etapas
* [Suporte de plataforma de migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [Perguntas frequentes: Plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Confira os erros mais comuns de migração e as mitigações](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
