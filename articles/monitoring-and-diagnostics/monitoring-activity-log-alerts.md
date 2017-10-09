---
title: alertas de log de atividade de aaaCreate | Microsoft Docs
description: "Ser notificado por email, SMS e webhook quando ocorrem determinados eventos no log de atividades de saudação."
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
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="08d2b-103">Criar alertas do log de atividades</span><span class="sxs-lookup"><span data-stu-id="08d2b-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="08d2b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="08d2b-104">Overview</span></span>
<span data-ttu-id="08d2b-105">Alertas de log de atividade são alertas que ativar quando um novo evento de log de atividade que ocorre atender às condições de saudação especificadas no alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches hello conditions specified in hello alert.</span></span> <span data-ttu-id="08d2b-106">Eles são recursos do Azure e, portanto, podem ser criados usando um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08d2b-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="08d2b-107">Eles também podem ser criados, atualizados ou excluídos em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08d2b-107">They also can be created, updated, or deleted in hello Azure portal.</span></span> <span data-ttu-id="08d2b-108">Este artigo apresenta conceitos de saudação dos alertas de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="08d2b-108">This article introduces hello concepts behind activity log alerts.</span></span> <span data-ttu-id="08d2b-109">Em seguida, mostra como toouse Olá tooset portal do Azure a um alerta em eventos de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="08d2b-109">It then shows you how toouse hello Azure portal tooset up an alert on activity log events.</span></span>

<span data-ttu-id="08d2b-110">Normalmente, você cria os alertas de log de atividade tooreceive notificações quando:</span><span class="sxs-lookup"><span data-stu-id="08d2b-110">Typically, you create activity log alerts tooreceive notifications when:</span></span>

* <span data-ttu-id="08d2b-111">Alterações específicas ocorrem em recursos na sua assinatura do Azure, grupos de recursos tooparticular geralmente no escopo ou recursos.</span><span class="sxs-lookup"><span data-stu-id="08d2b-111">Specific changes occur on resources in your Azure subscription, often scoped tooparticular resource groups or resources.</span></span> <span data-ttu-id="08d2b-112">Por exemplo, convém toobe notificado quando qualquer máquina virtual em myProductionResourceGroup é excluída.</span><span class="sxs-lookup"><span data-stu-id="08d2b-112">For example, you might want toobe notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="08d2b-113">Ou, talvez você queira toobe notificado se quaisquer novas funções forem atribuídas tooa usuário em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="08d2b-113">Or, you might want toobe notified if any new roles are assigned tooa user in your subscription.</span></span>
* <span data-ttu-id="08d2b-114">Ocorre um evento de integridade do serviço.</span><span class="sxs-lookup"><span data-stu-id="08d2b-114">A service health event occurs.</span></span> <span data-ttu-id="08d2b-115">Eventos de integridade do serviço incluem uma notificação de incidentes e eventos de manutenção que se aplicam a tooresources em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="08d2b-115">Service health events include notification of incidents and maintenance events that apply tooresources in your subscription.</span></span>

<span data-ttu-id="08d2b-116">Em ambos os casos, um alerta do log de atividade monitora apenas eventos na assinatura Olá no qual Olá alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="08d2b-116">In either case, an activity log alert monitors only for events in hello subscription in which hello alert is created.</span></span>

<span data-ttu-id="08d2b-117">Você pode configurar um alerta de log de atividade com base em qualquer propriedade de nível superior no objeto JSON de saudação para um evento de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="08d2b-117">You can configure an activity log alert based on any top-level property in hello JSON object for an activity log event.</span></span> <span data-ttu-id="08d2b-118">No entanto, o portal de saudação mostra opções mais comuns de saudação:</span><span class="sxs-lookup"><span data-stu-id="08d2b-118">However, hello portal shows hello most common options:</span></span>

- <span data-ttu-id="08d2b-119">**Categoria**: Administrativa, Integridade do Serviço, Dimensionamento Automático e Recomendação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="08d2b-120">Para obter mais informações, consulte [visão geral do log de atividades do Azure Olá](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="08d2b-120">For more information, see [Overview of hello Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="08d2b-121">toolearn mais informações sobre eventos de integridade do serviço, consulte [receber alertas de log de atividade em notificações de serviço](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-121">toolearn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="08d2b-122">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="08d2b-122">**Resource group**</span></span>
- <span data-ttu-id="08d2b-123">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="08d2b-123">**Resource**</span></span>
- <span data-ttu-id="08d2b-124">**Tipo de recurso**</span><span class="sxs-lookup"><span data-stu-id="08d2b-124">**Resource type**</span></span>
- <span data-ttu-id="08d2b-125">**Nome da operação**: nome de operação de controle de acesso baseado em função do recurso Gerenciador hello.</span><span class="sxs-lookup"><span data-stu-id="08d2b-125">**Operation name**: hello Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="08d2b-126">**Nível de**: Olá nível de severidade do evento hello (detalhado, informativo, aviso, erro ou crítico).</span><span class="sxs-lookup"><span data-stu-id="08d2b-126">**Level**: hello severity level of hello event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="08d2b-127">**Status**: status de saudação do evento hello, normalmente iniciados, falhou ou foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="08d2b-127">**Status**: hello status of hello event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="08d2b-128">**Evento iniciado por**: Olá também conhecido como "chamador".</span><span class="sxs-lookup"><span data-stu-id="08d2b-128">**Event initiated by**: Also known as hello "caller."</span></span> <span data-ttu-id="08d2b-129">endereço de email de saudação ou identificador de Active Directory do Azure do usuário de saudação que realizou a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-129">hello email address or Azure Active Directory identifier of hello user who performed hello operation.</span></span>

>[!NOTE]
><span data-ttu-id="08d2b-130">Você deve especificar pelo menos duas das Olá precedem critérios em seu alerta, com uma categoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-130">You must specify at least two of hello preceding criteria in your alert, with one being hello category.</span></span> <span data-ttu-id="08d2b-131">Você não pode criar um alerta que é ativado sempre que um evento é criado nos logs de atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-131">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
>
>

<span data-ttu-id="08d2b-132">Quando um alerta de log de atividades é ativado, ele usa uma ação toogenerate ações ou notificações de grupo.</span><span class="sxs-lookup"><span data-stu-id="08d2b-132">When an activity log alert is activated, it uses an action group toogenerate actions or notifications.</span></span> <span data-ttu-id="08d2b-133">Um grupo de ações é um conjunto reutilizável de destinatários de notificação, como endereços de email, URLs de webhook ou números de telefone de SMS.</span><span class="sxs-lookup"><span data-stu-id="08d2b-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="08d2b-134">receptores de saudação podem ser referenciados de vários toocentralize de alertas e agrupe seus canais de notificação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-134">hello receivers can be referenced from multiple alerts toocentralize and group your notification channels.</span></span> <span data-ttu-id="08d2b-135">Quando você define o alerta do log de atividades, tem duas opções.</span><span class="sxs-lookup"><span data-stu-id="08d2b-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="08d2b-136">Você pode:</span><span class="sxs-lookup"><span data-stu-id="08d2b-136">You can:</span></span>

* <span data-ttu-id="08d2b-137">Use um grupo existente no seu alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="08d2b-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="08d2b-138">Crie um novo grupo de ações.</span><span class="sxs-lookup"><span data-stu-id="08d2b-138">Create a new action group.</span></span> 

<span data-ttu-id="08d2b-139">toolearn mais sobre grupos de ação, consulte [criar e gerenciar grupos de ação no portal do Azure de saudação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-139">toolearn more about action groups, see [Create and manage action groups in hello Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="08d2b-140">toolearn mais sobre as notificações de integridade do serviço, consulte [receber alertas de log de atividade sobre as notificações de integridade do serviço](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-140">toolearn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="08d2b-141">Criar um alerta em um evento de log de atividade com um novo grupo de ação usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="08d2b-141">Create an alert on an activity log event with a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="08d2b-142">Em Olá [portal](https://portal.azure.com), selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="08d2b-142">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![saudação de serviço do "Monitor"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="08d2b-144">Em Olá **log de atividades** seção, selecione **alertas**.</span><span class="sxs-lookup"><span data-stu-id="08d2b-144">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Guia de "Alertas" Hello](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="08d2b-146">Selecione **adicionar alerta do log de atividade**e preencha os campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-146">Select **Add activity log alert**, and fill in hello fields.</span></span>

4. <span data-ttu-id="08d2b-147">Insira um nome no hello **nome do log de atividade alerta** caixa e selecione um **descrição**.</span><span class="sxs-lookup"><span data-stu-id="08d2b-147">Enter a name in hello **Activity log alert name** box, and select a **Description**.</span></span>

    ![Olá comando "Adicionar alerta do log de atividade"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="08d2b-149">Olá **assinatura** caixa autofills com sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="08d2b-149">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="08d2b-150">Esta assinatura está Olá um no qual grupo de ação de saudação é salvo.</span><span class="sxs-lookup"><span data-stu-id="08d2b-150">This subscription is hello one in which hello action group is saved.</span></span> <span data-ttu-id="08d2b-151">recurso de alerta de saudação é implantado toothis assinatura e monitores log eventos de atividade dele.</span><span class="sxs-lookup"><span data-stu-id="08d2b-151">hello alert resource is deployed toothis subscription and monitors activity log events from it.</span></span>

    ![caixa de diálogo "Adicionar alerta do log de atividade" Hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="08d2b-153">Selecione Olá **grupo de recursos** no qual Olá recursos de alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="08d2b-153">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="08d2b-154">Isso não é um grupo de recursos de saudação que é monitorado pelo alerta hello.</span><span class="sxs-lookup"><span data-stu-id="08d2b-154">This is not hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="08d2b-155">Em vez disso, é grupo de recursos de saudação onde o recurso de alerta de saudação está localizado.</span><span class="sxs-lookup"><span data-stu-id="08d2b-155">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="08d2b-156">Opcionalmente, selecione uma **categoria de evento** toomodify Olá filtros adicionais que são mostrados.</span><span class="sxs-lookup"><span data-stu-id="08d2b-156">Optionally, select an **Event category** toomodify hello additional filters that are shown.</span></span> <span data-ttu-id="08d2b-157">Para eventos administrativos, filtros de saudação incluem **grupo de recursos**, **recurso**, **tipo de recurso**, **nome da operação**, **Nível**, **Status**, e **evento iniciado por**.</span><span class="sxs-lookup"><span data-stu-id="08d2b-157">For Administrative events, hello filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="08d2b-158">Esses valores identificam quais eventos este alerta deverá monitorar.</span><span class="sxs-lookup"><span data-stu-id="08d2b-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="08d2b-159">Você deve especificar pelo menos um dos Olá precedem critérios em seu alerta.</span><span class="sxs-lookup"><span data-stu-id="08d2b-159">You must specify at least one of hello preceding criteria in your alert.</span></span> <span data-ttu-id="08d2b-160">Você não pode criar um alerta que é ativado sempre que um evento é criado nos logs de atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-160">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
    >
    >

8. <span data-ttu-id="08d2b-161">Insira um nome no hello **nome do grupo de ação** caixa e, em seguida, digite um nome em hello **nome curto** caixa.</span><span class="sxs-lookup"><span data-stu-id="08d2b-161">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="08d2b-162">nome curto de saudação é usado no lugar de um nome de grupo de ação completo quando as notificações são enviadas usando esse grupo.</span><span class="sxs-lookup"><span data-stu-id="08d2b-162">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="08d2b-163">Defina uma lista de ações, fornecendo da ação hello:</span><span class="sxs-lookup"><span data-stu-id="08d2b-163">Define a list of actions by providing hello action’s:</span></span>

    <span data-ttu-id="08d2b-164">a.</span><span class="sxs-lookup"><span data-stu-id="08d2b-164">a.</span></span> <span data-ttu-id="08d2b-165">**Nome**: insira o nome da ação hello, alias ou identificador.</span><span class="sxs-lookup"><span data-stu-id="08d2b-165">**Name**: Enter hello action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="08d2b-166">b.</span><span class="sxs-lookup"><span data-stu-id="08d2b-166">b.</span></span> <span data-ttu-id="08d2b-167">**Tipo de Ação**: selecione SMS, email ou webhook.</span><span class="sxs-lookup"><span data-stu-id="08d2b-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="08d2b-168">c.</span><span class="sxs-lookup"><span data-stu-id="08d2b-168">c.</span></span> <span data-ttu-id="08d2b-169">**Detalhes**: com base no tipo de ação de hello, insira um número de telefone, endereço de email ou webhook URI.</span><span class="sxs-lookup"><span data-stu-id="08d2b-169">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="08d2b-170">Selecione **Okey** toocreate alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-170">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="08d2b-171">alerta de saudação leva alguns minutos toofully se propague e, em seguida, se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="08d2b-171">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="08d2b-172">Ele dispara quando os critérios do alerta Olá correspondem a novos eventos.</span><span class="sxs-lookup"><span data-stu-id="08d2b-172">It triggers when new events match hello alert's criteria.</span></span>

<span data-ttu-id="08d2b-173">Para obter mais informações, consulte [esquema de webhook Olá compreender usada em alertas de log de atividade](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-173">For more information, see [Understand hello webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="08d2b-174">o grupo de ação Olá definido nessas etapas é reutilizável de um grupo existente de ação para todas as definições de alerta futuras.</span><span class="sxs-lookup"><span data-stu-id="08d2b-174">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="08d2b-175">Criar um alerta em um evento de log de atividade para um grupo existente, usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="08d2b-175">Create an alert on an activity log event for an existing action group by using hello Azure portal</span></span>
1. <span data-ttu-id="08d2b-176">Siga as etapas 1 a 7 em Olá anterior seção toocreate o alerta de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="08d2b-176">Follow steps 1 through 7 in hello previous section toocreate your activity log alert.</span></span>

2. <span data-ttu-id="08d2b-177">Em **notificar**, selecione Olá **existente** botão do grupo de ação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-177">Under **Notify via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="08d2b-178">Selecione um grupo existente na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-178">Select an existing action group from hello list.</span></span>

3. <span data-ttu-id="08d2b-179">Selecione **Okey** toocreate alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-179">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="08d2b-180">alerta de saudação leva alguns minutos toofully se propague e, em seguida, se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="08d2b-180">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="08d2b-181">Ele dispara quando os critérios do alerta Olá correspondem a novos eventos.</span><span class="sxs-lookup"><span data-stu-id="08d2b-181">It triggers when new events match hello alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="08d2b-182">Gerenciar seus alertas</span><span class="sxs-lookup"><span data-stu-id="08d2b-182">Manage your alerts</span></span>

<span data-ttu-id="08d2b-183">Depois de criar um alerta, ele está visível na seção de alertas de saudação da folha de Monitor de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-183">After you create an alert, it's visible in hello Alerts section of hello Monitor blade.</span></span> <span data-ttu-id="08d2b-184">Selecione o alerta de saudação desejado toomanage para:</span><span class="sxs-lookup"><span data-stu-id="08d2b-184">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="08d2b-185">Edite-o.</span><span class="sxs-lookup"><span data-stu-id="08d2b-185">Edit it.</span></span>
* <span data-ttu-id="08d2b-186">Exclua-o.</span><span class="sxs-lookup"><span data-stu-id="08d2b-186">Delete it.</span></span>
* <span data-ttu-id="08d2b-187">Desabilitar ou habilitá-lo, se você desejar tootemporarily parar ou continuar a receber notificações de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="08d2b-187">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08d2b-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08d2b-188">Next steps</span></span>
- <span data-ttu-id="08d2b-189">Obtenha uma [visão geral dos alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="08d2b-190">Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="08d2b-191">Saudação de revisão [webhook alerta esquema do log de atividade](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-191">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="08d2b-192">Saiba mais sobre [grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="08d2b-193">Saiba mais sobre as [notificações de integridade do serviço](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="08d2b-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="08d2b-194">Criar um [atividade todas as operações de mecanismo de dimensionamento automático em sua assinatura de alerta toomonitor log](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="08d2b-194">Create an [activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="08d2b-195">Criar um [atividade todas as operações de escala-em/expansão de dimensionamento automático com falha em sua assinatura de alerta toomonitor log](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="08d2b-195">Create an [activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
