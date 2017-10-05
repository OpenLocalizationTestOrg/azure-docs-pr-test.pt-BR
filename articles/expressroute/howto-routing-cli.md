---
title: 'Como configurar o roteamento de um circuito da ExpressRoute do Azure: CLI | Microsoft Docs'
description: "Este artigo ajuda a criar e provisionar o emparelhamento público, privado e da Microsoft de um circuito da ExpressRoute. Este artigo também mostra como verificar o status, atualizar ou excluir emparelhamentos de seu circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: fbf0bd9a139c22bbd63755f6df445f6596aaccc5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="20da9-104">Criar e modificar o roteamento de um circuito da ExpressRoute usando CLI</span><span class="sxs-lookup"><span data-stu-id="20da9-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="20da9-105">Esse artigo ajuda a criar e gerenciar a configuração de roteamento de um circuito da ExpressRoute no modelo de implantação do Gerenciador de Recursos usando CLI.</span><span class="sxs-lookup"><span data-stu-id="20da9-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="20da9-106">Você também pode verificar o status, atualizar ou excluir e desprovisionar emparelhamentos de um circuito da ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="20da9-107">Se quiser usar um método diferente para trabalhar com seu circuito, selecione um artigo na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="20da9-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="20da9-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="20da9-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20da9-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="20da9-110">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="20da9-111">Vídeo – Emparelhamento privado</span><span class="sxs-lookup"><span data-stu-id="20da9-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="20da9-112">Vídeo – Emparelhamento público</span><span class="sxs-lookup"><span data-stu-id="20da9-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="20da9-113">Vídeo – Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="20da9-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="20da9-114">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="20da9-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="20da9-115">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="20da9-115">Configuration prerequisites</span></span>

* <span data-ttu-id="20da9-116">Antes de começar, instale a versão mais recente dos comandos da CLI (2.0 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="20da9-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="20da9-117">Para saber mais sobre como instalar os comandos do CLI, veja [Instalar a CLI do Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="20da9-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="20da9-118">Certifique-se de que você leu as páginas de [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md) e [fluxo de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="20da9-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="20da9-119">Você deve ter um circuito da ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="20da9-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="20da9-120">Antes de continuar, siga as instruções para [criar um circuito da ExpressRoute](howto-circuit-cli.md) e para que o circuito seja habilitado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="20da9-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="20da9-121">O circuito da ExpressRoute deve estar em um estado provisionado e habilitado e para que você possa executar os comandos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="20da9-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="20da9-122">Estas instruções se aplicam apenas a circuitos criados com provedores de serviço que oferecem serviços de conectividade de Camada 2.</span><span class="sxs-lookup"><span data-stu-id="20da9-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="20da9-123">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="20da9-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="20da9-124">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito da ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="20da9-125">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="20da9-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="20da9-126">No entanto, você deve concluir a configuração de um emparelhamento por vez.</span><span class="sxs-lookup"><span data-stu-id="20da9-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="20da9-127">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-127">Azure private peering</span></span>

<span data-ttu-id="20da9-128">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento privado do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-128">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="20da9-129">Criar um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-129">To create Azure private peering</span></span>

1. <span data-ttu-id="20da9-130">Instale a versão mais recente do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="20da9-130">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="20da9-131">Você deve usar a versão mais recente do CLI do Azure (Interface de linha de comando). * Leia os [pré-requisitos](expressroute-prerequisites.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="20da9-131">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="20da9-132">Selecionar a assinatura na qual você deseja criar um circuito da ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="20da9-132">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="20da9-133">Criar um circuito da ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="20da9-134">Siga as instruções para criar um [circuito do ExpressRoute](howto-circuit-cli.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="20da9-134">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="20da9-135">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="20da9-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="20da9-136">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="20da9-136">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="20da9-137">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, continue a configuração executando as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="20da9-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="20da9-138">Verifique se o circuito do ExpressRoute está provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="20da9-138">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="20da9-139">Use o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-139">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="20da9-140">A resposta é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-140">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="20da9-141">Configure o emparelhamento privado do Azure para o circuito.</span><span class="sxs-lookup"><span data-stu-id="20da9-141">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="20da9-142">Verifique se você tem os seguintes itens antes de continuar com as próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="20da9-142">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="20da9-143">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="20da9-143">A /30 subnet for the primary link.</span></span> <span data-ttu-id="20da9-144">A sub-rede não deve fazer parte de nenhum espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="20da9-144">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="20da9-145">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="20da9-145">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="20da9-146">A sub-rede não deve fazer parte de nenhum espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="20da9-146">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="20da9-147">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="20da9-147">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="20da9-148">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="20da9-148">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="20da9-149">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="20da9-149">AS number for peering.</span></span> <span data-ttu-id="20da9-150">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="20da9-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="20da9-151">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="20da9-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="20da9-152">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="20da9-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="20da9-153">**Opcional –** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="20da9-153">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="20da9-154">Use o seguinte exemplo para configurar o emparelhamento privado do Azure para seu circuito:</span><span class="sxs-lookup"><span data-stu-id="20da9-154">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="20da9-155">Se você optar por usar um hash MD5, use o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="20da9-155">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="20da9-156">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="20da9-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="20da9-157">Para exibir detalhes sobre o emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-157">To view Azure private peering details</span></span>

<span data-ttu-id="20da9-158">Você pode obter detalhes de configuração usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="20da9-158">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="20da9-159">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-159">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="20da9-160">Atualizar a configuração de emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-160">To update Azure private peering configuration</span></span>

<span data-ttu-id="20da9-161">Você pode atualizar qualquer parte da configuração usando o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="20da9-161">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="20da9-162">Neste exemplo, a ID da VLAN do circuito está sendo atualizada de 100 para 500.</span><span class="sxs-lookup"><span data-stu-id="20da9-162">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="20da9-163">Excluir um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-163">To delete Azure private peering</span></span>

<span data-ttu-id="20da9-164">Você pode remover a configuração de emparelhamento executando o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-164">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="20da9-165">Verifique se todas as redes virtuais estão desvinculadas do circuito do ExpressRoute antes de executar esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="20da9-165">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="20da9-166">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-166">Azure public peering</span></span>

<span data-ttu-id="20da9-167">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento público do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-167">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="20da9-168">Criar o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-168">To create Azure public peering</span></span>

1. <span data-ttu-id="20da9-169">Instale a versão mais recente do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="20da9-169">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="20da9-170">Você deve usar a versão mais recente do CLI do Azure (Interface de linha de comando). * Leia os [pré-requisitos](expressroute-prerequisites.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="20da9-170">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="20da9-171">Selecione a assinatura para a qual você deseja criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-171">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="20da9-172">Criar um circuito da ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="20da9-173">Siga as instruções para criar um [circuito da ExpressRoute](howto-circuit-cli.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="20da9-173">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="20da9-174">Caso seu provedor de conectividade ofereça serviços gerenciados de Camada 3, você pode solicitar a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="20da9-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="20da9-175">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="20da9-175">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="20da9-176">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, continue a configuração executando as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="20da9-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="20da9-177">Verifique se o circuito do ExpressRoute está provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="20da9-177">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="20da9-178">Use o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-178">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="20da9-179">A resposta é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-179">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="20da9-180">Configure o emparelhamento público do Azure para o circuito.</span><span class="sxs-lookup"><span data-stu-id="20da9-180">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="20da9-181">Verifique se você tem as informações a seguir antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="20da9-181">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="20da9-182">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="20da9-182">A /30 subnet for the primary link.</span></span> <span data-ttu-id="20da9-183">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="20da9-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="20da9-184">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="20da9-184">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="20da9-185">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="20da9-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="20da9-186">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="20da9-186">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="20da9-187">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="20da9-187">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="20da9-188">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="20da9-188">AS number for peering.</span></span> <span data-ttu-id="20da9-189">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="20da9-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="20da9-190">**Opcional -** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="20da9-190">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="20da9-191">Executar o seguinte exemplo para configurar o emparelhamento público do Azure para seu circuito:</span><span class="sxs-lookup"><span data-stu-id="20da9-191">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="20da9-192">Se você optar por usar um hash MD5, use o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="20da9-192">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="20da9-193">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="20da9-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="20da9-194">Para exibir detalhes sobre o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-194">To view Azure public peering details</span></span>

<span data-ttu-id="20da9-195">Você pode obter detalhes de configuração usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="20da9-195">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="20da9-196">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-196">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="20da9-197">Atualizar a configuração de emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-197">To update Azure public peering configuration</span></span>

<span data-ttu-id="20da9-198">Você pode atualizar qualquer parte da configuração usando o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="20da9-198">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="20da9-199">Neste exemplo, a ID da VLAN do circuito está sendo atualizada de 200 para 600.</span><span class="sxs-lookup"><span data-stu-id="20da9-199">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="20da9-200">Excluir o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="20da9-200">To delete Azure public peering</span></span>

<span data-ttu-id="20da9-201">Você pode remover a configuração de emparelhamento executando o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-201">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="20da9-202">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="20da9-202">Microsoft peering</span></span>

<span data-ttu-id="20da9-203">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento da Microsoft para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-203">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20da9-204">O emparelhamento da Microsoft de circuitos do ExpressRoute configurados antes de 1º de agosto de 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft, mesmo que os filtros de rota não estejam definidos.</span><span class="sxs-lookup"><span data-stu-id="20da9-204">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="20da9-205">O emparelhamento da Microsoft de circuitos de ExpressRoute configurados em ou após 1º de agosto de 2017 não terá nenhum prefixo anunciado até que um filtro de rota seja anexado ao circuito.</span><span class="sxs-lookup"><span data-stu-id="20da9-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="20da9-206">Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="20da9-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="20da9-207">Criar emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="20da9-207">To create Microsoft peering</span></span>

1. <span data-ttu-id="20da9-208">Instale a versão mais recente do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="20da9-208">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="20da9-209">Use a versão mais recente do CLI do Azure (Interface de linha de comando).* Leia os [pré-requisitos](expressroute-prerequisites.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="20da9-209">Use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="20da9-210">Selecione a assinatura para a qual você deseja criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-210">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="20da9-211">Criar um circuito da ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20da9-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="20da9-212">Siga as instruções para criar um [circuito do ExpressRoute](howto-circuit-cli.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="20da9-212">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="20da9-213">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="20da9-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="20da9-214">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="20da9-214">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="20da9-215">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, continue a configuração executando as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="20da9-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="20da9-216">Verifique se o circuito do ExpressRoute está provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="20da9-216">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="20da9-217">Use o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-217">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="20da9-218">A resposta é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-218">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="20da9-219">Configurar o emparelhamento da Microsoft para o circuito.</span><span class="sxs-lookup"><span data-stu-id="20da9-219">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="20da9-220">Você precisa ter as seguintes informações antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="20da9-220">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="20da9-221">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="20da9-221">A /30 subnet for the primary link.</span></span> <span data-ttu-id="20da9-222">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="20da9-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="20da9-223">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="20da9-223">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="20da9-224">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="20da9-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="20da9-225">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="20da9-225">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="20da9-226">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="20da9-226">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="20da9-227">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="20da9-227">AS number for peering.</span></span> <span data-ttu-id="20da9-228">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="20da9-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="20da9-229">Prefixos anunciados: forneça uma lista com todos os prefixos que você pretende anunciar na sessão BGP.</span><span class="sxs-lookup"><span data-stu-id="20da9-229">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="20da9-230">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="20da9-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="20da9-231">Caso você planeje enviar um conjunto de prefixos, poderá enviar uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="20da9-231">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="20da9-232">Esses prefixos devem ser registrados em seu nome em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="20da9-232">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="20da9-233">**Opcional –** ASN de cliente: se você estiver anunciando prefixos não registrados com o número AS de emparelhamento, especifique o número AS com o qual eles estão registrados.</span><span class="sxs-lookup"><span data-stu-id="20da9-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="20da9-234">Nome do registro de roteamento: você pode especificar o RIR/IRR com base no qual o número de AS e os prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="20da9-234">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="20da9-235">**Opcional -** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="20da9-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="20da9-236">Execute o exemplo a seguir para configurar o emparelhamento da Microsoft para seu circuito:</span><span class="sxs-lookup"><span data-stu-id="20da9-236">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="20da9-237">Obter detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="20da9-237">To get Microsoft peering details</span></span>

<span data-ttu-id="20da9-238">Você pode obter detalhes de configuração usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="20da9-238">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="20da9-239">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-239">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="20da9-240">Atualizar a configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="20da9-240">To update Microsoft peering configuration</span></span>

<span data-ttu-id="20da9-241">Você pode atualizar qualquer parte da configuração.</span><span class="sxs-lookup"><span data-stu-id="20da9-241">You can update any part of the configuration.</span></span> <span data-ttu-id="20da9-242">Os prefixos anunciados do circuito estão sendo atualizados de 123.1.0.0/24 para 124.1.0.0/24 no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="20da9-242">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="20da9-243">Excluir emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="20da9-243">To delete Microsoft peering</span></span>

<span data-ttu-id="20da9-244">Você pode remover a configuração de emparelhamento executando o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="20da9-244">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="20da9-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20da9-245">Next steps</span></span>

<span data-ttu-id="20da9-246">A próxima etapa será [Vincular uma Rede Virtual a um circuito do ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="20da9-246">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="20da9-247">Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="20da9-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="20da9-248">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="20da9-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="20da9-249">Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20da9-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>