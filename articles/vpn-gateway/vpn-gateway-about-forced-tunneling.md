---
title: "Configurar o túnel forçado para conexões Site a Site: clássico | Microsoft Docs"
description: "Como tooyour voltar do tráfego de Internet associado do tooredirect ou 'force' todos os no local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="a010e-103">Configurar o túnel forçado usando o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="a010e-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="a010e-104">Forçado permite redirecionar ou "forçar" todos os direcionado à Internet tráfego tooyour back local através de um túnel VPN Site a Site para inspeção e auditoria de túnel.</span><span class="sxs-lookup"><span data-stu-id="a010e-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="a010e-105">Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais.</span><span class="sxs-lookup"><span data-stu-id="a010e-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="a010e-106">Sem o túnel forçado, o tráfego direcionado à Internet de suas VMs no Azure sempre percorrerá da infraestrutura de rede do Azure diretamente out toohello Internet, sem Olá opção tooallow você tráfego de saudação tooinspect ou auditoria.</span><span class="sxs-lookup"><span data-stu-id="a010e-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="a010e-107">Acesso não autorizado pode levar a divulgação de tooinformation ou outros tipos de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="a010e-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="a010e-108">Este artigo o orienta pela configuração forçado túnel para redes virtuais criadas usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="a010e-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="a010e-109">O túnel forçado pode ser configurado usando o PowerShell, não por meio do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a010e-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="a010e-110">Se você quiser tooconfigure encapsulamento para modelo de implantação do Gerenciador de recursos de saudação forçado, selecione artigo clássico Olá lista suspensa a seguir:</span><span class="sxs-lookup"><span data-stu-id="a010e-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a010e-111">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="a010e-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="a010e-112">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a010e-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="a010e-113">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="a010e-113">Requirements and considerations</span></span>
<span data-ttu-id="a010e-114">O túnel forçado no Azure é configurado por meio de UDR (rotas de definidas pelo usuário) de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a010e-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="a010e-115">Redirecionar o tráfego tooan local do site é expressa como um gateway de VPN do Azure toohello rota padrão.</span><span class="sxs-lookup"><span data-stu-id="a010e-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="a010e-116">Olá, seção a seguir lista limitação atual Olá da tabela de roteamento hello e rotas para uma rede Virtual do Azure:</span><span class="sxs-lookup"><span data-stu-id="a010e-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="a010e-117">Cada sub-rede de rede virtual tem uma tabela de roteamento interna do sistema.</span><span class="sxs-lookup"><span data-stu-id="a010e-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="a010e-118">tabela de roteamento de sistema Olá tem Olá três grupos de rotas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a010e-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="a010e-119">**Rotas de rede virtual locais:** diretamente toohello VMs de destino na Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a010e-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="a010e-120">**Rotas locais:** toohello gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="a010e-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="a010e-121">**Rota padrão:** toohello diretamente da Internet.</span><span class="sxs-lookup"><span data-stu-id="a010e-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="a010e-122">Pacotes destinados toohello endereços IP privados não cobertos por rotas Olá dois anterior serão removidos.</span><span class="sxs-lookup"><span data-stu-id="a010e-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="a010e-123">Com o lançamento de saudação de rotas definidas pelo usuário, crie um tooadd de tabela de roteamento uma rota padrão e, em seguida, associar Olá roteamento tabela tooyour VNet sub-redes tooenable forçado túnel nessas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="a010e-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="a010e-124">É necessário tooset "site padrão" entre a rede virtual de toohello conectado Olá de sites locais entre locais.</span><span class="sxs-lookup"><span data-stu-id="a010e-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="a010e-125">O túnel forçado deve ser associado a uma Rede Virtual que tem um gateway de VPN de roteamento dinâmico (e não um gateway estático).</span><span class="sxs-lookup"><span data-stu-id="a010e-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="a010e-126">Túnel forçado do ExpressRoute não está configurado por meio desse mecanismo, mas em vez disso, é habilitado por anuncia uma rota padrão por meio de saudação ExpressRoute BGP sessões de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="a010e-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="a010e-127">Consulte Olá [documentação de rota expressa](https://azure.microsoft.com/documentation/services/expressroute/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a010e-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="a010e-128">Visão geral de configuração</span><span class="sxs-lookup"><span data-stu-id="a010e-128">Configuration overview</span></span>
<span data-ttu-id="a010e-129">Em Olá exemplo a seguir, Olá front-end subrede não será forçada encapsulado.</span><span class="sxs-lookup"><span data-stu-id="a010e-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="a010e-130">cargas de trabalho Olá na sub-rede de front-end Olá podem continuar tooaccept e responde solicitações toocustomer de saudação Internet diretamente.</span><span class="sxs-lookup"><span data-stu-id="a010e-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="a010e-131">Olá sub-redes de camada intermediária e back-end são forçados encapsulado.</span><span class="sxs-lookup"><span data-stu-id="a010e-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="a010e-132">Quaisquer conexões de saída da toohello duas sub-redes Internet será tooan forçada ou redirecionado de volta no site local por meio de saudação que encapsulamentos VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="a010e-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="a010e-133">Isso permite que você toorestrict e inspecione o acesso à Internet de suas máquinas virtuais ou serviços no Azure, de nuvem enquanto continua tooenable sua arquitetura de serviço de várias camadas necessária.</span><span class="sxs-lookup"><span data-stu-id="a010e-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="a010e-134">Você também pode aplicar forçado túnel toohello redes virtuais inteiras se não houver nenhuma carga de trabalho para a Internet em suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="a010e-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Túnel forçado](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="a010e-136">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a010e-136">Before you begin</span></span>
<span data-ttu-id="a010e-137">Verifique se você tem Olá itens antes de começar a configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="a010e-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="a010e-138">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a010e-138">An Azure subscription.</span></span> <span data-ttu-id="a010e-139">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a010e-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a010e-140">Uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="a010e-140">A configured virtual network.</span></span> 
* <span data-ttu-id="a010e-141">versão mais recente de saudação do hello cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="a010e-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="a010e-142">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a010e-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="a010e-143">Configurar o túnel forçado</span><span class="sxs-lookup"><span data-stu-id="a010e-143">Configure forced tunneling</span></span>
<span data-ttu-id="a010e-144">Olá procedimento a seguir ajudarão você a especificar um túnel forçado para uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a010e-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="a010e-145">etapas de configuração de saudação correspondem toohello arquivo de configuração de rede de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a010e-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="a010e-146">Neste exemplo, a rede virtual de saudação 'MultiTier-VNet' tem três sub-redes: sub-redes 'Front-end', 'Midtier' e 'Back-end', com conexões locais entre quatro: 'DefaultSiteHQ' e três ramificações.</span><span class="sxs-lookup"><span data-stu-id="a010e-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="a010e-147">Olá etapas definir Olá 'DefaultSiteHQ' como conexão de site saudação padrão para túnel forçado e configurar Olá Midtier e Backend sub-redes toouse túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="a010e-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="a010e-148">Crie uma tabela de roteamento.</span><span class="sxs-lookup"><span data-stu-id="a010e-148">Create a routing table.</span></span> <span data-ttu-id="a010e-149">Use Olá toocreate cmdlet a seguir em sua tabela de rotas.</span><span class="sxs-lookup"><span data-stu-id="a010e-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="a010e-150">Adicione uma tabela de roteamento de toohello de rota padrão.</span><span class="sxs-lookup"><span data-stu-id="a010e-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="a010e-151">Olá, exemplo a seguir adiciona uma rota toohello tabela de roteamento padrão criada na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="a010e-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="a010e-152">Observe que Olá somente rota com suporte é o prefixo de destino de saudação de "0.0.0.0/0" toohello NextHop "VPNGateway".</span><span class="sxs-lookup"><span data-stu-id="a010e-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="a010e-153">Associe sub-redes de toohello de tabela de roteamento hello.</span><span class="sxs-lookup"><span data-stu-id="a010e-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="a010e-154">Depois de uma tabela de roteamento é criada e adicionada uma rota, use Olá tooadd de exemplo a seguir ou associar a sub-rede de rede virtual Olá rota tabela tooa.</span><span class="sxs-lookup"><span data-stu-id="a010e-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="a010e-155">exemplo Hello adiciona Olá rota tabela "MyRouteTable" toohello Midtier e sub-redes de back-end do VNet MultiTier-VNet.</span><span class="sxs-lookup"><span data-stu-id="a010e-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="a010e-156">Atribua um site padrão ao túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="a010e-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="a010e-157">Em Olá anterior da etapa, scripts de cmdlet de exemplo hello criado Olá tabela de roteamento em associados Olá tootwo de tabela de rota de sub-redes de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="a010e-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="a010e-158">etapa restante Olá é tooselect um site local entre conexões de vários locais de saudação da rede virtual Olá Olá site ou túnel padrão.</span><span class="sxs-lookup"><span data-stu-id="a010e-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="a010e-159">Cmdlets do PowerShell adicionais</span><span class="sxs-lookup"><span data-stu-id="a010e-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="a010e-160">toodelete uma tabela de rotas</span><span class="sxs-lookup"><span data-stu-id="a010e-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="a010e-161">toolist uma tabela de rotas</span><span class="sxs-lookup"><span data-stu-id="a010e-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="a010e-162">toodelete uma rota de uma tabela de rota</span><span class="sxs-lookup"><span data-stu-id="a010e-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="a010e-163">tooremove uma rota de uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="a010e-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="a010e-164">tabela de rotas Olá toolist associada a uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="a010e-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="a010e-165">tooremove um site padrão de um gateway de VPN VNet</span><span class="sxs-lookup"><span data-stu-id="a010e-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```