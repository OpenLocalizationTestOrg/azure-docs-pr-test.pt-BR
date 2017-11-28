---
title: 'Como tooconfigure roteamento para um circuito de rota expressa do Azure: CLI | Microsoft Docs'
description: "Este artigo ajuda você a criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
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
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="ed16d-104">Criar e modificar o roteamento de um circuito da ExpressRoute usando CLI</span><span class="sxs-lookup"><span data-stu-id="ed16d-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="ed16d-105">Este artigo ajuda você a criar e gerenciar a configuração de roteamento para um circuito de rota expressa no modelo de implantação do Gerenciador de recursos do hello usando a CLI.</span><span class="sxs-lookup"><span data-stu-id="ed16d-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="ed16d-106">Você também pode verificar status hello, update ou delete e desprovisionar emparelhamentos de um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ed16d-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="ed16d-107">Se você quiser toouse toowork um método diferente com o circuito, selecione um artigo de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed16d-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="ed16d-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed16d-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="ed16d-110">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="ed16d-111">Vídeo – Emparelhamento privado</span><span class="sxs-lookup"><span data-stu-id="ed16d-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ed16d-112">Vídeo – Emparelhamento público</span><span class="sxs-lookup"><span data-stu-id="ed16d-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ed16d-113">Vídeo – Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="ed16d-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ed16d-114">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="ed16d-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="ed16d-115">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="ed16d-115">Configuration prerequisites</span></span>

* <span data-ttu-id="ed16d-116">Antes de começar, instale a versão mais recente Olá de comandos CLI hello (2.0 ou posteriores).</span><span class="sxs-lookup"><span data-stu-id="ed16d-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="ed16d-117">Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ed16d-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="ed16d-118">Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxo de trabalho](expressroute-workflows.md) páginas antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="ed16d-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="ed16d-119">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="ed16d-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="ed16d-120">Siga as instruções de saudação muito[criar um circuito de rota expressa](howto-circuit-cli.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ed16d-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ed16d-121">Olá circuito de rota expressa deve estar no estado habilitado e configurado para você comandos de saudação capaz de toorun toobe neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ed16d-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="ed16d-122">Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="ed16d-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="ed16d-123">Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="ed16d-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="ed16d-124">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito da ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ed16d-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="ed16d-125">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="ed16d-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="ed16d-126">No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez.</span><span class="sxs-lookup"><span data-stu-id="ed16d-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="ed16d-127">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-127">Azure private peering</span></span>

<span data-ttu-id="ed16d-128">Esta seção ajuda você a criar, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ed16d-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="ed16d-129">toocreate emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="ed16d-130">Instale a versão mais recente de saudação do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed16d-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="ed16d-131">Você deve usar a versão mais recente de saudação do hello Azure Interface de linha de comando (CLI). * hello revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="ed16d-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="ed16d-132">Selecionar assinatura Olá deseja toocreate circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="ed16d-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="ed16d-133">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ed16d-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="ed16d-134">Siga Olá instruções toocreate um [circuito de rota expressa](howto-circuit-cli.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed16d-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="ed16d-135">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="ed16d-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="ed16d-136">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="ed16d-137">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="ed16d-138">Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="ed16d-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="ed16d-139">Use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="ed16d-140">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-140">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="ed16d-141">Configure o emparelhamento particular do Azure para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed16d-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="ed16d-142">Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:</span><span class="sxs-lookup"><span data-stu-id="ed16d-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="ed16d-143">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="ed16d-144">subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ed16d-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="ed16d-145">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="ed16d-146">subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ed16d-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="ed16d-147">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ed16d-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="ed16d-148">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="ed16d-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="ed16d-149">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ed16d-149">AS number for peering.</span></span> <span data-ttu-id="ed16d-150">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="ed16d-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="ed16d-151">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ed16d-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="ed16d-152">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="ed16d-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="ed16d-153">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="ed16d-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="ed16d-154">Use hello Azure privado de emparelhamento para o circuito de tooconfigure de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="ed16d-155">Se você escolher toouse um hash MD5, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="ed16d-156">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="ed16d-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="ed16d-157">tooview privado emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-157">tooview Azure private peering details</span></span>

<span data-ttu-id="ed16d-158">Você pode obter os detalhes de configuração usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="ed16d-159">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-159">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="ed16d-160">tooupdate configuração emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="ed16d-161">Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed16d-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="ed16d-162">Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too500 100.</span><span class="sxs-lookup"><span data-stu-id="ed16d-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="ed16d-163">toodelete emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-163">toodelete Azure private peering</span></span>

<span data-ttu-id="ed16d-164">Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="ed16d-165">Certifique-se de que todas as redes virtuais são desvinculadas do hello circuito de rota expressa antes de executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="ed16d-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="ed16d-166">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-166">Azure public peering</span></span>

<span data-ttu-id="ed16d-167">Esta seção ajuda você a criar, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ed16d-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="ed16d-168">toocreate emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="ed16d-169">Instale a versão mais recente de saudação do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed16d-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="ed16d-170">Você deve usar a versão mais recente de saudação do hello Azure Interface de linha de comando (CLI). * hello revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="ed16d-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="ed16d-171">Selecione a assinatura de saudação do qual você deseja que o circuito de rota expressa toocreate.</span><span class="sxs-lookup"><span data-stu-id="ed16d-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="ed16d-172">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ed16d-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="ed16d-173">Siga Olá instruções toocreate um [circuito de rota expressa](howto-circuit-cli.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed16d-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="ed16d-174">Caso seu provedor de conectividade ofereça serviços gerenciados de Camada 3, você pode solicitar a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed16d-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="ed16d-175">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="ed16d-176">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="ed16d-177">Verifique tooensure de circuito de rota expressa Olá provisionado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="ed16d-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="ed16d-178">Use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="ed16d-179">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-179">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="ed16d-180">Configure o emparelhamento público do Azure para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed16d-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="ed16d-181">Certifique-se de que você tenha Olá informações a seguir antes de você continuar.</span><span class="sxs-lookup"><span data-stu-id="ed16d-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="ed16d-182">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="ed16d-183">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="ed16d-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="ed16d-184">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="ed16d-185">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="ed16d-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="ed16d-186">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ed16d-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="ed16d-187">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="ed16d-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="ed16d-188">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ed16d-188">AS number for peering.</span></span> <span data-ttu-id="ed16d-189">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="ed16d-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="ed16d-190">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="ed16d-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="ed16d-191">Execute hello Azure público de emparelhamento para o circuito de tooconfigure de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="ed16d-192">Se você escolher toouse um hash MD5, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="ed16d-193">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="ed16d-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="ed16d-194">tooview público emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-194">tooview Azure public peering details</span></span>

<span data-ttu-id="ed16d-195">Você pode obter os detalhes de configuração usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="ed16d-196">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-196">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="ed16d-197">tooupdate configuração de emparelhamento pública do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="ed16d-198">Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed16d-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="ed16d-199">Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too600 200.</span><span class="sxs-lookup"><span data-stu-id="ed16d-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="ed16d-200">toodelete emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="ed16d-200">toodelete Azure public peering</span></span>

<span data-ttu-id="ed16d-201">Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="ed16d-202">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="ed16d-202">Microsoft peering</span></span>

<span data-ttu-id="ed16d-203">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ed16d-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed16d-204">Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft hello, mesmo se os filtros de roteamento não estão definidos.</span><span class="sxs-lookup"><span data-stu-id="ed16d-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="ed16d-205">Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="ed16d-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="ed16d-206">Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ed16d-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="ed16d-207">toocreate emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="ed16d-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="ed16d-208">Instale a versão mais recente de saudação do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed16d-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="ed16d-209">Versão mais recente de saudação de uso do hello Azure Interface de linha de comando (CLI). * hello revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="ed16d-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="ed16d-210">Selecione a assinatura de saudação do qual você deseja que o circuito de rota expressa toocreate.</span><span class="sxs-lookup"><span data-stu-id="ed16d-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="ed16d-211">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ed16d-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="ed16d-212">Siga Olá instruções toocreate um [circuito de rota expressa](howto-circuit-cli.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed16d-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="ed16d-213">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="ed16d-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="ed16d-214">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="ed16d-215">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="ed16d-216">Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="ed16d-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="ed16d-217">Use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="ed16d-218">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-218">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="ed16d-219">Configure o emparelhamento do circuito de saudação do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ed16d-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="ed16d-220">Certifique-se de que você tenha Olá seguintes informações antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ed16d-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="ed16d-221">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="ed16d-222">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="ed16d-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="ed16d-223">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="ed16d-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="ed16d-224">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="ed16d-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="ed16d-225">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ed16d-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="ed16d-226">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="ed16d-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="ed16d-227">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ed16d-227">AS number for peering.</span></span> <span data-ttu-id="ed16d-228">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="ed16d-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="ed16d-229">Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed16d-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="ed16d-230">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="ed16d-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="ed16d-231">Se você planejar toosend um conjunto de prefixos, você pode enviar uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="ed16d-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="ed16d-232">Esses prefixos devem ser registrado tooyou em um RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="ed16d-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="ed16d-233">**Opcional -** cliente ASN: se você estiver prefixos de anúncios que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, eles são registrados.</span><span class="sxs-lookup"><span data-stu-id="ed16d-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="ed16d-234">Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="ed16d-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="ed16d-235">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="ed16d-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="ed16d-236">Execute Olá exemplo tooconfigure emparelhamento da Microsoft para o circuito a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="ed16d-237">tooget detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="ed16d-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="ed16d-238">Você pode obter os detalhes de configuração usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="ed16d-239">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-239">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="ed16d-240">tooupdate configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="ed16d-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="ed16d-241">Você pode atualizar qualquer parte da configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed16d-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="ed16d-242">Olá anunciado prefixos de circuito Olá estão sendo atualizados no too124.1.0.0/24 123.1.0.0/24 em Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="ed16d-243">toodelete emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="ed16d-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="ed16d-244">Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed16d-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="ed16d-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed16d-245">Next steps</span></span>

<span data-ttu-id="ed16d-246">Próxima etapa, [vincular um circuito de rota expressa do tooan de VNet](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ed16d-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="ed16d-247">Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="ed16d-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="ed16d-248">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="ed16d-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="ed16d-249">Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed16d-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>