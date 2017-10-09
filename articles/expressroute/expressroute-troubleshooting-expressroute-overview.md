---
title: "Verificando a conectividade: Guia de Solução de Problemas do Azure ExpressRoute | Microsoft Docs"
description: "Esta página fornece instruções sobre solução de problemas e validando a conectividade de tooend final de um circuito de rota expressa."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>Verificando a conectividade do ExpressRoute
Rota expressa, que se estende uma rede local para o hello nuvem da Microsoft em uma conexão privada que é facilitada por um provedor de conectividade, envolve Olá três zonas de rede distintas a seguir:

-   Rede do Cliente
-   Rede do Provedor
-   Microsoft Datacenter

Olá finalidade deste documento é toohelp usuário tooidentify onde (ou até mesmo se) existe um problema de conectividade e em qual zona, assim, tooseek Ajuda do problema de saudação tooresolve equipe apropriada. Se o suporte da Microsoft é um problema de tooresolve necessária, abra um tíquete de suporte com [Microsoft Support][Support].

> [!IMPORTANT]
> Este documento é pretendido toohelp diagnosticar e corrigir problemas simples. Não é pretendido toobe uma substituição para o suporte da Microsoft. Abrir um tíquete de suporte com [Microsoft Support] [ Support] se você estiver toosolve não é possível problema de saudação usando Olá diretrizes fornecidas.
>
>

## <a name="overview"></a>Visão geral
Olá diagrama a seguir mostra a conectividade lógica saudação de uma rede de tooMicrosoft de rede do cliente usando o ExpressRoute.
[![1]][1]

Olá precede o diagrama, Olá números indicam pontos principais de rede. pontos de saudação à rede são referenciados geralmente este artigo por seu número associado.

Dependendo da conectividade de rota expressa Olá modelo (colocalização do Exchange de nuvem, ponto a ponto Ethernet Conexão ou para qualquer (IPVPN)) Olá rede pontos 3 e 4 podem ser comutadores (dispositivos de camada 2). pontos de chave de rede Olá ilustrados são da seguinte maneira:

1.  Dispositivo de computação de cliente (por exemplo, um servidor ou PC)
2.  CEs: roteadores de borda do cliente 
3.  PEs (voltados para CE): roteadores/comutadores de borda do provedor que estão voltados para os roteadores de borda do cliente. Chamado tooas PE CEs neste documento.
4.  PEs (voltados para MSEE): roteadores/comutadores de borda do provedor que estão voltados para MSEEs. Chamado tooas PE MSEEs neste documento.
5.  MSEEs: roteadores ExpressRoute do MSEE (Microsoft Enterprise Edge)
6.  Gateway de Rede Virtual (VNet)
7.  Computação dispositivo Olá VNet do Azure

Se os modelos de conectividade de posicionamento do Exchange de nuvem ou ponto a ponto Ethernet Conexão hello são usados, o roteador de borda do cliente hello (2) seria estabelecer BGP de emparelhamento com MSEEs (5). Os pontos de rede 3 e 4 ainda existiriam, mas seriam um tanto transparentes como dispositivos de rede de Camada 2.

Se o modelo de conectividade Olá para qualquer (IPVPN) for usado, Olá PEs (voltado para a MSEE) (4) seria estabelecer BGP de emparelhamento com MSEEs (5). Rotas depois propagará toohello back rede de cliente por meio da rede do provedor de serviços IPVPN de saudação.

>[!NOTE]
>Para alta disponibilidade do ExpressRoute, a Microsoft exige um par redundante de sessões BGP entre MSEEs (5) e PE-MSEEs (4). Recomenda-se também mobilizar um par redundante de caminhos de rede entre a rede do cliente e PE-CEs. No entanto, no modelo de conexão para qualquer (IPVPN), um único dispositivo CE (2) pode ser conectado tooone ou mais PEs (3).
>
>

toovalidate um circuito de rota expressa, Olá etapas a seguir são abordados (com o ponto de rede Olá indicado pelo número de saudação associado):
1. [Validar o estado e o provisionamento do circuito (5)](#validate-circuit-provisioning-and-state)
2. [Validar que pelo menos um emparelhamento do ExpressRoute está configurado (5)](#validate-peering-configuration)
3. [Validar ARP entre o provedor de serviços Microsoft e hello (link entre 4 e 5)](#validate-arp-between-microsoft-and-the-service-provider)
4. [Validar o BGP e rotas Olá MSEE (BGP entre too5 4 e 5 too6 se estiver conectada a uma rede virtual)](#validate-bgp-and-routes-on-the-msee)
5. [Saudação de verificação de estatísticas de tráfego (tráfego que passa pelo 5)](#check-the-traffic-statistics)

Mais validações e verificações serão adicionadas em Olá futuras, visite mensal!

##<a name="validate-circuit-provisioning-and-state"></a>Validar o estado e o provisionamento do circuito
Independentemente do modelo de conectividade de saudação, um circuito ExpressRoute tem toobe criado e, portanto, um serviço de chave gerada para o provisionamento do circuito. O provisionamento de um circuito do ExpressRoute estabelece uma conexão de Camada 2 redundante entre PE-MSEEs (4) e MSEEs (5). Para obter mais informações sobre como toocreate, modificar, configurar e verificar um circuito ExpressRoute, consulte o artigo Olá [criar e modificar um circuito ExpressRoute][CreateCircuit].

>[!TIP]
>Uma chave de serviço identifica exclusivamente um circuito do ExpressRoute. Essa chave é necessária para a maioria dos comandos do powershell Olá mencionados neste documento. Além disso, se você precisar de assistência da Microsoft ou de um parceiro de rota expressa tootroubleshoot um problema de rota expressa, fornecer serviço Olá tooreadily chave identificar circuito hello.
>
>

###<a name="verification-via-hello-azure-portal"></a>Verificação via Olá portal do Azure
No portal do Azure de Olá, status de saudação de um circuito de rota expressa pode ser verificado selecionando ![2][2] em Olá menu da barra de lado esquerdo e, em seguida, selecionando Olá circuito de rota expressa. Selecionando uma rota expressa circuito listado em "Todos os recursos" abre a folha de circuito de rota expressa de saudação. Em Olá ![3][3] seção da folha de Olá Olá essentials é listado como mostrado na seguinte captura de tela de saudação do ExpressRoute:

![4][4]    

Em Olá Essentials de rota expressa, *circuito status* indica o status de saudação do circuito Olá Olá lado da Microsoft. *Status do provedor* indica se o circuito de saudação foi *provisionado ou não provisionado* no lado do provedor de serviços de saudação. 

Para um toobe de circuito de rota expressa operacional, Olá *circuito status* devem ser *habilitado* e hello *status do provedor* devem ser *provisionado*.

>[!NOTE]
>Se hello *circuito status* não é habilitado, entre em contato com [Microsoft Support][Support]. Se hello *status do provedor* não é provisionado, entre em contato com seu provedor de serviços.
>
>

###<a name="verification-via-powershell"></a>Verificação por meio do PowerShell
toolist todos Olá circuitos de rota expressa em um grupo de recursos, use Olá comando a seguir:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>Você pode obter o nome do seu grupo de recursos por meio de saudação portal do Azure. Consulte a subseção anterior Olá deste documento e anote que esse nome de grupo de recursos de saudação está listado na captura de tela de exemplo hello.
>
>

tooselect um circuito de rota expressa específico em um grupo de recursos, use Olá comando a seguir:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Uma resposta de exemplo é:

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm se um circuito ExpressRoute está funcionando, preste atenção especial toohello campos a seguir:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Se hello *CircuitProvisioningState* não é habilitado, entre em contato com [Microsoft Support][Support]. Se hello *ServiceProviderProvisioningState* não é provisionado, entre em contato com seu provedor de serviços.
>
>

###<a name="verification-via-powershell-classic"></a>Verificação por meio do PowerShell (Clássico)
toolist todos Olá circuitos de rota expressa em uma assinatura, use Olá comando a seguir:

    Get-AzureDedicatedCircuit

tooselect um circuito de rota expressa específico, use Olá comando a seguir:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Uma resposta de exemplo é:

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm se um circuito ExpressRoute está funcionando, preste atenção especial toohello campos a seguir: ServiceProviderProvisioningState: Status provisionado: habilitada

>[!NOTE]
>Se hello *Status* não é habilitado, entre em contato com [Microsoft Support][Support]. Se hello *ServiceProviderProvisioningState* não é provisionado, entre em contato com seu provedor de serviços.
>
>

##<a name="validate-peering-configuration"></a>Validar Configuração de Emparelhamento
Provedor de serviços de Olá Olá concluído provisionamento do circuito de rota expressa hello, após uma configuração de roteamento pode ser criada pela Olá circuito de rota expressa entre MSEE-PRs (4) e MSEEs (5). Cada circuito de rota expressa pode ter um, dois ou três contextos de roteamentos habilitados: emparelhamento particular do Azure (tráfego tooprivate redes virtuais no Azure), emparelhamento público do Azure (tráfego toopublic endereços IP no Azure) e (tráfego tooOffice 365 emparelhamento da Microsoft e Dynamics 365). Para obter mais informações sobre como toocreate e modificar a configuração de roteamento, consulte o artigo Olá [criar e modificar o roteamento para um circuito ExpressRoute][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Verificação via Olá portal do Azure
>[!IMPORTANT]
>Há um bug conhecido no hello portal do Azure no qual os emparelhamentos de rota expressa são *não* mostrado no portal de saudação se configurado pelo provedor de serviços de saudação. Adicionando emparelhamentos de rota expressa por meio do portal de saudação ou o PowerShell *substitui as configurações do provedor de serviço Olá*. Essa ação quebras Olá roteamento no circuito de rota expressa hello e requer suporte Olá Olá configurações de serviço provedor toorestore hello e restabelecer o roteamento normal. Modificar emparelhamentos de rota expressa Olá apenas se você tiver certeza de que o provedor de serviços hello está fornecendo serviços de camada 2 apenas!
>
>

<p/>
>[!NOTE]
>Se fornecida pelo Olá emparelhamentos de provedor e hello serviço estão em branco no portal de saudação camada 3, o PowerShell pode ser usado toosee Olá serviço provedor configurado configurações.
>
>

No hello portal do Azure, o status de um circuito de rota expressa pode ser verificado selecionando ![2][2] em Olá menu da barra de lado esquerdo e, em seguida, selecionando Olá circuito de rota expressa. Selecionando uma rota expressa circuito listado em "Todos os recursos" abrir folha de circuito de rota expressa hello. Em Olá ![3][3] seção da folha de Olá Olá essentials é listado como mostrado na seguinte captura de tela de saudação do ExpressRoute:

![5][5]

Em Olá anterior de exemplo, como observado Azure contexto de roteamento de emparelhamento privado é habilitado, enquanto pública do Azure e contextos de roteamento emparelhamento Microsoft não estão habilitados. Um contexto de emparelhamento habilitado com êxito também teria sub-redes de primárias e secundárias ponto a ponto (necessária para BGP) Olá listados. subredes Olá /30 são usados para endereço IP de interface de saudação do hello MSEEs e MSEEs PE. 

>[!NOTE]
>Se um emparelhamento não estiver habilitado, verifique se sub-redes primários e secundários Olá atribuídas correspondem configuração Olá MSEEs PE. Se não, toochange Olá configuração em roteadores MSEE, consulte muito[criar e modificar o roteamento para um circuito de rota expressa][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>Verificação por meio do PowerShell
tooget hello Azure privado emparelhamento detalhes de configuração, use Olá comandos a seguir:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Uma resposta de exemplo para um emparelhamento privado configurado com êxito é:

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Um contexto de emparelhamento habilitado com êxito teria prefixos de endereço primário e secundário Olá listados. subredes Olá /30 são usados para endereço IP de interface de saudação do hello MSEEs e MSEEs PE.

tooget hello Azure público emparelhamento detalhes de configuração, use Olá comandos a seguir:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget Olá emparelhamento configuração detalhes da Microsoft, use Olá comandos a seguir:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Se um emparelhamento não for configurado, haverá uma mensagem de erro. Uma resposta de exemplo, quando Olá mencionado emparelhamento (público do Azure emparelhamento neste exemplo) não está configurada no circuito de saudação:

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Se um emparelhamento não estiver habilitado, verifique se Olá primários e secundários sub-redes atribuídas correspondência Olá configuração Olá vinculado MSEE PE. Também verifique se hello corrigir *VlanId*, *AzureASN*, e *PeerASN* são usados em MSEEs e se esses valores mapeia toohello usados em Olá vinculado MSEE PE. Se o hash MD5 for escolhido, chave compartilhada Olá deve ser idênticos em par MSEE e MSEE PE. configuração de saudação toochange em roteadores MSEE hello, consulte muito [criar e modificar o roteamento para um circuito ExpressRoute] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>Verificação por meio do PowerShell (Clássico)
tooget hello Azure privado emparelhamento detalhes de configuração, use Olá comando a seguir:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Uma resposta de exemplo para um emparelhamento privado configurado com êxito é:

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

Habilitado com êxito, de um contexto emparelhamento teria sub-redes de par primário e secundário Olá listados. subredes Olá /30 são usados para endereço IP de interface de saudação do hello MSEEs e MSEEs PE.

tooget hello Azure público emparelhamento detalhes de configuração, use Olá comandos a seguir:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget Olá emparelhamento configuração detalhes da Microsoft, use Olá comandos a seguir:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Se emparelhamentos de camada 3 foram definidos pelo provedor de serviços de Olá, Olá emparelhamentos de rota expressa por meio do portal de saudação ou o PowerShell de configuração substitui as configurações do provedor de serviço de saudação. Redefinir as configurações de emparelhamento Olá provedor no lado do requer suporte Olá Olá do provedor de serviços. Modificar emparelhamentos de rota expressa Olá apenas se você tiver certeza de que o provedor de serviços hello está fornecendo serviços de camada 2 apenas!
>
>

<p/>
>[!NOTE]
>Se um emparelhamento não estiver habilitado, verifique se Olá par primário e secundário sub-redes atribuídas correspondência Olá configuração Olá vinculado MSEE PE. Também verifique se hello corrigir *VlanId*, *AzureAsn*, e *PeerAsn* são usados em MSEEs e se esses valores mapeia toohello usados em Olá vinculado MSEE PE. configuração de saudação toochange em roteadores MSEE hello, consulte muito [criar e modificar o roteamento para um circuito ExpressRoute] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Validar ARP entre o provedor de serviços Microsoft e hello
Esta seção usa comandos do PowerShell (Clássico). Se você tiver usando comandos do PowerShell do Azure Resource Manager, verifique se você tem acesso de administrador/coadministrador toohello assinatura por meio de [portal clássico do Azure][OldPortal]. Para solucionar o problema usando o Gerenciador de recursos do Azure comandos, consulte toohello [tabelas obtendo ARP no modelo de implantação do Gerenciador de recursos de saudação] [ ARP] documento.

>[!NOTE]
>tooget ARP, Olá portal do Azure e comandos do PowerShell do Azure Resource Manager pode ser usado. Se forem encontrados erros com comandos do PowerShell do Azure Resource Manager hello, clássicos comandos do PowerShell devem funcionar como PowerShell clássico comandos também funcionam com circuitos ExpressRoute do Gerenciador de recursos do Azure.
>
>

tooget Olá tabela ARP do roteador MSEE primária Olá para emparelhamento privado do hello, use Olá comando a seguir:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Um exemplo de resposta para comando hello, no cenário de êxito hello:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

Da mesma forma, você pode verificar Olá tabela ARP do hello MSEE em Olá *primário*/*secundário* caminho, para *privada* /  *Público*/*Microsoft* emparelhamentos.

Olá exemplo a seguir mostra Olá resposta do comando de saudação para um emparelhamento não existe.

    ARP Info:
       
>[!NOTE]
>Se não tiver Olá tabela ARP desses endereços IP das interfaces de saudação mapeado tooMAC endereços, Olá revisar informações a seguir:
>1. Se Olá primeiro endereço IP de sub-rede Olá /30 atribuído para Olá link entre Olá PR MSEE e MSEE é usado na interface de saudação do MSEE pr Azure sempre usa o endereço IP da segunda Olá para MSEEs.
>2. Confirme se Prezado cliente (C-Tag) e marcas de VLAN de serviço (S-Tag) correspondem em par PR MSEE e MSEE.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>Validar o BGP e rotas Olá MSEE
Esta seção usa comandos do PowerShell (Clássico). Se você tiver usando comandos do PowerShell do Azure Resource Manager, verifique se você tem acesso de administrador/coadministrador toohello assinatura via [portal clássico do Azure][OldPortal]

>[!NOTE]
>tooget informações sobre o BGP, ambos os Olá portal do Azure e comandos do PowerShell do Azure Resource Manager podem ser usados. Se forem encontrados erros com comandos do PowerShell do Azure Resource Manager hello, clássicos comandos do PowerShell devem funcionar como PowerShell clássico comandos também funcionam com circuitos ExpressRoute do Gerenciador de recursos do Azure.
>
>

tooget Olá a tabela de roteamento (vizinho BGP) resumida de um contexto de roteamento específico, use Olá comando a seguir:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Uma resposta de exemplo é:

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Conforme mostrado na saudação anterior de exemplo, o comando de Olá é útil toodetermine de quanto tempo o contexto de roteamento Olá foi estabelecido. Ele também indica o número de prefixos de rota anunciadas pelo roteador de emparelhamento hello.

>[!NOTE]
>Se Olá estado é ativo ou inativo, verifique se Olá par primário e secundário sub-redes atribuídas correspondência Olá configuração Olá vinculado MSEE PE. Também verifique se hello corrigir *VlanId*, *AzureAsn*, e *PeerAsn* são usados em MSEEs e se esses valores mapeia toohello usados em Olá vinculado MSEE PE. Se o hash MD5 for escolhido, chave compartilhada Olá deve ser idênticos em par MSEE e MSEE PE. configuração de saudação toochange em roteadores MSEE hello, consulte muito[criar e modificar o roteamento para um circuito ExpressRoute][CreatePeering].
>
>

<p/>
>[!NOTE]
>Se determinados destinos não estão acessíveis por um emparelhamento particular, consulte a tabela de rota de saudação de saudação MSEEs pertencentes toohello contexto específico de emparelhamento. Se um prefixo correspondente (pode ser NATed IP) está presente na tabela de roteamento hello, verifique se há firewalls/NSG/ACLs no caminho de saudação e permitir o tráfego de saudação.
>
>

tooget Olá tabela completa de roteamento de MSEE em Olá *primário* caminho Olá específico *privada* contexto de roteamento, use Olá comando a seguir:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Um resultado de exemplo com êxito para o comando Olá é:

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

Da mesma forma, você pode verificar a tabela de roteamento de saudação do hello MSEE em hello *primário*/*secundário* caminho, para *privada* / *Pública*/*Microsoft* um contexto de emparelhamento.

Olá exemplo a seguir mostra Olá resposta do comando de saudação para um emparelhamento não existe:

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Saudação de verificação de estatísticas de tráfego
Olá tooget combinadas estatísticas de tráfego de caminho primário e secundário – bytes e sair – de um contexto de emparelhamento, use Olá comando a seguir:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Um exemplo de saída do comando de saudação é:

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

É um exemplo de saída do comando de saudação para um emparelhamento inexistente:

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações ou Ajuda, consulte Olá links a seguir:

- [Suporte da Microsoft][Support]
- [Criar e modificar um circuito do ExpressRoute][CreateCircuit]
- [Criar e modificar o roteamento de um circuito do ExpressRoute][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Conectividade lógica do ExpressRoute"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Ícone Todos os Recursos"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Ícone Visão Geral"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Captura de tela de exemplo do ExpressRoute Essentials"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Captura de tela de exemplo do ExpressRoute Essentials"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






