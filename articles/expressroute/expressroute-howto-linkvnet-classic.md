---
title: "Vincular um circuito de rota expressa do tooan de rede virtual: PowerShell: clássico: Azure | Microsoft Docs"
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets) usando o modelo de implantação clássico hello e PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Conecte-se a um circuito de rota expressa do tooan de rede virtual usando o PowerShell (clássico)
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [CLI do Azure](howto-linkvnet-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-linkvnet-classic.md)
>

Este artigo o ajudará a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando o modelo de implantação clássico hello e PowerShell. Redes virtuais podem ser em Olá a mesma assinatura ou pode fazer parte de outra assinatura.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Pré-requisitos de configuração
1. Você precisa Olá a versão mais recente dos módulos do PowerShell do Azure hello. Você pode baixar módulos do PowerShell mais recentes de saudação do hello seção PowerShell Olá [página Downloads do Azure](https://azure.microsoft.com/downloads/). Siga as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter orientação passo a passo sobre como tooconfigure os módulos do computador toouse hello Azure PowerShell.
2. Você precisa Olá tooreview [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.
3. Você deve ter um circuito do ExpressRoute ativo.
   * Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-classic.md) e ter seu provedor de conectividade habilitar circuito hello.
   * Verifique se o emparelhamento privado do Azure está configurado para seu circuito. Consulte Olá [Configurar roteamento](expressroute-howto-routing-classic.md) artigo para obter instruções de roteamentos.
   * Certifique-se de que o emparelhamento particular do Azure está configurado e Olá emparelhamento via protocolo BGP entre sua rede e a Microsoft está ativo para que você pode habilitar a conectividade de ponta a ponta.
   * É necessário ter uma rede virtual e um gateway de rede virtual criados e totalmente provisionados. Siga as instruções de saudação muito[configurar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).

Você pode vincular o too10 redes virtuais tooan circuito de rota expressa. Todas as redes virtuais devem estar em Olá mesma região geopolíticas. Você pode vincular um número maior de redes virtuais tooyour circuito de rota expressa ou vincular redes virtuais que estão em outras regiões geopolíticas se você habilitou o complemento do premium Olá rota expressa. Verificar Olá [perguntas frequentes sobre](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura
Você pode vincular um circuito de rota expressa do tooan de rede virtual usando Olá cmdlet a seguir. Verifique se esse gateway de rede virtual Olá é criado e está pronto para vinculação antes de executar o cmdlet hello.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Conectar uma rede virtual em um circuito de tooa assinatura diferente
Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas. Olá figura a seguir mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.

Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização. Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços – mas departamentos Olá pode compartilhar uma única rede rota expressa circuito tooconnect tooyour back local. Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello. Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.

> [!NOTE]
> Encargos de largura de banda e conectividade para o circuito dedicado de saudação será proprietário do circuito de rota expressa toohello aplicado. Todas as redes virtuais compartilham Olá mesma largura de banda.
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Administração
Olá *proprietário do circuito* é Olá administrador/coadministrator de assinatura de saudação na qual Olá rota expressa circuito é criado. Olá proprietário do circuito pode autorizar os administradores/coadministrators de outras assinaturas, chamado tooas *circuito usuários*, Olá toouse dedicado circuito que eles possuem. Usuários circuito pode de circuito de rota expressa toouse autorizados Olá organização vincular a rede virtual de saudação em seu toohello assinatura circuito de rota expressa depois que eles são autorizados.

proprietário do circuito Olá tem autorizações de toomodify e revoke power Olá a qualquer momento. Revogar uma autorização resultará em todos os links sejam excluídos da assinatura Olá cujo acesso foi revogado.

### <a name="circuit-owner-operations"></a>Operações do proprietário do circuito

**Criando uma autorização**

Olá, proprietário do circuito autoriza os administradores de saudação de outras assinaturas toouse Olá especificado circuito. Em Olá exemplo a seguir, administrador de saudação do circuito hello (TI da Contoso) habilita administrador Olá de outro toolink de assinatura (desenvolvimento de teste), o circuito de toohello tootwo redes virtuais. administrador de TI da Contoso Olá permite isso especificando a ID de teste de desenvolvimento Microsoft hello. Olá cmdlet não envia email toohello especificado o ID da Microsoft. proprietário do circuito Olá precisa tooexplicitly notificar Olá outro proprietário da assinatura que Olá autorização é concluído.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Examinando autorizações**

proprietário do circuito Olá pode revisar todas as autorizações que são emitidas em um circuito específico executando Olá cmdlet a seguir:

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Atualizando autorizações**

proprietário do circuito Olá pode modificar autorizações usando Olá cmdlet a seguir:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Excluindo autorizações**

proprietário do circuito Olá pode revogar/excluir autorizações toohello usuário executando Olá cmdlet a seguir:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Operações do usuário do circuito

**Examinando autorizações**

usuários do circuito Olá poderá examinar autorizações usando Olá cmdlet a seguir:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Resgatando autorizações de link**

usuários do circuito Olá podem executar Olá tooredeem cmdlet a seguir uma autorização de link:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Execute este comando em assinatura Olá recentemente vinculado para rede virtual hello:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).

