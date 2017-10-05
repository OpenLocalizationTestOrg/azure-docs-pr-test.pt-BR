---
title: "Criar um balanceador de carga voltado para a Internet - Azure PowerShell clássico | Microsoft Docs"
description: "Saiba como criar um balanceador de carga para a Internet no modo clássico usando o PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1a41f3ba199fb692c111ea6a40ddb09605f91da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="5e0a7-103">Introdução à criação de um balanceador de carga para a Internet (clássico) no PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e0a7-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e0a7-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="5e0a7-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="5e0a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e0a7-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="5e0a7-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5e0a7-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="5e0a7-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="5e0a7-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="5e0a7-108">Antes de trabalhar com os recursos do Azure, é importante entender que, no momento, o Azure apresenta dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="5e0a7-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="5e0a7-110">Você pode exibir a documentação para ferramentas diferentes clicando nas guias na parte superior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="5e0a7-111">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="5e0a7-112">Também é possível [Saber como criar um balanceador de carga para a Internet usando o Gerenciador de Recursos do Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5e0a7-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="5e0a7-113">Configurar o balanceador de carga usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e0a7-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="5e0a7-114">Para configurar um balanceador de carga usando o powershell, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="5e0a7-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="5e0a7-115">Se você nunca usou o Azure PowerShell, consulte [Como Instalar e Configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções até o fim para entrar no Azure e selecionar sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="5e0a7-116">Depois de criar uma máquina virtual, você pode usar os cmdlets do PowerShell para adicionar um balanceador de carga a uma máquina virtual no mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="5e0a7-117">No exemplo a seguir, você adicionará um conjunto de balanceadores de carga chamado "webfarm" ao serviço de nuvem "mytestcloud" (ou myctestcloud.cloudapp.net), adicionando os pontos de extremidade para o balanceador de carga às máquinas virtuais chamadas "web1" e "web2".</span><span class="sxs-lookup"><span data-stu-id="5e0a7-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="5e0a7-118">O balanceador de carga recebe tráfego de rede na porta 80 e faz o balanceamento de carga entre as máquinas virtuais definidas pelo ponto de extremidade local (nesse caso, na porta 80) usando TCP.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="5e0a7-119">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="5e0a7-119">Step 1</span></span>

<span data-ttu-id="5e0a7-120">Criar um ponto de extremidade com balanceamento de carga para a primeira VM "web1"</span><span class="sxs-lookup"><span data-stu-id="5e0a7-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="5e0a7-121">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="5e0a7-121">Step 2</span></span>

<span data-ttu-id="5e0a7-122">Criar outro ponto de extremidade para a segunda VM "web2" usando o mesmo nome do conjunto de balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="5e0a7-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="5e0a7-123">Remover uma máquina virtual de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="5e0a7-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="5e0a7-124">Você pode usar Remove-AzureEndpoint para remover um ponto de extremidade de máquina virtual do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="5e0a7-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="5e0a7-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e0a7-125">Next steps</span></span>

<span data-ttu-id="5e0a7-126">Você também pode [começar a criar um balanceador de carga interno](load-balancer-get-started-ilb-classic-ps.md) e configurar o tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="5e0a7-127">Se seu aplicativo precisar manter conexões ativas para servidores por trás de um balanceador de carga, você poderá entender mais sobre as [configurações de tempo limite de TCP ocioso para um balanceador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="5e0a7-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="5e0a7-128">Assim, você saberá mais sobre o comportamento da conexão ociosa quando estiver usando um Balanceador de Carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e0a7-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
