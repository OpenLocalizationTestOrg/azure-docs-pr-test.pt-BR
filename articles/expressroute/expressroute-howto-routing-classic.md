---
title: "Como tooconfigure roteamento (emparelhamento) para um circuito de rota expressa: Azure: clássico | Microsoft Docs"
description: "Este artigo o orienta pelas etapas de saudação para criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Criar e modificar o emparelhamento de um circuito de ExpressRoute (clássico)
> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI do Azure](howto-routing-cli.md)
> * [Vídeo – Emparelhamento privado](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo – Emparelhamento público](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo – Emparelhamento da Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-routing-classic.md)
> 

Este artigo orienta Olá etapas toocreate e gerenciar a configuração de roteamento para um circuito de rota expressa usando o modelo de implantação clássico hello e PowerShell. Olá estas etapas também mostra como status de saudação toocheck, atualizar, ou excluir e desprovisionar emparelhamentos de um circuito de rota expressa.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Pré-requisitos de configuração
* Você precisará a versão mais recente de saudação do hello cmdlets do PowerShell de gerenciamento de serviço do Azure (SM). Para saber mais, confira [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) (Introdução aos cmdlets do Azure PowerShell).  
* Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) página hello [requisitos de roteamento](expressroute-routing.md) página e hello [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração de página.
* Você deve ter um circuito do ExpressRoute ativo. Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-classic.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar. Olá circuito de rota expressa deve estar no estado habilitado e configurado para você toobe toorun capaz de saudação cmdlets descritos abaixo.

> [!IMPORTANT]
> Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2. Se você estiver usando um provedor de serviços que oferece serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.
> 
> 

Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute. Você pode configurar emparelhamentos em qualquer ordem escolhida. No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Faça logon no tooyour conta do Azure e selecione uma assinatura
1. Abra o console do PowerShell com direitos elevados e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

        Login-AzureRmAccount

2. Verificar as assinaturas de saudação para conta de saudação.

        Get-AzureRmSubscription

3. Se você tiver mais de uma assinatura, selecione a assinatura de saudação que você deseja toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Em seguida, use Olá tooadd cmdlet a seguir tooPowerShell sua assinatura do Azure para o modelo de implantação clássico hello.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Emparelhamento privado do Azure
Esta seção fornece instruções sobre como toocreate, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa. 

### <a name="toocreate-azure-private-peering"></a>toocreate emparelhamento particular do Azure
1. **Importe o módulo do PowerShell de saudação do ExpressRoute.**
   
    Você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello. A seguir Olá execução comandos módulos do Azure e rota expressa Olá tooimport na sessão do PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Criar um circuito do ExpressRoute.**
   
    Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-classic.md) e fornecidos pelo provedor de conectividade de saudação. Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, siga as instruções de saudação abaixo. 
3. **Verifique Olá tooensure de circuito de rota expressa que é provisionado.**
   
    Primeiro, você deve verificar toosee se hello circuito de rota expressa é provisionado e também está habilitado. Consulte o exemplo hello abaixo.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Certifique-se de que o circuito Olá mostra como provisionado e habilitado. Se não estiver, trabalhe com seu tooget do provedor de conectividade seu circuito toohello necessária e o status.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configure o emparelhamento particular do Azure para o circuito de saudação.**
   
    Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:
   
   * Um /30 sub-rede para o link primário hello. Ela não deve fazer parte de qualquer espaço de endereçamento reservado para redes virtuais.
   * Um /30 sub-rede para o link secundário hello. Ela não deve fazer parte de qualquer espaço de endereçamento reservado para redes virtuais.
   * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
   * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes. Você pode usar um número de AS privado para esse emparelhamento. Não use 65515.
   * Um hash MD5 se você escolher toouse um. **Isso é opcional**.
     
    Você pode executar Olá tooconfigure cmdlet emparelhamento particular do Azure para o circuito a seguir.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
     
    Você pode usar o cmdlet de saudação abaixo se você escolher toouse um hash MD5.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview privado emparelhamento detalhes do Azure
Você pode obter os detalhes de configuração usando o cmdlet a seguir de saudação

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuração emparelhamento particular do Azure
Você pode atualizar qualquer parte da configuração de saudação usando Olá cmdlet a seguir. O exemplo hello abaixo, Olá VLAN ID de circuito hello está sendo atualizado de 100 too500.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete emparelhamento particular do Azure
Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir.

> [!WARNING]
> Certifique-se de que todas as redes virtuais são desvinculadas do hello circuito de rota expressa antes de executar este cmdlet. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Emparelhamento público do Azure
Esta seção fornece instruções sobre como toocreate, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.

### <a name="toocreate-azure-public-peering"></a>toocreate emparelhamento público do Azure
1. **Importe o módulo do PowerShell de saudação do ExpressRoute.**
   
    Você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello. A seguir Olá execução comandos módulos do Azure e rota expressa Olá tooimport na sessão do PowerShell hello. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Criar um circuito do ExpressRoute**
   
    Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-classic.md) e fornecidos pelo provedor de conectividade de saudação. Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade do Azure público de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, siga as instruções de saudação abaixo.
3. **Verificar tooensure de circuito de rota expressa, que ela é provisionada**
   
    Primeiro, você deve verificar toosee se hello circuito de rota expressa é provisionado e também está habilitado. Consulte o exemplo hello abaixo.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Certifique-se de que o circuito Olá mostra como provisionado e habilitado. Se não estiver, trabalhe com seu tooget do provedor de conectividade seu circuito toohello necessária e o status.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurar o emparelhamento público do Azure para o circuito Olá**
   
    Certifique-se de que você tenha Olá informações a seguir antes de você continuar.
   
   * Um /30 sub-rede para o link primário hello. Precisa ser um prefixo IPv4 público válido.
   * Um /30 sub-rede para o link secundário hello. Precisa ser um prefixo IPv4 público válido.
   * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
   * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
   * Um hash MD5 se você escolher toouse um. **Isso é opcional**.
     
    Você pode executar Olá após tooconfigure cmdlet emparelhamento público do Azure para o circuito
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
     
    Você pode usar o cmdlet de saudação abaixo se você escolher toouse um hash MD5
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Especifique o número de AS como um ASN de emparelhamento e não um ASN de cliente.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview público emparelhamento detalhes do Azure
Você pode obter os detalhes de configuração usando o cmdlet a seguir de saudação

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuração de emparelhamento pública do Azure
Você pode atualizar qualquer parte da configuração de saudação usando Olá cmdlet a seguir

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Olá VLAN ID de circuito hello está sendo atualizado de 200 too600 em Olá exemplo acima.

### <a name="toodelete-azure-public-peering"></a>toodelete emparelhamento público do Azure
Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Emparelhamento da Microsoft
Esta seção fornece instruções sobre como toocreate, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa. 

### <a name="toocreate-microsoft-peering"></a>toocreate emparelhamento da Microsoft
1. **Importe o módulo do PowerShell de saudação do ExpressRoute.**
   
    Você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello. A seguir Olá execução comandos módulos do Azure e rota expressa Olá tooimport na sessão do PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Criar um circuito do ExpressRoute**
   
    Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-classic.md) e fornecidos pelo provedor de conectividade de saudação. Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, siga as instruções de saudação abaixo.
3. **Verificar tooensure de circuito de rota expressa, que ela é provisionada**
   
    Primeiro, você deve verificar toosee se Olá circuito ExpressRoute está em estado provisionado e habilitado.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Certifique-se de que o circuito Olá mostra como provisionado e habilitado. Se não estiver, trabalhe com seu tooget do provedor de conectividade seu circuito toohello necessária e o status.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurar o emparelhamento do circuito de saudação do Microsoft**
   
    Certifique-se de que você tenha Olá seguintes informações antes de continuar.
   
   * Um /30 sub-rede para o link primário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
   * Um /30 sub-rede para o link secundário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
   * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
   * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
   * Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação. Somente prefixos de endereços IP públicos são aceitos. Você pode enviar uma lista separada por vírgulas se você planejar toosend um conjunto de prefixos. Esses prefixos devem ser registrado tooyou em um RIR / IRR.
   * Cliente ASN: Se você estiver publicidade prefixos que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, que eles são registrados. **Isso é opcional**.
   * Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.
   * Um hash MD5, se você escolher toouse um. **Isso é opcional.**
     
    Você pode executar Olá após pering de Microsoft tooconfigure cmdlet para o circuito
     
        New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>tooview detalhes de emparelhamento da Microsoft
Você pode obter os detalhes de configuração usando Olá cmdlet a seguir.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate configuração de emparelhamento da Microsoft
Você pode atualizar qualquer parte da configuração de saudação usando Olá cmdlet a seguir.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete emparelhamento da Microsoft
Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Próximas etapas
Em seguida, [vincular um circuito de rota expressa do tooan de VNet](expressroute-howto-linkvnet-classic.md).

* Para obter mais informações sobre fluxos de trabalho, veja [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).
* Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).

