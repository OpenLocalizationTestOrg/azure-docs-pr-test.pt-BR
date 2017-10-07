---
title: "Conectar redes virtuais clássicas tooAzure VNets Gerenciador de recursos: PowerShell | Microsoft Docs"
description: "Saiba como toocreate uma conexão VPN entre clássico VNets e VNets Gerenciador de recursos usando o PowerShell e o Gateway de VPN"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="cb932-103">Conectar redes virtuais de diferentes modelos de implantação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb932-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="cb932-104">Este artigo mostra como tooconnect de clássico VNets tooResource tooallow Manager VNets Olá recursos localizados em toocommunicate de modelos de implantação separado Olá entre si.</span><span class="sxs-lookup"><span data-stu-id="cb932-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="cb932-105">etapas Olá neste artigo usam o PowerShell, mas você também pode criar essa configuração usando Olá portal do Azure, selecionando o artigo Olá desta lista.</span><span class="sxs-lookup"><span data-stu-id="cb932-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb932-106">Portal</span><span class="sxs-lookup"><span data-stu-id="cb932-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="cb932-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb932-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="cb932-108">Conectar um tooa de rede virtual clássica VNet Gerenciador de recursos é semelhante tooconnecting uma VNet tooan no site local.</span><span class="sxs-lookup"><span data-stu-id="cb932-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="cb932-109">Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="cb932-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="cb932-110">Você pode criar uma conexão entre redes virtuais em assinaturas e regiões diferentes.</span><span class="sxs-lookup"><span data-stu-id="cb932-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="cb932-111">Você também pode conectar VNets que já têm redes de tooon locais de conexões, como gateway Olá que eles foram configurados com é dinâmica ou baseadas em rota.</span><span class="sxs-lookup"><span data-stu-id="cb932-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="cb932-112">Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="cb932-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="cb932-113">Se seus VNets estão em Olá mesma região, talvez você queira tooinstead considere conectá-los usando o emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cb932-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="cb932-114">O emparelhamento Vnet não usa um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="cb932-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="cb932-115">Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cb932-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="cb932-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="cb932-116">Before beginning</span></span>

<span data-ttu-id="cb932-117">Olá etapas a seguir orientam Olá configurações necessárias tooconfigure um gateway dinâmico ou baseadas em rota para cada rede virtual e criar uma conexão VPN entre os gateways de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="cb932-118">Essa configuração não dá suporte a gateways estáticos ou baseados em política.</span><span class="sxs-lookup"><span data-stu-id="cb932-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cb932-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb932-119">Prerequisites</span></span>

* <span data-ttu-id="cb932-120">Ambas as redes virtuais já foram criadas.</span><span class="sxs-lookup"><span data-stu-id="cb932-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="cb932-121">intervalos de endereços Olá para Olá VNets não se sobrepõem uns com os outros, ou se sobrepõem com nenhum dos intervalos de saudação para outras conexões que gateways Olá podem estar conectados ao.</span><span class="sxs-lookup"><span data-stu-id="cb932-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="cb932-122">Você instalou hello mais recente cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb932-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="cb932-123">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="cb932-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="cb932-124">Certifique-se de que instalar Olá gerenciamento de serviço (SM) e Olá cmdlets do Gerenciador de recursos (RM).</span><span class="sxs-lookup"><span data-stu-id="cb932-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="cb932-125"><a name="exampleref"></a>Configurações de exemplo</span><span class="sxs-lookup"><span data-stu-id="cb932-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="cb932-126">Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="cb932-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="cb932-127">**Configurações da Rede Virtual clássica**</span><span class="sxs-lookup"><span data-stu-id="cb932-127">**Classic VNet settings**</span></span>

<span data-ttu-id="cb932-128">Nome da rede virtual = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="cb932-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="cb932-129">Local = Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="cb932-129">Location = West US</span></span> <br>
<span data-ttu-id="cb932-130">Espaços de Endereço da Rede Virtual = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cb932-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="cb932-131">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="cb932-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="cb932-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="cb932-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="cb932-133">Nome da rede local = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="cb932-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="cb932-134">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="cb932-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="cb932-135">**Configurações de Rede Virtual do Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="cb932-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="cb932-136">Nome da VNet = RMVNet </span><span class="sxs-lookup"><span data-stu-id="cb932-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="cb932-137">Grupo de recursos = RG1</span><span class="sxs-lookup"><span data-stu-id="cb932-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="cb932-138">Espaços de Endereço do IP da Rede Virtual = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="cb932-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="cb932-139">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="cb932-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="cb932-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="cb932-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="cb932-141">Local = Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="cb932-141">Location = East US</span></span> <br>
<span data-ttu-id="cb932-142">Nome do IP Público do Gateway = gwpip</span><span class="sxs-lookup"><span data-stu-id="cb932-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="cb932-143">Gateway de Rede Local = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="cb932-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="cb932-144">Nome do Gateway de Rede Virtual = RMGateway</span><span class="sxs-lookup"><span data-stu-id="cb932-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="cb932-145">Configuração de endereçamento IP do gateway = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="cb932-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="cb932-146"><a name="createsmgw"></a>Seção 1 - Configurar Olá VNet clássico</span><span class="sxs-lookup"><span data-stu-id="cb932-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="cb932-147">Parte 1 - Baixar o arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="cb932-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="cb932-148">Faça logon no tooyour conta do Azure no console do PowerShell Olá com direitos elevados.</span><span class="sxs-lookup"><span data-stu-id="cb932-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="cb932-149">Olá cmdlet a seguir solicita credenciais de logon Olá para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb932-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="cb932-150">Após o logon, ele baixa as configurações de conta para que fiquem disponível tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb932-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="cb932-151">Você usar Olá toocomplete de cmdlets do PowerShell SM essa parte da configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="cb932-152">Exporte o arquivo de configuração de rede do Azure executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="cb932-153">Você pode alterar o local de saudação do hello tooexport tooa diferentes local do arquivo se necessário.</span><span class="sxs-lookup"><span data-stu-id="cb932-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="cb932-154">Arquivo. XML de saudação abertos que você baixou tooedit-lo.</span><span class="sxs-lookup"><span data-stu-id="cb932-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="cb932-155">Para obter um exemplo de arquivo de configuração de rede hello, consulte Olá [esquema de configuração de rede](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb932-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="cb932-156">Parte 2 - Verifique a sub-rede de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="cb932-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="cb932-157">Em Olá **VirtualNetworkSites** elemento, adicionar uma sub-rede de gateway tooyour VNet se já não foi criado.</span><span class="sxs-lookup"><span data-stu-id="cb932-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="cb932-158">Ao trabalhar com o arquivo de configuração de rede hello, sub-rede de gateway Olá deve ser nomeado "GatewaySubnet" ou o Azure não pode reconhecer e usá-lo como uma sub-rede do gateway.</span><span class="sxs-lookup"><span data-stu-id="cb932-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="cb932-159">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="cb932-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="cb932-160">Parte 3 - adicionar o site de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="cb932-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="cb932-161">site de rede local Olá que adicionar representa Olá toowhich RM VNet que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cb932-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="cb932-162">Adicionar um **LocalNetworkSites** arquivo toohello de elemento se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="cb932-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="cb932-163">Nesse ponto na configuração de saudação Olá VPNGatewayAddress pode ser qualquer endereço IP público válido porque nós ainda não tiver criado o gateway Olá Olá VNet Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="cb932-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="cb932-164">Quando criamos o gateway hello, substituímos esse endereço IP de espaço reservado com hello correto endereço IP público que recebeu o gateway do RM toohello.</span><span class="sxs-lookup"><span data-stu-id="cb932-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="cb932-165">Parte 4: associar Olá VNet com o site de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="cb932-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="cb932-166">Nesta seção, podemos especificar o site de rede local Olá que você deseja tooconnect Olá VNet para.</span><span class="sxs-lookup"><span data-stu-id="cb932-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="cb932-167">Nesse caso, é Olá VNet Gerenciador de recursos que você referenciou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb932-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="cb932-168">Verifique se nomes de saudação corresponder.</span><span class="sxs-lookup"><span data-stu-id="cb932-168">Make sure hello names match.</span></span> <span data-ttu-id="cb932-169">Esta etapa não cria um gateway.</span><span class="sxs-lookup"><span data-stu-id="cb932-169">This step does not create a gateway.</span></span> <span data-ttu-id="cb932-170">Ele especifica a rede local Olá Olá gateway será conectado ao.</span><span class="sxs-lookup"><span data-stu-id="cb932-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="cb932-171">Parte 5 - salvar arquivo hello e carregar</span><span class="sxs-lookup"><span data-stu-id="cb932-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="cb932-172">Salve o arquivo hello e importá-lo tooAzure executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="cb932-173">Certifique-se de que alterar o caminho do arquivo hello conforme necessário para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="cb932-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="cb932-174">Você verá um resultado semelhante mostrando importação Olá foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="cb932-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="cb932-175">Parte 6 - criar gateway Olá</span><span class="sxs-lookup"><span data-stu-id="cb932-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="cb932-176">Antes de executar este exemplo, consulte toohello arquivo de configuração de rede que você baixou de Olá exata de nomes que o Azure espera toosee.</span><span class="sxs-lookup"><span data-stu-id="cb932-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="cb932-177">arquivo de configuração de rede Olá contém valores de saudação para suas redes virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="cb932-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="cb932-178">Às vezes, nomes de saudação para clássico em que vnets são alterados no arquivo de configuração de rede Olá ao criar configurações de rede virtual clássicas Olá portal do Azure devido a diferenças toohello nos modelos de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="cb932-179">Por exemplo, se você usou hello Azure toocreate portal uma rede virtual clássica chamada 'VNet clássico' e criou em um grupo de recursos denominado 'ClassicRG', o nome de saudação que está contida no arquivo de configuração de rede de saudação é convertido too'Group VNet clássico ClassicRG'.</span><span class="sxs-lookup"><span data-stu-id="cb932-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="cb932-180">Ao especificar o nome de saudação de uma rede virtual que contém espaços, use aspas ao redor do valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="cb932-181">Use Olá exemplo toocreate um gateway de roteamento dinâmico a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb932-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="cb932-182">Você pode verificar o status de saudação do gateway hello usando Olá **Get-AzureVNetGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb932-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="cb932-183"><a name="creatermgw"></a>Seção 2: Configurar Olá gateway de rede virtual do RM</span><span class="sxs-lookup"><span data-stu-id="cb932-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="cb932-184">toocreate um gateway VPN para Olá RM VNet, Olá siga as instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb932-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="cb932-185">Não inicie etapas Olá até depois de recuperar o endereço IP público de saudação para gateway Olá clássico da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cb932-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="cb932-186">Faça logon no tooyour conta do Azure no console do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="cb932-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="cb932-187">Olá cmdlet a seguir solicita credenciais de logon Olá para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb932-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="cb932-188">Após o logon, as configurações de conta são baixadas para que fiquem disponível tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb932-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="cb932-189">Obtenha uma lista de suas assinaturas do Azure, se você tiver mais de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="cb932-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="cb932-190">Especifique que você deseja toouse de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="cb932-191">Criar um gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="cb932-191">Create a local network gateway.</span></span> <span data-ttu-id="cb932-192">Em uma rede virtual, o gateway de rede local Olá geralmente se refere a tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="cb932-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="cb932-193">Nesse caso, o gateway de rede local Olá refere-se tooyour VNet clássico.</span><span class="sxs-lookup"><span data-stu-id="cb932-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="cb932-194">Dê um nome pelo qual Azure pode consulte tooit e também especificar o prefixo do espaço de endereço de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="cb932-195">O Azure usa o prefixo de endereço IP de saudação especificar tooidentify tooyour de toosend qual tráfego local.</span><span class="sxs-lookup"><span data-stu-id="cb932-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="cb932-196">Se você precisar tooadjust Olá aqui as informações mais tarde, antes de criar o gateway, você pode modificar os valores hello e exemplo hello execução novamente.</span><span class="sxs-lookup"><span data-stu-id="cb932-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="cb932-197">**-Nome** é Olá nome você deseja que o gateway de rede local tooassign toorefer toohello.</span><span class="sxs-lookup"><span data-stu-id="cb932-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="cb932-198">
   **-AddressPrefix** é hello espaço de endereço para sua rede virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="cb932-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="cb932-199">
**-GatewayIpAddress** é o endereço IP público de saudação do gateway Olá clássico da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cb932-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="cb932-200">Certifique-se de que a seguir Olá toochange tooreflect Olá endereço IP de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cb932-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="cb932-201">Solicite um público IP endereço toobe toohello alocado gateway de rede virtual para Olá VNet Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="cb932-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="cb932-202">Não é possível especificar o endereço IP de saudação que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="cb932-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="cb932-203">endereço IP de saudação é alocado dinamicamente toohello gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cb932-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="cb932-204">No entanto, isso não significa alterações de endereço IP hello.</span><span class="sxs-lookup"><span data-stu-id="cb932-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="cb932-205">somente tempo de saudação alterações de endereço IP do gateway de rede virtual hello quando é Olá gateway é excluído e recriado.</span><span class="sxs-lookup"><span data-stu-id="cb932-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="cb932-206">Ele não altera em redimensionamento, redefinir ou outros internas manutenção/atualizações do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="cb932-207">Nesta etapa, também definimos uma variável usada em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="cb932-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="cb932-208">Verifique se sua rede virtual tem uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="cb932-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="cb932-209">Se não houver sub-rede de gateway, adicione uma.</span><span class="sxs-lookup"><span data-stu-id="cb932-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="cb932-210">Certifique-se de sub-rede de gateway Olá é denominado *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="cb932-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="cb932-211">Recupere sub-rede Olá usada para o gateway de saudação executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="cb932-212">Nesta etapa, podemos também definir uma variável toobe usado na próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="cb932-213">**-Nome** é Olá nome de sua VNet do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="cb932-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="cb932-214">
   **-ResourceGroupName** é o grupo de recursos Olá que hello rede virtual está associado.</span><span class="sxs-lookup"><span data-stu-id="cb932-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="cb932-215">sub-rede de gateway Olá já deve existir para essa rede virtual e deve ser nomeado *GatewaySubnet* toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="cb932-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="cb932-216">Crie a configuração de endereçamento IP do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="cb932-217">configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello.</span><span class="sxs-lookup"><span data-stu-id="cb932-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="cb932-218">Use Olá de exemplo a seguir toocreate sua configuração de gateway.</span><span class="sxs-lookup"><span data-stu-id="cb932-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="cb932-219">Nesta etapa, Olá **- SubnetId** e **- PublicIpAddressId** parâmetros devem ser passados a propriedade id Olá da sub-rede hello e objetos de endereço IP, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="cb932-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="cb932-220">Você não pode usar uma cadeia de caracteres simples.</span><span class="sxs-lookup"><span data-stu-id="cb932-220">You can't use a simple string.</span></span> <span data-ttu-id="cb932-221">Essas variáveis são definidas em Olá etapa toorequest um IP público e Olá etapa tooretrieve Olá sub-rede.</span><span class="sxs-lookup"><span data-stu-id="cb932-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="cb932-222">Crie gateway de rede virtual do Gerenciador de recursos de saudação executando Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb932-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="cb932-223">Olá `-VpnType` devem ser *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="cb932-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="cb932-224">Pode levar até 45 minutos ou mais para Olá gateway toocreate.</span><span class="sxs-lookup"><span data-stu-id="cb932-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="cb932-225">Copie o endereço IP público de saudação após a criação de gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="cb932-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="cb932-226">Você usá-lo quando você configura as configurações de rede local Olá para a sua rede virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="cb932-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="cb932-227">Você pode usar o hello endereço IP público do cmdlet tooretrieve Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb932-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="cb932-228">Olá endereço IP público está listado no hello retorno como *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="cb932-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="cb932-229">Seção 3: Modificar configurações de site local de rede virtual clássicas Olá</span><span class="sxs-lookup"><span data-stu-id="cb932-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="cb932-230">Nesta seção, você trabalha com hello VNet clássico.</span><span class="sxs-lookup"><span data-stu-id="cb932-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="cb932-231">Substitua o endereço IP do espaço reservado Olá usado ao especificar as configurações de site local Olá que serão usado tooconnect toohello VNet Gerenciador de recursos de gateway.</span><span class="sxs-lookup"><span data-stu-id="cb932-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="cb932-232">Exporte arquivo de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="cb932-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="cb932-233">Usando um editor de texto, modifique o valor de saudação para VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="cb932-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="cb932-234">Substitua o endereço IP de espaço reservado de saudação com endereço IP público de saudação do gateway do Gerenciador de recursos de saudação e, em seguida, salvar as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="cb932-235">Saudação de importação modificado tooAzure de arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="cb932-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="cb932-236"><a name="connect"></a>Seção 4: Criar uma conexão entre os gateways Olá</span><span class="sxs-lookup"><span data-stu-id="cb932-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="cb932-237">Criar uma conexão entre os gateways Olá requer o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb932-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="cb932-238">Talvez você precise tooadd sua conta do Azure toouse Olá clássica versão Olá de cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb932-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="cb932-239">Assim, use toodo **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="cb932-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="cb932-240">No console do PowerShell hello, defina a chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="cb932-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="cb932-241">Antes de executar os cmdlets de hello, consulte toohello arquivo de configuração de rede que você baixou de Olá exata de nomes que o Azure espera toosee.</span><span class="sxs-lookup"><span data-stu-id="cb932-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="cb932-242">Ao especificar o nome de saudação de uma rede virtual que contém espaços, use aspas ao redor do valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="cb932-243">No exemplo a seguir, **- VNetName** é o nome de saudação do hello clássico VNet e **- LocalNetworkSiteName** é Olá nome especificado para o site de rede local hello.</span><span class="sxs-lookup"><span data-stu-id="cb932-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="cb932-244">Olá **- SharedKey** é um valor que você gera e especificar.</span><span class="sxs-lookup"><span data-stu-id="cb932-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="cb932-245">No exemplo hello, usamos 'abc123', mas você pode gerar e usar algo mais complexas.</span><span class="sxs-lookup"><span data-stu-id="cb932-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="cb932-246">Olá importante é esse valor de saudação que você especificar aqui deve ser Olá que mesmo valor que você especificar na próxima etapa do hello quando você criar sua conexão.</span><span class="sxs-lookup"><span data-stu-id="cb932-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="cb932-247">Olá retorno deve mostrar **Status: bem-sucedida**.</span><span class="sxs-lookup"><span data-stu-id="cb932-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="cb932-248">Crie conexão de VPN Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb932-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="cb932-249">Definir variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb932-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="cb932-250">Crie conexão hello.</span><span class="sxs-lookup"><span data-stu-id="cb932-250">Create hello connection.</span></span> <span data-ttu-id="cb932-251">Observe que Olá **- ConnectionType** é IPsec, não Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="cb932-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="cb932-252">Seção 5: Verificar suas conexões</span><span class="sxs-lookup"><span data-stu-id="cb932-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="cb932-253">conexão de saudação tooverify de seu tooyour de rede virtual clássica VNet Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="cb932-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="cb932-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb932-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="cb932-255">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cb932-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="cb932-256">conexão de saudação tooverify de tooyour sua VNet Gerenciador de recursos de rede virtual clássica</span><span class="sxs-lookup"><span data-stu-id="cb932-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="cb932-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb932-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="cb932-258">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cb932-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="cb932-259"><a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="cb932-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

