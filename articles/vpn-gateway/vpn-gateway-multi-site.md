---
title: "Conectar sites de toomultiple uma rede virtual usando o PowerShell e o Gateway de VPN: clássico | Microsoft Docs"
description: "Este artigo lhe orientará conectar vários local no local sites tooa rede virtual usando um Gateway de VPN para o modelo de implantação clássico hello."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="aca64-103">Adicionar um tooa de conexão Site a Site VNet com uma conexão de gateway VPN existente (clássico)</span><span class="sxs-lookup"><span data-stu-id="aca64-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aca64-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aca64-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="aca64-105">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="aca64-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="aca64-106">Este artigo orienta você a usar o PowerShell tooadd Site a Site (S2S) conexões tooa gateway VPN que tenha uma conexão existente.</span><span class="sxs-lookup"><span data-stu-id="aca64-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="aca64-107">Esse tipo de conexão geralmente é chamado tooas uma configuração de "multissite".</span><span class="sxs-lookup"><span data-stu-id="aca64-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="aca64-108">Olá etapas neste artigo se aplicam redes toovirtual criadas usando o modelo de implantação clássico hello (também conhecido como gerenciamento de serviço).</span><span class="sxs-lookup"><span data-stu-id="aca64-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="aca64-109">Essas etapas não se aplicam a configurações de conexão coexistentes tooExpressRoute/Site a Site.</span><span class="sxs-lookup"><span data-stu-id="aca64-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="aca64-110">Modelos e métodos de implantação</span><span class="sxs-lookup"><span data-stu-id="aca64-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="aca64-111">Atualizamos esta tabela conforme novos artigos e ferramentas adicionais ficam disponíveis para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="aca64-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="aca64-112">Quando um artigo está disponível, vinculamos diretamente tooit desta tabela.</span><span class="sxs-lookup"><span data-stu-id="aca64-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="aca64-113">Sobre a conexão</span><span class="sxs-lookup"><span data-stu-id="aca64-113">About connecting</span></span>

<span data-ttu-id="aca64-114">Você pode se conectar a vários locais sites tooa única rede virtual.</span><span class="sxs-lookup"><span data-stu-id="aca64-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="aca64-115">Isso é especialmente atraente para criar soluções de nuvem híbrida.</span><span class="sxs-lookup"><span data-stu-id="aca64-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="aca64-116">Criar um gateway de rede virtual do Azure multissite conexão tooyour é toocreating semelhante a outras conexões Site a Site.</span><span class="sxs-lookup"><span data-stu-id="aca64-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="aca64-117">Na verdade, você pode usar um gateway de VPN do Azure existente, desde que o gateway de saudação é dinâmico (baseado em rota).</span><span class="sxs-lookup"><span data-stu-id="aca64-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="aca64-118">Se você já tiver uma rede virtual do gateway estático tooyour conectado, você pode alterar Olá toodynamic de tipo de gateway sem a necessidade de rede virtual do toorebuild Olá em vários locais do pedido tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="aca64-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="aca64-119">Antes de alterar o tipo de roteamento hello, certifique-se de que o gateway VPN local oferece suporte a configurações de VPN com base em rota.</span><span class="sxs-lookup"><span data-stu-id="aca64-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="aca64-120">![diagrama multissites](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span><span class="sxs-lookup"><span data-stu-id="aca64-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="aca64-121">Pontos tooconsider</span><span class="sxs-lookup"><span data-stu-id="aca64-121">Points tooconsider</span></span>

<span data-ttu-id="aca64-122">**Você não será capaz de toouse Olá toomake portal alterações toothis VPN.**</span><span class="sxs-lookup"><span data-stu-id="aca64-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="aca64-123">É necessário um arquivo de configuração de rede toomake alterações toohello em vez de usar o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="aca64-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="aca64-124">Se você fizer alterações no portal de hello, elas vão substituir as configurações de referência multilocal para essa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="aca64-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="aca64-125">Você deve se sentir confortável usando o arquivo de configuração de rede de saudação pelo tempo de saudação você concluiu o procedimento de multissite hello.</span><span class="sxs-lookup"><span data-stu-id="aca64-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="aca64-126">No entanto, se você tiver várias pessoas trabalhando em sua configuração de rede, será necessário toomake-se de que todos sabem desta limitação.</span><span class="sxs-lookup"><span data-stu-id="aca64-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="aca64-127">Isso não significa que você não pode usar o portal de saudação em todos os.</span><span class="sxs-lookup"><span data-stu-id="aca64-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="aca64-128">Você pode usá-lo para tudo, exceto fazer configuração alterações toothis rede virtual específico.</span><span class="sxs-lookup"><span data-stu-id="aca64-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="aca64-129">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="aca64-129">Before you begin</span></span>

<span data-ttu-id="aca64-130">Antes de começar a configuração, verifique se Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="aca64-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="aca64-131">Hardware de VPN compatível para cada caminho no local.</span><span class="sxs-lookup"><span data-stu-id="aca64-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="aca64-132">Verificar [sobre dispositivos VPN para conectividade de rede Virtual](vpn-gateway-about-vpn-devices.md) tooverify se o dispositivo de saudação que você deseja toouse é algo que é conhecido toobe compatível.</span><span class="sxs-lookup"><span data-stu-id="aca64-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="aca64-133">Um endereço IP IPv4 público voltado para o exterior para cada dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="aca64-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="aca64-134">endereço IP de saudação não pode ser localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="aca64-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="aca64-135">Isso é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="aca64-135">This is requirement.</span></span>
* <span data-ttu-id="aca64-136">Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="aca64-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="aca64-137">Verifique se que você instalou a versão de gerenciamento de serviço (SM) Olá na versão do Gerenciador de recursos de toohello de adição.</span><span class="sxs-lookup"><span data-stu-id="aca64-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="aca64-138">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="aca64-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="aca64-139">Alguém que seja proficiente na configuração de seu hardware de VPN.</span><span class="sxs-lookup"><span data-stu-id="aca64-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="aca64-140">Você terá toohave uma compreensão sólida de como tooconfigure seu dispositivo VPN ou trabalhar com alguém que pertença.</span><span class="sxs-lookup"><span data-stu-id="aca64-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="aca64-141">intervalos de endereços IP Hello que você deseja toouse para sua rede virtual (se você ainda não tiver criado uma).</span><span class="sxs-lookup"><span data-stu-id="aca64-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="aca64-142">intervalos de endereços IP de saudação para cada um dos sites de rede local Olá que você vai se conectar ao.</span><span class="sxs-lookup"><span data-stu-id="aca64-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="aca64-143">Você precisará toomake-se de que os intervalos de endereço IP de saudação para cada um dos sites de rede local Olá que você deseja tooconnect toodo não se sobrepõem.</span><span class="sxs-lookup"><span data-stu-id="aca64-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="aca64-144">Caso contrário, portal hello ou hello API REST rejeitará configuração hello está sendo carregada.</span><span class="sxs-lookup"><span data-stu-id="aca64-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="aca64-145">Por exemplo, se você tiver dois sites de rede local que contêm Olá IP endereço intervalo 10.2.3.0/24 e você tiver um pacote com um endereço de destino 10.2.3.3, o Azure não saberia qual site você deseja intervalos de endereços do toosend Olá pacote toobecause Olá são sobreposição.</span><span class="sxs-lookup"><span data-stu-id="aca64-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="aca64-146">problemas de roteamento de tooprevent Azure não permite que você tooupload um arquivo de configuração com sobreposição de intervalos.</span><span class="sxs-lookup"><span data-stu-id="aca64-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="aca64-147">1. Criar uma VPN site a site</span><span class="sxs-lookup"><span data-stu-id="aca64-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="aca64-148">Se você já tiver uma VPN site a site com um gateway de roteamento dinâmico, ótimo!</span><span class="sxs-lookup"><span data-stu-id="aca64-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="aca64-149">Você pode continuar muito[exportar definições de configuração de rede virtual Olá](#export).</span><span class="sxs-lookup"><span data-stu-id="aca64-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="aca64-150">Se não, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="aca64-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="aca64-151">Se você já tiver uma rede virtual site a site, mas ela tiver um gateway de roteamento estático (baseado em política):</span><span class="sxs-lookup"><span data-stu-id="aca64-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="aca64-152">Altere o tipo de gateway toodynamic roteamento.</span><span class="sxs-lookup"><span data-stu-id="aca64-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="aca64-153">Uma VPN multissites exige um gateway de roteamento dinâmico (também chamado de baseado em rota).</span><span class="sxs-lookup"><span data-stu-id="aca64-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="aca64-154">tipo do toochange seu gateway, você precisa excluir de toofirst Olá gateway existente e criar um novo.</span><span class="sxs-lookup"><span data-stu-id="aca64-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="aca64-155">Para obter instruções, consulte [como toochange Olá tipo de roteamento de VPN para o seu gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="aca64-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="aca64-156">Configure seu novo gateway e crie seu túnel de VPN.</span><span class="sxs-lookup"><span data-stu-id="aca64-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="aca64-157">Para obter instruções, consulte [configurar um Gateway de VPN no Portal clássico do Azure de saudação](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="aca64-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="aca64-158">Primeiro, altere o tipo de gateway toodynamic roteamento.</span><span class="sxs-lookup"><span data-stu-id="aca64-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="aca64-159">Se você não tiver uma rede virtual site a site:</span><span class="sxs-lookup"><span data-stu-id="aca64-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="aca64-160">Criar sua rede virtual Site a Site usando estas instruções: [criar uma rede Virtual com uma Conexão de VPN Site a Site no Portal clássico do Azure de saudação](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="aca64-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="aca64-161">Configure um gateway de roteamento dinâmico usando estas instruções: [Configurar um gateway de VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="aca64-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="aca64-162">Ser tooselect se **roteamento dinâmico** para seu tipo de gateway.</span><span class="sxs-lookup"><span data-stu-id="aca64-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="aca64-163"><a name="export"></a>2. Exportar o arquivo de configuração de rede Olá</span><span class="sxs-lookup"><span data-stu-id="aca64-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="aca64-164">Exporte o arquivo de configuração de rede do Azure executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="aca64-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="aca64-165">Você pode alterar o local de saudação do hello tooexport tooa diferentes local do arquivo se necessário.</span><span class="sxs-lookup"><span data-stu-id="aca64-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="aca64-166">3. Arquivo de configuração de rede Olá aberto</span><span class="sxs-lookup"><span data-stu-id="aca64-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="aca64-167">Abra o arquivo de configuração de rede de saudação que você baixou na última etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="aca64-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="aca64-168">Use qualquer editor de xml que desejar.</span><span class="sxs-lookup"><span data-stu-id="aca64-168">Use any xml editor that you like.</span></span> <span data-ttu-id="aca64-169">arquivo Hello deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="aca64-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="aca64-170">4. Adicionar referências a vários sites</span><span class="sxs-lookup"><span data-stu-id="aca64-170">4. Add multiple site references</span></span>
<span data-ttu-id="aca64-171">Quando você adicionar ou remove informações de referência do site, você fará alterações de configuração toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="aca64-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="aca64-172">Adicionando uma nova referência de site local aciona o Azure toocreate um novo túnel.</span><span class="sxs-lookup"><span data-stu-id="aca64-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="aca64-173">O exemplo hello abaixo, a configuração de rede de saudação é para uma conexão de site único.</span><span class="sxs-lookup"><span data-stu-id="aca64-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="aca64-174">Salve o arquivo de hello quando você terminar de fazer suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aca64-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="aca64-175">referências a sites adicionais tooadd (criar uma configuração de vários local), basta adicionar linhas "LocalNetworkSiteRef" adicionais, conforme mostrado no exemplo hello abaixo:</span><span class="sxs-lookup"><span data-stu-id="aca64-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="aca64-176">5. Importar arquivo de configuração de rede Olá</span><span class="sxs-lookup"><span data-stu-id="aca64-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="aca64-177">Importar arquivo de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="aca64-177">Import hello network configuration file.</span></span> <span data-ttu-id="aca64-178">Quando você importar este arquivo com alterações hello, novos túneis de saudação serão adicionados.</span><span class="sxs-lookup"><span data-stu-id="aca64-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="aca64-179">túneis Olá usará o gateway de dinâmico Olá que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="aca64-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="aca64-180">Você pode usar portal clássico do hello, ou arquivo de saudação do PowerShell tooimport.</span><span class="sxs-lookup"><span data-stu-id="aca64-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="aca64-181">6. Baixar chaves</span><span class="sxs-lookup"><span data-stu-id="aca64-181">6. Download keys</span></span>
<span data-ttu-id="aca64-182">Depois de adicionar os novos túneis, use Olá PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Olá IPsec/IKE chaves pré-compartilhadas para cada túnel.</span><span class="sxs-lookup"><span data-stu-id="aca64-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="aca64-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aca64-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="aca64-184">Se preferir, você também pode usar o hello *obter Gateway chave compartilhada rede Virtual* tooget da API REST Olá chaves pré-compartilhadas.</span><span class="sxs-lookup"><span data-stu-id="aca64-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="aca64-185">7. Verificar as conexões</span><span class="sxs-lookup"><span data-stu-id="aca64-185">7. Verify your connections</span></span>
<span data-ttu-id="aca64-186">Verificar o status do túnel multissites hello.</span><span class="sxs-lookup"><span data-stu-id="aca64-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="aca64-187">Depois de baixar chaves Olá para cada túnel, você desejará tooverify conexões.</span><span class="sxs-lookup"><span data-stu-id="aca64-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="aca64-188">Use 'Get-AzureVnetConnection' tooget túneis de uma lista de rede virtual, conforme mostrado no exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="aca64-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="aca64-189">VNet1 é o nome de saudação do hello VNet.</span><span class="sxs-lookup"><span data-stu-id="aca64-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="aca64-190">Exemplo de retorno:</span><span class="sxs-lookup"><span data-stu-id="aca64-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="aca64-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aca64-191">Next steps</span></span>

<span data-ttu-id="aca64-192">toolearn mais informações sobre Gateways VPN, consulte [sobre Gateways de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="aca64-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
