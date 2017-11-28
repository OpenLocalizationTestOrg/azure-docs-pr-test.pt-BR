---
title: "Excluir um gateway de rede virtual: PowerShell: clássico do Azure | Microsoft Docs"
description: "Exclua um gateway de rede virtual usando o PowerShell no modelo de implantação clássico."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="cf897-103">Excluir um gateway de rede virtual usando o PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="cf897-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf897-104">Resource Manager – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cf897-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="cf897-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf897-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="cf897-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf897-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="cf897-107">Este artigo ajuda você a excluir um gateway de VPN no modelo de implantação clássico usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf897-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="cf897-108">Depois que o gateway de rede virtual tiver sido excluído, modifique o arquivo de configuração de rede para remover elementos que você não está mais usando.</span><span class="sxs-lookup"><span data-stu-id="cf897-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="cf897-109"><a name="connect"></a>Etapa 1: Conectar ao Azure</span><span class="sxs-lookup"><span data-stu-id="cf897-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="cf897-110">1. Instale os cmdlets mais recentes do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf897-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="cf897-111">Baixe e instale a versão mais recente dos cmdlets do PowerShell do SM (Gerenciamento de Serviços) do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf897-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="cf897-112">Para saber mais, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="cf897-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="cf897-113">2. Conectar-se à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf897-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="cf897-114">Abra o console do PowerShell com direitos elevados e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="cf897-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="cf897-115">Use o exemplo a seguir para ajudar a se conectar:</span><span class="sxs-lookup"><span data-stu-id="cf897-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="cf897-116"><a name="export"></a>Etapa 2: Exportar e exibir o arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="cf897-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="cf897-117">Crie um diretório em seu computador e exporte o arquivo de configuração de rede para o diretório.</span><span class="sxs-lookup"><span data-stu-id="cf897-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="cf897-118">Use esse arquivo para exibir as informações da configuração atual e também para modificar a configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="cf897-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="cf897-119">Neste exemplo, o arquivo de configuração de rede é exportado para C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="cf897-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="cf897-120">Abra o arquivo com um editor de texto e exiba o nome da rede virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="cf897-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="cf897-121">Quando você cria uma VNet no portal do Azure, o nome completo usado pelo Azure não fica visível no portal.</span><span class="sxs-lookup"><span data-stu-id="cf897-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="cf897-122">Por exemplo, uma VNet que parece ser chamada “ClassicVNet1” no portal do Azure pode ter um nome muito mais longo no arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="cf897-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="cf897-123">O nome pode ser algo parecido com ‘Grupo ClassicRG1 ClassicVNet1’.</span><span class="sxs-lookup"><span data-stu-id="cf897-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="cf897-124">Os nomes de rede virtual são listados como **'VirtualNetworkSite name ='**.</span><span class="sxs-lookup"><span data-stu-id="cf897-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="cf897-125">Use os nomes no arquivo de configuração de rede ao executar os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf897-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="cf897-126"><a name="delete"></a>Etapa 3: Excluir o gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="cf897-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="cf897-127">Quando você exclui um gateway de rede virtual, todas as conexões com a rede virtual por meio do gateway são desconectadas.</span><span class="sxs-lookup"><span data-stu-id="cf897-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="cf897-128">Se você tiver clientes P2S conectados à rede virtual, eles serão desconectados sem aviso.</span><span class="sxs-lookup"><span data-stu-id="cf897-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="cf897-129">Este exemplo exclui o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cf897-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="cf897-130">Lembre-se de usar o nome completo da rede virtual do arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="cf897-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="cf897-131">Se for bem-sucedido, o retorno mostrará:</span><span class="sxs-lookup"><span data-stu-id="cf897-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="cf897-132"><a name="modify"></a>Etapa 4: Modificar o arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="cf897-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="cf897-133">Quando você exclui um gateway de rede virtual, o cmdlet não modifica o arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="cf897-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="cf897-134">Você precisa modificar o arquivo para remover os elementos que não estão mais sendo usados.</span><span class="sxs-lookup"><span data-stu-id="cf897-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="cf897-135">As seções a seguir ajudarão você a modificar o arquivo de configuração de rede que baixou.</span><span class="sxs-lookup"><span data-stu-id="cf897-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="cf897-136"><a name="lnsref"></a>Referências do Site de Rede Local</span><span class="sxs-lookup"><span data-stu-id="cf897-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="cf897-137">Para remover as informações de referência do site, faça alterações de configuração em **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="cf897-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="cf897-138">A remoção de uma referência de site local dispara o Azure para excluir um túnel.</span><span class="sxs-lookup"><span data-stu-id="cf897-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="cf897-139">Dependendo da configuração que você criou, é possível que não haja uma **LocalNetworkSiteRef** listada.</span><span class="sxs-lookup"><span data-stu-id="cf897-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="cf897-140">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf897-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="cf897-141"><a name="lns"></a>Sites de Rede Local</span><span class="sxs-lookup"><span data-stu-id="cf897-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="cf897-142">Remova os sites locais que não estiver mais usando.</span><span class="sxs-lookup"><span data-stu-id="cf897-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="cf897-143">Dependendo da configuração que você criou, é possível que não haja um **LocalNetworkSite** listado.</span><span class="sxs-lookup"><span data-stu-id="cf897-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="cf897-144">Neste exemplo, removemos apenas Site3.</span><span class="sxs-lookup"><span data-stu-id="cf897-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="cf897-145"><a name="clientaddresss"></a>AddressPool do cliente</span><span class="sxs-lookup"><span data-stu-id="cf897-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="cf897-146">Caso tenha uma conexão P2S com a VNet, você terá um **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="cf897-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="cf897-147">Remova os pools de endereços de cliente que correspondem ao gateway de rede virtual que você excluiu.</span><span class="sxs-lookup"><span data-stu-id="cf897-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="cf897-148">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf897-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="cf897-149"><a name="gwsub"></a>GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="cf897-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="cf897-150">Exclua a **GatewaySubnet** que corresponde à VNet.</span><span class="sxs-lookup"><span data-stu-id="cf897-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="cf897-151">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf897-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="cf897-152"><a name="upload"></a>Etapa 5: Carregar o arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="cf897-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="cf897-153">Salve suas alterações e faça upload do arquivo de configuração de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="cf897-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="cf897-154">Altere o caminho do arquivo conforme for necessário para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="cf897-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="cf897-155">Se for bem-sucedido, o retorno mostrará algo semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf897-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded