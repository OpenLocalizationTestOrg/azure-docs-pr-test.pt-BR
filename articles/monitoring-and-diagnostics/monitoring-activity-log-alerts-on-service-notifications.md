---
title: "Receber alertas do log de atividades em notificações de serviço | Microsoft Docs"
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
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="32a10-103">Criar alertas do log de atividades em notificações de serviço</span><span class="sxs-lookup"><span data-stu-id="32a10-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="32a10-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="32a10-104">Overview</span></span>
<span data-ttu-id="32a10-105">Este artigo mostra como configurar alertas do log de atividades para notificações de integridade do serviço usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32a10-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="32a10-106">Você pode receber um alerta quando o Azure envia notificações de integridade do serviço para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="32a10-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="32a10-107">Você pode configurar o alerta de acordo com:</span><span class="sxs-lookup"><span data-stu-id="32a10-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="32a10-108">A classe de notificação de integridade do serviço (incidente, manutenção, informações etc.).</span><span class="sxs-lookup"><span data-stu-id="32a10-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="32a10-109">Os serviços afetados.</span><span class="sxs-lookup"><span data-stu-id="32a10-109">The service(s) affected.</span></span>
- <span data-ttu-id="32a10-110">As regiões afetadas.</span><span class="sxs-lookup"><span data-stu-id="32a10-110">The region(s) affected.</span></span>
- <span data-ttu-id="32a10-111">O status da notificação (ativo versus resolvido).</span><span class="sxs-lookup"><span data-stu-id="32a10-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="32a10-112">O nível das notificações (informativo, aviso ou erro).</span><span class="sxs-lookup"><span data-stu-id="32a10-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="32a10-113">Também é possível configurar para quem o alerta deve ser enviado:</span><span class="sxs-lookup"><span data-stu-id="32a10-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="32a10-114">Selecione um grupo de ações existente.</span><span class="sxs-lookup"><span data-stu-id="32a10-114">Select an existing action group.</span></span>
- <span data-ttu-id="32a10-115">Crie um novo grupo de ações (que pode ser usado posteriormente para futuros alertas).</span><span class="sxs-lookup"><span data-stu-id="32a10-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="32a10-116">Para saber mais sobre grupos de ações, veja [Criar e gerenciar grupos de ações](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="32a10-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="32a10-117">Para saber mais sobre como configurar alertas de notificação de integridade do serviço usando modelos do Azure Resource Manager, consulte [modelos do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="32a10-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="32a10-118">Criar um alerta em uma notificação de integridade do serviço para um novo grupo de ação usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32a10-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="32a10-119">No [portal](https://portal.azure.com), selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="32a10-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![O serviço “Monitor”](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="32a10-121">Na seção **Log de atividades**, selecione **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="32a10-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![A guia “Alertas”](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="32a10-123">Selecione **Adicionar alerta do log de atividades** e preencha os campos.</span><span class="sxs-lookup"><span data-stu-id="32a10-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![O comando "Adicionar alerta do log de atividades"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="32a10-125">Insira um nome na caixa **Nome do log de atividades alerta** e forneça uma **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="32a10-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![A caixa de diálogo "Adicionar alerta do log de atividades"](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="32a10-127">A caixa **Assinatura** é automaticamente preenchida com a sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="32a10-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="32a10-128">Esta assinatura é usada para salvar o alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="32a10-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="32a10-129">O recurso de alerta é implantado para essa assinatura e monitora os eventos no log de atividades para ele.</span><span class="sxs-lookup"><span data-stu-id="32a10-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="32a10-130">Selecione o **Grupo de recursos** no qual o recurso de alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="32a10-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="32a10-131">Este não é o grupo de recursos monitorado pelo alerta.</span><span class="sxs-lookup"><span data-stu-id="32a10-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="32a10-132">Em vez disso, é o grupo de recursos onde se encontra o recurso de alerta.</span><span class="sxs-lookup"><span data-stu-id="32a10-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="32a10-133">Na caixa **Categoria de evento**, selecione **Integridade do Serviço**.</span><span class="sxs-lookup"><span data-stu-id="32a10-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="32a10-134">Opcionalmente, selecione as notificações **Serviço**, **Região**, **Tipo**, **Status** e **Nível** de integridade do serviço que você deseja receber.</span><span class="sxs-lookup"><span data-stu-id="32a10-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="32a10-135">Em **Alerta via**, selecione o botão **Novo** grupo de ações.</span><span class="sxs-lookup"><span data-stu-id="32a10-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="32a10-136">Insira um nome na caixa **Nome do grupo de ação** e, em seguida, digite um nome na caixa **Nome curto**.</span><span class="sxs-lookup"><span data-stu-id="32a10-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="32a10-137">O nome curto é referenciado nas notificações enviadas quando esse alerta é acionado.</span><span class="sxs-lookup"><span data-stu-id="32a10-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="32a10-138">Defina uma lista de destinatários fornecendo os seguintes itens do destinatário:</span><span class="sxs-lookup"><span data-stu-id="32a10-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="32a10-139">a.</span><span class="sxs-lookup"><span data-stu-id="32a10-139">a.</span></span> <span data-ttu-id="32a10-140">**Nome**: nome, alias ou identificador do destinatário.</span><span class="sxs-lookup"><span data-stu-id="32a10-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="32a10-141">b.</span><span class="sxs-lookup"><span data-stu-id="32a10-141">b.</span></span> <span data-ttu-id="32a10-142">**Tipo de Ação**: selecione SMS, email ou webhook.</span><span class="sxs-lookup"><span data-stu-id="32a10-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="32a10-143">c.</span><span class="sxs-lookup"><span data-stu-id="32a10-143">c.</span></span> <span data-ttu-id="32a10-144">**Detalhes**: de acordo com o tipo de ação escolhido, insira um número de telefone, endereço de email ou URI de webhook.</span><span class="sxs-lookup"><span data-stu-id="32a10-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="32a10-145">Selecione **OK** para criar o alerta.</span><span class="sxs-lookup"><span data-stu-id="32a10-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="32a10-146">Em alguns minutos, o alerta estará ativo e começará a disparar com base nas condições especificadas durante a criação.</span><span class="sxs-lookup"><span data-stu-id="32a10-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="32a10-147">Para saber mais sobre o esquema do webhook para alertas de log de atividades, veja [Webhooks para alertas do log de atividades do Azure](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="32a10-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="32a10-148">O grupo de ações definido nessas etapas é reutilizável, como um grupo de ação existente, para todas as definições de alerta futuras.</span><span class="sxs-lookup"><span data-stu-id="32a10-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="32a10-149">Criar um alerta em uma notificação de integridade do serviço para um grupo de ação existente usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32a10-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="32a10-150">Siga as etapas 1 a 7 na seção anterior para criar a notificação de integridade do serviço.</span><span class="sxs-lookup"><span data-stu-id="32a10-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="32a10-151">Em **Alerta via**, selecione o botão Grupo de ações **existente**.</span><span class="sxs-lookup"><span data-stu-id="32a10-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="32a10-152">Selecione o grupo de ação apropriado.</span><span class="sxs-lookup"><span data-stu-id="32a10-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="32a10-153">Selecione **OK** para criar o alerta.</span><span class="sxs-lookup"><span data-stu-id="32a10-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="32a10-154">Em alguns minutos, o alerta estará ativo e começará a disparar com base nas condições especificadas durante a criação.</span><span class="sxs-lookup"><span data-stu-id="32a10-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="32a10-155">Gerenciar seus alertas</span><span class="sxs-lookup"><span data-stu-id="32a10-155">Manage your alerts</span></span>

<span data-ttu-id="32a10-156">Depois de criar um alerta, ele ficará visível na seção **Alertas** da folha **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="32a10-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="32a10-157">Selecione o alerta que você deseja gerenciar:</span><span class="sxs-lookup"><span data-stu-id="32a10-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="32a10-158">Edite-o.</span><span class="sxs-lookup"><span data-stu-id="32a10-158">Edit it.</span></span>
* <span data-ttu-id="32a10-159">Exclua-o.</span><span class="sxs-lookup"><span data-stu-id="32a10-159">Delete it.</span></span>
* <span data-ttu-id="32a10-160">Desabilite-o ou habilite-o, se desejar interromper temporariamente ou continuar recebendo notificações do alerta.</span><span class="sxs-lookup"><span data-stu-id="32a10-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32a10-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32a10-161">Next steps</span></span>
- <span data-ttu-id="32a10-162">Saiba mais sobre as [notificações de integridade do serviço](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="32a10-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="32a10-163">Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="32a10-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="32a10-164">Examine o [esquema do webhook de alertas de log de atividades](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="32a10-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="32a10-165">Obtenha uma [visão geral dos alertas do log de atividades](monitoring-overview-alerts.md) e saiba como receber alertas.</span><span class="sxs-lookup"><span data-stu-id="32a10-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="32a10-166">Saiba mais sobre [grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="32a10-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
