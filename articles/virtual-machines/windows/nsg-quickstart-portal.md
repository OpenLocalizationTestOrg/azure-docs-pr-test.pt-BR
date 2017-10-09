---
title: "aaaOpen portas tooa VM usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Windows usando o modelo de implantação do Gerenciador de recursos de Olá Olá Portal do Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="1bf3e-103">Como tooopen portas tooa máquina virtual Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1bf3e-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="1bf3e-104">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="1bf3e-104">Quick commands</span></span>
<span data-ttu-id="1bf3e-105">Você também pode [executar essas etapas usando o Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1bf3e-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="1bf3e-106">Primeiro, crie o seu Grupo de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-106">First, create your Network Security Group.</span></span> <span data-ttu-id="1bf3e-107">Selecione um grupo de recursos no portal de saudação, escolha **adicionar**, em seguida, procure e selecione **grupo de segurança de rede**:</span><span class="sxs-lookup"><span data-stu-id="1bf3e-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Adicionar um Grupo de Segurança de Rede](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="1bf3e-109">Insira um nome para o seu Grupo de Segurança de Rede, selecione ou crie um grupo de recursos e selecione uma localização.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="1bf3e-110">Selecione **Criar** quando terminar:</span><span class="sxs-lookup"><span data-stu-id="1bf3e-110">Select **Create** when finished:</span></span>

![Criar um grupo de segurança de rede](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="1bf3e-112">Selecione o novo Grupo de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-112">Select your new Network Security Group.</span></span> <span data-ttu-id="1bf3e-113">Selecione as regras de segurança de entrada e selecione Olá **adicionar** botão toocreate uma regra:</span><span class="sxs-lookup"><span data-stu-id="1bf3e-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Adicionar uma regra de entrada](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="1bf3e-115">Escolha um comum **Service** do menu suspenso de hello, tais como *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="1bf3e-116">Você também pode selecionar *personalizado* tooprovide toouse uma porta específica.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="1bf3e-117">Se desejar, altere a prioridade de saudação ou nome.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="1bf3e-118">prioridade Hello afeta ordem Olá na qual as regras são aplicadas - Olá inferior Olá numérico valor, hello anteriores Olá regra é aplicada.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="1bf3e-119">Você também pode selecionar **avançado** na parte superior de saudação do tooenter tela uma determinada fonte de intervalo de porta ou bloco IP, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="1bf3e-120">Quando você estiver pronto, selecione **Okey** toocreate regra de saudação:</span><span class="sxs-lookup"><span data-stu-id="1bf3e-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Criar uma regra de entrada](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="1bf3e-122">A etapa final é tooassociate ao grupo de segurança da sua rede com uma sub-rede ou uma interface de rede específico.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="1bf3e-123">Vamos associar Olá grupo de segurança de rede com uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="1bf3e-124">Selecione **Sub-redes** e escolha **Associar**:</span><span class="sxs-lookup"><span data-stu-id="1bf3e-124">Select **Subnets**, then choose **Associate**:</span></span>

![Associar um Grupo de Segurança de Rede a uma sub-rede](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="1bf3e-126">Selecione a rede virtual e selecione sub-rede apropriada hello:</span><span class="sxs-lookup"><span data-stu-id="1bf3e-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Associar um Grupo de Segurança de Rede à rede virtual](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="1bf3e-128">Você criou um Grupo de Segurança de Rede, uma regra de entrada que permite o tráfego na porta 80 e o associou a uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="1bf3e-129">Todas as máquinas virtuais que você se conectar a sub-rede toothat estão acessíveis na porta 80.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="1bf3e-130">Mais informações sobre os Grupos de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="1bf3e-130">More information on Network Security Groups</span></span>
<span data-ttu-id="1bf3e-131">Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="1bf3e-132">Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="1bf3e-133">Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1bf3e-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="1bf3e-134">Para aplicativos Web altamente disponíveis, você deve colocar suas VMs atrás de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="1bf3e-135">Balanceador de carga Olá distribui tráfego tooVMs, com um grupo de segurança de rede que fornece filtragem.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="1bf3e-136">Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas no Azure toocreate um aplicativo altamente disponível](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="1bf3e-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bf3e-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1bf3e-137">Next steps</span></span>
<span data-ttu-id="1bf3e-138">Neste exemplo, você criou um tráfego HTTP de tooallow regra simples.</span><span class="sxs-lookup"><span data-stu-id="1bf3e-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="1bf3e-139">Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bf3e-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="1bf3e-140">Visão geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1bf3e-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="1bf3e-141">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="1bf3e-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)