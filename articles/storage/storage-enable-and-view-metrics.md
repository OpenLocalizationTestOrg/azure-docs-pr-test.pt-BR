---
title: "Habilitando métricas de armazenamento no Portal do Azure | Microsoft Docs"
description: "Como habilitar métricas de armazenamento para os serviços Blob, Fila, Tabela e Arquivo"
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
ms.openlocfilehash: 2906f808482d0b990e3ddd31ef5368e9fdd9f646
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="2e804-103">Habilitando métricas do Armazenamento do Azure e exibição de dados de métricas</span><span class="sxs-lookup"><span data-stu-id="2e804-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="2e804-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2e804-104">Overview</span></span>
<span data-ttu-id="2e804-105">As Métricas de Armazenamento são habilitadas por padrão quando você cria uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="2e804-106">Você pode configurar o monitoramento por meio do [Portal do Azure](https://portal.azure.com) ou o Windows PowerShell ou programaticamente por meio de uma das bibliotecas de cliente de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span></span>

<span data-ttu-id="2e804-107">Você pode configurar um período de retenção para os dados de métricas: este período determina quanto tempo o serviço de armazenamento mantém as métricas e as cobranças para o espaço necessário para armazená-los.</span><span class="sxs-lookup"><span data-stu-id="2e804-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="2e804-108">Normalmente, você deve usar um período de retenção mais curto para métricas de minuto em vez de métricas por hora por causa do espaço extra significativo necessário para métricas de minuto.</span><span class="sxs-lookup"><span data-stu-id="2e804-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="2e804-109">Você deve escolher um período de retenção que você tenha tempo suficiente para analisar os dados e baixar qualquer métricas que você deseja manter para análise offline ou para fins de relatório.</span><span class="sxs-lookup"><span data-stu-id="2e804-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="2e804-110">Lembre-se de que você também será cobrado para baixar dados de métrica de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-metrics-using-the-azure-portal"></a><span data-ttu-id="2e804-111">Como habilitar métricas usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2e804-111">How to enable metrics using the Azure portal</span></span>
<span data-ttu-id="2e804-112">Siga estas etapas para habilitar as métricas no [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="2e804-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="2e804-113">Navegue até sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-113">Navigate to your storage account.</span></span>
1. <span data-ttu-id="2e804-114">Selecione **diagnóstico** sobre o **Menu** folha</span><span class="sxs-lookup"><span data-stu-id="2e804-114">Select **Diagnostics** on the **Menu** blade</span></span>
1. <span data-ttu-id="2e804-115">O **Status** deve ser definido como **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="2e804-115">Ensure that **Status** is set to **On**.</span></span>
1. <span data-ttu-id="2e804-116">Selecione as métricas para os serviços que deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="2e804-116">Select the metrics for the services you wish to monitor.</span></span>
1. <span data-ttu-id="2e804-117">Especifica uma política de retenção para indicar por quanto tempo deve-se manter as métricas e os dados de log.</span><span class="sxs-lookup"><span data-stu-id="2e804-117">Specify a retention policy to indicate how long to retain metrics and log data.</span></span>
1. <span data-ttu-id="2e804-118">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2e804-118">Select **Save**.</span></span>

<span data-ttu-id="2e804-119">Observe que o [portal do Azure](https://portal.azure.com) não permite atualmente configurar métricas de minuto em sua conta de armazenamento. Habilite a métrica de minutos usando o PowerShell ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="2e804-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-metrics-using-powershell"></a><span data-ttu-id="2e804-120">Como habilitar métricas usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e804-120">How to enable metrics using PowerShell</span></span>
<span data-ttu-id="2e804-121">Você pode usar o PowerShell no computador local para configurar as métricas de armazenamento na sua conta de armazenamento usando o cmdlet do PowerShell do Azure Get-AzureStorageServiceMetricsProperty para recuperar as configurações atuais, e o cmdlet Set-AzureStorageServiceMetricsProperty para alterar as configurações atuais.</span><span class="sxs-lookup"><span data-stu-id="2e804-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="2e804-122">Os cmdlets que controlam as métricas de armazenamento usam os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2e804-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="2e804-123">Os valorespossíveis de MetricsType são hora e minuto.</span><span class="sxs-lookup"><span data-stu-id="2e804-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="2e804-124">ServiceType: os possíveis valores são Blob, Fila e Tabela.</span><span class="sxs-lookup"><span data-stu-id="2e804-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="2e804-125">MetricsLevel: os valores possíveis são None, Serviço e ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="2e804-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="2e804-126">Por exemplo, o comando a seguir ativa a métrica de minutos para o Serviço Blob na conta de armazenamento padrão com o período de retenção definido para cinco dias:</span><span class="sxs-lookup"><span data-stu-id="2e804-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="2e804-127">O comando a seguir recupera o nível de métricas por hora atual e dias de retenção para o serviço blob na conta de armazenamento padrão:</span><span class="sxs-lookup"><span data-stu-id="2e804-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="2e804-128">Para saber mais sobre como configurar os cmdlets do PowerShell do Azure para funcionar com sua assinatura do Azure e como selecionar a conta de armazenamento padrão para usar, consulte: [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e804-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="2e804-129">Como habilitar métricas de armazenamento por meio de programação</span><span class="sxs-lookup"><span data-stu-id="2e804-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="2e804-130">O trecho em C# a seguir mostra como habilitar métricas e a criação de log para o serviço Blob usando a biblioteca de cliente de armazenamento para .NET:</span><span class="sxs-lookup"><span data-stu-id="2e804-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="2e804-131">Exibindo as métricas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2e804-131">Viewing Storage metrics</span></span>
<span data-ttu-id="2e804-132">Após configurar as métricas Análise de Armazenamento para monitorar sua conta de armazenamento, a Análise de Armazenamento registra as métricas em um conjunto conhecido de tabelas na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="2e804-133">Você pode configurar gráficos para exibir as métricas por hora no [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="2e804-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="2e804-134">Navegue até sua conta de armazenamento no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e804-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2e804-135">Selecione **métricas** no **Menu** folha para o serviço cujas métricas que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="2e804-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span></span>
1. <span data-ttu-id="2e804-136">Selecione **editar** no gráfico que você deseja configurar.</span><span class="sxs-lookup"><span data-stu-id="2e804-136">Select **Edit** on the chart you want to configure.</span></span>
1. <span data-ttu-id="2e804-137">No **Editar gráfico** folha, selecione o **intervalo de tempo**, **tipo de gráfico**e as métricas que deseja exibir no gráfico.</span><span class="sxs-lookup"><span data-stu-id="2e804-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span></span>
1. <span data-ttu-id="2e804-138">Selecione **OK**</span><span class="sxs-lookup"><span data-stu-id="2e804-138">Select **OK**</span></span>

<span data-ttu-id="2e804-139">Se você quiser baixar as métricas para armazenamento de longo prazo ou para analisá-las localmente, precisará:</span><span class="sxs-lookup"><span data-stu-id="2e804-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span></span>

* <span data-ttu-id="2e804-140">Usar uma ferramenta que reconheça essas tabelas e permita que você as exiba e as baixe.</span><span class="sxs-lookup"><span data-stu-id="2e804-140">Use a tool that is aware of these tables and will allow you to view and download them.</span></span>
* <span data-ttu-id="2e804-141">Escrever um aplicativo ou script personalizado para ler e armazenar as tabelas.</span><span class="sxs-lookup"><span data-stu-id="2e804-141">Write a custom application or script to read and store the tables.</span></span>

<span data-ttu-id="2e804-142">Muitas ferramentas de navegação de armazenamento de terceiros reconhecem essas tabelas e permitem que você as exiba diretamente.</span><span class="sxs-lookup"><span data-stu-id="2e804-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span></span>
<span data-ttu-id="2e804-143">Confira [Ferramentas de Cliente do Armazenamento do Azure](storage-explorers.md) para obter uma lista de ferramentas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2e804-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="2e804-144">Da versão 0.8.0 do [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/) em diante, você pode exibir e baixar as tabelas de métricas de análise.</span><span class="sxs-lookup"><span data-stu-id="2e804-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="2e804-145">Para acessar as tabelas de análise de forma programática, observe que as tabelas de análise não são mostradas quando você lista todas as tabelas em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span></span> <span data-ttu-id="2e804-146">Você pode acessá-las diretamente por nome ou usar [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) na biblioteca de cliente .NET para consultar os nomes de tabela.</span><span class="sxs-lookup"><span data-stu-id="2e804-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="2e804-147">Métricas por hora</span><span class="sxs-lookup"><span data-stu-id="2e804-147">Hourly metrics</span></span>
* <span data-ttu-id="2e804-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="2e804-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="2e804-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="2e804-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="2e804-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="2e804-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="2e804-151">Métricas por minuto</span><span class="sxs-lookup"><span data-stu-id="2e804-151">Minute metrics</span></span>
* <span data-ttu-id="2e804-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="2e804-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="2e804-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="2e804-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="2e804-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="2e804-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="2e804-155">Capacidade</span><span class="sxs-lookup"><span data-stu-id="2e804-155">Capacity</span></span>
* <span data-ttu-id="2e804-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="2e804-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="2e804-157">Você pode encontrar detalhes completos dos esquemas para essas tabelas no [Esquema da tabela de métricas da análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e804-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="2e804-158">As linhas de exemplo a seguir mostram apenas um subconjunto das colunas disponíveis, mas ilustram alguns recursos importantes da maneira como as métricas de armazenamento salvam essas métricas:</span><span class="sxs-lookup"><span data-stu-id="2e804-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="2e804-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="2e804-159">PartitionKey</span></span> | <span data-ttu-id="2e804-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="2e804-160">RowKey</span></span> | <span data-ttu-id="2e804-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2e804-161">Timestamp</span></span> | <span data-ttu-id="2e804-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="2e804-162">TotalRequests</span></span> | <span data-ttu-id="2e804-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="2e804-163">TotalBillableRequests</span></span> | <span data-ttu-id="2e804-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="2e804-164">TotalIngress</span></span> | <span data-ttu-id="2e804-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="2e804-165">TotalEgress</span></span> | <span data-ttu-id="2e804-166">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="2e804-166">Availability</span></span> | <span data-ttu-id="2e804-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="2e804-167">AverageE2ELatency</span></span> | <span data-ttu-id="2e804-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="2e804-168">AverageServerLatency</span></span> | <span data-ttu-id="2e804-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="2e804-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2e804-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="2e804-170">20140522T1100</span></span> |<span data-ttu-id="2e804-171">user;All</span><span class="sxs-lookup"><span data-stu-id="2e804-171">user;All</span></span> |<span data-ttu-id="2e804-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="2e804-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="2e804-173">7</span><span class="sxs-lookup"><span data-stu-id="2e804-173">7</span></span> |<span data-ttu-id="2e804-174">7</span><span class="sxs-lookup"><span data-stu-id="2e804-174">7</span></span> |<span data-ttu-id="2e804-175">4003</span><span class="sxs-lookup"><span data-stu-id="2e804-175">4003</span></span> |<span data-ttu-id="2e804-176">46801</span><span class="sxs-lookup"><span data-stu-id="2e804-176">46801</span></span> |<span data-ttu-id="2e804-177">100</span><span class="sxs-lookup"><span data-stu-id="2e804-177">100</span></span> |<span data-ttu-id="2e804-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="2e804-178">104.4286</span></span> |<span data-ttu-id="2e804-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="2e804-179">6.857143</span></span> |<span data-ttu-id="2e804-180">100</span><span class="sxs-lookup"><span data-stu-id="2e804-180">100</span></span> |
| <span data-ttu-id="2e804-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="2e804-181">20140522T1100</span></span> |<span data-ttu-id="2e804-182">usuário;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="2e804-182">user;QueryEntities</span></span> |<span data-ttu-id="2e804-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="2e804-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="2e804-184">5</span><span class="sxs-lookup"><span data-stu-id="2e804-184">5</span></span> |<span data-ttu-id="2e804-185">5</span><span class="sxs-lookup"><span data-stu-id="2e804-185">5</span></span> |<span data-ttu-id="2e804-186">2694</span><span class="sxs-lookup"><span data-stu-id="2e804-186">2694</span></span> |<span data-ttu-id="2e804-187">45951</span><span class="sxs-lookup"><span data-stu-id="2e804-187">45951</span></span> |<span data-ttu-id="2e804-188">100</span><span class="sxs-lookup"><span data-stu-id="2e804-188">100</span></span> |<span data-ttu-id="2e804-189">143.8</span><span class="sxs-lookup"><span data-stu-id="2e804-189">143.8</span></span> |<span data-ttu-id="2e804-190">7.8</span><span class="sxs-lookup"><span data-stu-id="2e804-190">7.8</span></span> |<span data-ttu-id="2e804-191">100</span><span class="sxs-lookup"><span data-stu-id="2e804-191">100</span></span> |
| <span data-ttu-id="2e804-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="2e804-192">20140522T1100</span></span> |<span data-ttu-id="2e804-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="2e804-193">user;QueryEntity</span></span> |<span data-ttu-id="2e804-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="2e804-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="2e804-195">1</span><span class="sxs-lookup"><span data-stu-id="2e804-195">1</span></span> |<span data-ttu-id="2e804-196">1</span><span class="sxs-lookup"><span data-stu-id="2e804-196">1</span></span> |<span data-ttu-id="2e804-197">538</span><span class="sxs-lookup"><span data-stu-id="2e804-197">538</span></span> |<span data-ttu-id="2e804-198">633</span><span class="sxs-lookup"><span data-stu-id="2e804-198">633</span></span> |<span data-ttu-id="2e804-199">100</span><span class="sxs-lookup"><span data-stu-id="2e804-199">100</span></span> |<span data-ttu-id="2e804-200">3</span><span class="sxs-lookup"><span data-stu-id="2e804-200">3</span></span> |<span data-ttu-id="2e804-201">3</span><span class="sxs-lookup"><span data-stu-id="2e804-201">3</span></span> |<span data-ttu-id="2e804-202">100</span><span class="sxs-lookup"><span data-stu-id="2e804-202">100</span></span> |
| <span data-ttu-id="2e804-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="2e804-203">20140522T1100</span></span> |<span data-ttu-id="2e804-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="2e804-204">user;UpdateEntity</span></span> |<span data-ttu-id="2e804-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="2e804-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="2e804-206">1</span><span class="sxs-lookup"><span data-stu-id="2e804-206">1</span></span> |<span data-ttu-id="2e804-207">1</span><span class="sxs-lookup"><span data-stu-id="2e804-207">1</span></span> |<span data-ttu-id="2e804-208">771</span><span class="sxs-lookup"><span data-stu-id="2e804-208">771</span></span> |<span data-ttu-id="2e804-209">217</span><span class="sxs-lookup"><span data-stu-id="2e804-209">217</span></span> |<span data-ttu-id="2e804-210">100</span><span class="sxs-lookup"><span data-stu-id="2e804-210">100</span></span> |<span data-ttu-id="2e804-211">9</span><span class="sxs-lookup"><span data-stu-id="2e804-211">9</span></span> |<span data-ttu-id="2e804-212">6</span><span class="sxs-lookup"><span data-stu-id="2e804-212">6</span></span> |<span data-ttu-id="2e804-213">100</span><span class="sxs-lookup"><span data-stu-id="2e804-213">100</span></span> |

<span data-ttu-id="2e804-214">Neste exemplo dos dados de métrica de minutos, a chave de partição usa o tempo de resolução minuto.</span><span class="sxs-lookup"><span data-stu-id="2e804-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="2e804-215">A chave de linha identifica o tipo de informação que é armazenado na linha, e isso é composto de duas partes de informações, o tipo de acesso e o tipo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="2e804-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="2e804-216">O tipo de acesso é um usuário ou sistema, onde o usuário refere-se a todas as solicitações de usuário para o serviço de armazenamento e o sistema refere-se às solicitações feitas pela análise de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="2e804-217">O tipo de solicitação é tudo que nesse caso é uma linha de resumo, ou ele identifica a API específica, como QueryEntity ou UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="2e804-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="2e804-218">Os dados de exemplo acima mostram todos os registros de um minuto (iniciando às 11h00), para o número de solicitações de QueryEntities mais o número de solicitações de QueryEntity mais o número de solicitações de UpdateEntity adicionam até sete, que é o total mostrado na linha user:All.</span><span class="sxs-lookup"><span data-stu-id="2e804-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="2e804-219">Da mesma forma, você pode derivar a latência média de ponta a ponta 104.4286 na linha user:All ao calcular ((143.8 * 5) + 3 + 9)/7.</span><span class="sxs-lookup"><span data-stu-id="2e804-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="2e804-220">Alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="2e804-220">Metrics alerts</span></span>
<span data-ttu-id="2e804-221">Considere configurar alertas no [Portal do Azure](https://portal.azure.com) para que as Métricas de Armazenamento possam notificá-lo automaticamente sobre todas as alterações importantes no comportamento dos seus serviços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span></span> <span data-ttu-id="2e804-222">Se você usar uma ferramenta de Gerenciador de armazenamento para baixar esses dados de métricas em um formato delimitado, você pode usar o Microsoft Excel para analisar os dados.</span><span class="sxs-lookup"><span data-stu-id="2e804-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="2e804-223">Confira [Ferramentas de Cliente do Armazenamento do Azure](storage-explorers.md) para obter uma lista de ferramentas do gerenciador de armazenamento disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2e804-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="2e804-224">Você pode configurar alertas na folha **Regras de alerta**, acessível em **Monitoramento** na folha Menu da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e804-225">Pode haver um atraso entre um evento de armazenamento e quando os dados de métricas por hora ou minuto correspondentes são registrados.</span><span class="sxs-lookup"><span data-stu-id="2e804-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="2e804-226">No caso de métricas por minuto, diversos minutos de dados podem ser gravados de uma só vez.</span><span class="sxs-lookup"><span data-stu-id="2e804-226">In the case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="2e804-227">Isso pode levar à agregação de transações de minutos anteriores à transação do minuto atual.</span><span class="sxs-lookup"><span data-stu-id="2e804-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span></span> <span data-ttu-id="2e804-228">Quando isso acontece, o serviço de alerta pode não ter todos os dados de métricas disponíveis para o intervalo de alerta configurado, o que pode levar ao acionamento inesperado de alertas.</span><span class="sxs-lookup"><span data-stu-id="2e804-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="2e804-229">Acessando dados de métrica programaticamente</span><span class="sxs-lookup"><span data-stu-id="2e804-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="2e804-230">A listagem a seguir mostra o código C# de exemplo, que acessa a métrica de minutos para um intervalo de minutos e exibe os resultados em uma janela de console.</span><span class="sxs-lookup"><span data-stu-id="2e804-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="2e804-231">Ele usa a biblioteca de armazenamento do Azure versão 4, o que inclui a classe CloudAnalyticsClient que simplifica o acesso às tabelas de métricas no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e804-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="2e804-232">Quais taxas você provoca quando habilita a métrica de armazenamento?</span><span class="sxs-lookup"><span data-stu-id="2e804-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="2e804-233">Gravar solicitações para criar entidades de tabela para métricas são cobradas de acordo com as taxas padrão aplicáveis a todas as operações de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e804-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="2e804-234">Solicitações de leitura e exclusão por um cliente para dados de métrica também são faturáveis em taxas padrão.</span><span class="sxs-lookup"><span data-stu-id="2e804-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="2e804-235">Se você configurou uma política de retenção de dados, que não seja cobrado quando o armazenamento do Azure excluir dados de métricas antigos.</span><span class="sxs-lookup"><span data-stu-id="2e804-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="2e804-236">No entanto, se você excluir dados de análise, sua conta será cobrada para as operações de exclusão.</span><span class="sxs-lookup"><span data-stu-id="2e804-236">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="2e804-237">A capacidade usada pelas tabelas de métricas também é faturável. Você pode usar o seguinte para estimar a quantidade de capacidade usada para armazenar dados de métricas:</span><span class="sxs-lookup"><span data-stu-id="2e804-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="2e804-238">Se cada hora de um serviço utiliza todas as APIs de cada serviço, então aproximadamente 148KB de dados serão armazenados nas tabelas de transações de métricas a cada hora se você tiver habilitado o serviço e o resumo de nível de API.</span><span class="sxs-lookup"><span data-stu-id="2e804-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="2e804-239">Se cada hora de um serviço utiliza todas as APIs de cada serviço, então cerca de 12KB de dados serão armazenados nas tabelas de transação de métricas a cada hora se você tiver habilitado apenas o resumo do nível de serviço.</span><span class="sxs-lookup"><span data-stu-id="2e804-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="2e804-240">A tabela de capacidade para blobs tem duas linhas adicionadas por dia (fornecida pelo usuário que optou pelos logs). Isso implica que todos os dias o tamanho dessa tabela aumenta em até aproximadamente 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="2e804-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e804-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e804-241">Next steps</span></span>
[<span data-ttu-id="2e804-242">Habilitando o armazenamento de log e acessando os dados de log</span><span class="sxs-lookup"><span data-stu-id="2e804-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
