---
title: aaaWorkflows para configurar um circuito de rota expressa | Microsoft Docs
description: "Esta página orientará fluxos de trabalho Olá para configurar emparelhamentos e o circuito de rota expressa"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>Fluxos de trabalho do ExpressRoute para provisionamento e estados do circuito
Esta página orienta você durante o provisionamento do serviço hello e roteamento fluxos de trabalho de configuração em um alto nível.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Olá figura a seguir e as etapas correspondentes mostram tarefas Olá que siga na ordem toohave uma rota expressa circuito provisionado ponta a ponta. 

1. Use o PowerShell tooconfigure um circuito de rota expressa. Siga as instruções de Olá Olá [circuitos ExpressRoute criar](expressroute-howto-circuit-classic.md) artigo para obter mais detalhes.
2. Conectividade de ordem de provedor de serviços de saudação. Esse processo varia. Entre em contato com seu provedor de conectividade para obter mais detalhes sobre como tooorder conectividade.
3. Certifique-se de que circuito Olá foi provisionado com êxito verificando o circuito de rota expressa Olá estado por meio do PowerShell de provisionamento. 
4. Configure os domínios de roteamento. Se seu provedor de conectividade gerencia a camada 3 para você, ele configurará o roteamento para o circuito. Se seu provedor de conectividade apenas oferece serviços de camada 2, você deve configurar o roteamento de acordo com as diretrizes descritas em Olá [requisitos de roteamento](expressroute-routing.md) e [configuração de roteamento](expressroute-howto-routing-classic.md) páginas.
   
   * Habilitar o emparelhamento particular do Azure - você deve habilitar esta tooVMs tooconnect emparelhamento / serviços implantados dentro das redes virtuais na nuvem.
   * Habilitar o emparelhamento público do Azure - você deve habilitar o emparelhamento público do Azure se desejar tooconnect tooAzure serviços hospedados em endereços IP públicos. Este é um requisito tooaccess recursos do Azure se você tiver escolhido o roteamento padrão de tooenable para emparelhamento particular do Azure.
   * Habilitar o emparelhamento da Microsoft - você deve habilitar esta tooaccess Office 365 e Dynamics 365. 
     
     > [!IMPORTANT]
     > Você deve garantir que você usar um proxy separado / borda tooconnect tooMicrosoft de Olá você utiliza para Olá da Internet. Usando Olá mesmo borda da saudação da Internet e de rota expressa será fazer com que o serviço de roteamento assimétrico e causar falhas de conectividade para sua rede.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Vinculando virtual redes tooExpressRoute circuitos - você pode vincular um circuito de rota expressa tooyour redes virtuais. Siga as instruções [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuito. Essas VNets pode ser Olá a mesma assinatura do Azure que o circuito de rota expressa hello, ou pode estar em uma assinatura diferente.

## <a name="expressroute-circuit-provisioning-states"></a>Estados de provisionamento de circuito do ExpressRoute
Cada circuito de ExpressRoute tem dois estados:

* Estado de provisionamento do provedor de serviço
* Status

O status representa o estado de provisionamento da Microsoft. Essa propriedade é definida tooEnabled quando você criar um circuito de rota expressa

estado de provisionamento do provedor de conectividade de saudação representa o estado de saudação no lado do provedor de conectividade hello. Ele pode ser *Não Provisionado*, *Provisionando* ou *Provisionado*. Olá circuito de rota expressa deve estar no estado provisionado para você toobe capaz de toouse-lo.

### <a name="possible-states-of-an-expressroute-circuit"></a>Possíveis estados de um circuito do ExpressRoute
Esta seção lista estados possíveis de saudação para um circuito de rota expressa.

**No momento da criação**

Você verá circuito de rota expressa Olá no hello estado a seguir assim que você executar o circuito de rota expressa Olá PowerShell cmdlet toocreate hello.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Quando o provedor de conectividade está em processo de saudação de provisionamento do circuito Olá**

Você verá circuito de rota expressa Olá no hello estado a seguir assim que você passe Olá toohello chave conectividade provedor e eles começaram a saudação processo de provisionamento.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**Quando o provedor de conectividade concluiu Olá processo de provisionamento**

Você verá Olá circuito de rota expressa em Olá estado a seguir como provedor de conectividade Olá concluiu Olá processo de provisionamento.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Configurado e ativado é Olá somente circuito de saudação do estado pode estar para você toobe capaz de toouse. Se você estiver usando um provedor de camada 2, configure o roteamento para o circuito somente quando ele estiver nesse estado.

**Quando o provedor de conectividade é desprovisionamento circuito Olá**

Se você solicitou o circuito de rota expressa Olá serviço provedor toodeprovision hello, você verá circuito Olá definir toohello estado a seguir após provedor Olá Olá desprovisionamento de processo.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Você pode escolher habilitar toore se necessário, ou executar cmdlets do PowerShell toodelete circuito de saudação.  

> [!IMPORTANT]
> Se você executar Olá circuito PowerShell cmdlet toodelete hello quando Olá ServiceProviderProvisioningState é provisionamento ou provisionado Olá falhará. Trabalhe com seu circuito de rota expressa conectividade provedor toodeprovision Olá primeiro e, em seguida, excluir o circuito de saudação. A Microsoft continuará circuito de saudação toobill até que você execute Olá circuito de saudação de toodelete de cmdlet do PowerShell.
> 
> 

## <a name="routing-session-configuration-state"></a>Estado de configuração da sessão de roteamento
Olá estado de provisionamento do BGP permite que você saiba se foi habilitado privado Olá Olá Microsoft edge. Olá estado deve ser habilitado para você toobe toouse capaz de saudação emparelhamento.

É o estado da sessão BGP toocheck importante Olá especialmente para emparelhamento da Microsoft. Adição toohello BGP estado de provisionamento, há outro estado chamado *anunciado estado prefixos públicos*. Olá anunciado estado prefixos públicos deve estar no *configurado* state, tanto para Olá toobe de sessão BGP para cima e para a roteamento toowork ponta a ponta. 

Se Olá anunciado estado prefixo público definido tooa *validação necessária* estado, sessão BGP de saudação não estiver habilitado, como Olá anunciado prefixos não correspondeu hello como número em qualquer um dos registros de roteamento hello. 

> [!IMPORTANT]
> Se Olá anunciado estado prefixos públicos *validação manual* de estado, você deve abrir um tíquete de suporte com [o suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e fornecem evidências de que você possui endereços IP de saudação anunciado ao longo com hello associado número de sistema autônomo.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Configurar sua conexão do ExpressRoute.
  
  * [Criar um circuito do ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configurar o roteamento](expressroute-howto-routing-arm.md)
  * [Vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-arm.md)

