---
title: "aaaCreate e gerenciar grupos de ação no hello portal do Azure | Microsoft Docs"
description: "Saiba como toocreate e gerenciar grupos de ação no hello portal do Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="e2f44-103">Criar e gerenciar grupos de ação no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2f44-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="e2f44-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e2f44-104">Overview</span></span> ##
<span data-ttu-id="e2f44-105">Este artigo mostra como toocreate e gerenciar grupos de ação no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f44-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="e2f44-106">Você pode configurar uma lista de ações com grupos de ações.</span><span class="sxs-lookup"><span data-stu-id="e2f44-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="e2f44-107">Então, esses grupos podem ser usados quando você define alertas de log de atividades.</span><span class="sxs-lookup"><span data-stu-id="e2f44-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="e2f44-108">Esses grupos podem ser reutilizados por cada alerta do log de atividade que definir, garantindo que Olá mesmo ações são executadas a cada hora hello atividade log alerta for disparado.</span><span class="sxs-lookup"><span data-stu-id="e2f44-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="e2f44-109">Um grupo pode ter até too10 de cada tipo de ação.</span><span class="sxs-lookup"><span data-stu-id="e2f44-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="e2f44-110">Cada ação é composta por Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2f44-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="e2f44-111">**Nome**: um identificador exclusivo dentro do grupo de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f44-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="e2f44-112">**Tipo de ação**: envie um SMS, envie um email ou chame um webhook.</span><span class="sxs-lookup"><span data-stu-id="e2f44-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="e2f44-113">**Detalhes**: Olá webhook URI, endereço de email ou número de telefone correspondente.</span><span class="sxs-lookup"><span data-stu-id="e2f44-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="e2f44-114">Para obter informações sobre como grupos de ação de tooconfigure toouse do Azure Resource Manager modelos, consulte [modelos do Gerenciador de recursos de grupo de ação](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e2f44-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="e2f44-115">Criar um grupo de ação usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2f44-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="e2f44-116">Em Olá [portal](https://portal.azure.com), selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="e2f44-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="e2f44-117">Olá **Monitor** folha consolida todas as suas configurações e dados em uma exibição de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="e2f44-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![saudação de serviço do "Monitor"](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="e2f44-119">Em Olá **log de atividades** seção, selecione **grupos de ação**.</span><span class="sxs-lookup"><span data-stu-id="e2f44-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![Guia de "Grupos de ação" Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="e2f44-121">Selecione **adicionar grupo de ação**e preencha os campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f44-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![Olá "Adicionar grupo de ação de" comando](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="e2f44-123">Insira um nome no hello **nome do grupo de ação** caixa e, em seguida, digite um nome em hello **nome curto** caixa.</span><span class="sxs-lookup"><span data-stu-id="e2f44-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="e2f44-124">nome curto de saudação é usado no lugar de um nome de grupo de ação completo quando as notificações são enviadas usando esse grupo.</span><span class="sxs-lookup"><span data-stu-id="e2f44-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![caixa de diálogo do grupo de ação de adicionar Hello"](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="e2f44-126">Olá **assinatura** caixa autofills com sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="e2f44-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="e2f44-127">Esta assinatura está Olá um no qual grupo de ação de saudação é salvo.</span><span class="sxs-lookup"><span data-stu-id="e2f44-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="e2f44-128">Selecione Olá **grupo de recursos** qual ação Olá grupo é salvo.</span><span class="sxs-lookup"><span data-stu-id="e2f44-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="e2f44-129">Defina uma lista de ações fornecendo estas ações:</span><span class="sxs-lookup"><span data-stu-id="e2f44-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="e2f44-130">a.</span><span class="sxs-lookup"><span data-stu-id="e2f44-130">a.</span></span> <span data-ttu-id="e2f44-131">**Nome**: insira um identificador exclusivo para esta ação.</span><span class="sxs-lookup"><span data-stu-id="e2f44-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="e2f44-132">b.</span><span class="sxs-lookup"><span data-stu-id="e2f44-132">b.</span></span> <span data-ttu-id="e2f44-133">**Tipo de Ação**: selecione SMS, email ou webhook.</span><span class="sxs-lookup"><span data-stu-id="e2f44-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="e2f44-134">c.</span><span class="sxs-lookup"><span data-stu-id="e2f44-134">c.</span></span> <span data-ttu-id="e2f44-135">**Detalhes**: com base no tipo de ação de hello, insira um número de telefone, endereço de email ou webhook URI.</span><span class="sxs-lookup"><span data-stu-id="e2f44-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="e2f44-136">Selecione **Okey** toocreate grupo de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f44-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="e2f44-137">Gerenciar seus grupos de ação</span><span class="sxs-lookup"><span data-stu-id="e2f44-137">Manage your action groups</span></span> ##
<span data-ttu-id="e2f44-138">Depois de criar um grupo, ela é visível no hello **grupos de ação** seção Olá **Monitor** folha.</span><span class="sxs-lookup"><span data-stu-id="e2f44-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="e2f44-139">Selecione o grupo de ações de saudação desejado toomanage para:</span><span class="sxs-lookup"><span data-stu-id="e2f44-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="e2f44-140">Adicionar, editar ou remover ações.</span><span class="sxs-lookup"><span data-stu-id="e2f44-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="e2f44-141">Exclua grupo de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f44-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2f44-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2f44-142">Next steps</span></span> ##
* <span data-ttu-id="e2f44-143">Saiba mais sobre o [comportamento de alertas por SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e2f44-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="e2f44-144">Obter um [entendimento do esquema de webhook alerta do log de atividade de saudação](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="e2f44-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="e2f44-145">Saiba mais sobre a [limitação de taxa](monitoring-alerts-rate-limiting.md) para alertas.</span><span class="sxs-lookup"><span data-stu-id="e2f44-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="e2f44-146">Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md)e saiba como tooreceive alertas.</span><span class="sxs-lookup"><span data-stu-id="e2f44-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="e2f44-147">Saiba como muito[configurar alertas sempre que uma notificação de integridade do serviço é postada](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="e2f44-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
