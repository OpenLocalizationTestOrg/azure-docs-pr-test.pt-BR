---
title: aaaCreate uma regra de Balanceador de carga do Azure para um cluster
description: Configure as portas de tooopen um balanceador de carga do Azure para o cluster do Azure Service Fabric.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="30ca3-103">Abrir portas para um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="30ca3-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="30ca3-104">Balanceador de carga Olá implantado com o cluster do Service Fabric do Azure direciona o tráfego tooyour aplicativo em execução em um nó.</span><span class="sxs-lookup"><span data-stu-id="30ca3-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="30ca3-105">Se você alterar sua toouse aplicativo uma porta diferente, você deve expor essa porta (ou rotear uma porta diferente) em Olá balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="30ca3-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="30ca3-106">Quando você implantou seu tooAzure de cluster de malha do serviço, um balanceador de carga foi criado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="30ca3-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="30ca3-107">Caso não tenha um balanceador de carga, confira [Configurar um balanceador de carga voltado para Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="30ca3-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="30ca3-108">Configurar o Service Fabric</span><span class="sxs-lookup"><span data-stu-id="30ca3-108">Configure service fabric</span></span>

<span data-ttu-id="30ca3-109">Seu aplicativo do Service Fabric **ServiceManifest.xml** arquivo de configuração define pontos de extremidade de saudação toouse espera que seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30ca3-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="30ca3-110">Depois que o arquivo de configuração Olá foi atualizada toodefine um ponto de extremidade, o balanceador de carga Olá deve ser atualizada tooexpose que (ou um diferente) porta.</span><span class="sxs-lookup"><span data-stu-id="30ca3-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="30ca3-111">Para obter mais informações sobre como toocreate Olá ponto de extremidade de malha de serviço, consulte [um ponto de extremidade de instalação](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="30ca3-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="30ca3-112">Criar uma regra de balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="30ca3-112">Create a load balancer rule</span></span>

<span data-ttu-id="30ca3-113">Uma regra de Balanceador de carga abre uma porta para a internet e encaminha a porta do nó interno toohello tráfego usada pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30ca3-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="30ca3-114">Caso não tenha um balanceador de carga, confira [Configurar um balanceador de carga voltado para Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="30ca3-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="30ca3-115">regra de toocreate um balanceador de carga, você precisa Olá toocollect informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="30ca3-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="30ca3-116">Nome do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="30ca3-116">Load balancer name.</span></span>
- <span data-ttu-id="30ca3-117">Grupo de recursos Olá balanceador de carga e cluster do service fabric.</span><span class="sxs-lookup"><span data-stu-id="30ca3-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="30ca3-118">Porta externa.</span><span class="sxs-lookup"><span data-stu-id="30ca3-118">External port.</span></span>
- <span data-ttu-id="30ca3-119">Porta interna.</span><span class="sxs-lookup"><span data-stu-id="30ca3-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="30ca3-120">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="30ca3-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="30ca3-121">Se você precisar de nome de saudação toodetermine saudação do balanceador de carga, use get de tooquickly esse comando uma lista de todos os balanceadores de carga e grupos de recursos de saudação associado.</span><span class="sxs-lookup"><span data-stu-id="30ca3-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="30ca3-122">Leva apenas um único comando toocreate uma regra de Balanceador de carga com hello **CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="30ca3-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="30ca3-123">Basta tooknow ambos os nome de saudação do hello carga balanceador e o recurso grupo toocreate uma nova regra.</span><span class="sxs-lookup"><span data-stu-id="30ca3-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="30ca3-124">Olá comando CLI do Azure tem alguns parâmetros que são descritos em Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="30ca3-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="30ca3-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="30ca3-125">Parameter</span></span> | <span data-ttu-id="30ca3-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="30ca3-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="30ca3-127">o aplicativo de malha do Hello porta Olá serviço está escutando.</span><span class="sxs-lookup"><span data-stu-id="30ca3-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="30ca3-128">saudação de porta Olá carregar balanceador expõe para conexões externas.</span><span class="sxs-lookup"><span data-stu-id="30ca3-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="30ca3-129">nome Hello de saudação toochange do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="30ca3-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="30ca3-130">grupo de recursos de saudação que tem o balanceador de carga hello e o cluster do service fabric.</span><span class="sxs-lookup"><span data-stu-id="30ca3-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="30ca3-131">Olá escolhida o nome da regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ca3-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="30ca3-132">Para obter mais informações sobre como toocreate um balanceador de carga com hello CLI do Azure, consulte [criar um balanceador de carga com hello CLI do Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="30ca3-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="30ca3-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="30ca3-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="30ca3-134">Se você precisar de nome de saudação toodetermine saudação do balanceador de carga, use get de tooquickly esse comando uma lista de todos os balanceadores de carga e grupos de recursos associado.</span><span class="sxs-lookup"><span data-stu-id="30ca3-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="30ca3-135">PowerShell é um pouco mais complicado do que Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="30ca3-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="30ca3-136">Conceitualmente, faça uma regra Olá toocreate as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="30ca3-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="30ca3-137">Obter o balanceador de carga de saudação do Azure.</span><span class="sxs-lookup"><span data-stu-id="30ca3-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="30ca3-138">Criar uma regra.</span><span class="sxs-lookup"><span data-stu-id="30ca3-138">Create a rule.</span></span>
3. <span data-ttu-id="30ca3-139">Adicione o balanceador de carga Olá regra toohello.</span><span class="sxs-lookup"><span data-stu-id="30ca3-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="30ca3-140">Atualize balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ca3-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="30ca3-141">Sobre Olá `New-AzureRmLoadBalancerRuleConfig` comando hello `-FrontendPort` balanceador de carga representa Olá porta Olá expõe para conexões externas e hello `-BackendPort` aplicativo de malha representa Olá porta saudação do serviço está escutando.</span><span class="sxs-lookup"><span data-stu-id="30ca3-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="30ca3-142">Para obter mais informações sobre como toocreate um balanceador de carga com o PowerShell, consulte [criar um balanceador de carga com o PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="30ca3-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

