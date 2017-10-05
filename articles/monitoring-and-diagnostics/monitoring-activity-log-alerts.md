---
title: Criar alertas do log de atividades | Microsoft Docs
description: Seja notificado por SMS, webhook e email quando ocorrerem determinados eventos no log de atividades.
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: 3885469ec0e1fcc31386dd0ad7fe6cb5d03ab28e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="301ac-103">Criar alertas do log de atividades</span><span class="sxs-lookup"><span data-stu-id="301ac-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="301ac-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="301ac-104">Overview</span></span>
<span data-ttu-id="301ac-105">Os alertas de log de atividades são alertas ativados quando ocorre um novo evento de log de atividades que corresponde às condições especificadas no alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches the conditions specified in the alert.</span></span> <span data-ttu-id="301ac-106">Eles são recursos do Azure e, portanto, podem ser criados usando um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="301ac-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="301ac-107">Eles também podem ser criados, atualizados ou excluídos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="301ac-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="301ac-108">Este artigo apresenta os conceitos por trás de alertas de log de atividades.</span><span class="sxs-lookup"><span data-stu-id="301ac-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="301ac-109">Ele então mostra como usar o portal do Azure para configurar um alerta em eventos do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="301ac-109">It then shows you how to use the Azure portal to set up an alert on activity log events.</span></span>

<span data-ttu-id="301ac-110">Normalmente, você cria alertas de log de atividade para receber notificações quando:</span><span class="sxs-lookup"><span data-stu-id="301ac-110">Typically, you create activity log alerts to receive notifications when:</span></span>

* <span data-ttu-id="301ac-111">As alterações específicas nos recursos de sua assinatura do Azure, normalmente com escopo para recursos ou grupos de recursos específicos.</span><span class="sxs-lookup"><span data-stu-id="301ac-111">Specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resources.</span></span> <span data-ttu-id="301ac-112">Por exemplo, convém ser notificado quando qualquer máquina virtual em myProductionResourceGroup for excluída.</span><span class="sxs-lookup"><span data-stu-id="301ac-112">For example, you might want to be notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="301ac-113">Ou você pode receber uma notificação se quaisquer funções novas forem atribuídas a um usuário em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="301ac-113">Or, you might want to be notified if any new roles are assigned to a user in your subscription.</span></span>
* <span data-ttu-id="301ac-114">Ocorre um evento de integridade do serviço.</span><span class="sxs-lookup"><span data-stu-id="301ac-114">A service health event occurs.</span></span> <span data-ttu-id="301ac-115">Os eventos de integridade de serviço incluem uma notificação de incidentes e eventos de manutenção que se aplicam aos recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="301ac-115">Service health events include notification of incidents and maintenance events that apply to resources in your subscription.</span></span>

<span data-ttu-id="301ac-116">Em ambos os casos, o alerta do log de atividades só monitorará eventos na assinatura na qual o alerta foi criado.</span><span class="sxs-lookup"><span data-stu-id="301ac-116">In either case, an activity log alert monitors only for events in the subscription in which the alert is created.</span></span>

<span data-ttu-id="301ac-117">Você pode configurar um alerta do log de atividades com base em qualquer propriedade de nível superior no objeto JSON de um evento do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="301ac-117">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="301ac-118">No entanto, o portal mostra as opções mais comuns:</span><span class="sxs-lookup"><span data-stu-id="301ac-118">However, the portal shows the most common options:</span></span>

- <span data-ttu-id="301ac-119">**Categoria**: Administrativa, Integridade do Serviço, Dimensionamento Automático e Recomendação.</span><span class="sxs-lookup"><span data-stu-id="301ac-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="301ac-120">Para saber mais, veja [Visão geral do log de atividades](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="301ac-120">For more information, see [Overview of the Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="301ac-121">Para saber mais sobre os eventos de integridade do serviço, veja [Receber alertas do log de atividades em notificações de serviço](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-121">To learn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="301ac-122">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="301ac-122">**Resource group**</span></span>
- <span data-ttu-id="301ac-123">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="301ac-123">**Resource**</span></span>
- <span data-ttu-id="301ac-124">**Tipo de recurso**</span><span class="sxs-lookup"><span data-stu-id="301ac-124">**Resource type**</span></span>
- <span data-ttu-id="301ac-125">**Nome da operação**: nome da operação de Controle de Acesso Baseado em Função do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="301ac-125">**Operation name**: The Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="301ac-126">**Nível**: o nível de gravidade do evento (Detalhado, Informativo, Aviso, Erro ou Crítico).</span><span class="sxs-lookup"><span data-stu-id="301ac-126">**Level**: The severity level of the event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="301ac-127">**Status**: o status do evento, normalmente Iniciado, Falha ou Êxito.</span><span class="sxs-lookup"><span data-stu-id="301ac-127">**Status**: The status of the event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="301ac-128">**Evento iniciado por**: também conhecido como o "chamador".</span><span class="sxs-lookup"><span data-stu-id="301ac-128">**Event initiated by**: Also known as the "caller."</span></span> <span data-ttu-id="301ac-129">O endereço de email ou o identificador do Azure Active Directory do usuário que realizou a operação.</span><span class="sxs-lookup"><span data-stu-id="301ac-129">The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

>[!NOTE]
><span data-ttu-id="301ac-130">Você deve especificar pelo menos dois dos critérios anteriores em seu alerta, sendo que um deve ser a categoria.</span><span class="sxs-lookup"><span data-stu-id="301ac-130">You must specify at least two of the preceding criteria in your alert, with one being the category.</span></span> <span data-ttu-id="301ac-131">Você não pode criar um alerta que seja ativado sempre que um evento for criado nos logs de atividades.</span><span class="sxs-lookup"><span data-stu-id="301ac-131">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>
>

<span data-ttu-id="301ac-132">Quando um alerta do log de atividades é ativado, ele usa um grupo de ações para gerar ações ou notificações.</span><span class="sxs-lookup"><span data-stu-id="301ac-132">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="301ac-133">Um grupo de ações é um conjunto reutilizável de destinatários de notificação, como endereços de email, URLs de webhook ou números de telefone de SMS.</span><span class="sxs-lookup"><span data-stu-id="301ac-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="301ac-134">Os destinatários podem ser referenciados de vários alertas para centralizar e agrupar seus canais de notificação.</span><span class="sxs-lookup"><span data-stu-id="301ac-134">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="301ac-135">Quando você define o alerta do log de atividades, tem duas opções.</span><span class="sxs-lookup"><span data-stu-id="301ac-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="301ac-136">Você pode:</span><span class="sxs-lookup"><span data-stu-id="301ac-136">You can:</span></span>

* <span data-ttu-id="301ac-137">Use um grupo existente no seu alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="301ac-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="301ac-138">Crie um novo grupo de ações.</span><span class="sxs-lookup"><span data-stu-id="301ac-138">Create a new action group.</span></span> 

<span data-ttu-id="301ac-139">Para saber mais sobre grupos de ações, veja [Criar e gerenciar grupos de ações no portal do Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-139">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="301ac-140">Para saber mais sobre as notificações de integridade do serviço, veja [Receber alertas do log de atividades sobre as notificações de integridade do serviço](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-140">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="301ac-141">Criar um alerta em um evento do log de atividades com um novo grupo de ações usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="301ac-141">Create an alert on an activity log event with a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="301ac-142">No [portal](https://portal.azure.com), selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="301ac-142">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![O serviço “Monitor”](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="301ac-144">Na seção **Log de atividades**, selecione **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="301ac-144">In the **Activity log** section, select **Alerts**.</span></span>

    ![A guia “Alertas”](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="301ac-146">Selecione **Adicionar alerta do log de atividades** e preencha os campos.</span><span class="sxs-lookup"><span data-stu-id="301ac-146">Select **Add activity log alert**, and fill in the fields.</span></span>

4. <span data-ttu-id="301ac-147">Insira um nome na caixa **Nome do log de atividades alerta** e selecione uma **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="301ac-147">Enter a name in the **Activity log alert name** box, and select a **Description**.</span></span>

    ![O comando "Adicionar alerta do log de atividades"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="301ac-149">A caixa **Assinatura** é automaticamente preenchida com a sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="301ac-149">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="301ac-150">Esta assinatura é aquela na qual o grupo de ação é salvo.</span><span class="sxs-lookup"><span data-stu-id="301ac-150">This subscription is the one in which the action group is saved.</span></span> <span data-ttu-id="301ac-151">O recurso de alerta é implantado nessa assinatura e monitora os eventos do log de atividades dela.</span><span class="sxs-lookup"><span data-stu-id="301ac-151">The alert resource is deployed to this subscription and monitors activity log events from it.</span></span>

    ![A caixa de diálogo "Adicionar alerta do log de atividades"](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="301ac-153">Selecione o **Grupo de recursos** no qual o recurso de alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="301ac-153">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="301ac-154">Esse não é o grupo de recursos monitorado pelo alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-154">This is not the resource group that's monitored by the alert.</span></span> <span data-ttu-id="301ac-155">Em vez disso, é o grupo de recursos onde se encontra o recurso de alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-155">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="301ac-156">Opcionalmente, selecione uma **Categoria de evento** para modificar os filtros adicionais que são mostrados.</span><span class="sxs-lookup"><span data-stu-id="301ac-156">Optionally, select an **Event category** to modify the additional filters that are shown.</span></span> <span data-ttu-id="301ac-157">Para eventos administrativos, os filtros incluem **Grupo de recursos**, **Recurso**, **Ripo de recurso**, **Nome da operação**, **Nível**, **Status** e **Evento iniciado por**.</span><span class="sxs-lookup"><span data-stu-id="301ac-157">For Administrative events, the filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="301ac-158">Esses valores identificam quais eventos este alerta deverá monitorar.</span><span class="sxs-lookup"><span data-stu-id="301ac-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="301ac-159">Você deve especificar pelo menos um dos critérios anteriores em seu alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-159">You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="301ac-160">Você não pode criar um alerta que seja ativado sempre que um evento for criado nos logs de atividades.</span><span class="sxs-lookup"><span data-stu-id="301ac-160">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
    >
    >

8. <span data-ttu-id="301ac-161">Insira um nome na caixa **Nome do grupo de ação** e, em seguida, digite um nome na caixa **Nome curto**.</span><span class="sxs-lookup"><span data-stu-id="301ac-161">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="301ac-162">O nome curto é usado no lugar de um nome de grupo de ação completo quando as notificações são enviadas usando esse grupo.</span><span class="sxs-lookup"><span data-stu-id="301ac-162">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="301ac-163">Defina uma lista de ações fornecendo os seguintes dados da ação:</span><span class="sxs-lookup"><span data-stu-id="301ac-163">Define a list of actions by providing the action’s:</span></span>

    <span data-ttu-id="301ac-164">a.</span><span class="sxs-lookup"><span data-stu-id="301ac-164">a.</span></span> <span data-ttu-id="301ac-165">**Nome**: insira o nome, o alias ou o identificador da ação.</span><span class="sxs-lookup"><span data-stu-id="301ac-165">**Name**: Enter the action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="301ac-166">b.</span><span class="sxs-lookup"><span data-stu-id="301ac-166">b.</span></span> <span data-ttu-id="301ac-167">**Tipo de Ação**: selecione SMS, email ou webhook.</span><span class="sxs-lookup"><span data-stu-id="301ac-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="301ac-168">c.</span><span class="sxs-lookup"><span data-stu-id="301ac-168">c.</span></span> <span data-ttu-id="301ac-169">**Detalhes**: de acordo com o tipo de ação escolhido, insira um número de telefone, um endereço de email ou um URI de webhook.</span><span class="sxs-lookup"><span data-stu-id="301ac-169">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="301ac-170">Selecione **OK** para criar o alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-170">Select **OK** to create the alert.</span></span>

<span data-ttu-id="301ac-171">O alerta leva alguns minutos para se propagar totalmente e então se tornar ativo.</span><span class="sxs-lookup"><span data-stu-id="301ac-171">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="301ac-172">Ele dispara quando novos eventos correspondem aos critérios do alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-172">It triggers when new events match the alert's criteria.</span></span>

<span data-ttu-id="301ac-173">Para saber mais, veja [Noções básicas sobre o esquema de webhook usado em alertas do log de atividades](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-173">For more information, see [Understand the webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="301ac-174">O grupo de ações definido nessas etapas é reutilizável, como um grupo de ação existente, para todas as definições de alerta futuras.</span><span class="sxs-lookup"><span data-stu-id="301ac-174">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="301ac-175">Criar um alerta em um evento do log de atividades para um grupo de ações existente usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="301ac-175">Create an alert on an activity log event for an existing action group by using the Azure portal</span></span>
1. <span data-ttu-id="301ac-176">Siga as etapas 1 a 7 na seção anterior para criar o alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="301ac-176">Follow steps 1 through 7 in the previous section to create your activity log alert.</span></span>

2. <span data-ttu-id="301ac-177">Em **Notificar via**, selecione o botão Grupo de ações **existente**.</span><span class="sxs-lookup"><span data-stu-id="301ac-177">Under **Notify via**, select the **Existing** action group button.</span></span> <span data-ttu-id="301ac-178">Selecione um grupo de ações existente na lista.</span><span class="sxs-lookup"><span data-stu-id="301ac-178">Select an existing action group from the list.</span></span>

3. <span data-ttu-id="301ac-179">Selecione **OK** para criar o alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-179">Select **OK** to create the alert.</span></span>

<span data-ttu-id="301ac-180">O alerta leva alguns minutos para se propagar totalmente e então se tornar ativo.</span><span class="sxs-lookup"><span data-stu-id="301ac-180">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="301ac-181">Ele dispara quando novos eventos correspondem aos critérios do alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-181">It triggers when new events match the alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="301ac-182">Gerenciar seus alertas</span><span class="sxs-lookup"><span data-stu-id="301ac-182">Manage your alerts</span></span>

<span data-ttu-id="301ac-183">Depois de criar um alerta, ele ficará visível na seção Alertas da folha Monitor.</span><span class="sxs-lookup"><span data-stu-id="301ac-183">After you create an alert, it's visible in the Alerts section of the Monitor blade.</span></span> <span data-ttu-id="301ac-184">Selecione o alerta que você deseja gerenciar:</span><span class="sxs-lookup"><span data-stu-id="301ac-184">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="301ac-185">Edite-o.</span><span class="sxs-lookup"><span data-stu-id="301ac-185">Edit it.</span></span>
* <span data-ttu-id="301ac-186">Exclua-o.</span><span class="sxs-lookup"><span data-stu-id="301ac-186">Delete it.</span></span>
* <span data-ttu-id="301ac-187">Desabilite-o ou habilite-o, se desejar interromper temporariamente ou continuar recebendo notificações do alerta.</span><span class="sxs-lookup"><span data-stu-id="301ac-187">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="301ac-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="301ac-188">Next steps</span></span>
- <span data-ttu-id="301ac-189">Obtenha uma [visão geral dos alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="301ac-190">Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="301ac-191">Examine o [esquema do webhook de alertas de log de atividades](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-191">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="301ac-192">Saiba mais sobre [grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="301ac-193">Saiba mais sobre as [notificações de integridade do serviço](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="301ac-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="301ac-194">Crie um [alerta de log de atividades para monitorar todas as operações de mecanismo de dimensionamento automático em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="301ac-194">Create an [activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="301ac-195">Crie um [alerta de log de atividades para monitorar todas as operações de escalar horizontalmente/reduzir horizontalmente com falha na sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="301ac-195">Create an [activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
