---
title: "aaaCreate uma instância do observador de rede do Azure | Microsoft Docs"
description: "Esta página fornece Olá etapas toocreate uma instância do observador de rede usando o portal de saudação e a API REST do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="dfa17-103">Criar uma instância do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="dfa17-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="dfa17-104">Observador de rede é um serviço regional que permite que você toomonitor e diagnosticar as condições em uma rede cenário nível, para e do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfa17-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="dfa17-105">Monitoramento do nível do cenário permite que você toodiagnose problemas em uma exibição de nível de rede de tooend final.</span><span class="sxs-lookup"><span data-stu-id="dfa17-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="dfa17-106">Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure.</span><span class="sxs-lookup"><span data-stu-id="dfa17-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="dfa17-107">Observador de rede atualmente suporta apenas CLI 1.0, Olá instruções toocreate uma nova instância do observador de rede é fornecida para CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="dfa17-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="dfa17-108">Criar um observador de rede no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="dfa17-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="dfa17-109">Navegue muito**mais serviços** > **rede** > **observador de rede**.</span><span class="sxs-lookup"><span data-stu-id="dfa17-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="dfa17-110">Você pode selecionar todas as assinaturas de saudação desejado tooenable observador de rede para.</span><span class="sxs-lookup"><span data-stu-id="dfa17-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="dfa17-111">Essa ação cria um Observador de Rede em todas as regiões que ele está disponível.</span><span class="sxs-lookup"><span data-stu-id="dfa17-111">This action creates a Network Watcher in every region that is available.</span></span>

![criar um observador de rede][1]

<span data-ttu-id="dfa17-113">Quando você habilita o observador de rede usando o Portal de saudação, Olá nome da instância do observador de rede Olá será automaticamente definido tooNetworkWatcher_region_name onde region_name corresponde toohello região do Azure em que a instância de saudação foi habilitada.</span><span class="sxs-lookup"><span data-stu-id="dfa17-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="dfa17-114">Por exemplo, um Observador de Rede habilitado na região Centro-Oeste dos EUA será nomeado NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="dfa17-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="dfa17-115">Além disso, instância do observador de rede Olá automaticamente será adicionada a um grupo de recursos denominado NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="dfa17-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="dfa17-116">Esse grupo de recursos será criado, se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="dfa17-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="dfa17-117">Se desejar que o nome da saudação toocustomize de uma instância do observador de rede e hello grupo de recursos que ele é colocado no, você pode usar o Powershell, Olá API REST ou ARMClient métodos descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="dfa17-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="dfa17-118">Cada opção, Olá grupo de recursos deve existir antes de você colocar Olá observador de rede para ele.</span><span class="sxs-lookup"><span data-stu-id="dfa17-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="dfa17-119">Criar um Observador de Rede com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfa17-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="dfa17-120">toocreate uma instância do observador de rede, execute Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfa17-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="dfa17-121">Criar um observador de rede com hello API REST</span><span class="sxs-lookup"><span data-stu-id="dfa17-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="dfa17-122">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dfa17-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="dfa17-123">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="dfa17-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="dfa17-124">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="dfa17-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="dfa17-125">Criar o observador de rede Olá</span><span class="sxs-lookup"><span data-stu-id="dfa17-125">Create hello network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="dfa17-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dfa17-126">Next steps</span></span>

<span data-ttu-id="dfa17-127">Agora que você tem uma instância do observador de rede, saiba mais sobre os recursos de saudação disponíveis:</span><span class="sxs-lookup"><span data-stu-id="dfa17-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="dfa17-128">Topologia</span><span class="sxs-lookup"><span data-stu-id="dfa17-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="dfa17-129">Captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="dfa17-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="dfa17-130">Verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="dfa17-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="dfa17-131">Próximo salto</span><span class="sxs-lookup"><span data-stu-id="dfa17-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="dfa17-132">Exibição de grupo de segurança</span><span class="sxs-lookup"><span data-stu-id="dfa17-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="dfa17-133">Registro do fluxo NSG</span><span class="sxs-lookup"><span data-stu-id="dfa17-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="dfa17-134">Solução de problemas do Gateway de Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="dfa17-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="dfa17-135">Quando uma instância do observador de rede tiver sido criada, captura de pacote pode ser configurada pelo seguinte artigo Olá: [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="dfa17-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











