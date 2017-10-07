---
title: "alertas de aaaCreate para serviços do Azure - portal do Azure | Microsoft Docs"
description: "Disparar emails, notificações, URLs de sites de chamada (webhooks) ou automação quando Olá que especificar condições."
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
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="37f24-103">Criar alertas de métrica no Azure Monitor para serviços do Azure – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="37f24-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37f24-104">Portal</span><span class="sxs-lookup"><span data-stu-id="37f24-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="37f24-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37f24-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="37f24-106">CLI</span><span class="sxs-lookup"><span data-stu-id="37f24-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="37f24-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="37f24-107">Overview</span></span>
<span data-ttu-id="37f24-108">Este artigo mostra como tooset alertas de métrica do Azure usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="37f24-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="37f24-109">Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="37f24-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="37f24-110">**Valores da métrica** - Olá gatilhos de alerta quando o valor de saudação de uma métrica especificada cruza um limite que você atribui em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="37f24-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="37f24-111">Ou seja, ela aciona ambos quando Olá primeiro condição e, em seguida, posteriormente quando que condição é não está sendo atendida.</span><span class="sxs-lookup"><span data-stu-id="37f24-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="37f24-112">**Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem.</span><span class="sxs-lookup"><span data-stu-id="37f24-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="37f24-113">mais sobre alertas de log de atividade de toolearn [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="37f24-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="37f24-114">Você pode configurar uma saudação de métrica toodo alerta após quando ele dispara:</span><span class="sxs-lookup"><span data-stu-id="37f24-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="37f24-115">enviar o administrador do serviço de toohello de notificações de email e coadministradores</span><span class="sxs-lookup"><span data-stu-id="37f24-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="37f24-116">Envie email tooadditional emails que você especificar.</span><span class="sxs-lookup"><span data-stu-id="37f24-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="37f24-117">chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="37f24-117">call a webhook</span></span>
* <span data-ttu-id="37f24-118">Iniciar a execução de um runbook do Azure (apenas de saudação portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="37f24-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="37f24-119">Você pode configurar e obter informações sobre regras de alerta de métrica usando</span><span class="sxs-lookup"><span data-stu-id="37f24-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="37f24-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="37f24-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="37f24-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37f24-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="37f24-122">CLI (Interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="37f24-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="37f24-123">API REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="37f24-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="37f24-124">Criar uma regra de alerta em uma métrica com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="37f24-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="37f24-125">Em Olá [portal](https://portal.azure.com/), localize o recurso Olá você está interessado no monitoramento e selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="37f24-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="37f24-126">Selecione **alertas** ou **regras de alerta** em Olá seção monitoramento.</span><span class="sxs-lookup"><span data-stu-id="37f24-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="37f24-127">ícone e o texto de saudação podem variar um pouco para recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="37f24-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![Monitoramento](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="37f24-129">Selecione Olá **adicionar alerta** de comando e preencha os campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="37f24-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Adicionar alerta](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="37f24-131">Dê um **Nome** para o alerta de regra e escolha uma **Descrição**, que também mostre os emails de notificação.</span><span class="sxs-lookup"><span data-stu-id="37f24-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="37f24-132">Selecione Olá **métrica** você deseja toomonitor, em seguida, escolha um **condição** e **limite** valor de métrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="37f24-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="37f24-133">Também tiver escolhido Olá **período** de tempo que Olá métrica regra deve ser atendida antes de gatilhos de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="37f24-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="37f24-134">Por exemplo, se você usar o período de hello "PT5M" e a alerta de procura da CPU acima de 80%, alerta Olá dispara quando Olá CPU foi consistentemente acima de 80% por 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="37f24-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="37f24-135">Depois que o primeiro gatilho de saudação ocorre, ele novamente dispara quando Olá da CPU permanece abaixo de 80% de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="37f24-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="37f24-136">Olá medida de CPU ocorre a cada 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="37f24-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="37f24-137">Verificar **proprietários de Email...**  se você quiser que os administradores e coadministradores toobe enviado por email quando Olá alerta acionado.</span><span class="sxs-lookup"><span data-stu-id="37f24-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="37f24-138">Se você quiser emails adicionais tooreceive notificação hello quando o alerta é acionado, adicioná-los em Olá **email(s) administrador adicional** campo.</span><span class="sxs-lookup"><span data-stu-id="37f24-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="37f24-139">Vários emails separados com ponto e vírgula – *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="37f24-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="37f24-140">Colocar em um URI válido no hello **Webhook** campo se você quiser chamada hello alerta acionado quando.</span><span class="sxs-lookup"><span data-stu-id="37f24-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="37f24-141">Se você usar a automação do Azure, você pode selecionar um toobe Runbook executado quando Olá alerta será acionado.</span><span class="sxs-lookup"><span data-stu-id="37f24-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="37f24-142">Selecione **Okey** quando concluído toocreate Olá alerta.</span><span class="sxs-lookup"><span data-stu-id="37f24-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="37f24-143">Em poucos minutos, o alerta de hello está ativa e dispara conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="37f24-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="37f24-144">Gerenciar seus alertas</span><span class="sxs-lookup"><span data-stu-id="37f24-144">Managing your alerts</span></span>
<span data-ttu-id="37f24-145">Depois de criar um alerta, você poderá selecioná-lo e:</span><span class="sxs-lookup"><span data-stu-id="37f24-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="37f24-146">Exiba um gráfico que mostra o limite de métrica hello e os valores reais de Olá Olá dia anterior.</span><span class="sxs-lookup"><span data-stu-id="37f24-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="37f24-147">Editar ou exclui-lo.</span><span class="sxs-lookup"><span data-stu-id="37f24-147">Edit or delete it.</span></span>
* <span data-ttu-id="37f24-148">**Desabilitar** ou **habilitar** se deseja tootemporarily parar ou continuar recebendo notificações para o alerta.</span><span class="sxs-lookup"><span data-stu-id="37f24-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37f24-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37f24-149">Next steps</span></span>
* <span data-ttu-id="37f24-150">[Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) incluindo Olá tipos de informações você pode coletar e monitorar.</span><span class="sxs-lookup"><span data-stu-id="37f24-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="37f24-151">Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="37f24-152">Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="37f24-153">Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="37f24-154">Tenha uma [visão geral dos logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) e colete métricas detalhadas de alta frequência em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="37f24-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="37f24-155">Obter um [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.</span><span class="sxs-lookup"><span data-stu-id="37f24-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
