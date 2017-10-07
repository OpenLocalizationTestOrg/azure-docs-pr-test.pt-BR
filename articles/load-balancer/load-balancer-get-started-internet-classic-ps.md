---
title: "aaaCreate um voltados para Internet carregar balanceador - clássico do Azure PowerShell | Microsoft Docs"
description: "Saiba como toocreate voltado para a Internet um balanceador de carga no modo clássico, usando o PowerShell"
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
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="35d85-103">Introdução à criação de um balanceador de carga para a Internet (clássico) no PowerShell</span><span class="sxs-lookup"><span data-stu-id="35d85-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35d85-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="35d85-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="35d85-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35d85-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="35d85-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="35d85-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="35d85-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="35d85-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="35d85-108">Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico.</span><span class="sxs-lookup"><span data-stu-id="35d85-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="35d85-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="35d85-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="35d85-110">Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo.</span><span class="sxs-lookup"><span data-stu-id="35d85-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="35d85-111">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="35d85-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="35d85-112">Você também pode [aprender a usar o Gerenciador de recursos do Azure de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="35d85-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="35d85-113">Configurar o balanceador de carga usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="35d85-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="35d85-114">tooset backup de um balanceador de carga usando o powershell, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="35d85-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="35d85-115">Se você nunca usou o Azure PowerShell, consulte [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções Olá todos os toohello de maneira Olá terminar toosign no Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="35d85-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="35d85-116">Depois de criar uma máquina virtual, você pode usar os cmdlets de PowerShell tooadd uma máquina virtual de tooa de Balanceador de carga dentro Olá mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="35d85-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="35d85-117">Olá o exemplo a seguir você irá adicionar um conjunto de Balanceador de carga chamado "webfarm" toocloud máquinas "mytestcloud" (ou myctestcloud.cloudapp.net), a adição de pontos de extremidade Olá Olá toovirtual do balanceador de carga de serviço denominado "web1" e "web2".</span><span class="sxs-lookup"><span data-stu-id="35d85-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="35d85-118">Balanceador de carga Hello recebe tráfego de rede na porta 80 e o balanceamento de carga entre máquinas virtuais de saudação definidas pelo ponto de extremidade local (no caso, a porta 80) hello usando TCP.</span><span class="sxs-lookup"><span data-stu-id="35d85-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="35d85-119">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="35d85-119">Step 1</span></span>

<span data-ttu-id="35d85-120">Criar um ponto de extremidade com balanceamento de carga para web1"hello primeira VM"</span><span class="sxs-lookup"><span data-stu-id="35d85-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="35d85-121">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="35d85-121">Step 2</span></span>

<span data-ttu-id="35d85-122">Crie outro ponto de extremidade para hello segundo VM "web2" usando Olá mesmo carregar nome do balanceador de conjunto</span><span class="sxs-lookup"><span data-stu-id="35d85-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="35d85-123">Remover uma máquina virtual de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="35d85-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="35d85-124">Você pode usar o Remove-AzureEndpoint tooremove um ponto de extremidade de máquina virtual do balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="35d85-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="35d85-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35d85-125">Next steps</span></span>

<span data-ttu-id="35d85-126">Você também pode [começar a criar um balanceador de carga interno](load-balancer-get-started-ilb-classic-ps.md) e configurar o tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="35d85-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="35d85-127">Se seu aplicativo precisa tookeep conexões ativo para os servidores atrás de um balanceador de carga, você pode saber mais sobre [ocioso configurações de tempo limite TCP para um balanceador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="35d85-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="35d85-128">Ele ajudará toolearn sobre o comportamento de conexão ociosa, quando você estiver usando um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="35d85-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
