---
title: "Conecte-se a uma rede virtual do Azure usando o Site de ponto de tooan do computador e autenticação de certificado: PowerShell | Microsoft Docs"
description: "Conecte uma rede virtual do computador tooyour com segurança por meio da criação de uma conexão de gateway VPN ponto a Site usando a autenticação de certificado. Este artigo se aplica o modelo de implantação do Gerenciador de recursos de toohello e usa o PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="98fba-104">Configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificado: PowerShell</span><span class="sxs-lookup"><span data-stu-id="98fba-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="98fba-105">Este artigo mostra como uma rede virtual com uma conexão ponto a Site na implantação do Gerenciador de recursos de saudação do toocreate modelo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98fba-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="98fba-106">Essa configuração usa Olá tooauthenticate de certificados conexão cliente.</span><span class="sxs-lookup"><span data-stu-id="98fba-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="98fba-107">Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="98fba-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="98fba-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="98fba-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="98fba-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98fba-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="98fba-110">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="98fba-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="98fba-111">Um gateway VPN ponto a Site (P2S) permite criar uma rede virtual de tooyour de conexão segura de um computador cliente individual.</span><span class="sxs-lookup"><span data-stu-id="98fba-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="98fba-112">Conexões VPN Site a ponto são úteis quando você deseja tooconnect tooyour VNet de um local remoto, como quando você está comunicando em casa ou em uma conferência.</span><span class="sxs-lookup"><span data-stu-id="98fba-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="98fba-113">Uma VPN de P2S também é toouse uma solução útil em vez de uma VPN Site a Site quando você tiver apenas alguns clientes que precisam de tooconnect tooa VNet.</span><span class="sxs-lookup"><span data-stu-id="98fba-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="98fba-114">Usa P2S Olá SSTP Secure Socket Tunneling Protocol (), que é um protocolo VPN baseada em SSL.</span><span class="sxs-lookup"><span data-stu-id="98fba-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="98fba-115">Uma conexão VPN de P2S é estabelecido pela iniciá-lo do computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Conectar uma rede virtual do Azure - diagrama de conexão de ponto para Site de tooan do computador](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="98fba-117">Conexões de autenticação de certificado de ponto a Site requerem a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="98fba-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="98fba-118">Gateway de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="98fba-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="98fba-119">Olá chave pública (arquivo. cer) para um certificado raiz, que é carregado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="98fba-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="98fba-120">Depois que o certificado Olá é carregado, ele é considerado um certificado confiável e é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="98fba-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="98fba-121">Um certificado de cliente que é gerado a partir do certificado de raiz de saudação e instalado em cada computador cliente que se conectam toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="98fba-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="98fba-122">Esse certificado é usado para autenticação do cliente.</span><span class="sxs-lookup"><span data-stu-id="98fba-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="98fba-123">Um pacote de configuração de cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="98fba-123">A VPN client configuration package.</span></span> <span data-ttu-id="98fba-124">pacote de configuração de cliente VPN Olá contém informações necessárias Olá Olá cliente tooconnect toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="98fba-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="98fba-125">pacote de saudação configura o cliente VPN existente Olá que é nativa toohello sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="98fba-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="98fba-126">Cada cliente que se conecta deve ser configurado usando o pacote de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="98fba-127">As conexões Ponto a Site não exigem um dispositivo VPN ou um endereço IP voltado para o público local.</span><span class="sxs-lookup"><span data-stu-id="98fba-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="98fba-128">Olá conexão VPN é criado por protocolo SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="98fba-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="98fba-129">No lado do servidor de saudação, há suporte para as versões 1.0, 1.1 e 1.2 do SSTP.</span><span class="sxs-lookup"><span data-stu-id="98fba-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="98fba-130">cliente Olá decide qual toouse de versão.</span><span class="sxs-lookup"><span data-stu-id="98fba-130">hello client decides which version toouse.</span></span> <span data-ttu-id="98fba-131">Por padrão, para Windows 8.1 e posterior, o SSTP usa 1.2.</span><span class="sxs-lookup"><span data-stu-id="98fba-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="98fba-132">Para obter mais informações sobre conexões ponto a Site, consulte Olá [ponto a Site perguntas frequentes sobre](#faq) final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="98fba-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="98fba-133">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="98fba-133">Before beginning</span></span>

* <span data-ttu-id="98fba-134">Verifique se você tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="98fba-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="98fba-135">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="98fba-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="98fba-136">Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="98fba-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="98fba-137">Para obter mais informações sobre como instalar os cmdlets do PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="98fba-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="98fba-138"><a name="example"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="98fba-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="98fba-139">Você pode usar toocreate valores de exemplo hello um ambiente de teste, ou consulte valores toothese toobetter entender exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="98fba-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="98fba-140">Vamos definir variáveis de saudação na seção [1](#declare) artigo hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="98fba-141">Você pode usar etapas hello como uma passo a passo e usar valores de saudação sem alterá-los ou alterá-los tooreflect seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="98fba-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="98fba-142">**Nome: VNet1**</span><span class="sxs-lookup"><span data-stu-id="98fba-142">**Name: VNet1**</span></span>
* <span data-ttu-id="98fba-143">**Espaço de endereço: 192.168.0.0/16** e **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="98fba-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="98fba-144">Neste exemplo, podemos usar mais de um tooillustrate de espaço de endereço que essa configuração funciona com vários espaços de endereço.</span><span class="sxs-lookup"><span data-stu-id="98fba-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="98fba-145">No entanto, vários espaços de endereço não são necessários para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="98fba-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="98fba-146">**Nome da sub-rede: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="98fba-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="98fba-147">**Intervalo de endereços da sub-rede: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="98fba-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="98fba-148">**Nome da sub-rede: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="98fba-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="98fba-149">**Intervalo de endereços da sub-rede: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="98fba-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="98fba-150">**Nome da sub-rede: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="98fba-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="98fba-151">nome da sub-rede Olá *GatewaySubnet* é obrigatório para Olá toowork de gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="98fba-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="98fba-152">**Intervalo de endereços da GatewaySubnet: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="98fba-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="98fba-153">**Pool de endereços do cliente VPN: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="98fba-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="98fba-154">Clientes VPN que se conectam toohello usando esta conexão ponto a Site de rede virtual recebem um endereço IP hello pool de endereços de cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="98fba-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="98fba-155">**Assinatura:** se você tiver mais de uma assinatura, verifique se você estiver usando Olá correto.</span><span class="sxs-lookup"><span data-stu-id="98fba-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="98fba-156">**Grupo de Recursos: TestRG**</span><span class="sxs-lookup"><span data-stu-id="98fba-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="98fba-157">**Local: Leste dos EUA**</span><span class="sxs-lookup"><span data-stu-id="98fba-157">**Location: East US**</span></span>
* <span data-ttu-id="98fba-158">**Servidor DNS: Endereço IP** do servidor DNS Olá que você deseja toouse para resolução de nome.</span><span class="sxs-lookup"><span data-stu-id="98fba-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="98fba-159">**Nome de GW: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="98fba-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="98fba-160">**Nome do IP público: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="98fba-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="98fba-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="98fba-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="98fba-162"><a name="declare"></a>1. Fazer logon e definir variáveis</span><span class="sxs-lookup"><span data-stu-id="98fba-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="98fba-163">Nesta seção, faça logon e declarar Olá valores usados para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="98fba-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="98fba-164">Olá declarado valores são usados em scripts de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="98fba-165">Altere Olá valores tooreflect seu próprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="98fba-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="98fba-166">Ou, você pode usar Olá declarado valores e percorrer as etapas de saudação como um exercício.</span><span class="sxs-lookup"><span data-stu-id="98fba-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="98fba-167">Abra o console do PowerShell com privilégios elevados e faça logon no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="98fba-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="98fba-168">Esse cmdlet solicita credenciais de logon de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="98fba-169">Após o logon, ele baixa as configurações de conta para que fiquem disponível tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98fba-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="98fba-170">Obtenha uma lista das assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="98fba-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="98fba-171">Especifique que você deseja toouse de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="98fba-172">Declare variáveis Olá que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="98fba-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="98fba-173">Use Olá exemplo a seguir, substituindo valores de saudação para seu próprio quando necessário.</span><span class="sxs-lookup"><span data-stu-id="98fba-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="98fba-174"><a name="ConfigureVNet"></a>2. Configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="98fba-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="98fba-175">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="98fba-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="98fba-176">Criar configurações de sub-rede da rede virtual do hello, nomeá-los de saudação *front-end*, *back-end*, e *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="98fba-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="98fba-177">Esses prefixos devem fazer parte da saudação espaço de endereço de rede virtual que é declarada.</span><span class="sxs-lookup"><span data-stu-id="98fba-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="98fba-178">Crie rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-178">Create hello virtual network.</span></span>

  <span data-ttu-id="98fba-179">Neste exemplo, o servidor DNS de saudação é opcional.</span><span class="sxs-lookup"><span data-stu-id="98fba-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="98fba-180">A especificação de um valor não cria um novo servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="98fba-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="98fba-181">Olá endereço IP do servidor DNS que você especificar deve ser um servidor DNS que pode resolver nomes Olá para recursos de saudação que você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="98fba-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="98fba-182">Neste exemplo, usamos um endereço IP privado, mas é provável que isso não é Olá endereço IP do servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="98fba-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="98fba-183">Ser toouse-se de que seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="98fba-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="98fba-184">Especifica variáveis de saudação para rede virtual hello, que você criou.</span><span class="sxs-lookup"><span data-stu-id="98fba-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="98fba-185">Um gateway de VPN deve ter um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="98fba-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="98fba-186">Você primeiro solicitar o recurso de endereço IP hello e, em seguida, consulte tooit ao criar o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="98fba-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="98fba-187">endereço IP de saudação é atribuído dinamicamente recursos toohello ao gateway de VPN Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="98fba-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="98fba-188">O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*.</span><span class="sxs-lookup"><span data-stu-id="98fba-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="98fba-189">Você não pode solicitar uma atribuição de endereço IP Público Estático.</span><span class="sxs-lookup"><span data-stu-id="98fba-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="98fba-190">No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="98fba-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="98fba-191">somente tempo de saudação alterações de endereço IP público hello quando é Olá gateway é excluído e criado novamente.</span><span class="sxs-lookup"><span data-stu-id="98fba-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="98fba-192">Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="98fba-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="98fba-193">Solicite um endereço IP público atribuído dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="98fba-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="98fba-194"><a name="creategateway"></a>3. Criar gateway VPN Olá</span><span class="sxs-lookup"><span data-stu-id="98fba-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="98fba-195">Configurar e criar o gateway de rede virtual Olá para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="98fba-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="98fba-196">Olá *- GatewayType* devem ser **Vpn** e hello *- VpnType* devem ser **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="98fba-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="98fba-197">Um gateway de VPN pode levar até too45 toocomplete de minutos, dependendo da saudação [sku de gateway](vpn-gateway-about-vpn-gateway-settings.md) você selecionar.</span><span class="sxs-lookup"><span data-stu-id="98fba-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="98fba-198"><a name="addresspool"></a>4. Adicionar pool de endereços de cliente VPN Olá</span><span class="sxs-lookup"><span data-stu-id="98fba-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="98fba-199">Depois que o gateway de VPN Olá termina de criar, você pode adicionar pool de endereços de cliente VPN hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="98fba-200">Olá pool de endereços de cliente VPN é o intervalo de saudação do qual os clientes VPN Olá recebem um endereço IP ao se conectar.</span><span class="sxs-lookup"><span data-stu-id="98fba-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="98fba-201">Use um intervalo de endereços IP particular que não coincida com hello no local que você se conectar de, ou com hello VNet que você deseja tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="98fba-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="98fba-202">Neste exemplo, Olá pool de endereços de cliente VPN está declarado como um [variável](#declare) na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="98fba-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="98fba-203"><a name="Certificates"></a>5. Gerar certificados</span><span class="sxs-lookup"><span data-stu-id="98fba-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="98fba-204">Certificados são usados por clientes VPN do Azure tooauthenticate para VPNs ponto a Site.</span><span class="sxs-lookup"><span data-stu-id="98fba-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="98fba-205">Você carregar as informações de chave pública do hello de saudação tooAzure de certificado de raiz.</span><span class="sxs-lookup"><span data-stu-id="98fba-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="98fba-206">chave pública Olá é considerado 'confiável'.</span><span class="sxs-lookup"><span data-stu-id="98fba-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="98fba-207">Certificados de cliente devem ser gerados a partir do certificado de raiz confiável do hello e, em seguida, em cada computador cliente no repositório de certificados de usuário/pessoal de certificados atual hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="98fba-208">certificado de saudação é cliente de saudação tooauthenticate usado quando ele inicia uma conexão toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="98fba-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="98fba-209">Se você usa certificados autoassinados, eles devem ser criados usando parâmetros específicos.</span><span class="sxs-lookup"><span data-stu-id="98fba-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="98fba-210">Você pode criar um certificado autoassinado usando instruções Olá para [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md), ou, se você não tiver o Windows 10, você pode usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="98fba-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="98fba-211">É importante que você siga as etapas de saudação nas instruções de saudação ao gerar os certificados raiz autoassinados e certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="98fba-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="98fba-212">Caso contrário, certificados Olá que gerar não será compatíveis com conexões de P2S, e você receberá um erro de conexão.</span><span class="sxs-lookup"><span data-stu-id="98fba-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="98fba-213"><a name="cer"></a>1. Obter arquivo hello. cer certificado de raiz de saudação</span><span class="sxs-lookup"><span data-stu-id="98fba-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="98fba-214"><a name="generate"></a>2. Gerar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="98fba-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="98fba-215"><a name="upload"></a>6. Carregar Olá raiz certificado informações de chave pública</span><span class="sxs-lookup"><span data-stu-id="98fba-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="98fba-216">Verifique se a criação do gateway de VPN foi concluída.</span><span class="sxs-lookup"><span data-stu-id="98fba-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="98fba-217">Depois de concluído, você pode carregar o arquivo. cer de saudação (que contém as informações de chave pública Olá) para um tooAzure de certificado raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="98fba-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="98fba-218">Uma vez carregado o arquivo a.cer, Azure pode usá-lo tooauthenticate clientes que instalaram um certificado de cliente gerado a partir do certificado de raiz confiável do hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="98fba-219">Você pode carregar arquivos de certificado raiz confiável adicionais - tooa total de 20 - posteriormente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="98fba-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="98fba-220">Declare a variável de saudação para seu nome de certificado, substituindo o valor de saudação com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="98fba-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="98fba-221">Substitua o caminho do arquivo hello com seus próprios e execute Olá cmdlets.</span><span class="sxs-lookup"><span data-stu-id="98fba-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="98fba-222">Carregar Olá tooAzure de informações de chave pública.</span><span class="sxs-lookup"><span data-stu-id="98fba-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="98fba-223">Depois que as informações de certificado de saudação são carregadas, o Azure considera esse toobe um certificado raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="98fba-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="98fba-224"><a name="clientconfig"></a>7. Baixe o pacote de configuração de cliente VPN Olá</span><span class="sxs-lookup"><span data-stu-id="98fba-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="98fba-225">tooconnect tooa VNet usando uma VPN ponto a Site, cada cliente deve instalar um pacote de configuração de cliente que configura o cliente VPN nativo de saudação com configurações de saudação e arquivos de rede virtual do toohello tooconnect necessário.</span><span class="sxs-lookup"><span data-stu-id="98fba-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="98fba-226">pacote de configuração de cliente VPN Olá configura native cliente de VPN do Windows hello, não instala um cliente VPN novo ou diferente.</span><span class="sxs-lookup"><span data-stu-id="98fba-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="98fba-227">Você pode usar o hello a mesma configuração de cliente VPN do pacote em cada computador cliente, como versão Olá corresponde a arquitetura de saudação para cliente hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="98fba-228">Para lista de saudação dos sistemas operacionais cliente com suporte, consulte Olá [conexõespontoaSiteperguntas frequentes sobre](#faq) final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="98fba-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="98fba-229">Depois de saudação gateway foi criado, você pode gerar e baixar o pacote de configuração de cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="98fba-230">Este exemplo baixa o pacote de saudação para clientes de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="98fba-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="98fba-231">Se desejar que o cliente de 32 bits do toodownload hello, substitua 'Amd64' 'x86'.</span><span class="sxs-lookup"><span data-stu-id="98fba-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="98fba-232">Você também pode baixar o cliente VPN hello usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="98fba-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="98fba-233">Copie e cole o link Olá retornado pacote tooa web navegador toodownload hello, tomando cuidado aspas de saudação tooremove ao redor de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="98fba-234">Baixe e instale o pacote de saudação no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="98fba-235">Se vir um pop-up do SmartScreen, clique em **Mais informações** e em **Executar mesmo assim**.</span><span class="sxs-lookup"><span data-stu-id="98fba-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="98fba-236">Você também pode salvar Olá pacote tooinstall em outros computadores cliente.</span><span class="sxs-lookup"><span data-stu-id="98fba-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="98fba-237">No computador do cliente hello, navegue muito**as configurações de rede** e clique em **VPN**.</span><span class="sxs-lookup"><span data-stu-id="98fba-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="98fba-238">Olá conexão VPN mostra o nome de saudação da rede virtual de saudação que ele se conecta ao.</span><span class="sxs-lookup"><span data-stu-id="98fba-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="98fba-239"><a name="clientcertificate"></a>8. Instalar um certificado do cliente exportado</span><span class="sxs-lookup"><span data-stu-id="98fba-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="98fba-240">Se você quiser toocreate um P2S conexão de um computador cliente que não sejam Olá você usado certificados de cliente toogenerate Olá, é necessário tooinstall um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="98fba-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="98fba-241">Ao instalar um certificado de cliente, é necessário senha Olá que foi criada quando o certificado de cliente Olá foi exportado.</span><span class="sxs-lookup"><span data-stu-id="98fba-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="98fba-242">Normalmente, ele é apenas uma questão de duas vezes em Olá certificado e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="98fba-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="98fba-243">Verifique se o certificado de cliente hello exportado como um. pfx juntamente com a cadeia de certificado inteiro hello (que é o padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="98fba-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="98fba-244">Caso contrário, informações de certificado raiz Olá não está presentes no computador do cliente hello e cliente Olá não será capaz de tooauthenticate corretamente.</span><span class="sxs-lookup"><span data-stu-id="98fba-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="98fba-245">Para saber mais informações consulte, [Instalar um certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="98fba-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="98fba-246"><a name="connect"></a>9. Conecte-se tooAzure</span><span class="sxs-lookup"><span data-stu-id="98fba-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="98fba-247">tooconnect tooyour VNet, no computador do cliente hello, navegar tooVPN conexões e localize a conexão de VPN Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="98fba-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="98fba-248">Ele é chamado hello mesmo nome de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="98fba-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="98fba-249">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="98fba-249">Click **Connect**.</span></span> <span data-ttu-id="98fba-250">Pode aparecer uma mensagem pop-up que refere-se o certificado de saudação toousing.</span><span class="sxs-lookup"><span data-stu-id="98fba-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="98fba-251">Clique em **continuar** privilégios elevados do toouse.</span><span class="sxs-lookup"><span data-stu-id="98fba-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="98fba-252">Em Olá **Conexão** página de status, clique em **conectar** toostart conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="98fba-253">Se você vir um **Selecionar certificado** tela, verifique se mostrando de certificado de cliente Olá Olá um que você deseja toouse tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98fba-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="98fba-254">Se não for, use Olá seta suspensa tooselect Olá correto certificado e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="98fba-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![Cliente VPN conecta tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="98fba-256">A conexão é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="98fba-256">Your connection is established.</span></span>

  ![Conexão estabelecida](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="98fba-258">Solucionar problemas de conexões P2S</span><span class="sxs-lookup"><span data-stu-id="98fba-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="98fba-259"><a name="verify"></a>10. Verificar a conexão</span><span class="sxs-lookup"><span data-stu-id="98fba-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="98fba-260">tooverify que a conexão VPN estiver ativa, abra um prompt de comando com privilégios elevados e execute *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="98fba-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="98fba-261">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="98fba-261">View hello results.</span></span> <span data-ttu-id="98fba-262">Observe que o endereço IP hello recebido é um dos endereços de saudação em Olá ponto a Site VPN cliente Pool de endereços que você especificou na sua configuração.</span><span class="sxs-lookup"><span data-stu-id="98fba-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="98fba-263">resultados de saudação são exemplo toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="98fba-263">hello results are similar toothis example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="98fba-264"><a name="connectVM"></a>Conecte-se a máquina virtual de tooa</span><span class="sxs-lookup"><span data-stu-id="98fba-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="98fba-265"><a name="addremovecert"></a>Adicionar ou remover um certificado raiz</span><span class="sxs-lookup"><span data-stu-id="98fba-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="98fba-266">Você pode adicionar e remover um certificado raiz do Azure.</span><span class="sxs-lookup"><span data-stu-id="98fba-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="98fba-267">Quando você remove um certificado raiz, os clientes que têm um certificado gerado do certificado de raiz de saudação não podem autenticar e não serão capaz de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98fba-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="98fba-268">Se você quiser um tooauthenticate de cliente e se conectar, você precisa tooinstall um novo certificado de cliente gerado a partir de um certificado raiz confiável tooAzure (carregado).</span><span class="sxs-lookup"><span data-stu-id="98fba-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="98fba-269"><a name="addtrustedroot"></a>tooadd um certificado raiz confiável</span><span class="sxs-lookup"><span data-stu-id="98fba-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="98fba-270">Você pode somar too20 raiz certificado. cer arquivos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="98fba-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="98fba-271">as etapas a seguir de saudação ajuda a adicionar um certificado raiz:</span><span class="sxs-lookup"><span data-stu-id="98fba-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="98fba-272"><a name="certmethod1"></a>Método 1</span><span class="sxs-lookup"><span data-stu-id="98fba-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="98fba-273">Isso é tooupload de método mais eficiente de saudação um certificado raiz.</span><span class="sxs-lookup"><span data-stu-id="98fba-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="98fba-274">Prepare tooupload de arquivo. cer hello:</span><span class="sxs-lookup"><span data-stu-id="98fba-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="98fba-275">Carregar arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-275">Upload hello file.</span></span> <span data-ttu-id="98fba-276">Você só pode carregar um arquivo por vez.</span><span class="sxs-lookup"><span data-stu-id="98fba-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="98fba-277">tooverify que Olá carregado do arquivo de certificado:</span><span class="sxs-lookup"><span data-stu-id="98fba-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="98fba-278"><a name="certmethod2"></a>Método 2</span><span class="sxs-lookup"><span data-stu-id="98fba-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="98fba-279">Esse método é tem mais etapas que o método 1, mas tem Olá mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="98fba-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="98fba-280">Ele está incluído no caso de você precisar tooview Olá certificado dados.</span><span class="sxs-lookup"><span data-stu-id="98fba-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="98fba-281">Criar e preparar Olá nova raiz certificado tooadd tooAzure.</span><span class="sxs-lookup"><span data-stu-id="98fba-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="98fba-282">Exportar a chave pública do hello como x. 509 codificado de Base 64 (. CER) e abra-o com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="98fba-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="98fba-283">Copie os valores hello, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="98fba-283">Copy hello values, as shown in hello following example:</span></span>

  ![certificado](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="98fba-285">Ao copiar dados do certificado hello, certifique-se de que você copiar o texto de saudação como uma linha contínua sem retornos de carro ou alimentações de linha.</span><span class="sxs-lookup"><span data-stu-id="98fba-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="98fba-286">Talvez seja necessário toomodify exibição em too'Show de editor de texto de saudação símbolo/Mostrar toosee Olá de carro todos os caracteres retorna e alimentação de linha.</span><span class="sxs-lookup"><span data-stu-id="98fba-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="98fba-287">Especifique o nome do certificado hello e informações de chave como uma variável.</span><span class="sxs-lookup"><span data-stu-id="98fba-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="98fba-288">Substitua as informações de saudação com seu próprio, conforme mostrado no hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="98fba-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="98fba-289">Adicione novo certificado raiz do hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-289">Add hello new root certificate.</span></span> <span data-ttu-id="98fba-290">Você pode adicionar apenas um certificado por vez.</span><span class="sxs-lookup"><span data-stu-id="98fba-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="98fba-291">Você pode verificar o que novo certificado Olá foi adicionado corretamente usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="98fba-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="98fba-292"><a name="removerootcert"></a>tooremove um certificado raiz</span><span class="sxs-lookup"><span data-stu-id="98fba-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="98fba-293">Declare variáveis hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="98fba-294">Remova certificado hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="98fba-295">Saudação de uso tooverify de exemplo que Olá certificado a seguir foi removida com êxito.</span><span class="sxs-lookup"><span data-stu-id="98fba-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="98fba-296"><a name="revoke"></a>Revogar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="98fba-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="98fba-297">É possível revogar certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="98fba-297">You can revoke client certificates.</span></span> <span data-ttu-id="98fba-298">certificado Olá lista de revogação permite que você tooselectively negar conectividade ponto a Site com base em certificados de cliente individuais.</span><span class="sxs-lookup"><span data-stu-id="98fba-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="98fba-299">Isso é diferente da remoção de um certificado raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="98fba-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="98fba-300">Se você remover um certificado de raiz confiável. cer do Azure, ela revoga o acesso de Olá para todos os certificados de cliente gerado/assinado pelo certificado de raiz revogado hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="98fba-301">Revogar um certificado de cliente, em vez de certificado de raiz hello, permite Olá outros certificados que foram gerados a partir do certificado de raiz de saudação toocontinue toobe usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="98fba-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="98fba-302">uma prática comum Olá é o acesso de toomanage de certificado toouse Olá raiz nos níveis de equipe ou organização, durante o uso de certificados do cliente revogados para controle de acesso refinado sobre usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="98fba-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="98fba-303"><a name="revokeclientcert"></a>toorevoke um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="98fba-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="98fba-304">Recupere a impressão digital do certificado de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="98fba-305">Para obter mais informações, consulte [como tooretrieve Olá impressão digital de um certificado](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="98fba-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="98fba-306">Copie o editor de texto Olá informações tooa e remover todos os espaços para que seja uma cadeia de caracteres contínua.</span><span class="sxs-lookup"><span data-stu-id="98fba-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="98fba-307">Essa cadeia de caracteres é declarada como uma variável na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="98fba-308">Declare variáveis hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-308">Declare hello variables.</span></span> <span data-ttu-id="98fba-309">Verifique se toodeclare Olá impressão digital recuperado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="98fba-310">Adicione Olá impressão digital toohello lista de certificados revogados.</span><span class="sxs-lookup"><span data-stu-id="98fba-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="98fba-311">Consulte o "Êxito" quando a impressão digital de saudação foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="98fba-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="98fba-312">Verifique se que essa impressão digital de saudação foi adicionado toohello lista de revogação de certificado.</span><span class="sxs-lookup"><span data-stu-id="98fba-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="98fba-313">Depois que tiver sido adicionado a impressão digital do hello, certificado Olá não pode mais ser usado tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98fba-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="98fba-314">Os clientes que tentam tooconnect usando este certificado recebem uma mensagem dizendo que Olá certificado não é mais válido.</span><span class="sxs-lookup"><span data-stu-id="98fba-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="98fba-315"><a name="reinstateclientcert"></a>tooreinstate um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="98fba-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="98fba-316">Você pode restabelecer um certificado de cliente, removendo a impressão digital de saudação da lista de saudação de certificados de cliente revogados.</span><span class="sxs-lookup"><span data-stu-id="98fba-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="98fba-317">Declare variáveis hello.</span><span class="sxs-lookup"><span data-stu-id="98fba-317">Declare hello variables.</span></span> <span data-ttu-id="98fba-318">Verifique se que você declarar Olá correto impressão digital Olá certificado que você deseja tooreinstate.</span><span class="sxs-lookup"><span data-stu-id="98fba-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="98fba-319">Remova a impressão digital do certificado Olá da lista de revogação de certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="98fba-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="98fba-320">Verifique se a impressão digital de saudação é removido da saudação revogado lista.</span><span class="sxs-lookup"><span data-stu-id="98fba-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="98fba-321"><a name="faq"></a>Perguntas frequentes sobre Ponto a site</span><span class="sxs-lookup"><span data-stu-id="98fba-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="98fba-322">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98fba-322">Next steps</span></span>
<span data-ttu-id="98fba-323">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="98fba-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="98fba-324">Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="98fba-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="98fba-325">toounderstand mais sobre redes e máquinas virtuais, consulte [visão geral de rede do Azure e a VM do Linux](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98fba-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
