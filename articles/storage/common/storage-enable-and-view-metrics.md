---
title: "as métricas de armazenamento aaaEnabling em Olá portal do Azure | Microsoft Docs"
description: "Como as métricas de armazenamento tooenable para Olá serviços Blob, fila, tabela e arquivo"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="96ca6-103">Habilitando métricas do Armazenamento do Azure e exibição de dados de métricas</span><span class="sxs-lookup"><span data-stu-id="96ca6-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="96ca6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="96ca6-104">Overview</span></span>
<span data-ttu-id="96ca6-105">As Métricas de Armazenamento são habilitadas por padrão quando você cria uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="96ca6-106">Você pode configurar o monitoramento por meio de saudação [portal do Azure](https://portal.azure.com) ou o Windows PowerShell, ou programaticamente por meio de bibliotecas de saudação do cliente de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="96ca6-107">Você pode configurar um período de retenção de dados de métricas de saudação: esse período determina para armazenamento de saudação quanto tempo o serviço mantém métricas hello e encargos por Olá espaço necessário toostore-los.</span><span class="sxs-lookup"><span data-stu-id="96ca6-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="96ca6-108">Normalmente, você deve usar um período de retenção mais curto para métricas de minuto de hora devido a espaço adicional significativo Olá necessário para métricas de minuto.</span><span class="sxs-lookup"><span data-stu-id="96ca6-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="96ca6-109">Você deve escolher um período de retenção, de modo que você tem dados suficientes de saudação de tooanalyze tempo e baixar as métricas que você deseja tookeep para análise offline ou para fins de relatório.</span><span class="sxs-lookup"><span data-stu-id="96ca6-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="96ca6-110">Lembre-se de que você também será cobrado para baixar dados de métrica de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="96ca6-111">Como as métricas de tooenable usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="96ca6-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="96ca6-112">Siga essas métricas de tooenable etapas no hello [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="96ca6-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="96ca6-113">Navegue tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="96ca6-114">Selecione **diagnóstico** em Olá **Menu** folha</span><span class="sxs-lookup"><span data-stu-id="96ca6-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="96ca6-115">Certifique-se de que **Status** está definido muito**em**.</span><span class="sxs-lookup"><span data-stu-id="96ca6-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="96ca6-116">Métricas de saudação Select para serviços de saudação desejar toomonitor.</span><span class="sxs-lookup"><span data-stu-id="96ca6-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="96ca6-117">Especifique um tooindicate de política de retenção quanto tempo dados de log e métricas de tooretain.</span><span class="sxs-lookup"><span data-stu-id="96ca6-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="96ca6-118">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="96ca6-118">Select **Save**.</span></span>

<span data-ttu-id="96ca6-119">Observe que Olá [portal do Azure](https://portal.azure.com) atualmente permite que você tooconfigure métricas de minutos em sua conta de armazenamento; você deve habilitar métricas de minuto usando o PowerShell ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="96ca6-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="96ca6-120">Como as métricas de tooenable usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="96ca6-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="96ca6-121">Você pode usar o PowerShell em tooconfigure seu computador local as métricas de armazenamento em sua conta de armazenamento usando hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve Olá configurações atuais e Olá cmdlet Set-AzureStorageServiceMetricsProperty toochange Olá as configurações atuais.</span><span class="sxs-lookup"><span data-stu-id="96ca6-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="96ca6-122">Olá que controlam as métricas de armazenamento usam Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="96ca6-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="96ca6-123">Os valorespossíveis de MetricsType são hora e minuto.</span><span class="sxs-lookup"><span data-stu-id="96ca6-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="96ca6-124">ServiceType: os possíveis valores são Blob, Fila e Tabela.</span><span class="sxs-lookup"><span data-stu-id="96ca6-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="96ca6-125">MetricsLevel: os valores possíveis são None, Serviço e ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="96ca6-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="96ca6-126">Por exemplo, hello seguinte comando ativa em minuto métricas para serviço de Blob de saudação em sua conta de armazenamento padrão com o período de retenção Olá definir toofive dias:</span><span class="sxs-lookup"><span data-stu-id="96ca6-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="96ca6-127">Olá seguinte comando recupera Olá atual por hora métricas nível e retenção de dias para o serviço de blob de saudação em sua conta de armazenamento padrão:</span><span class="sxs-lookup"><span data-stu-id="96ca6-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="96ca6-128">Para obter informações sobre como tooconfigure hello Azure PowerShell cmdlets toowork com sua assinatura do Azure e como tooselect Olá armazenamento padrão da conta toouse, consulte: [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96ca6-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="96ca6-129">Como tooenable as métricas de armazenamento programaticamente</span><span class="sxs-lookup"><span data-stu-id="96ca6-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="96ca6-130">saudação de trecho de código c# a seguir mostra como tooenable métricas e registro em log para usar o serviço Blob Olá Olá biblioteca de cliente de armazenamento para .NET:</span><span class="sxs-lookup"><span data-stu-id="96ca6-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="96ca6-131">Exibindo as métricas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="96ca6-131">Viewing Storage metrics</span></span>
<span data-ttu-id="96ca6-132">Depois de configurar a análise de armazenamento métricas toomonitor sua conta de armazenamento, o Storage Analytics registra métricas Olá em um conjunto de tabelas bem conhecidas em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="96ca6-133">Você pode configurar métricas de hora gráficos tooview Olá [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="96ca6-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="96ca6-134">Navegue de conta de armazenamento tooyour Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96ca6-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="96ca6-135">Selecione **métricas** em Olá **Menu** folha para Olá cujas métricas de serviço você deseja tooview.</span><span class="sxs-lookup"><span data-stu-id="96ca6-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="96ca6-136">Selecione **editar** no gráfico de saudação desejado tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="96ca6-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="96ca6-137">Em Olá **Editar gráfico** folha, selecione Olá **intervalo de tempo**, **tipo de gráfico**e você deseja exibir no gráfico de saudação de métricas de saudação.</span><span class="sxs-lookup"><span data-stu-id="96ca6-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="96ca6-138">Selecione **OK**</span><span class="sxs-lookup"><span data-stu-id="96ca6-138">Select **OK**</span></span>

<span data-ttu-id="96ca6-139">Se você quiser que as métricas de saudação toodownload para armazenamento de longo prazo ou tooanalyze-las localmente, você precisará:</span><span class="sxs-lookup"><span data-stu-id="96ca6-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="96ca6-140">Use uma ferramenta que está ciente dessas tabelas e permitem que você tooview e baixá-los.</span><span class="sxs-lookup"><span data-stu-id="96ca6-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="96ca6-141">Gravar um tooread de aplicativo ou script personalizado e armazenar tabelas hello.</span><span class="sxs-lookup"><span data-stu-id="96ca6-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="96ca6-142">Muitas ferramentas de navegação de armazenamento de terceiros reconhecem essas tabelas e permitem que você tooview-los diretamente.</span><span class="sxs-lookup"><span data-stu-id="96ca6-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="96ca6-143">Confira [Ferramentas de Cliente do Armazenamento do Azure](storage-explorers.md) para obter uma lista de ferramentas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="96ca6-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="96ca6-144">Começando com a versão 0.8.0 de saudação [Microsoft Azure Storage Explorer](http://storageexplorer.com/), você pode exibir e baixar as tabelas de métricas de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="96ca6-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="96ca6-145">Na análise de saudação do pedido tooaccess tabelas programaticamente, observe que tabelas de análise de saudação não aparecerá se você listar todas as tabelas de saudação em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="96ca6-146">Você pode acessá-los diretamente por nome ou usar Olá [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) em nomes de tabela Olá de tooquery biblioteca de cliente .NET de saudação.</span><span class="sxs-lookup"><span data-stu-id="96ca6-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="96ca6-147">Métricas por hora</span><span class="sxs-lookup"><span data-stu-id="96ca6-147">Hourly metrics</span></span>
* <span data-ttu-id="96ca6-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="96ca6-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="96ca6-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="96ca6-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="96ca6-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="96ca6-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="96ca6-151">Métricas por minuto</span><span class="sxs-lookup"><span data-stu-id="96ca6-151">Minute metrics</span></span>
* <span data-ttu-id="96ca6-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="96ca6-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="96ca6-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="96ca6-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="96ca6-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="96ca6-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="96ca6-155">Capacidade</span><span class="sxs-lookup"><span data-stu-id="96ca6-155">Capacity</span></span>
* <span data-ttu-id="96ca6-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="96ca6-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="96ca6-157">Você pode encontrar detalhes completos de esquemas Olá para essas tabelas em [esquema de tabela de métricas de análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="96ca6-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="96ca6-158">linhas de exemplo Hello abaixo mostram apenas um subconjunto de colunas de saudação disponíveis, mas ilustram alguns recursos importantes da maneira Olá que métricas de armazenamento salvam essas métricas:</span><span class="sxs-lookup"><span data-stu-id="96ca6-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="96ca6-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="96ca6-159">PartitionKey</span></span> | <span data-ttu-id="96ca6-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="96ca6-160">RowKey</span></span> | <span data-ttu-id="96ca6-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="96ca6-161">Timestamp</span></span> | <span data-ttu-id="96ca6-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="96ca6-162">TotalRequests</span></span> | <span data-ttu-id="96ca6-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="96ca6-163">TotalBillableRequests</span></span> | <span data-ttu-id="96ca6-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="96ca6-164">TotalIngress</span></span> | <span data-ttu-id="96ca6-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="96ca6-165">TotalEgress</span></span> | <span data-ttu-id="96ca6-166">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="96ca6-166">Availability</span></span> | <span data-ttu-id="96ca6-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="96ca6-167">AverageE2ELatency</span></span> | <span data-ttu-id="96ca6-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="96ca6-168">AverageServerLatency</span></span> | <span data-ttu-id="96ca6-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="96ca6-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="96ca6-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="96ca6-170">20140522T1100</span></span> |<span data-ttu-id="96ca6-171">user;All</span><span class="sxs-lookup"><span data-stu-id="96ca6-171">user;All</span></span> |<span data-ttu-id="96ca6-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="96ca6-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="96ca6-173">7</span><span class="sxs-lookup"><span data-stu-id="96ca6-173">7</span></span> |<span data-ttu-id="96ca6-174">7</span><span class="sxs-lookup"><span data-stu-id="96ca6-174">7</span></span> |<span data-ttu-id="96ca6-175">4003</span><span class="sxs-lookup"><span data-stu-id="96ca6-175">4003</span></span> |<span data-ttu-id="96ca6-176">46801</span><span class="sxs-lookup"><span data-stu-id="96ca6-176">46801</span></span> |<span data-ttu-id="96ca6-177">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-177">100</span></span> |<span data-ttu-id="96ca6-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="96ca6-178">104.4286</span></span> |<span data-ttu-id="96ca6-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="96ca6-179">6.857143</span></span> |<span data-ttu-id="96ca6-180">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-180">100</span></span> |
| <span data-ttu-id="96ca6-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="96ca6-181">20140522T1100</span></span> |<span data-ttu-id="96ca6-182">usuário;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="96ca6-182">user;QueryEntities</span></span> |<span data-ttu-id="96ca6-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="96ca6-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="96ca6-184">5</span><span class="sxs-lookup"><span data-stu-id="96ca6-184">5</span></span> |<span data-ttu-id="96ca6-185">5</span><span class="sxs-lookup"><span data-stu-id="96ca6-185">5</span></span> |<span data-ttu-id="96ca6-186">2694</span><span class="sxs-lookup"><span data-stu-id="96ca6-186">2694</span></span> |<span data-ttu-id="96ca6-187">45951</span><span class="sxs-lookup"><span data-stu-id="96ca6-187">45951</span></span> |<span data-ttu-id="96ca6-188">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-188">100</span></span> |<span data-ttu-id="96ca6-189">143.8</span><span class="sxs-lookup"><span data-stu-id="96ca6-189">143.8</span></span> |<span data-ttu-id="96ca6-190">7.8</span><span class="sxs-lookup"><span data-stu-id="96ca6-190">7.8</span></span> |<span data-ttu-id="96ca6-191">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-191">100</span></span> |
| <span data-ttu-id="96ca6-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="96ca6-192">20140522T1100</span></span> |<span data-ttu-id="96ca6-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="96ca6-193">user;QueryEntity</span></span> |<span data-ttu-id="96ca6-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="96ca6-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="96ca6-195">1</span><span class="sxs-lookup"><span data-stu-id="96ca6-195">1</span></span> |<span data-ttu-id="96ca6-196">1</span><span class="sxs-lookup"><span data-stu-id="96ca6-196">1</span></span> |<span data-ttu-id="96ca6-197">538</span><span class="sxs-lookup"><span data-stu-id="96ca6-197">538</span></span> |<span data-ttu-id="96ca6-198">633</span><span class="sxs-lookup"><span data-stu-id="96ca6-198">633</span></span> |<span data-ttu-id="96ca6-199">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-199">100</span></span> |<span data-ttu-id="96ca6-200">3</span><span class="sxs-lookup"><span data-stu-id="96ca6-200">3</span></span> |<span data-ttu-id="96ca6-201">3</span><span class="sxs-lookup"><span data-stu-id="96ca6-201">3</span></span> |<span data-ttu-id="96ca6-202">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-202">100</span></span> |
| <span data-ttu-id="96ca6-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="96ca6-203">20140522T1100</span></span> |<span data-ttu-id="96ca6-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="96ca6-204">user;UpdateEntity</span></span> |<span data-ttu-id="96ca6-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="96ca6-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="96ca6-206">1</span><span class="sxs-lookup"><span data-stu-id="96ca6-206">1</span></span> |<span data-ttu-id="96ca6-207">1</span><span class="sxs-lookup"><span data-stu-id="96ca6-207">1</span></span> |<span data-ttu-id="96ca6-208">771</span><span class="sxs-lookup"><span data-stu-id="96ca6-208">771</span></span> |<span data-ttu-id="96ca6-209">217</span><span class="sxs-lookup"><span data-stu-id="96ca6-209">217</span></span> |<span data-ttu-id="96ca6-210">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-210">100</span></span> |<span data-ttu-id="96ca6-211">9</span><span class="sxs-lookup"><span data-stu-id="96ca6-211">9</span></span> |<span data-ttu-id="96ca6-212">6</span><span class="sxs-lookup"><span data-stu-id="96ca6-212">6</span></span> |<span data-ttu-id="96ca6-213">100</span><span class="sxs-lookup"><span data-stu-id="96ca6-213">100</span></span> |

<span data-ttu-id="96ca6-214">Este exemplo de dados de métricas de minutos, chave de partição Olá usa tempo de saudação na resolução de minutos.</span><span class="sxs-lookup"><span data-stu-id="96ca6-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="96ca6-215">chave de linha de saudação identifica o tipo de saudação de informações armazenadas em linha hello e isso é composto de duas partes de informações, o tipo de acesso hello e tipo de solicitação de saudação:</span><span class="sxs-lookup"><span data-stu-id="96ca6-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="96ca6-216">tipo de acesso de saudação é o usuário ou sistema, em que o usuário refere-se o serviço de armazenamento do tooall usuário solicitações toohello e refere-se toorequests feitas pela análise de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="96ca6-217">tipo de solicitação de saudação é todos os caso em que é uma linha de resumo, ou ele identifica a API específica hello como QueryEntity ou UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="96ca6-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="96ca6-218">dados de exemplo Hello acima mostra que todos os Olá registra para um único minuto (começando às 11:00 AM), portanto número de saudação de solicitações de QueryEntities mais hello número de solicitações de QueryEntity mais o número de saudação de solicitações de UpdateEntity somar tooseven, que é Olá total mostrado em linha do usuário: All Hello.</span><span class="sxs-lookup"><span data-stu-id="96ca6-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="96ca6-219">Da mesma forma, você pode derivar Olá latência média de ponta a ponta 104,4286 na linha de user: All Olá Calculando ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="96ca6-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="96ca6-220">Alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="96ca6-220">Metrics alerts</span></span>
<span data-ttu-id="96ca6-221">Você deve considerar a configuração de alertas no hello [portal do Azure](https://portal.azure.com) para métricas de armazenamento pode notificá-lo automaticamente de alterações importantes no comportamento de saudação de seus serviços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="96ca6-222">Se você usar esses dados de métricas de um toodownload de ferramenta do Gerenciador de armazenamento em um formato delimitado, você pode usar dados do Microsoft Excel tooanalyze saudação.</span><span class="sxs-lookup"><span data-stu-id="96ca6-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="96ca6-223">Confira [Ferramentas de Cliente do Armazenamento do Azure](storage-explorers.md) para obter uma lista de ferramentas do gerenciador de armazenamento disponíveis.</span><span class="sxs-lookup"><span data-stu-id="96ca6-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="96ca6-224">Você pode configurar alertas em Olá **regras de alerta** folha, acessível em **monitoramento** na folha de menu de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="96ca6-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96ca6-225">Pode haver um atraso entre um evento de armazenamento e quando Olá correspondente de dados de métricas de horas ou minutos é registrado.</span><span class="sxs-lookup"><span data-stu-id="96ca6-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="96ca6-226">No caso de saudação de métricas de minutos, vários minutos de dados podem ser gravados uma vez.</span><span class="sxs-lookup"><span data-stu-id="96ca6-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="96ca6-227">Isso pode levar tootransactions de minutos anteriores que está sendo agregados em transação Olá para Olá minuto atual.</span><span class="sxs-lookup"><span data-stu-id="96ca6-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="96ca6-228">Quando isso acontece, o alerta Olá serviço pode não ter todos os dados de métricas disponíveis para hello configurado intervalo do alerta, que pode levar tooalerts acionamento inesperadamente.</span><span class="sxs-lookup"><span data-stu-id="96ca6-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="96ca6-229">Acessando dados de métrica programaticamente</span><span class="sxs-lookup"><span data-stu-id="96ca6-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="96ca6-230">Olá lista a seguir mostra exemplo código c# que acessa as métricas de minutos de saudação para um intervalo de minutos e exibe os resultados de saudação em uma janela do console.</span><span class="sxs-lookup"><span data-stu-id="96ca6-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="96ca6-231">Ele usa Olá biblioteca de armazenamento do Azure versão 4, que inclui Olá CloudAnalyticsClient classe que simplifica ao acessar tabelas de métricas de saudação no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96ca6-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="96ca6-232">Quais taxas você provoca quando habilita a métrica de armazenamento?</span><span class="sxs-lookup"><span data-stu-id="96ca6-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="96ca6-233">Grave solicitações toocreate de entidades de tabela para métricas são cobradas a operações de armazenamento do Azure Olá taxas padrão tooall aplicável.</span><span class="sxs-lookup"><span data-stu-id="96ca6-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="96ca6-234">Solicitações de leitura e exclusão por um toometrics de dados do cliente também são faturáveis com taxas padrão.</span><span class="sxs-lookup"><span data-stu-id="96ca6-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="96ca6-235">Se você configurou uma política de retenção de dados, que não seja cobrado quando o armazenamento do Azure excluir dados de métricas antigos.</span><span class="sxs-lookup"><span data-stu-id="96ca6-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="96ca6-236">No entanto, se você excluir dados de análise, sua conta é cobrada Olá para operações de exclusão.</span><span class="sxs-lookup"><span data-stu-id="96ca6-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="96ca6-237">capacidade de saudação usada por tabelas de métricas de saudação também é cobrável: você pode usar o hello tooestimate quantidade de saudação do usado para armazenar dados de métricas de capacidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="96ca6-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="96ca6-238">Se a cada hora um serviço utilizar cada API em cada serviço, cerca de 148KB de dados é armazenado nas tabelas de transações de métricas de saudação a cada hora se você tiver ativado o serviço e o resumo de nível de API.</span><span class="sxs-lookup"><span data-stu-id="96ca6-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="96ca6-239">Se a cada hora um serviço utilizar cada API em cada serviço, cerca de 12KB de dados é armazenado nas tabelas de transações de métricas de saudação a cada hora se você tiver habilitado o nível de serviço apenas resumo.</span><span class="sxs-lookup"><span data-stu-id="96ca6-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="96ca6-240">Olá, tabela de capacidade para blobs tem duas linhas adicionadas por dia (fornecida pelo usuário tenha optado pelos logs): isso implica que cada dia Olá tamanho dessa tabela aumenta conforme o tooapproximately 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="96ca6-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96ca6-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96ca6-241">Next steps</span></span>
[<span data-ttu-id="96ca6-242">Habilitando o armazenamento de log e acessando os dados de log</span><span class="sxs-lookup"><span data-stu-id="96ca6-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
