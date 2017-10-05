---
title: Como monitorar uma conta de Armazenamento do Azure | Microsoft Docs
description: Saiba como monitorar uma conta de armazenamento no Azure usando o portal do Azure.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: b49e06da0019a50cc8e50c4da47e42c03b44bcc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-storage-account-in-the-azure-portal"></a><span data-ttu-id="dc43a-103">Monitorar uma conta de armazenamento no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dc43a-103">Monitor a storage account in the Azure portal</span></span>

<span data-ttu-id="dc43a-104">[Análise de Armazenamento do Azure](storage-analytics.md) fornece métricas para todos os serviços de armazenamento e logs para blobs, filas e tabelas.</span><span class="sxs-lookup"><span data-stu-id="dc43a-104">[Azure Storage Analytics](storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="dc43a-105">Você pode usar o [portal do Azure](https://portal.azure.com) de configurar quais métricas e logs são registrados para sua conta e configurar gráficos que fornecem representações visuais dos dados de métricas.</span><span class="sxs-lookup"><span data-stu-id="dc43a-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="dc43a-106">Há custos associados ao exame de dados de monitoramento no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc43a-106">There are costs associated with examining monitoring data in the Azure portal.</span></span> <span data-ttu-id="dc43a-107">Para obter mais informações, consulte [Análise de armazenamento e cobrança](/rest/api/storageservices/Storage-Analytics-and-Billing).</span><span class="sxs-lookup"><span data-stu-id="dc43a-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="dc43a-108">O Armazenamento de arquivos do Azure atualmente dá suporte às métricas de Análise de Armazenamento, mas ainda não dá suporte ao registro em log.</span><span class="sxs-lookup"><span data-stu-id="dc43a-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="dc43a-109">As contas de armazenamento com um tipo de replicação de armazenamento com redundância de zona (ZRS) não têm métricas ou funcionalidade de log habilitadas no momento.</span><span class="sxs-lookup"><span data-stu-id="dc43a-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="dc43a-110">Para um guia aprofundado sobre como usar a Análise de Armazenamento e outras ferramentas para identificar, diagnosticar e solucionar problemas relacionados ao Armazenamento do Azure, consulte [Monitorar, diagnosticar e solucionar problemas do Armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="dc43a-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="dc43a-111">Configurar o monitoramento para uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="dc43a-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="dc43a-112">No [portal do Azure](https://portal.azure.com), selecione **Contas de armazenamento** e o nome de conta de armazenamento para abrir o painel de conta.</span><span class="sxs-lookup"><span data-stu-id="dc43a-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span></span>
1. <span data-ttu-id="dc43a-113">Selecione **Diagnóstico** na seção **MONITORAMENTO** da folha de menu.</span><span class="sxs-lookup"><span data-stu-id="dc43a-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Opções de monitoramento](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="dc43a-115">Selecione o **tipo** de dados de métrica para cada **serviço** que você deseja monitorar e a **política de retenção** para os dados.</span><span class="sxs-lookup"><span data-stu-id="dc43a-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span></span> <span data-ttu-id="dc43a-116">Você também pode desabilitar o monitoramento definindo **Status** como **Desativado**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-116">You can also disable monitoring by setting **Status** to **Off**.</span></span>

    ![Opções de monitoramento](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="dc43a-118">Há dois tipos de métricas que você pode habilitar para cada serviço. Ambas são habilitadas por padrão para novas contas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="dc43a-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="dc43a-119">**Agregação**: coleta métricas como percentuais de entrada/saída, disponibilidade, latência e sucesso.</span><span class="sxs-lookup"><span data-stu-id="dc43a-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="dc43a-120">Essas métricas são agregadas para os serviços de blob, fila, tabela e arquivo.</span><span class="sxs-lookup"><span data-stu-id="dc43a-120">These metrics are aggregated for the blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="dc43a-121">**Por API**: além das métricas agregadas, coleta o mesmo conjunto de métricas para cada operação de armazenamento na API de serviço de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc43a-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span></span>

   <span data-ttu-id="dc43a-122">Para definir a política de retenção de dados, mova o controle deslizante **Retenção (dias)** ou insira o número de dias de dados devem ser retidos, de 1 a 365.</span><span class="sxs-lookup"><span data-stu-id="dc43a-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span></span> <span data-ttu-id="dc43a-123">O padrão para novas contas de armazenamento é de sete dias.</span><span class="sxs-lookup"><span data-stu-id="dc43a-123">The default for new storage accounts is seven days.</span></span> <span data-ttu-id="dc43a-124">Se não desejar definir uma política de retenção, digite zero.</span><span class="sxs-lookup"><span data-stu-id="dc43a-124">If you do not want to set a retention policy, enter zero.</span></span> <span data-ttu-id="dc43a-125">Se não houver nenhuma política de retenção, cabe a você excluir os dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="dc43a-125">If there is no retention policy, it is up to you to delete the monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="dc43a-126">Você é cobrado quando exclui manualmente dados de métricas.</span><span class="sxs-lookup"><span data-stu-id="dc43a-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="dc43a-127">Dados de análise obsoletos (dados anteriores à política de retenção) são excluídos pelo sistema sem custo.</span><span class="sxs-lookup"><span data-stu-id="dc43a-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span></span> <span data-ttu-id="dc43a-128">É recomendável configurar uma política de retenção com base no tempo pelo qual você deseja manter os dados de análise de armazenamento para sua conta.</span><span class="sxs-lookup"><span data-stu-id="dc43a-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span></span> <span data-ttu-id="dc43a-129">Confira [Quais são os encargos quando você habilita as métricas de armazenamento?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="dc43a-129">See [What charges do you incur when you enable storage metrics?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="dc43a-130">Ao concluir a configuração de monitoramento, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-130">When you finish the monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="dc43a-131">Um conjunto de métricas padrão é exibido em gráficos na folha da conta de armazenamento, bem como nas folhas de serviço individuais (blob, fila, tabela e arquivo).</span><span class="sxs-lookup"><span data-stu-id="dc43a-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="dc43a-132">Depois que você habilita métricas para um serviço, pode levar até uma hora para que os dados apareçam nos gráficos.</span><span class="sxs-lookup"><span data-stu-id="dc43a-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span></span> <span data-ttu-id="dc43a-133">Você pode selecionar **Editar** em qualquer gráfico de métricas para [configurar quais métricas](#how-to-customize-metrics-charts) são exibidas no gráfico.</span><span class="sxs-lookup"><span data-stu-id="dc43a-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span></span>

<span data-ttu-id="dc43a-134">Você pode desabilitar a coleta de métricas e o registro em log definindo **Status** como **Desativado**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="dc43a-135">O Armazenamento do Azure usa o [armazenamento de tabelas](storage-introduction.md#table-storage) para armazenar as métricas para sua conta de armazenamento e armazena as métricas em tabelas em sua conta.</span><span class="sxs-lookup"><span data-stu-id="dc43a-135">Azure Storage uses [table storage](storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span></span> <span data-ttu-id="dc43a-136">Para obter mais informações, confira:</span><span class="sxs-lookup"><span data-stu-id="dc43a-136">For more information, see.</span></span> <span data-ttu-id="dc43a-137">[Como as métricas são armazenadas](storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="dc43a-137">[How metrics are stored](storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="dc43a-138">Personalizar gráficos de métricas</span><span class="sxs-lookup"><span data-stu-id="dc43a-138">Customize metrics charts</span></span>

<span data-ttu-id="dc43a-139">Use o procedimento a seguir para escolher quais métricas de armazenamento devem ser exibidas em um gráfico de métricas.</span><span class="sxs-lookup"><span data-stu-id="dc43a-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span></span> 

1. <span data-ttu-id="dc43a-140">Comece exibindo um gráfico de métricas de armazenamento no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc43a-140">Start by displaying a storage metric chart in the Azure portal.</span></span> <span data-ttu-id="dc43a-141">Você pode encontrar gráficos na **folha da conta de armazenamento** e na folha **Métricas** de um serviço individual (blob, fila, tabela, arquivo).</span><span class="sxs-lookup"><span data-stu-id="dc43a-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="dc43a-142">Neste exemplo, trabalhamos com o gráfico a seguir, que aparece na **folha de conta de armazenamento**:</span><span class="sxs-lookup"><span data-stu-id="dc43a-142">In this example, we work with the following chart that appears on the **storage account blade**:</span></span>

   ![Seleção de gráfico no portal do Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="dc43a-144">Em seguida, clique em qualquer lugar no gráfico para abrir a folha **Métrica**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-144">Next, click anywhere within the chart to open the **Metric** blade.</span></span> <span data-ttu-id="dc43a-145">Selecione **Editar gráfico** para abrir a folha **Editar Gráfico**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-145">Select **Edit chart** to open the **Edit Chart** blade.</span></span>

   ![Editar botão de gráfico na folha de gráfico](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="dc43a-147">Na folha **Editar Gráfico**, selecione o **Intervalo de Tempo** das métricas para exibir no gráfico e o **service** (blob, fila, tabela, arquivo) cujas métricas você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="dc43a-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span></span> <span data-ttu-id="dc43a-148">Aqui, selecionamos a exibição das métricas da semana passada para o serviço de blob:</span><span class="sxs-lookup"><span data-stu-id="dc43a-148">Here we've selected to display the past week's metrics for the blob service:</span></span>

   ![Intervalo de tempo e seleção de serviço na folha Editar Gráfico](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="dc43a-150">Selecione as **métricas** individuais que deseja exibir no gráfico e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span></span> <span data-ttu-id="dc43a-151">Por exemplo, aqui, optamos por exibir as métricas *ContainerCount* e *ObjectCount*:</span><span class="sxs-lookup"><span data-stu-id="dc43a-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![Seleção de métrica individual na folha Editar Gráfico](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="dc43a-153">As configurações de gráfico não afetam a coleta, a agregação ou o armazenamento de dados de monitoramento na conta de armazenamento, somente a exibição de dados de métricas.</span><span class="sxs-lookup"><span data-stu-id="dc43a-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="dc43a-154">Disponibilidade de métricas em gráficos</span><span class="sxs-lookup"><span data-stu-id="dc43a-154">Metrics availability in charts</span></span>

<span data-ttu-id="dc43a-155">A lista de métricas disponíveis é alterada com base em qual serviço você escolheu na lista suspensa e qual tipo de unidade do gráfico você está editando.</span><span class="sxs-lookup"><span data-stu-id="dc43a-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span></span> <span data-ttu-id="dc43a-156">Por exemplo, você só poderá selecionar as métricas de percentual como *PercentNetworkError* e *PercentThrottlingError* se estiver editando um gráfico que exiba as unidades em percentual:</span><span class="sxs-lookup"><span data-stu-id="dc43a-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Gráfico de percentual de erro de solicitação no portal do Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="dc43a-158">Resolução de métricas</span><span class="sxs-lookup"><span data-stu-id="dc43a-158">Metrics resolution</span></span>

<span data-ttu-id="dc43a-159">As métricas que você selecionou em Diagnósticos determinam a resolução das métricas que estão disponíveis para sua conta:</span><span class="sxs-lookup"><span data-stu-id="dc43a-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span></span>

* <span data-ttu-id="dc43a-160">O monitoramento **Agregado** fornece métricas como percentuais de entrada/saída, disponibilidade, latência e sucesso.</span><span class="sxs-lookup"><span data-stu-id="dc43a-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="dc43a-161">Essas métricas são agregadas dos serviços de blob, tabela, arquivo e fila.</span><span class="sxs-lookup"><span data-stu-id="dc43a-161">These metrics are aggregated from the blob, table, file, and queue services.</span></span>
* <span data-ttu-id="dc43a-162">**Por API** fornece resolução mais detalhada, com métricas disponíveis para operações de armazenamento individuais, além de agregações de nível de serviço.</span><span class="sxs-lookup"><span data-stu-id="dc43a-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="dc43a-163">Configurar alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="dc43a-163">Configure metrics alerts</span></span>

<span data-ttu-id="dc43a-164">Você pode criar alertas para notificá-lo quando os limites forem atingidos para métricas de recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc43a-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="dc43a-165">Para abrir a **folha de Regras de alerta**, role para baixo até a seção **MONITORAMENTO** da **folha de Menu** e selecione **Regras de alerta**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="dc43a-166">Selecione **Adicionar alerta** para abrir a folha **Adicionar uma regra de alerta**</span><span class="sxs-lookup"><span data-stu-id="dc43a-166">Select **Add alert** to open the **Add an alert rule** blade</span></span>
1. <span data-ttu-id="dc43a-167">Selecione um **Recurso** (blob, arquivo, fila, tabela) na lista suspensa e digite um **Nome** e **Descrição** para a nova regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="dc43a-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="dc43a-168">Selecione a **Métrica** para a qual você deseja adicionar um alerta, uma **Condição** de alerta e um **Limite**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="dc43a-169">O tipo de unidade de limite é alterado dependendo da métrica que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="dc43a-169">The threshold unit type changes depending on the metric you've chosen.</span></span> <span data-ttu-id="dc43a-170">Por exemplo, "count" é o tipo de unidade para *ContainerCount*, enquanto a unidade para a métrica *PercentNetworkError* é um percentual.</span><span class="sxs-lookup"><span data-stu-id="dc43a-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="dc43a-171">Selecione o **Período**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-171">Select the **Period**.</span></span> <span data-ttu-id="dc43a-172">As métricas que atingiram ou excederam o limite dentro do período disparam um alerta.</span><span class="sxs-lookup"><span data-stu-id="dc43a-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span></span>
1. <span data-ttu-id="dc43a-173">(Opcional) Configurar notificações de **Email** e **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="dc43a-174">Para obter mais informações sobre webhooks, confira [Configurar um webhook em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="dc43a-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="dc43a-175">Se você não configurar notificações por email ou webhook, serão exibidos alertas somente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc43a-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span></span>

![Folha 'Adicionar uma regra de alerta' no portal do Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-to-the-portal-dashboard"></a><span data-ttu-id="dc43a-177">Adicionar gráficos de métricas para o painel do portal</span><span class="sxs-lookup"><span data-stu-id="dc43a-177">Add metrics charts to the portal dashboard</span></span>

<span data-ttu-id="dc43a-178">Você pode adicionar gráficos de métricas do Armazenamento do Azure para qualquer uma de suas contas de armazenamento no painel do portal.</span><span class="sxs-lookup"><span data-stu-id="dc43a-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span></span>

1. <span data-ttu-id="dc43a-179">Clique para selecionar **Editar painel** ao exibir o painel no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc43a-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="dc43a-180">Na **Galeria de Blocos**, selecione **Localizar blocos por** > **Tipo**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="dc43a-181">Selecione **Tipo** > **Contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="dc43a-182">Em **Recursos**, selecione a conta de armazenamento cujas métricas deseja adicionar ao painel.</span><span class="sxs-lookup"><span data-stu-id="dc43a-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span></span>
1. <span data-ttu-id="dc43a-183">Selecione **Categorias** > **Monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="dc43a-184">Arraste e solte o bloco do gráfico no painel para a métrica que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="dc43a-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span></span> <span data-ttu-id="dc43a-185">Repita para todas as métricas que deseja exibir no painel.</span><span class="sxs-lookup"><span data-stu-id="dc43a-185">Repeat for all metrics you'd like displayed on the dashboard.</span></span> <span data-ttu-id="dc43a-186">Na imagem a seguir, o gráfico "Blobs - total de solicitações" está realçado como um exemplo, mas todos os gráficos estão disponíveis para posicionamento em seu painel.</span><span class="sxs-lookup"><span data-stu-id="dc43a-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span></span>

   ![Galeria de blocos no portal do Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="dc43a-188">Selecione **Personalização concluída** na parte superior do painel quando terminar a adição de gráficos.</span><span class="sxs-lookup"><span data-stu-id="dc43a-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span></span>

<span data-ttu-id="dc43a-189">Depois de adicionar gráficos ao painel, você pode personalizá-los conforme descrito em [Personalizar gráficos de métricas](#how-to-customize-metrics-charts).</span><span class="sxs-lookup"><span data-stu-id="dc43a-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="dc43a-190">Configurar o registro em log</span><span class="sxs-lookup"><span data-stu-id="dc43a-190">Configure logging</span></span>

<span data-ttu-id="dc43a-191">Você pode instruir o Armazenamento do Azure a salvar logs de diagnóstico para ler, gravar e excluir solicitações para os serviços de fila, blob e tabela.</span><span class="sxs-lookup"><span data-stu-id="dc43a-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span></span> <span data-ttu-id="dc43a-192">A política de retenção de dados que você define também se aplica a esses logs.</span><span class="sxs-lookup"><span data-stu-id="dc43a-192">The data retention policy you set also applies to these logs.</span></span>

> [!NOTE]
> <span data-ttu-id="dc43a-193">O Armazenamento de arquivos do Azure atualmente dá suporte às métricas de Análise de Armazenamento, mas ainda não dá suporte ao registro em log.</span><span class="sxs-lookup"><span data-stu-id="dc43a-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="dc43a-194">No [portal do Azure](https://portal.azure.com), selecione **Contas de armazenamento** e o nome da conta de armazenamento para abrir a folha de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc43a-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span></span>
1. <span data-ttu-id="dc43a-195">Selecione **Diagnóstico** na seção **MONITORAMENTO** da folha de menu.</span><span class="sxs-lookup"><span data-stu-id="dc43a-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Item do menu de diagnóstico em MONITORAMENTO no portal do Azure.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="dc43a-197">Verifique se **Status** está definido como **Ativado**e selecione os **Serviços** para os quais deseja habilitar os logs.</span><span class="sxs-lookup"><span data-stu-id="dc43a-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span></span>

    ![Configure os logs no portal do Azure.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="dc43a-199">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dc43a-199">Click **Save**.</span></span>

<span data-ttu-id="dc43a-200">Os logs de diagnóstico são salvos em um contêiner de blob denominado $logs em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc43a-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="dc43a-201">Você pode exibir os dados de log usando um gerenciador de armazenamento como o [Gerenciador de Armazenamento da Microsoft](http://storageexplorer.com) ou de forma programática, usando a biblioteca de cliente de armazenamento ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc43a-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span></span>

<span data-ttu-id="dc43a-202">Para obter informações sobre como acessar o contêiner $logs, confira [Habilitando o log de armazenamento e acessando dados de log](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span><span class="sxs-lookup"><span data-stu-id="dc43a-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc43a-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc43a-203">Next steps</span></span>

* <span data-ttu-id="dc43a-204">Encontre mais detalhes sobre [métricas, logs e cobrança](storage-analytics.md) para Análise de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc43a-204">Find more details about [metrics, logging, and billing](storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="dc43a-205">[Habilitar métricas do Armazenamento do Azure e exibir dados de métricas](storage-enable-and-view-metrics.md) usando o PowerShell e de forma programática com C#.</span><span class="sxs-lookup"><span data-stu-id="dc43a-205">[Enable Azure Storage metrics and view metrics data](storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>
