---
title: "Conectar um computador a uma rede virtual do Azure usando autenticação Ponto a site e de certificado: PowerShell | Microsoft Docs"
description: "Conectar com segurança um computador à rede virtual criando uma conexão de gateway de VPN Ponto a Site usando autenticação de certificado. Este artigo se aplica ao modelo de implantação do Gerenciador de Recursos e usa o PowerShell."
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
ms.openlocfilehash: 2e072ada13b8c742fe7f2e14737c9376f7677906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="b12f2-104">Configurar uma conexão Ponto a Site com uma autenticação de certificado usando VNet: PowerShell</span><span class="sxs-lookup"><span data-stu-id="b12f2-104">Configure a Point-to-Site connection to a VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="b12f2-105">Este artigo mostra como criar uma rede virtual com uma conexão Ponto a Site no modelo de implantação do Resource Manager usando o portal o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b12f2-105">This article shows you how to create a VNet with a Point-to-Site connection in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="b12f2-106">Essa configuração usa certificados para autenticar o cliente de conexão.</span><span class="sxs-lookup"><span data-stu-id="b12f2-106">This configuration uses certificates to authenticate the connecting client.</span></span> <span data-ttu-id="b12f2-107">Você também pode criar essa configuração usando uma ferramenta de implantação ou um modelo de implantação diferente, selecionando uma opção diferente na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12f2-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b12f2-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b12f2-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="b12f2-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b12f2-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="b12f2-110">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="b12f2-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="b12f2-111">Um gateway VPN Ponto a Site (P2S) permite que você crie uma conexão segura para sua rede virtual a partir de um computador cliente individual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection to your virtual network from an individual client computer.</span></span> <span data-ttu-id="b12f2-112">As conexões VPN Ponto a Site são úteis quando você deseja se conectar à rede virtual de um local remoto, como ao trabalhar de casa ou em uma conferência.</span><span class="sxs-lookup"><span data-stu-id="b12f2-112">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="b12f2-113">Uma VPN P2S também é uma solução útil para usar em vez de uma VPN Site a Site, quando você tiver apenas alguns clientes que precisam se conectar a uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-113">A P2S VPN is also a useful solution to use instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span>

<span data-ttu-id="b12f2-114">P2S usa o SSTP (Secure Socket Tunneling Protocol), que é um protocolo VPN baseado em SSL.</span><span class="sxs-lookup"><span data-stu-id="b12f2-114">P2S uses the Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="b12f2-115">Uma conexão VPN P2S é estabelecida iniciando-a do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-115">A P2S VPN connection is established by starting it from the client computer.</span></span>

![Conectar um computador a um diagrama de conexão de ponto para Site da rede virtual do Azure](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="b12f2-117">Conexões de autenticação de certificado de Ponto a Site exigem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b12f2-117">Point-to-Site certificate authentication connections require the following:</span></span>

* <span data-ttu-id="b12f2-118">Gateway de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="b12f2-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="b12f2-119">A chave pública (arquivo .cer) para um certificado raiz, que é carregado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-119">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span></span> <span data-ttu-id="b12f2-120">Depois que o certificado é carregado, ele é considerado um certificado confiável e é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="b12f2-120">Once the certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="b12f2-121">O certificado do cliente gerado do certificado raiz e instalado em cada computador cliente que irá se conectar à VNet.</span><span class="sxs-lookup"><span data-stu-id="b12f2-121">A client certificate that is generated from the root certificate and installed on each client computer that will connect to the VNet.</span></span> <span data-ttu-id="b12f2-122">Esse certificado é usado para autenticação do cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="b12f2-123">Um pacote de configuração de cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="b12f2-123">A VPN client configuration package.</span></span> <span data-ttu-id="b12f2-124">O pacote de configuração de cliente VPN contém as informações necessárias para o cliente se conectar à VNet.</span><span class="sxs-lookup"><span data-stu-id="b12f2-124">The VPN client configuration package contains the necessary information for the client to connect to the VNet.</span></span> <span data-ttu-id="b12f2-125">O pacote configura o cliente VPN existente que é nativo do sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="b12f2-125">The package configures the existing VPN client that is native to the Windows operating system.</span></span> <span data-ttu-id="b12f2-126">Cada cliente que se conecta deve ser configurado usando o pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="b12f2-126">Each client that connects must be configured using the configuration package.</span></span>

<span data-ttu-id="b12f2-127">As conexões Ponto a Site não exigem um dispositivo VPN ou um endereço IP voltado para o público local.</span><span class="sxs-lookup"><span data-stu-id="b12f2-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="b12f2-128">A conexão VPN é criada no SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="b12f2-128">The VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="b12f2-129">No lado do servidor, há suporte para as versões 1.0, 1.1 e 1.2 do SSTP.</span><span class="sxs-lookup"><span data-stu-id="b12f2-129">On the server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="b12f2-130">O cliente decide qual versão usar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-130">The client decides which version to use.</span></span> <span data-ttu-id="b12f2-131">Por padrão, para Windows 8.1 e posterior, o SSTP usa 1.2.</span><span class="sxs-lookup"><span data-stu-id="b12f2-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="b12f2-132">Para saber mais sobre conexões Ponto a site, consulte as [Perguntas frequentes sobre Ponto a site](#faq) no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="b12f2-132">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="b12f2-133">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b12f2-133">Before beginning</span></span>

* <span data-ttu-id="b12f2-134">Verifique se você tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="b12f2-135">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="b12f2-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="b12f2-136">Instale a versão mais recente dos cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b12f2-136">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b12f2-137">Para saber mais sobre como instalar cmdlets do PowerShell, confira [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b12f2-137">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="b12f2-138"><a name="example"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="b12f2-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="b12f2-139">Você pode usar os valores do exemplo para criar um ambiente de teste ou fazer referência a esses valores para entender melhor os exemplos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b12f2-139">You can use the example values to create a test environment, or refer to these values to better understand the examples in this article.</span></span> <span data-ttu-id="b12f2-140">Definimos as variáveis na seção [1](#declare) do artigo.</span><span class="sxs-lookup"><span data-stu-id="b12f2-140">We set the variables in section [1](#declare) of the article.</span></span> <span data-ttu-id="b12f2-141">Você pode usar as etapas como um passo a passo e usar os valores sem alterá-los, ou alterá-los para refletir seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-141">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span></span> 

* <span data-ttu-id="b12f2-142">**Nome: VNet1**</span><span class="sxs-lookup"><span data-stu-id="b12f2-142">**Name: VNet1**</span></span>
* <span data-ttu-id="b12f2-143">**Espaço de endereço: 192.168.0.0/16** e **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="b12f2-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="b12f2-144">Neste exemplo, usamos mais de um espaço de endereço para ilustrar que esta configuração funciona com vários espaços de endereço.</span><span class="sxs-lookup"><span data-stu-id="b12f2-144">For this example, we use more than one address space to illustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="b12f2-145">No entanto, vários espaços de endereço não são necessários para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="b12f2-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="b12f2-146">**Nome da sub-rede: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="b12f2-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="b12f2-147">**Intervalo de endereços da sub-rede: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="b12f2-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="b12f2-148">**Nome da sub-rede: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="b12f2-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="b12f2-149">**Intervalo de endereços da sub-rede: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="b12f2-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="b12f2-150">**Nome da sub-rede: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="b12f2-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="b12f2-151">O nome da Sub-rede *GatewaySubnet* é obrigatório para que o gateway de VPN funcione.</span><span class="sxs-lookup"><span data-stu-id="b12f2-151">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span></span>
  * <span data-ttu-id="b12f2-152">**Intervalo de endereços da GatewaySubnet: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="b12f2-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="b12f2-153">**Pool de endereços do cliente VPN: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="b12f2-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="b12f2-154">Os clientes VPN que se conectarem à rede virtual usando esta conexão Ponto a Site receberão um endereço IP do pool de endereços do cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="b12f2-154">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span></span>
* <span data-ttu-id="b12f2-155">**Assinatura:** verifique se você tem mais de uma assinatura, verifique se está usando a correta.</span><span class="sxs-lookup"><span data-stu-id="b12f2-155">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="b12f2-156">**Grupo de Recursos: TestRG**</span><span class="sxs-lookup"><span data-stu-id="b12f2-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="b12f2-157">**Local: Leste dos EUA**</span><span class="sxs-lookup"><span data-stu-id="b12f2-157">**Location: East US**</span></span>
* <span data-ttu-id="b12f2-158">**Servidor DNS: Endereço IP** do servidor DNS que você deseja usar para a resolução de nome.</span><span class="sxs-lookup"><span data-stu-id="b12f2-158">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span></span>
* <span data-ttu-id="b12f2-159">**Nome de GW: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="b12f2-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="b12f2-160">**Nome do IP público: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="b12f2-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="b12f2-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="b12f2-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="b12f2-162"><a name="declare"></a>1. Fazer logon e definir variáveis</span><span class="sxs-lookup"><span data-stu-id="b12f2-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="b12f2-163">Nesta seção, faça logon e declare os valores usados para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="b12f2-163">In this section, you log in and declare the values used for this configuration.</span></span> <span data-ttu-id="b12f2-164">Os valores declarados são usados nos scripts de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b12f2-164">The declared values are used in the sample scripts.</span></span> <span data-ttu-id="b12f2-165">Altere os valores para refletir seu próprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-165">Change the values to reflect your own environment.</span></span> <span data-ttu-id="b12f2-166">Ou, você pode usar os valores declarados e percorrer as etapas como um exercício.</span><span class="sxs-lookup"><span data-stu-id="b12f2-166">Or, you can use the declared values and go through the steps as an exercise.</span></span>

1. <span data-ttu-id="b12f2-167">Abra o console do PowerShell com privilégios elevados e entre na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-167">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span></span> <span data-ttu-id="b12f2-168">Esse cmdlet solicita as credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="b12f2-168">This cmdlet prompts you for the login credentials.</span></span> <span data-ttu-id="b12f2-169">Depois de entrar, ele baixa as configurações da conta para que elas estejam disponíveis para o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b12f2-169">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="b12f2-170">Obtenha uma lista das assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="b12f2-171">Especifique a assinatura que você quer usar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-171">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="b12f2-172">Declare as variáveis que você quer usar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-172">Declare the variables that you want to use.</span></span> <span data-ttu-id="b12f2-173">Use o exemplo a seguir, substituindo os valores existentes pelos seus quando necessário.</span><span class="sxs-lookup"><span data-stu-id="b12f2-173">Use the following sample, substituting the values for your own when necessary.</span></span>

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

## <span data-ttu-id="b12f2-174"><a name="ConfigureVNet"></a>2. Configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="b12f2-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="b12f2-175">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="b12f2-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="b12f2-176">Crie as configurações de sub-rede para a rede virtual e dê a elas os nomes *FrontEnd*, *BackEnd* e *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="b12f2-176">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="b12f2-177">Esses prefixos devem fazer parte do espaço de endereço da rede virtual declarada por você.</span><span class="sxs-lookup"><span data-stu-id="b12f2-177">These prefixes must be part of the VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="b12f2-178">Crie a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-178">Create the virtual network.</span></span>

  <span data-ttu-id="b12f2-179">Neste exemplo, o servidor DNS é opcional.</span><span class="sxs-lookup"><span data-stu-id="b12f2-179">In this example, the DNS server is optional.</span></span> <span data-ttu-id="b12f2-180">A especificação de um valor não cria um novo servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="b12f2-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="b12f2-181">O endereço IP do servidor DNS especificado deve ser um servidor DNS que pode resolver os nomes dos recursos aos quais você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="b12f2-181">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to.</span></span> <span data-ttu-id="b12f2-182">Neste exemplo, usamos um endereço IP privado, mas é provável que ele não seja o endereço IP do seu servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="b12f2-182">For this example, we used a private IP address, but it is likely that this is not the IP address of your DNS server.</span></span> <span data-ttu-id="b12f2-183">Use seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="b12f2-183">Be sure to use your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="b12f2-184">Especifique as variáveis da rede virtual que você criou.</span><span class="sxs-lookup"><span data-stu-id="b12f2-184">Specify the variables for the virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="b12f2-185">Um gateway de VPN deve ter um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="b12f2-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="b12f2-186">Você primeiro solicita o recurso de endereço IP e, em seguida, faz referência a ele ao criar seu gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-186">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="b12f2-187">O endereço IP é atribuído dinamicamente ao recurso quando o gateway de VPN é criado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-187">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="b12f2-188">O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*.</span><span class="sxs-lookup"><span data-stu-id="b12f2-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="b12f2-189">Você não pode solicitar uma atribuição de endereço IP Público Estático.</span><span class="sxs-lookup"><span data-stu-id="b12f2-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="b12f2-190">No entanto, isso não significa que o endereço IP mudará depois de ter sido atribuído ao seu gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="b12f2-190">However, it doesn't mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="b12f2-191">A única vez em que o endereço IP Público é alterado é quando o gateway é excluído e recriado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-191">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="b12f2-192">Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="b12f2-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="b12f2-193">Solicite um endereço IP público atribuído dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="b12f2-194"><a name="creategateway"></a>3. Criar o gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="b12f2-194"><a name="creategateway"></a>3. Create the VPN gateway</span></span>

<span data-ttu-id="b12f2-195">Configurar e criar o gateway de rede virtual para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-195">Configure and create the virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="b12f2-196">O *-GatewayType* deve ser **Vpn** e o *-VpnType* deve ser **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="b12f2-196">The *-GatewayType* must be **Vpn** and the *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="b12f2-197">Um gateway de VPN pode levar até 45 minutos para ser concluído, dependendo do [SKU de gateway](vpn-gateway-about-vpn-gateway-settings.md) selecionado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-197">A VPN gateway can take up to 45 minutes to complete, depending on the [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="b12f2-198"><a name="addresspool"></a>4. Adicionar o pool de endereços do cliente VPN</span><span class="sxs-lookup"><span data-stu-id="b12f2-198"><a name="addresspool"></a>4. Add the VPN client address pool</span></span>

<span data-ttu-id="b12f2-199">Depois que o gateway de VPN é criado, você pode adicionar o pool de endereços do cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="b12f2-199">After the VPN gateway finishes creating, you can add the VPN client address pool.</span></span> <span data-ttu-id="b12f2-200">O pool de endereços de cliente VPN é o intervalo do qual os clientes VPN recebem um endereço IP ao se conectar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-200">The VPN client address pool is the range from which the VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="b12f2-201">Use um intervalo de endereço IP privado que não coincida com o local de onde você se conecta ou com a rede virtual à qual você deseja se conectar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-201">Use a private IP address range that does not overlap with the on-premises location that you connect from, or with the VNet that you want to connect to.</span></span> <span data-ttu-id="b12f2-202">Neste exemplo, o pool de endereços de cliente VPN é declarado como uma [variável](#declare) na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="b12f2-202">In this example, the VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="b12f2-203"><a name="Certificates"></a>5. Gerar certificados</span><span class="sxs-lookup"><span data-stu-id="b12f2-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="b12f2-204">Os certificados são usados pelo Azure para autenticar clientes de VPN para as VPNs Ponto a Site.</span><span class="sxs-lookup"><span data-stu-id="b12f2-204">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="b12f2-205">Você pode carregar as informações da chave públicas do certificado raiz no Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-205">You upload the public key information of the root certificate to Azure.</span></span> <span data-ttu-id="b12f2-206">A chave pública é considerada “trusted” (confiável).</span><span class="sxs-lookup"><span data-stu-id="b12f2-206">The public key is then considered 'trusted'.</span></span> <span data-ttu-id="b12f2-207">Os certificados de cliente devem ser gerados a partir do certificado raiz confiável e, em seguida, em cada computador cliente no repositório de certificados de usuário/pessoal de certificados atual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-207">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="b12f2-208">O certificado é usado para autenticar o cliente quando ele inicia uma conexão de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-208">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span></span> 

<span data-ttu-id="b12f2-209">Se você usa certificados autoassinados, eles devem ser criados usando parâmetros específicos.</span><span class="sxs-lookup"><span data-stu-id="b12f2-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="b12f2-210">Você pode criar um certificado autoassinado usando as instruções para [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md) ou, se não tiver o Windows 10, com o [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="b12f2-210">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="b12f2-211">É importante que você siga as etapas nas instruções ao gerar os certificados raiz autoassinados e os certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-211">It's important that you follow the steps in the instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="b12f2-212">Caso contrário, os certificados gerados não serão compatíveis com conexões P2S e você receberá um erro de conexão.</span><span class="sxs-lookup"><span data-stu-id="b12f2-212">Otherwise, the certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="b12f2-213"><a name="cer"></a>1. Obter o arquivo .cer do certificado raiz</span><span class="sxs-lookup"><span data-stu-id="b12f2-213"><a name="cer"></a>1. Obtain the .cer file for the root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="b12f2-214"><a name="generate"></a>2. Gerar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b12f2-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="b12f2-215"><a name="upload"></a>6. Carregar informações de chave pública do certificado raiz</span><span class="sxs-lookup"><span data-stu-id="b12f2-215"><a name="upload"></a>6. Upload the root certificate public key information</span></span>

<span data-ttu-id="b12f2-216">Verifique se a criação do gateway de VPN foi concluída.</span><span class="sxs-lookup"><span data-stu-id="b12f2-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="b12f2-217">Depois de concluído, você pode carregar o arquivo. cer (que contém as informações de chave pública) para um certificado raiz confiável do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-217">Once it has completed, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span></span> <span data-ttu-id="b12f2-218">Uma vez carregado o arquivo .cer, o Azure pode usá-lo para autenticar clientes com um certificado de cliente instalado gerado a partir de um certificado raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="b12f2-218">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span></span> <span data-ttu-id="b12f2-219">Você pode carregar arquivos de certificado raiz confiável adicionais - até um total de 20 - posteriormente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="b12f2-219">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="b12f2-220">Declare a variável para o nome do certificado, substituindo o valor pelo seu.</span><span class="sxs-lookup"><span data-stu-id="b12f2-220">Declare the variable for your certificate name, replacing the value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="b12f2-221">Substitua o caminho do arquivo pelo seu e execute os cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b12f2-221">Replace the file path with your own, and then run the cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="b12f2-222">Carregue as informações de chave pública para o Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-222">Upload the public key information to Azure.</span></span> <span data-ttu-id="b12f2-223">Depois que as informações do certificado são carregadas, o Azure as considera como um certificado raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="b12f2-223">Once the certificate information is uploaded, Azure considers this to be a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="b12f2-224"><a name="clientconfig"></a>7. Baixar o pacote de configuração do cliente VPN</span><span class="sxs-lookup"><span data-stu-id="b12f2-224"><a name="clientconfig"></a>7. Download the VPN client configuration package</span></span>

<span data-ttu-id="b12f2-225">Para se conectar a uma rede virtual usando uma VPN Ponto a Site, cada cliente deve instalar um pacote de configuração de cliente que configura o cliente VPN nativo com as configurações e os arquivos necessários para a conexão com a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-225">To connect to a VNet using a Point-to-Site VPN, each client must install a client configuration package that configures the native VPN client with the settings and files that are necessary to connect to the virtual network.</span></span> <span data-ttu-id="b12f2-226">O pacote de configuração de cliente VPN configura o cliente VPN do Windows nativo, ele não instala um cliente VPN novo ou diferente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-226">The VPN client configuration package configures the native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="b12f2-227">Você pode usar o mesmo pacote de configuração de cliente VPN em cada computador cliente, desde que a versão corresponda à arquitetura do cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-227">You can use the same VPN client configuration package on each client computer, as long as the version matches the architecture for the client.</span></span> <span data-ttu-id="b12f2-228">Para obter a lista de sistemas operacionais clientes com suporte, consulte as [Perguntas frequentes sobre conexões Ponto a site](#faq) ao final desse artigo.</span><span class="sxs-lookup"><span data-stu-id="b12f2-228">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span></span>

1. <span data-ttu-id="b12f2-229">Depois que o gateway tiver sido criado, você poderá gerar e baixar o pacote de configuração do cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-229">After the gateway has been created, you can generate and download the client configuration package.</span></span> <span data-ttu-id="b12f2-230">Este exemplo baixa o pacote para clientes de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="b12f2-230">This example downloads the package for 64-bit clients.</span></span> <span data-ttu-id="b12f2-231">Se você quiser baixar o cliente de 32 bits, substitua 'Amd64' por 'x86'.</span><span class="sxs-lookup"><span data-stu-id="b12f2-231">If you want to download the 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="b12f2-232">Você também pode baixar o cliente VPN usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-232">You can also download the VPN client by using the Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="b12f2-233">Copie e cole o link que é retornado em um navegador da Web para baixar o pacote, tomando cuidado para remover as aspas ao redor do link.</span><span class="sxs-lookup"><span data-stu-id="b12f2-233">Copy and paste the link that is returned to a web browser to download the package, taking care to remove the quotes surrounding the link.</span></span> 
3. <span data-ttu-id="b12f2-234">Baixe e instale o pacote no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-234">Download and install the package on the client computer.</span></span> <span data-ttu-id="b12f2-235">Se vir um pop-up do SmartScreen, clique em **Mais informações** e em **Executar mesmo assim**.</span><span class="sxs-lookup"><span data-stu-id="b12f2-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="b12f2-236">Você também pode salvar o pacote de instalação em outros computadores clientes.</span><span class="sxs-lookup"><span data-stu-id="b12f2-236">You can also save the package to install on other client computers.</span></span>
4. <span data-ttu-id="b12f2-237">No computador cliente, navegue até **Configurações de Rede** e clique em **VPN**.</span><span class="sxs-lookup"><span data-stu-id="b12f2-237">On the client computer, navigate to **Network Settings** and click **VPN**.</span></span> <span data-ttu-id="b12f2-238">A conexão VPN mostra o nome da rede virtual a que ele se conecta.</span><span class="sxs-lookup"><span data-stu-id="b12f2-238">The VPN connection shows the name of the virtual network that it connects to.</span></span>

## <span data-ttu-id="b12f2-239"><a name="clientcertificate"></a>8. Instalar um certificado do cliente exportado</span><span class="sxs-lookup"><span data-stu-id="b12f2-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="b12f2-240">Se você quiser criar uma conexão P2S de um computador cliente diferente daquele usada para gerar os certificados cliente, instale um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-240">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="b12f2-241">Ao instalar um certificado do cliente, você precisará da senha criada durante a exportação do certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-241">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span> <span data-ttu-id="b12f2-242">Normalmente, é apenas uma questão de clicar duas vezes no certificado e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="b12f2-242">Typically, it is just a matter of double-clicking the certificate and installing it.</span></span>

<span data-ttu-id="b12f2-243">Verifique se o certificado do cliente foi exportado como um .pfx juntamente com a cadeia de certificado inteira (que é o padrão).</span><span class="sxs-lookup"><span data-stu-id="b12f2-243">Make sure the client certificate was exported as a .pfx along with the entire certificate chain (which is the default).</span></span> <span data-ttu-id="b12f2-244">Caso contrário, as informações do certificado raiz não estão presentes no computador cliente e este não será capaz de fazer a autenticação corretamente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-244">Otherwise, the root certificate information isn't present on the client computer and the client won't be able to authenticate properly.</span></span> <span data-ttu-id="b12f2-245">Para saber mais informações consulte, [Instalar um certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="b12f2-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="b12f2-246"><a name="connect"></a>9. Conecte-se ao Azure</span><span class="sxs-lookup"><span data-stu-id="b12f2-246"><a name="connect"></a>9. Connect to Azure</span></span>

1. <span data-ttu-id="b12f2-247">Para se conectar à sua rede virtual, no computador cliente, navegue até conexões VPN e localize a conexão VPN que você criou.</span><span class="sxs-lookup"><span data-stu-id="b12f2-247">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="b12f2-248">Ele terá o mesmo nome da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b12f2-248">It is named the same name as your virtual network.</span></span> <span data-ttu-id="b12f2-249">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="b12f2-249">Click **Connect**.</span></span> <span data-ttu-id="b12f2-250">Uma mensagem pop-up pode ser exibida sobre o uso do certificado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-250">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="b12f2-251">Clique em **Continuar** para usar os privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="b12f2-251">Click **Continue** to use elevated privileges.</span></span> 
2. <span data-ttu-id="b12f2-252">Na página de status **Conexão**, clique em **Conectar** para iniciar a conexão.</span><span class="sxs-lookup"><span data-stu-id="b12f2-252">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="b12f2-253">Se for exibida uma tela de **Selecionar certificado** , verifique se o certificado de cliente mostrado é o que você deseja usar para se conectar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-253">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="b12f2-254">Se não for, use a seta suspensa para selecionar o certificado correto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b12f2-254">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>

  ![Cliente VPN se conecta ao Azure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="b12f2-256">A conexão é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b12f2-256">Your connection is established.</span></span>

  ![Conexão estabelecida](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="b12f2-258">Solucionar problemas de conexões P2S</span><span class="sxs-lookup"><span data-stu-id="b12f2-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="b12f2-259"><a name="verify"></a>10. Verificar a conexão</span><span class="sxs-lookup"><span data-stu-id="b12f2-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="b12f2-260">Para verificar se a conexão VPN está ativa, abra um prompt de comandos com privilégios elevados e execute *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="b12f2-260">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="b12f2-261">Exiba os resultados.</span><span class="sxs-lookup"><span data-stu-id="b12f2-261">View the results.</span></span> <span data-ttu-id="b12f2-262">Observe que o endereço IP que você recebeu está dentro do pool de endereços de cliente VPN Ponto a Site especificado em sua configuração.</span><span class="sxs-lookup"><span data-stu-id="b12f2-262">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="b12f2-263">Os resultados são semelhantes a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="b12f2-263">The results are similar to this example:</span></span>

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

## <span data-ttu-id="b12f2-264"><a name="connectVM"></a>Conectar-se a uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b12f2-264"><a name="connectVM"></a>Connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="b12f2-265"><a name="addremovecert"></a>Adicionar ou remover um certificado raiz</span><span class="sxs-lookup"><span data-stu-id="b12f2-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="b12f2-266">Você pode adicionar e remover um certificado raiz do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="b12f2-267">Quando você remove um certificado raiz, os clientes que possuem um certificado gerado pelo certificado raiz não podem fazer a autenticação e, portanto, não conseguem se conectar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-267">When you remove a root certificate, clients that have a certificate generated from the root certificate can't authenticate and won't be able to connect.</span></span> <span data-ttu-id="b12f2-268">Se você deseja que um clientes faça autenticação e se conecte, você precisa instalar um novo certificado de cliente gerado a partir de um certificado confiável (carregado) no Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-268">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span></span>

### <span data-ttu-id="b12f2-269"><a name="addtrustedroot"></a>Para adicionar um certificado raiz confiável</span><span class="sxs-lookup"><span data-stu-id="b12f2-269"><a name="addtrustedroot"></a>To add a trusted root certificate</span></span>

<span data-ttu-id="b12f2-270">Você pode adicionar até 20 arquivos .cer de certificado raiz ao Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-270">You can add up to 20 root certificate .cer files to Azure.</span></span> <span data-ttu-id="b12f2-271">As seguintes etapas o ajudarão a adicionar um certificado raiz:</span><span class="sxs-lookup"><span data-stu-id="b12f2-271">The following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="b12f2-272"><a name="certmethod1"></a>Método 1</span><span class="sxs-lookup"><span data-stu-id="b12f2-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="b12f2-273">Esse é o método mais eficiente para carregar um certificado raiz.</span><span class="sxs-lookup"><span data-stu-id="b12f2-273">This is the most efficient method to upload a root certificate.</span></span>

1. <span data-ttu-id="b12f2-274">Prepare o arquivo .cer para upload:</span><span class="sxs-lookup"><span data-stu-id="b12f2-274">Prepare the .cer file to upload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="b12f2-275">Carregue o arquivo.</span><span class="sxs-lookup"><span data-stu-id="b12f2-275">Upload the file.</span></span> <span data-ttu-id="b12f2-276">Você só pode carregar um arquivo por vez.</span><span class="sxs-lookup"><span data-stu-id="b12f2-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="b12f2-277">Para verificar se o arquivo de certificado foi carregado:</span><span class="sxs-lookup"><span data-stu-id="b12f2-277">To verify that the certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="b12f2-278"><a name="certmethod2"></a>Método 2</span><span class="sxs-lookup"><span data-stu-id="b12f2-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="b12f2-279">Esse método tem mais etapas que o Método 1, mas com o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-279">This method is has more steps than Method 1, but has the same result.</span></span> <span data-ttu-id="b12f2-280">Ele foi incluído caso você precise exibir os dados do certificado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-280">It is included in case you need to view the certificate data.</span></span>

1. <span data-ttu-id="b12f2-281">Crie e prepare o novo certificado raiz para adicionar ao Azure.</span><span class="sxs-lookup"><span data-stu-id="b12f2-281">Create and prepare the new root certificate to add to Azure.</span></span> <span data-ttu-id="b12f2-282">Exporte a chave pública como X.509 codificado em Base 64 (.CER) e abra-a com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b12f2-282">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="b12f2-283">Copie os valores, conforme mostra o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12f2-283">Copy the values, as shown in the following example:</span></span>

  ![certificado](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="b12f2-285">Ao copiar os dados do certificado, certifique-se de copiar o texto como uma linha contínua sem retornos de carro ou alimentações de linha.</span><span class="sxs-lookup"><span data-stu-id="b12f2-285">When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="b12f2-286">Talvez seja necessário modificar a exibição no editor de texto para 'Mostrar símbolo/Mostrar todos os caracteres' para ver os retornos de carro e alimentações de linha.</span><span class="sxs-lookup"><span data-stu-id="b12f2-286">You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="b12f2-287">Especifique o nome do certificado e as informações de chave como uma variável.</span><span class="sxs-lookup"><span data-stu-id="b12f2-287">Specify the certificate name and key information as a variable.</span></span> <span data-ttu-id="b12f2-288">Substitua as informações por suas próprias, conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="b12f2-288">Replace the information with your own, as shown in the following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="b12f2-289">Adicionar o novo certificado raiz.</span><span class="sxs-lookup"><span data-stu-id="b12f2-289">Add the new root certificate.</span></span> <span data-ttu-id="b12f2-290">Você pode adicionar apenas um certificado por vez.</span><span class="sxs-lookup"><span data-stu-id="b12f2-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="b12f2-291">Você pode verificar se o novo certificado foi adicionado corretamente usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12f2-291">You can verify that the new certificate was added correctly by using the following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="b12f2-292"><a name="removerootcert"></a>Adicionar ou remover um certificado raiz</span><span class="sxs-lookup"><span data-stu-id="b12f2-292"><a name="removerootcert"></a>To remove a root certificate</span></span>

1. <span data-ttu-id="b12f2-293">Declare as variáveis.</span><span class="sxs-lookup"><span data-stu-id="b12f2-293">Declare the variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="b12f2-294">Remova o certificado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-294">Remove the certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="b12f2-295">Use o exemplo a seguir para verificar se o certificado foi removido com êxito.</span><span class="sxs-lookup"><span data-stu-id="b12f2-295">Use the following example to verify that the certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="b12f2-296"><a name="revoke"></a>Revogar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b12f2-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="b12f2-297">É possível revogar certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-297">You can revoke client certificates.</span></span> <span data-ttu-id="b12f2-298">A lista de certificados revogados permite que você negue seletivamente conectividade ponto a site com base em certificados de cliente individuais.</span><span class="sxs-lookup"><span data-stu-id="b12f2-298">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="b12f2-299">Isso é diferente da remoção de um certificado raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="b12f2-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="b12f2-300">Se você remover um arquivo .cer de certificado raiz confiável do Azure, ele revogará o acesso para todos os certificados de cliente gerados/assinados pelo certificado raiz revogado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-300">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="b12f2-301">Revogar um certificado de cliente, em vez do certificado raiz, permite que os outros certificados gerados a partir do certificado raiz continuem a ser usados para autenticação.</span><span class="sxs-lookup"><span data-stu-id="b12f2-301">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span></span>

<span data-ttu-id="b12f2-302">A prática comum é usar o certificado raiz para gerenciar o acesso em níveis de equipe ou organização, enquanto estiver usando certificados de cliente revogados para controle de acesso refinado em usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="b12f2-302">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="b12f2-303"><a name="revokeclientcert"></a>Para revogar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b12f2-303"><a name="revokeclientcert"></a>To revoke a client certificate</span></span>

1. <span data-ttu-id="b12f2-304">Recupere a impressão digital do certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="b12f2-304">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="b12f2-305">Para saber mais, confira [Como recuperar a impressão digital de um certificado](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="b12f2-305">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="b12f2-306">Copie as informações para um editor de texto e remova todos os espaços para que seja uma cadeia de caracteres contínua.</span><span class="sxs-lookup"><span data-stu-id="b12f2-306">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="b12f2-307">A cadeia de caracteres é declarada como uma variável na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="b12f2-307">This string is declared as a variable in the next step.</span></span>
3. <span data-ttu-id="b12f2-308">Declare as variáveis.</span><span class="sxs-lookup"><span data-stu-id="b12f2-308">Declare the variables.</span></span> <span data-ttu-id="b12f2-309">Declare a impressão digital recuperada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="b12f2-309">Make sure to declare the thumbprint you retrieved in the previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="b12f2-310">Adicione a impressão digital à lista de certificados revogados.</span><span class="sxs-lookup"><span data-stu-id="b12f2-310">Add the thumbprint to the list of revoked certificates.</span></span> <span data-ttu-id="b12f2-311">Você verá "Êxito" quando a impressão digital tiver sido adicionada.</span><span class="sxs-lookup"><span data-stu-id="b12f2-311">You see "Succeeded" when the thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="b12f2-312">Verifique se a impressão digital foi adicionada à lista de certificados revogados.</span><span class="sxs-lookup"><span data-stu-id="b12f2-312">Verify that the thumbprint was added to the certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="b12f2-313">Após a adição da impressão digital, o certificado não poderá mais ser usado para se conectar.</span><span class="sxs-lookup"><span data-stu-id="b12f2-313">After the thumbprint has been added, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="b12f2-314">Os clientes que tentam se conectar usando este certificado recebem uma mensagem informando que o certificado não é mais válido.</span><span class="sxs-lookup"><span data-stu-id="b12f2-314">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

### <span data-ttu-id="b12f2-315"><a name="reinstateclientcert"></a>Para restabelecer um certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="b12f2-315"><a name="reinstateclientcert"></a>To reinstate a client certificate</span></span>

<span data-ttu-id="b12f2-316">Você pode restabelecer um certificado de cliente removendo a impressão digital da lista de certificados de cliente revogados.</span><span class="sxs-lookup"><span data-stu-id="b12f2-316">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span></span>

1. <span data-ttu-id="b12f2-317">Declare as variáveis.</span><span class="sxs-lookup"><span data-stu-id="b12f2-317">Declare the variables.</span></span> <span data-ttu-id="b12f2-318">Declare a impressão digital correta para o certificado que você deseja restabelecer.</span><span class="sxs-lookup"><span data-stu-id="b12f2-318">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="b12f2-319">Remova a impressão digital do certificado da lista de revogação de certificado.</span><span class="sxs-lookup"><span data-stu-id="b12f2-319">Remove the certificate thumbprint from the certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="b12f2-320">Verifique se a impressão digital foi removida da lista revogada.</span><span class="sxs-lookup"><span data-stu-id="b12f2-320">Check if the thumbprint is removed from the revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="b12f2-321"><a name="faq"></a>Perguntas frequentes sobre Ponto a site</span><span class="sxs-lookup"><span data-stu-id="b12f2-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b12f2-322">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b12f2-322">Next steps</span></span>
<span data-ttu-id="b12f2-323">Quando sua conexão for concluída, você poderá adicionar máquinas virtuais às suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="b12f2-323">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="b12f2-324">Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="b12f2-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="b12f2-325">Para saber mais sobre redes e máquinas virtuais, consulte [Visão geral de rede do Azure e VM Linux](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b12f2-325">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>