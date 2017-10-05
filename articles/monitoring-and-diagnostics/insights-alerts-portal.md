---
title: "Criar alertas para serviços do Azure – Portal do Azure | Microsoft Docs"
description: "Disparar emails, notificações, chame URLs de sites (webhooks) ou automação quando as condições especificadas forem atendidas."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 745a9c016bd037f1051025a2c5a468c3935e4550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="826ca-103">Criar alertas de métrica no Azure Monitor para serviços do Azure – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="826ca-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="826ca-104">Portal</span><span class="sxs-lookup"><span data-stu-id="826ca-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="826ca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="826ca-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="826ca-106">CLI</span><span class="sxs-lookup"><span data-stu-id="826ca-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="826ca-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="826ca-107">Overview</span></span>
<span data-ttu-id="826ca-108">Este artigo mostra como configurar alertas de métrica do Azure usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="826ca-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="826ca-109">Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="826ca-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="826ca-110">**Valores da métrica** - o alerta dispara quando o valor de uma métrica especificada ultrapassa um limite que você atribui em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="826ca-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="826ca-111">Ou seja, ele dispara quando a condição é atendida pela primeira vez e posteriormente, quando essa condição não está sendo mais atendida.</span><span class="sxs-lookup"><span data-stu-id="826ca-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="826ca-112">**Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem.</span><span class="sxs-lookup"><span data-stu-id="826ca-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="826ca-113">Para saber mais sobre alertas de log de atividades, [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="826ca-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="826ca-114">Você pode configurar um alerta de métrica para fazer o seguinte quando ele dispara:</span><span class="sxs-lookup"><span data-stu-id="826ca-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="826ca-115">enviar um email para o administrador de serviços e os coadministradores</span><span class="sxs-lookup"><span data-stu-id="826ca-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="826ca-116">enviar email para outros emails que você especificar.</span><span class="sxs-lookup"><span data-stu-id="826ca-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="826ca-117">chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="826ca-117">call a webhook</span></span>
* <span data-ttu-id="826ca-118">iniciar a execução de um runbook do Azure (apenas no Portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="826ca-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="826ca-119">Você pode configurar e obter informações sobre regras de alerta de métrica usando</span><span class="sxs-lookup"><span data-stu-id="826ca-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="826ca-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="826ca-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="826ca-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="826ca-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="826ca-122">CLI (Interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="826ca-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="826ca-123">API REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="826ca-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="826ca-124">Criar uma regra de alerta em uma métrica com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="826ca-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="826ca-125">No [Portal](https://portal.azure.com/), localize o recurso no qual você está interessado em monitor e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="826ca-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="826ca-126">Selecione **Alertas** ou **Regras de alerta** na seção MONITORAMENTO.</span><span class="sxs-lookup"><span data-stu-id="826ca-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="826ca-127">O texto e o ícone podem variar um pouco para recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="826ca-127">The text and icon may vary slightly for different resources.</span></span>  

    ![Monitoramento](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="826ca-129">Selecione o comando **Adicionar alerta** e preencha os campos.</span><span class="sxs-lookup"><span data-stu-id="826ca-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![Adicionar alerta](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="826ca-131">Dê um **Nome** para o alerta de regra e escolha uma **Descrição**, que também mostre os emails de notificação.</span><span class="sxs-lookup"><span data-stu-id="826ca-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="826ca-132">Selecione a **Métrica** que você deseja monitorar, escolha uma **Condição** e um valor de **Limite** para a métrica.</span><span class="sxs-lookup"><span data-stu-id="826ca-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="826ca-133">Escolha também o **Período** durante o qual a regra de métrica deverá ser atendida antes de o alerta disparar.</span><span class="sxs-lookup"><span data-stu-id="826ca-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="826ca-134">Por exemplo, se você usar o período "PT5M" e o alerta procura por CPU acima de 80%, o alerta disparará quando a CPU estiver consistentemente acima de 80% por cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="826ca-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="826ca-135">Após o primeiro gatilho, ele disparará novamente quando a CPU permanecer abaixo de 80% durante cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="826ca-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="826ca-136">A medição da CPU ocorre a cada um minuto.</span><span class="sxs-lookup"><span data-stu-id="826ca-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="826ca-137">Verifique **Proprietários de email...** se quiser que os administradores e coadministradores recebem um email quando o alerta disparar.</span><span class="sxs-lookup"><span data-stu-id="826ca-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="826ca-138">Se você quiser que outros emails recebam uma notificação quando o alerta for disparado, adicione-os ao campo **Email(s) de administrador adicionais** .</span><span class="sxs-lookup"><span data-stu-id="826ca-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="826ca-139">Vários emails separados com ponto e vírgula – *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="826ca-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="826ca-140">Coloque um URI válido no campo **Webhook** se você quiser chamá-lo quando o alerta for disparado.</span><span class="sxs-lookup"><span data-stu-id="826ca-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="826ca-141">Se você usar a Automação do Azure, selecione um Runbook a ser executado quando o alerta for disparado.</span><span class="sxs-lookup"><span data-stu-id="826ca-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="826ca-142">Selecione **OK** ao concluir a criação do alerta.</span><span class="sxs-lookup"><span data-stu-id="826ca-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="826ca-143">Em alguns minutos, o alerta estará ativo e disparará conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="826ca-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="826ca-144">Gerenciar seus alertas</span><span class="sxs-lookup"><span data-stu-id="826ca-144">Managing your alerts</span></span>
<span data-ttu-id="826ca-145">Depois de criar um alerta, você poderá selecioná-lo e:</span><span class="sxs-lookup"><span data-stu-id="826ca-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="826ca-146">Exibir um gráfico mostrando o limite de métrica e os valores reais do dia anterior.</span><span class="sxs-lookup"><span data-stu-id="826ca-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="826ca-147">Editar ou exclui-lo.</span><span class="sxs-lookup"><span data-stu-id="826ca-147">Edit or delete it.</span></span>
* <span data-ttu-id="826ca-148">**Desabilitar** ou **Habilitar** se você quiser interromper temporariamente ou continuar recebendo notificações do alerta.</span><span class="sxs-lookup"><span data-stu-id="826ca-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="826ca-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="826ca-149">Next steps</span></span>
* <span data-ttu-id="826ca-150">[Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) , incluindo os tipos de informações que você pode coletar e monitorar.</span><span class="sxs-lookup"><span data-stu-id="826ca-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="826ca-151">Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="826ca-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="826ca-152">Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="826ca-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="826ca-153">Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="826ca-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="826ca-154">Tenha uma [visão geral dos logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) e colete métricas detalhadas de alta frequência em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="826ca-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="826ca-155">Tenha uma [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) para verificar se o serviço está disponível e responsivo.</span><span class="sxs-lookup"><span data-stu-id="826ca-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
