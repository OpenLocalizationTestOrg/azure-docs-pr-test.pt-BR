---
title: "Balanceador de carga aaaCreate um voltados para Internet - clássico do portal do Azure | Microsoft Docs"
description: "Saiba como toocreate um balanceador de carga voltado para Internet no modelo de implantação clássico usando Olá portal clássico do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="45afa-103">Introdução à criação de uma balanceador de carga (clássico) no portal clássico do Azure de saudação da Internet</span><span class="sxs-lookup"><span data-stu-id="45afa-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="45afa-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="45afa-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="45afa-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45afa-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="45afa-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="45afa-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="45afa-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="45afa-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="45afa-108">Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico.</span><span class="sxs-lookup"><span data-stu-id="45afa-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="45afa-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="45afa-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="45afa-110">Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo.</span><span class="sxs-lookup"><span data-stu-id="45afa-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="45afa-111">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="45afa-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="45afa-112">Você também pode [aprender a usar o Gerenciador de recursos do Azure de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="45afa-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="45afa-113">Configurar um balanceador de carga da Internet para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="45afa-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="45afa-114">No tráfego de rede ordem tooload saldo de saudação da Internet em máquinas virtuais de saudação de um serviço de nuvem, você deve criar um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="45afa-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="45afa-115">Esse procedimento pressupõe que você já criou máquinas virtuais de saudação e que são todos em Olá mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="45afa-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="45afa-116">**tooconfigure um conjunto com balanceamento de carga para máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="45afa-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="45afa-117">No portal clássico do Azure do hello, clique em **máquinas virtuais**e clique em nome de saudação de uma máquina virtual no conjunto de balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="45afa-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="45afa-118">Clique em **Pontos de Extremidade** e depois em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="45afa-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="45afa-119">Em Olá **adicionar uma máquina de virtual do ponto de extremidade tooa** página, clique na seta direita hello.</span><span class="sxs-lookup"><span data-stu-id="45afa-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="45afa-120">Em Olá **especificar detalhes de saudação do ponto de extremidade de saudação** página:</span><span class="sxs-lookup"><span data-stu-id="45afa-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="45afa-121">Em **nome**, digite um nome para o ponto de extremidade de saudação ou selecione o nome de saudação da lista de saudação de pontos de extremidade predefinidas para protocolos comuns.</span><span class="sxs-lookup"><span data-stu-id="45afa-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="45afa-122">Em **protocolo**, selecione o protocolo de saudação exigido pelo tipo de saudação do ponto de extremidade, TCP ou UDP, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="45afa-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="45afa-123">Em **porta pública e porta privada**, digite Olá números de porta que você deseja Olá toouse de máquina virtual, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="45afa-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="45afa-124">Você pode usar regras de firewall e porta privada Olá no tráfego de tooredirect Olá máquina virtual de forma que seja apropriado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45afa-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="45afa-125">porta privada Olá pode Olá igual a porta pública hello.</span><span class="sxs-lookup"><span data-stu-id="45afa-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="45afa-126">Por exemplo, um ponto de extremidade para o tráfego da web (HTTP), você pode atribuir tooboth 80 Olá públicas e privadas porta.</span><span class="sxs-lookup"><span data-stu-id="45afa-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="45afa-127">Selecione **criar um conjunto com balanceamento de carga**e, em seguida, clique na seta direita hello.</span><span class="sxs-lookup"><span data-stu-id="45afa-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="45afa-128">Em Olá **configurar conjunto de balanceamento de carga de saudação** página, digite um nome para o conjunto de balanceamento de carga hello e, em seguida, atribuir valores de saudação comportamento de sonda de saudação balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="45afa-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="45afa-129">Olá balanceador de carga usa testes toodetermine se máquinas virtuais de saudação em conjunto com balanceamento de carga de saudação tooreceive disponível o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="45afa-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="45afa-130">Clique em Olá marca de seleção toocreate Olá com balanceamento de carga de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="45afa-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="45afa-131">Você verá **Sim** em Olá **o nome do conjunto com balanceamento de carga** coluna da saudação **pontos de extremidade** página para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="45afa-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="45afa-132">No portal de saudação, clique em **máquinas virtuais**, clique em nome de saudação de uma máquina virtual adicional no conjunto de balanceamento de carga de saudação **pontos de extremidade**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="45afa-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="45afa-133">Em Olá **adicionar uma máquina de virtual do ponto de extremidade tooa** , clique em **Adicionar ponto de extremidade tooan existente com balanceamento de carga conjunto**, selecione o nome de saudação do conjunto de balanceamento de carga de hello e, em seguida, clique na seta direita hello.</span><span class="sxs-lookup"><span data-stu-id="45afa-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="45afa-134">Em Olá **especificar detalhes de saudação do ponto de extremidade de saudação** página, digite um nome para o ponto de extremidade de saudação e, em seguida, clique em marca de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="45afa-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="45afa-135">Para Olá máquinas virtuais em conjunto com balanceamento de carga do hello, repita as etapas 8 a 10.</span><span class="sxs-lookup"><span data-stu-id="45afa-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45afa-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45afa-136">Next steps</span></span>

[<span data-ttu-id="45afa-137">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="45afa-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="45afa-138">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="45afa-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="45afa-139">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="45afa-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
