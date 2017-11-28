---
title: 'Criar e modificar um circuito do Azure ExpressRoute: CLI | Microsoft Docs'
description: Este artigo descreve como toocreate, provisionar, verifique se, atualizar, excluir e cancelar o provisionamento de um circuito de rota expressa usando a CLI.
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="36430-103">Criar e modificar um circuito do ExpressRoute usando a CLI</span><span class="sxs-lookup"><span data-stu-id="36430-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="36430-104">Este artigo descreve como toocreate um circuito de rota expressa do Azure usando Olá Interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="36430-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="36430-105">Este artigo também mostra como toocheck Olá status, atualizar, ou excluir e cancelar o provisionamento de um circuito.</span><span class="sxs-lookup"><span data-stu-id="36430-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="36430-106">Se você quiser toouse toowork um método diferente com circuitos do ExpressRoute, você pode selecionar artigo Olá Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="36430-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="36430-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="36430-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36430-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="36430-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="36430-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="36430-110">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="36430-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="36430-111">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="36430-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="36430-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="36430-112">Before you begin</span></span>

* <span data-ttu-id="36430-113">Antes de começar, instale a versão mais recente Olá de comandos CLI hello (2.0 ou posteriores).</span><span class="sxs-lookup"><span data-stu-id="36430-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="36430-114">Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="36430-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="36430-115">Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="36430-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="36430-116">Criar e provisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="36430-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="36430-117">1. Entre no tooyour conta do Azure e selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="36430-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="36430-118">toobegin sua configuração, entrar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="36430-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="36430-119">Use Olá toohelp exemplos que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="36430-120">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="36430-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="36430-121">Selecione a assinatura de saudação do qual você deseja toocreate um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="36430-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="36430-122">2. Obter lista de saudação de provedores suportados, locais e larguras de banda</span><span class="sxs-lookup"><span data-stu-id="36430-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="36430-123">Antes de criar um circuito de rota expressa, você precisa de lista de saudação de provedores com suporte de conectividade, locais e as opções de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="36430-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="36430-124">Olá CLI comando 'az rota expressa lista-serviço-provedores de rede' retorna essas informações, que você usará em etapas posteriores:</span><span class="sxs-lookup"><span data-stu-id="36430-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="36430-125">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="36430-126">Verifique Olá resposta toosee se seu provedor de conectividade está listado.</span><span class="sxs-lookup"><span data-stu-id="36430-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="36430-127">Anote Olá informações que você precisará criar um circuito a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="36430-128">Nome</span><span class="sxs-lookup"><span data-stu-id="36430-128">Name</span></span>
* <span data-ttu-id="36430-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="36430-129">PeeringLocations</span></span>
* <span data-ttu-id="36430-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="36430-130">BandwidthsOffered</span></span>

<span data-ttu-id="36430-131">Agora você está pronto toocreate um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="36430-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="36430-132">3. Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="36430-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36430-133">O circuito de rota expressa é cobrado do momento Olá que uma chave de serviço é emitida.</span><span class="sxs-lookup"><span data-stu-id="36430-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="36430-134">Execute esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="36430-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="36430-135">Se você ainda não tiver um grupo de recursos, deverá criar um antes de criar o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="36430-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="36430-136">Você pode criar um grupo de recursos executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="36430-137">saudação de exemplo a seguir mostra como toocreate uma rota expressa de 200 Mbps de circuito por meio de Equinix no Vale do Silício.</span><span class="sxs-lookup"><span data-stu-id="36430-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="36430-138">Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação.</span><span class="sxs-lookup"><span data-stu-id="36430-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="36430-139">Certifique-se de que você especifique a camada SKU correta hello e família SKU:</span><span class="sxs-lookup"><span data-stu-id="36430-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="36430-140">A camada da SKU determina se um complemento padrão ou premium do ExpressRoute está habilitado.</span><span class="sxs-lookup"><span data-stu-id="36430-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="36430-141">Você pode especificar 'Padrão' hello de tooget SKU standard ou 'Premium' para o complemento do premium Olá.</span><span class="sxs-lookup"><span data-stu-id="36430-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="36430-142">A família SKU determina o tipo de cobrança de saudação.</span><span class="sxs-lookup"><span data-stu-id="36430-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="36430-143">Você pode especificar 'Metereddata' para um plano de dados limitado e 'Unlimiteddata' para um plano de dados ilimitado.</span><span class="sxs-lookup"><span data-stu-id="36430-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="36430-144">Você pode alterar o tipo de cobrança de saudação do ' Metereddata 'too'Unlimiteddata', mas você não pode alterar o tipo de saudação de 'Unlimiteddata' too'Metereddata'.</span><span class="sxs-lookup"><span data-stu-id="36430-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="36430-145">O circuito de rota expressa é cobrado do momento Olá que uma chave de serviço é emitida.</span><span class="sxs-lookup"><span data-stu-id="36430-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="36430-146">saudação de exemplo a seguir é uma solicitação para uma nova chave de serviço:</span><span class="sxs-lookup"><span data-stu-id="36430-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="36430-147">resposta de Olá contém a chave de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="36430-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="36430-148">4. Listar todos os circuitos do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="36430-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="36430-149">tooget uma lista de todos os circuitos de rota expressa Olá que você criou, execute o comando a ''az rede rota expressa lista hello.</span><span class="sxs-lookup"><span data-stu-id="36430-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="36430-150">Você pode recuperar essas informações a qualquer momento usando este comando.</span><span class="sxs-lookup"><span data-stu-id="36430-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="36430-151">toolist todos os circuitos, verifique Olá chamada sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="36430-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="36430-152">Sua chave de serviço está listada no hello *ServiceKey* campo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="36430-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="36430-153">Você pode obter descrições detalhadas de todos os parâmetros de saudação executando o comando hello usando Olá '-h' parâmetro.</span><span class="sxs-lookup"><span data-stu-id="36430-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="36430-154">5. Enviar Olá tooyour chave conectividade provedor para provisionamento</span><span class="sxs-lookup"><span data-stu-id="36430-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="36430-155">'ServiceProviderProvisioningState' fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="36430-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="36430-156">status de Olá fornece estado Olá em Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="36430-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="36430-157">Para obter mais informações, consulte Olá [artigo de fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="36430-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="36430-158">Quando você cria um novo circuito de rota expressa, circuito hello está em Olá estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="36430-159">Olá circuito alterações toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:</span><span class="sxs-lookup"><span data-stu-id="36430-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="36430-160">Para você toobe capaz de toouse um circuito de rota expressa, ele deve ser Olá estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="36430-161">6. Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação</span><span class="sxs-lookup"><span data-stu-id="36430-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="36430-162">Verificar o status de saudação e o estado de saudação da chave de circuito Olá permite que você saiba quando seu provedor habilitou o seu circuito.</span><span class="sxs-lookup"><span data-stu-id="36430-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="36430-163">Depois que o circuito Olá tiver sido configurado, 'ServiceProviderProvisioningState' aparece como 'Provisionado', conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="36430-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="36430-164">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-164">hello response is similar toohello following example:</span></span>

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="36430-165">7. Criar sua configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="36430-165">7. Create your routing configuration</span></span>

<span data-ttu-id="36430-166">Para obter instruções passo a passo, consulte Olá [configuração de roteamento de circuito de rota expressa](howto-routing-cli.md) artigo toocreate e modificar os emparelhamentos de circuito.</span><span class="sxs-lookup"><span data-stu-id="36430-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36430-167">Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade.</span><span class="sxs-lookup"><span data-stu-id="36430-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="36430-168">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="36430-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="36430-169">8. Vincular um circuito de rota expressa do tooan de rede virtual</span><span class="sxs-lookup"><span data-stu-id="36430-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="36430-170">Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="36430-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="36430-171">Saudação de uso [vinculação virtual redes circuitos tooExpressRoute](howto-linkvnet-cli.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="36430-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="36430-172"><a name="modify">
            </a>Modificar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="36430-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="36430-173">Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="36430-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="36430-174">Você pode fazer as seguintes alterações sem tempo de inatividade de saudação:</span><span class="sxs-lookup"><span data-stu-id="36430-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="36430-175">Você pode habilitar ou desabilitar o complemento ExpressRoute Premium para seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="36430-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="36430-176">Você pode aumentar a largura de banda de saudação do circuito ExpressRoute desde que haja capacidade disponível na porta hello.</span><span class="sxs-lookup"><span data-stu-id="36430-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="36430-177">No entanto, não há suporte para fazer o downgrade de largura de banda de saudação de um circuito.</span><span class="sxs-lookup"><span data-stu-id="36430-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="36430-178">Você pode alterar o plano de medição de saudação de dados limitados tooUnlimited dados.</span><span class="sxs-lookup"><span data-stu-id="36430-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="36430-179">No entanto, a alteração Olá plano de dados ilimitado tooMetered não há suporte para dados de medição.</span><span class="sxs-lookup"><span data-stu-id="36430-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="36430-180">Você pode habilitar e desabilitar *Permitir Operações Clássicas*.</span><span class="sxs-lookup"><span data-stu-id="36430-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="36430-181">Para obter mais informações sobre limitações e limites, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="36430-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="36430-182">complemento do premium tooenable Olá rota expressa</span><span class="sxs-lookup"><span data-stu-id="36430-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="36430-183">Você pode habilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="36430-184">circuito Olá agora tem habilitados dos recursos de complemento de premium Olá rota expressa.</span><span class="sxs-lookup"><span data-stu-id="36430-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="36430-185">Começamos a cobrança é para o recurso de complemento premium Olá assim que o comando Olá foi executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="36430-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="36430-186">complemento do premium toodisable Olá rota expressa</span><span class="sxs-lookup"><span data-stu-id="36430-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36430-187">Essa operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="36430-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="36430-188">Antes de desabilitar o complemento do premium Olá rota expressa, compreenda Olá critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="36430-189">Antes de você fazer o downgrade de toostandard premium, você deve se certificar que você tem menos de 10 circuito toohello vinculado de redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="36430-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="36430-190">Se existirem mais de 10, sua solicitação de atualização falhará e você será cobrado de acordo com as tarifas Premium.</span><span class="sxs-lookup"><span data-stu-id="36430-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="36430-191">Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="36430-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="36430-192">Se você não desvincular todas as redes virtuais, sua solicitação de atualização falhará e cobraremos de acordo com as tarifas premium.</span><span class="sxs-lookup"><span data-stu-id="36430-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="36430-193">Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado.</span><span class="sxs-lookup"><span data-stu-id="36430-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="36430-194">Se o tamanho da tabela de rota for maior que 4.000 rotas, descarta a sessão BGP de saudação.</span><span class="sxs-lookup"><span data-stu-id="36430-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="36430-195">sessão de saudação não ser habilitados novamente até que o número de saudação de prefixos anunciados está abaixo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="36430-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="36430-196">Você pode desabilitar o complemento do premium Olá rota expressa para o circuito existente hello usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="36430-197">largura de banda de circuito ExpressRoute tooupdate Olá</span><span class="sxs-lookup"><span data-stu-id="36430-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="36430-198">Para opções de largura de banda Olá tem suportada para o seu provedor, verifique Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="36430-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="36430-199">Você pode escolher qualquer tamanho maior do que o tamanho de saudação do circuito existente.</span><span class="sxs-lookup"><span data-stu-id="36430-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36430-200">Se não houver capacidade insuficiente na porta existente hello, você pode ter circuito de rota expressa toorecreate hello.</span><span class="sxs-lookup"><span data-stu-id="36430-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="36430-201">Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.</span><span class="sxs-lookup"><span data-stu-id="36430-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="36430-202">Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="36430-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="36430-203">Fazendo downgrade de largura de banda requer que você toodeprovision Olá circuito de rota expressa e, em seguida, Reprovisionar um novo circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="36430-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="36430-204">Depois de decidir tamanho Olá que é necessário usar o circuito de Olá tooresize de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="36430-205">O circuito será dimensionado para cima no lado do Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="36430-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="36430-206">Em seguida, você deve entrar em contato com suas configurações de tooupdate do provedor de conectividade em seu toomatch lado essa alteração.</span><span class="sxs-lookup"><span data-stu-id="36430-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="36430-207">Depois de fazer essa notificação, começamos a cobrança você para a opção de largura de banda Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="36430-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="36430-208">Olá toomove SKU de toounlimited limitado</span><span class="sxs-lookup"><span data-stu-id="36430-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="36430-209">Você pode alterar Olá SKU de um circuito de rota expressa usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="36430-210">toocontrol clássico de toohello de acesso e ambientes do Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="36430-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="36430-211">Consulte as instruções de saudação em [circuitos ExpressRoute mover de modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="36430-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="36430-212">Desprovisionamento e exclusão de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="36430-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="36430-213">toodeprovision e excluir um circuito de rota expressa, certifique-se de entender Olá critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="36430-214">Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="36430-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="36430-215">Se essa operação falhar, verifique toosee se todas as redes virtuais são vinculados toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="36430-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="36430-216">Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado**, você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado.</span><span class="sxs-lookup"><span data-stu-id="36430-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="36430-217">Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.</span><span class="sxs-lookup"><span data-stu-id="36430-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="36430-218">Você pode excluir o circuito de saudação se o provedor de serviços de saudação tem desprovisionada circuito hello.</span><span class="sxs-lookup"><span data-stu-id="36430-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="36430-219">Quando um circuito desprovisionado, estado de provisionamento do provedor de serviços de saudação é definido muito**não provisionado**.</span><span class="sxs-lookup"><span data-stu-id="36430-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="36430-220">Isso interrompe a cobrança para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="36430-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="36430-221">Você pode excluir o circuito de rota expressa executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="36430-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="36430-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36430-222">Next steps</span></span>

<span data-ttu-id="36430-223">Depois de criar o circuito, certifique-se de que você Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="36430-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="36430-224">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="36430-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="36430-225">Vincular sua rede virtual de tooyour circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="36430-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
