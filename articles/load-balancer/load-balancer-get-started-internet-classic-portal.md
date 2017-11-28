---
title: "Criar um balanceador de carga voltado para a Internet - Portal clássico do Azure | Microsoft Docs"
description: "Saiba como criar um balanceador de carga para a Internet no modelo de implantação clássico usando o portal clássico do Azure"
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
ms.openlocfilehash: a022154f5eca6de2d2dbfc1b9aa30d2ea0a7d650
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-classic-portal"></a><span data-ttu-id="13d0d-103">Introdução à criação de um balanceador de carga para a Internet (clássico) no portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="13d0d-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="13d0d-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="13d0d-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="13d0d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13d0d-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="13d0d-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="13d0d-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="13d0d-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="13d0d-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="13d0d-108">Antes de trabalhar com os recursos do Azure, é importante entender que, no momento, o Azure apresenta dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="13d0d-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="13d0d-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d0d-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="13d0d-110">Você pode exibir a documentação para ferramentas diferentes clicando nas guias na parte superior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="13d0d-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="13d0d-111">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="13d0d-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="13d0d-112">Também é possível [Saber como criar um balanceador de carga para a Internet usando o Gerenciador de Recursos do Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="13d0d-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="13d0d-113">Configurar um balanceador de carga da Internet para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="13d0d-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="13d0d-114">Para balancear carga de tráfego de rede da Internet entre máquinas virtuais de um serviço de nuvem, você deve criar um conjunto de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="13d0d-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="13d0d-115">Esse procedimento pressupõe que você já tenha criado as máquinas virtuais e que elas estejam todas no mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="13d0d-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span></span>

<span data-ttu-id="13d0d-116">**Para configurar um conjunto com balanceamento de carga de máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="13d0d-116">**To configure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="13d0d-117">No portal clássico do Azure, clique em **Máquinas Virtuais**e, em seguida, clique no nome de uma máquina virtual no conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="13d0d-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span></span>
2. <span data-ttu-id="13d0d-118">Clique em **Pontos de Extremidade** e depois em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="13d0d-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="13d0d-119">Na página **Adicionar um ponto de extremidade a uma máquina virtual** , clique na seta para a direita.</span><span class="sxs-lookup"><span data-stu-id="13d0d-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span></span>
4. <span data-ttu-id="13d0d-120">Na página **Especificar os detalhes do ponto de extremidade** :</span><span class="sxs-lookup"><span data-stu-id="13d0d-120">On the **Specify the details of the endpoint** page:</span></span>

   * <span data-ttu-id="13d0d-121">Em **Nome**, digite um nome para o ponto de extremidade ou selecione o nome da lista de pontos de extremidade predefinidos para protocolos comuns.</span><span class="sxs-lookup"><span data-stu-id="13d0d-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="13d0d-122">Em **Protocolo**, selecione o protocolo necessário para o tipo de ponto de extremidade, TCP ou UDP, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="13d0d-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="13d0d-123">Em **Porta pública e Porta privada**, digite os números de porta que você deseja que a máquina virtual use, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="13d0d-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span></span> <span data-ttu-id="13d0d-124">Você pode usar as regras de firewall e porta privada na máquina virtual para redirecionar o tráfego de uma maneira que seja apropriado ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="13d0d-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="13d0d-125">A porta privada pode ser a mesma que a porta pública.</span><span class="sxs-lookup"><span data-stu-id="13d0d-125">The private port can be the same as the public port.</span></span> <span data-ttu-id="13d0d-126">Por exemplo, para um ponto de extremidade para o tráfego da web (HTTP), você pode atribuir a porta 80 à porta pública e privada.</span><span class="sxs-lookup"><span data-stu-id="13d0d-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span></span>

5. <span data-ttu-id="13d0d-127">Selecione **Criar um conjunto de balanceamento de carga**e depois clique na seta para a direita.</span><span class="sxs-lookup"><span data-stu-id="13d0d-127">Select **Create a load-balanced set**, and then click the right arrow.</span></span>
6. <span data-ttu-id="13d0d-128">Na página **Configurar o conjunto de balanceamento de carga** , digite um nome para o conjunto e atribua os valores do comportamento de investigação do Balanceador de Carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d0d-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span></span> <span data-ttu-id="13d0d-129">O Balanceador de Carga usa testes para determinar se as máquinas virtuais do conjunto de balanceamento de carga estão disponíveis para receber o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="13d0d-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span></span>
7. <span data-ttu-id="13d0d-130">Clique na marca de seleção para criar o ponto de extremidade de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="13d0d-130">Click the check mark to create the load-balanced endpoint.</span></span> <span data-ttu-id="13d0d-131">Você verá **Sim** na coluna **Nome do conjunto de balanceamento de carga** da página **Pontos de extremidade** da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="13d0d-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span></span>
8. <span data-ttu-id="13d0d-132">No portal, clique em **Máquinas Virtuais**, clique no nome de uma máquina virtual adicional no conjunto de balanceamento de carga, clique em **Pontos de Extremidade** e em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="13d0d-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="13d0d-133">Na página **Adicionar ponto de extremidade a uma máquina virtual**, clique em **Adicionar ponto de extremidade a um conjunto existente de balanceamento de carga**, selecione o nome do conjunto de balanceamento de carga e, em seguida, clique na seta para a direita.</span><span class="sxs-lookup"><span data-stu-id="13d0d-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span></span>
10. <span data-ttu-id="13d0d-134">Na página **Especificar os detalhes do ponto de extremidade** , digite um nome para o ponto de extremidade e, em seguida, clique na marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="13d0d-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span></span>

<span data-ttu-id="13d0d-135">Para as outras máquinas virtuais no conjunto de balanceamento de carga, repita as etapas de 8 a 10.</span><span class="sxs-lookup"><span data-stu-id="13d0d-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13d0d-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13d0d-136">Next steps</span></span>

[<span data-ttu-id="13d0d-137">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="13d0d-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="13d0d-138">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="13d0d-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="13d0d-139">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="13d0d-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
