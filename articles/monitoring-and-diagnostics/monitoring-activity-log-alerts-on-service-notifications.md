---
title: "alertas de log de atividade aaaReceive em notificações de serviço | Microsoft Docs"
description: "Seja notificado por SMS, email ou webhook quando um serviço do Azure for executado."
author: johnkemnetz
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="13ffb-103">Criar alertas do log de atividades em notificações de serviço</span><span class="sxs-lookup"><span data-stu-id="13ffb-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="13ffb-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="13ffb-104">Overview</span></span>
<span data-ttu-id="13ffb-105">Este artigo mostra como tooset o log de atividades de alertas para notificações de integridade do serviço usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="13ffb-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="13ffb-106">Você pode receber um alerta quando o Azure envia tooyour de notificações de integridade do serviço assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="13ffb-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="13ffb-107">Você pode configurar um alerta de saudação com base em:</span><span class="sxs-lookup"><span data-stu-id="13ffb-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="13ffb-108">classe de saudação do serviço de notificação de integridade (incidente, manutenção, informações, etc.).</span><span class="sxs-lookup"><span data-stu-id="13ffb-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="13ffb-109">Olá serviço (s) afetado.</span><span class="sxs-lookup"><span data-stu-id="13ffb-109">hello service(s) affected.</span></span>
- <span data-ttu-id="13ffb-110">regiões de saudação afetados.</span><span class="sxs-lookup"><span data-stu-id="13ffb-110">hello region(s) affected.</span></span>
- <span data-ttu-id="13ffb-111">status de saudação de notificação de saudação (ativa versus resolvido).</span><span class="sxs-lookup"><span data-stu-id="13ffb-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="13ffb-112">nível de saudação de notificações de saudação (informação, aviso, erro).</span><span class="sxs-lookup"><span data-stu-id="13ffb-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="13ffb-113">Você também pode configurar que Olá alerta deve ser enviado para:</span><span class="sxs-lookup"><span data-stu-id="13ffb-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="13ffb-114">Selecione um grupo de ações existente.</span><span class="sxs-lookup"><span data-stu-id="13ffb-114">Select an existing action group.</span></span>
- <span data-ttu-id="13ffb-115">Crie um novo grupo de ações (que pode ser usado posteriormente para futuros alertas).</span><span class="sxs-lookup"><span data-stu-id="13ffb-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="13ffb-116">toolearn mais sobre grupos de ação, consulte [criar e gerenciar grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="13ffb-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="13ffb-117">Para obter informações sobre como alertas de notificação do serviço de integridade tooconfigure usando modelos do Azure Resource Manager, consulte [modelos do Gerenciador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="13ffb-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="13ffb-118">Criar um alerta em uma notificação de integridade do serviço para um novo grupo de ação usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="13ffb-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="13ffb-119">Em Olá [portal](https://portal.azure.com), selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="13ffb-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![saudação de serviço do "Monitor"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="13ffb-121">Em Olá **log de atividades** seção, selecione **alertas**.</span><span class="sxs-lookup"><span data-stu-id="13ffb-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Guia de "Alertas" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="13ffb-123">Selecione **adicionar alerta do log de atividade**e preencha os campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![Olá comando "Adicionar alerta do log de atividade"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="13ffb-125">Insira um nome no hello **nome do log de atividade alerta** caixa e forneça um **descrição**.</span><span class="sxs-lookup"><span data-stu-id="13ffb-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![caixa de diálogo "Adicionar alerta do log de atividade" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="13ffb-127">Olá **assinatura** caixa autofills com sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="13ffb-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="13ffb-128">Esta assinatura é alerta de log de atividade de saudação toosave usado.</span><span class="sxs-lookup"><span data-stu-id="13ffb-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="13ffb-129">recursos de alerta Olá está toothis implantado assinatura e monitora eventos no log de atividades de saudação para ele.</span><span class="sxs-lookup"><span data-stu-id="13ffb-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="13ffb-130">Selecione Olá **grupo de recursos** no qual Olá recursos de alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="13ffb-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="13ffb-131">Isso não é um grupo de recursos de saudação que é monitorado pelo alerta hello.</span><span class="sxs-lookup"><span data-stu-id="13ffb-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="13ffb-132">Em vez disso, é grupo de recursos de saudação onde o recurso de alerta de saudação está localizado.</span><span class="sxs-lookup"><span data-stu-id="13ffb-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="13ffb-133">Em Olá **categoria de evento** selecione **a integridade do serviço**.</span><span class="sxs-lookup"><span data-stu-id="13ffb-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="13ffb-134">Opcionalmente, selecione Olá **Service**, **região**, **tipo**, **Status**, e **nível** de serviço notificações de integridade que você deseja tooreceive.</span><span class="sxs-lookup"><span data-stu-id="13ffb-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="13ffb-135">Em **alerta via**, selecione Olá **novo** botão do grupo de ação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="13ffb-136">Insira um nome no hello **nome do grupo de ação** caixa e, em seguida, digite um nome em hello **nome curto** caixa.</span><span class="sxs-lookup"><span data-stu-id="13ffb-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="13ffb-137">nome curto de saudação é referenciado em notificações de saudação que são enviadas quando esse alerta será acionado.</span><span class="sxs-lookup"><span data-stu-id="13ffb-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="13ffb-138">Defina uma lista de destinatários, fornecendo o receptor de saudação:</span><span class="sxs-lookup"><span data-stu-id="13ffb-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="13ffb-139">a.</span><span class="sxs-lookup"><span data-stu-id="13ffb-139">a.</span></span> <span data-ttu-id="13ffb-140">**Nome**: insira o nome do destinatário hello, alias ou identificador.</span><span class="sxs-lookup"><span data-stu-id="13ffb-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="13ffb-141">b.</span><span class="sxs-lookup"><span data-stu-id="13ffb-141">b.</span></span> <span data-ttu-id="13ffb-142">**Tipo de Ação**: selecione SMS, email ou webhook.</span><span class="sxs-lookup"><span data-stu-id="13ffb-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="13ffb-143">c.</span><span class="sxs-lookup"><span data-stu-id="13ffb-143">c.</span></span> <span data-ttu-id="13ffb-144">**Detalhes**: com base no tipo de ação de saudação escolhido, digite um número de telefone, endereço de email ou webhook URI.</span><span class="sxs-lookup"><span data-stu-id="13ffb-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="13ffb-145">Selecione **Okey** toocreate alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="13ffb-146">Em poucos minutos, o alerta de hello está ativa e começa tootrigger com base nas condições de saudação especificado durante a criação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="13ffb-147">Para obter informações sobre o esquema de webhook Olá para alertas de log de atividade, consulte [Webhooks para atividades do Azure log alertas](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="13ffb-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="13ffb-148">o grupo de ação Olá definido nessas etapas é reutilizável de um grupo existente de ação para todas as definições de alerta futuras.</span><span class="sxs-lookup"><span data-stu-id="13ffb-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="13ffb-149">Criar um alerta em uma notificação de integridade do serviço para um grupo existente, usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="13ffb-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="13ffb-150">Siga as etapas 1 a 7 em Olá anterior seção toocreate a notificação de integridade do serviço.</span><span class="sxs-lookup"><span data-stu-id="13ffb-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="13ffb-151">Em **alerta via**, selecione Olá **existente** botão do grupo de ação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="13ffb-152">Selecione o grupo de ação apropriado Olá.</span><span class="sxs-lookup"><span data-stu-id="13ffb-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="13ffb-153">Selecione **Okey** toocreate alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="13ffb-154">Em poucos minutos, o alerta de hello está ativa e começa tootrigger com base nas condições de saudação especificado durante a criação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="13ffb-155">Gerenciar seus alertas</span><span class="sxs-lookup"><span data-stu-id="13ffb-155">Manage your alerts</span></span>

<span data-ttu-id="13ffb-156">Depois de criar um alerta, ela é visível no hello **alertas** seção Olá **Monitor** folha.</span><span class="sxs-lookup"><span data-stu-id="13ffb-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="13ffb-157">Selecione o alerta de saudação desejado toomanage para:</span><span class="sxs-lookup"><span data-stu-id="13ffb-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="13ffb-158">Edite-o.</span><span class="sxs-lookup"><span data-stu-id="13ffb-158">Edit it.</span></span>
* <span data-ttu-id="13ffb-159">Exclua-o.</span><span class="sxs-lookup"><span data-stu-id="13ffb-159">Delete it.</span></span>
* <span data-ttu-id="13ffb-160">Desabilitar ou habilitá-lo, se você desejar tootemporarily parar ou continuar a receber notificações de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="13ffb-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13ffb-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13ffb-161">Next steps</span></span>
- <span data-ttu-id="13ffb-162">Saiba mais sobre as [notificações de integridade do serviço](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="13ffb-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="13ffb-163">Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="13ffb-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="13ffb-164">Saudação de revisão [webhook alerta esquema do log de atividade](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="13ffb-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="13ffb-165">Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md)e saiba como tooreceive alertas.</span><span class="sxs-lookup"><span data-stu-id="13ffb-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="13ffb-166">Saiba mais sobre [grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="13ffb-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
