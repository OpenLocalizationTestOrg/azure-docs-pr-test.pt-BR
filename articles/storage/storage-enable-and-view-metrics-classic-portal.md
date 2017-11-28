---
title: "Habilitando métricas de armazenamento no Portal do Azure | Microsoft Docs"
description: "Como habilitar métricas de armazenamento para os serviços Blob, Fila, Tabela e Arquivo"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4d6065597a41372ea6d320ab318b0c71d6a48b2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="322e3-103">Habilitando métricas de armazenamento e exibição de dados de métricas</span><span class="sxs-lookup"><span data-stu-id="322e3-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="322e3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="322e3-104">Overview</span></span>
<span data-ttu-id="322e3-105">As Métricas de Armazenamento são habilitadas por padrão quando você cria uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="322e3-106">É possível configurar o monitoramento usando o [Portal Clássico do Azure](https://manage.windowsazure.com), o Windows PowerShell ou de forma programática por meio de uma API de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-106">You can configure monitoring using either the [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="322e3-107">Quando você habilita as métricas de armazenamento, você deve escolher um período de retenção para os dados: este período determina quanto tempo o serviço de armazenamento mantém as métricas e as cobranças para o espaço necessário para armazená-los.</span><span class="sxs-lookup"><span data-stu-id="322e3-107">When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="322e3-108">Normalmente, você deve usar um período de retenção mais curto para métricas de minuto em vez de métricas por hora por causa do espaço extra significativo necessário para métricas de minuto.</span><span class="sxs-lookup"><span data-stu-id="322e3-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="322e3-109">Você deve escolher um período de retenção que você tenha tempo suficiente para analisar os dados e baixar qualquer métricas que você deseja manter para análise offline ou para fins de relatório.</span><span class="sxs-lookup"><span data-stu-id="322e3-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="322e3-110">Lembre-se de que você também será cobrado para baixar dados de métrica de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-storage-metrics-using-the-azure-classic-portal"></a><span data-ttu-id="322e3-111">Como habilitar métricas de Armazenamento usando o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="322e3-111">How to enable Storage metrics using the Azure Classic Portal</span></span>
<span data-ttu-id="322e3-112">No [Portal clássico do Azure](https://manage.windowsazure.com), você pode usar a página Configurar para uma conta de armazenamento para controlar Métricas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-112">In the [Azure Classic Portal](https://manage.windowsazure.com), you use the Configure page for a storage account to control Storage Metrics.</span></span> <span data-ttu-id="322e3-113">Para monitoramento, você pode definir um nível e um período de retenção em dias para cada um dos blobs, tabelas e filas.</span><span class="sxs-lookup"><span data-stu-id="322e3-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="322e3-114">Em cada caso, o nível é um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="322e3-114">In each case, the level is one of the following:</span></span>

* <span data-ttu-id="322e3-115">Desativado — nenhuma métrica será coletada.</span><span class="sxs-lookup"><span data-stu-id="322e3-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="322e3-116">Mínimo — as métricas de armazenamento coletam um conjunto básico de métricas como ingresso/egresso, disponibilidade, latência e porcentagens de êxitos, que são agregadas para os serviços Blob, tabela e fila.</span><span class="sxs-lookup"><span data-stu-id="322e3-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="322e3-117">Detalhado — as métricas de armazenamento coletam um conjunto completo de métricas que inclui as mesmas métricas para cada operação de API, além das métricas de nível de serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-117">Verbose — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics.</span></span> <span data-ttu-id="322e3-118">As métricas no modo detalhado permitem uma análise mais próxima dos problemas que ocorrem durante operações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="322e3-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="322e3-119">Observe que o Portal clássico do Azure não permite atualmente configurar métricas por minuto em sua conta de armazenamento. Você deve habilitar a métrica de minutos usando o PowerShell ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="322e3-119">Note that the Azure Classic Portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-storage-metrics-using-powershell"></a><span data-ttu-id="322e3-120">Como habilitar métricas de armazenamento usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="322e3-120">How to enable Storage metrics using PowerShell</span></span>
<span data-ttu-id="322e3-121">Você pode usar o PowerShell no computador local para configurar as métricas de armazenamento na sua conta de armazenamento usando o cmdlet do PowerShell do Azure Get-AzureStorageServiceMetricsProperty para recuperar as configurações atuais, e o cmdlet Set-AzureStorageServiceMetricsProperty para alterar as configurações atuais.</span><span class="sxs-lookup"><span data-stu-id="322e3-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="322e3-122">Os cmdlets que controlam as métricas de armazenamento usam os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="322e3-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="322e3-123">Os valorespossíveis de MetricsType são hora e minuto.</span><span class="sxs-lookup"><span data-stu-id="322e3-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="322e3-124">Os possíveis valores de ServiceType são Blob, Fila e Tabela.</span><span class="sxs-lookup"><span data-stu-id="322e3-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="322e3-125">Os valores possíveis de MetricsLevel são None (equivalente a Desativado no Portal clássico do Azure), Service (equivalente ao Mínimo no Portal clássico do Azure) e ServiceAndApi (equivalente a Detalhado no Portal clássico do Azure).</span><span class="sxs-lookup"><span data-stu-id="322e3-125">MetricsLevel possible values are None (equivalent to Off in the Azure Classic Portal), Service (equivalent to Minimal in the Azure Classic Portal), and ServiceAndApi (equivalent to Verbose in the Azure Classic Portal).</span></span>

<span data-ttu-id="322e3-126">Por exemplo, o comando a seguir ativa a métrica de minutos para o serviço blob na conta de armazenamento padrão com o período de retenção definido para cinco dias:</span><span class="sxs-lookup"><span data-stu-id="322e3-126">For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="322e3-127">O comando a seguir recupera o nível de métricas por hora atual e dias de retenção para o serviço blob na conta de armazenamento padrão:</span><span class="sxs-lookup"><span data-stu-id="322e3-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="322e3-128">Para saber mais sobre como configurar os cmdlets do PowerShell do Azure para funcionar com sua assinatura do Azure e como selecionar a conta de armazenamento padrão para usar, consulte: [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="322e3-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="322e3-129">Como habilitar métricas de armazenamento por meio de programação</span><span class="sxs-lookup"><span data-stu-id="322e3-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="322e3-130">O trecho em C# a seguir mostra como habilitar métricas e a criação de log para o serviço Blob usando a biblioteca de cliente de armazenamento para .NET:</span><span class="sxs-lookup"><span data-stu-id="322e3-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="322e3-131">Exibindo as métricas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="322e3-131">Viewing Storage metrics</span></span>
<span data-ttu-id="322e3-132">Quando você tiver configurado as métricas de armazenamento para monitorar sua conta de armazenamento, ela registra as métricas em um conjunto de tabelas conhecido na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-132">When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="322e3-133">Você pode usar a página de Monitorar para sua conta de armazenamento no Portal clássico do Azure para exibir as métricas de hora assim que forem disponibilizadas em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="322e3-133">You can use the Monitor page for your storage account in the Azure Classic Portal to view the hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="322e3-134">Nesta página no Portal clássico do Azure, você pode:</span><span class="sxs-lookup"><span data-stu-id="322e3-134">On this page in the Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="322e3-135">Selecionar quais métricas plotar no gráfico (a opção de métricas disponíveis dependerá se você escolheu o monitoramento detalhado ou mínimo para o serviço na página Configurar).</span><span class="sxs-lookup"><span data-stu-id="322e3-135">Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the Configure page).</span></span>
* <span data-ttu-id="322e3-136">Selecionar o intervalo de tempo para as métricas exibidas no gráfico.</span><span class="sxs-lookup"><span data-stu-id="322e3-136">Select the time range for the metrics displayed on the chart.</span></span>
* <span data-ttu-id="322e3-137">Optar por usar um dimensionamento absoluto ou relativo para plotar as métricas.</span><span class="sxs-lookup"><span data-stu-id="322e3-137">Choose to use an absolute or relative scale to plot the metrics.</span></span>
* <span data-ttu-id="322e3-138">Configurar alertas de email para notificar quando uma métrica específica atinge um determinado valor.</span><span class="sxs-lookup"><span data-stu-id="322e3-138">Configure email alerts to notify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="322e3-139">Se você quiser baixar as métricas para armazenamento a longo prazo ou para analisá-las localmente, você precisará usar uma ferramenta ou escrever um código para ler as tabelas.</span><span class="sxs-lookup"><span data-stu-id="322e3-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables.</span></span> <span data-ttu-id="322e3-140">Você deve baixar a métrica de minutos para análise.</span><span class="sxs-lookup"><span data-stu-id="322e3-140">You must download the minute metrics for analysis.</span></span> <span data-ttu-id="322e3-141">As tabelas não aparecem quando você lista todas as tabelas em sua conta de armazenamento, mas você pode acessá-las diretamente por nome.</span><span class="sxs-lookup"><span data-stu-id="322e3-141">The tables do not appear if you list all the tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="322e3-142">Muitas ferramentas de navegação de armazenamento de terceiros estão cientes dessas tabelas e permitem que você as exiba diretamente (consulte a postagem do blog [Gerenciadores de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) para obter uma lista de ferramentas disponíveis).</span><span class="sxs-lookup"><span data-stu-id="322e3-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="322e3-143">Métricas por hora</span><span class="sxs-lookup"><span data-stu-id="322e3-143">Hourly metrics</span></span>
* <span data-ttu-id="322e3-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="322e3-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="322e3-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="322e3-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="322e3-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="322e3-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="322e3-147">Métricas por minuto</span><span class="sxs-lookup"><span data-stu-id="322e3-147">Minute metrics</span></span>
* <span data-ttu-id="322e3-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="322e3-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="322e3-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="322e3-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="322e3-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="322e3-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="322e3-151">Capacidade</span><span class="sxs-lookup"><span data-stu-id="322e3-151">Capacity</span></span>
* <span data-ttu-id="322e3-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="322e3-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="322e3-153">Você pode encontrar detalhes completos dos esquemas para essas tabelas no [Esquema da tabela de métricas da análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="322e3-153">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="322e3-154">As linhas de exemplo a seguir mostram apenas um subconjunto das colunas disponíveis, mas ilustram alguns recursos importantes da maneira como as métricas de armazenamento salvam essas métricas:</span><span class="sxs-lookup"><span data-stu-id="322e3-154">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="322e3-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="322e3-155">PartitionKey</span></span> | <span data-ttu-id="322e3-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="322e3-156">RowKey</span></span> | <span data-ttu-id="322e3-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="322e3-157">Timestamp</span></span> | <span data-ttu-id="322e3-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="322e3-158">TotalRequests</span></span> | <span data-ttu-id="322e3-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="322e3-159">TotalBillableRequests</span></span> | <span data-ttu-id="322e3-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="322e3-160">TotalIngress</span></span> | <span data-ttu-id="322e3-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="322e3-161">TotalEgress</span></span> | <span data-ttu-id="322e3-162">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="322e3-162">Availability</span></span> | <span data-ttu-id="322e3-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="322e3-163">AverageE2ELatency</span></span> | <span data-ttu-id="322e3-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="322e3-164">AverageServerLatency</span></span> | <span data-ttu-id="322e3-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="322e3-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="322e3-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="322e3-166">20140522T1100</span></span> |<span data-ttu-id="322e3-167">user;All</span><span class="sxs-lookup"><span data-stu-id="322e3-167">user;All</span></span> |<span data-ttu-id="322e3-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="322e3-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="322e3-169">7</span><span class="sxs-lookup"><span data-stu-id="322e3-169">7</span></span> |<span data-ttu-id="322e3-170">7</span><span class="sxs-lookup"><span data-stu-id="322e3-170">7</span></span> |<span data-ttu-id="322e3-171">4003</span><span class="sxs-lookup"><span data-stu-id="322e3-171">4003</span></span> |<span data-ttu-id="322e3-172">46801</span><span class="sxs-lookup"><span data-stu-id="322e3-172">46801</span></span> |<span data-ttu-id="322e3-173">100</span><span class="sxs-lookup"><span data-stu-id="322e3-173">100</span></span> |<span data-ttu-id="322e3-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="322e3-174">104.4286</span></span> |<span data-ttu-id="322e3-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="322e3-175">6.857143</span></span> |<span data-ttu-id="322e3-176">100</span><span class="sxs-lookup"><span data-stu-id="322e3-176">100</span></span> |
| <span data-ttu-id="322e3-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="322e3-177">20140522T1100</span></span> |<span data-ttu-id="322e3-178">usuário;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="322e3-178">user;QueryEntities</span></span> |<span data-ttu-id="322e3-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="322e3-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="322e3-180">5</span><span class="sxs-lookup"><span data-stu-id="322e3-180">5</span></span> |<span data-ttu-id="322e3-181">5</span><span class="sxs-lookup"><span data-stu-id="322e3-181">5</span></span> |<span data-ttu-id="322e3-182">2694</span><span class="sxs-lookup"><span data-stu-id="322e3-182">2694</span></span> |<span data-ttu-id="322e3-183">45951</span><span class="sxs-lookup"><span data-stu-id="322e3-183">45951</span></span> |<span data-ttu-id="322e3-184">100</span><span class="sxs-lookup"><span data-stu-id="322e3-184">100</span></span> |<span data-ttu-id="322e3-185">143.8</span><span class="sxs-lookup"><span data-stu-id="322e3-185">143.8</span></span> |<span data-ttu-id="322e3-186">7.8</span><span class="sxs-lookup"><span data-stu-id="322e3-186">7.8</span></span> |<span data-ttu-id="322e3-187">100</span><span class="sxs-lookup"><span data-stu-id="322e3-187">100</span></span> |
| <span data-ttu-id="322e3-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="322e3-188">20140522T1100</span></span> |<span data-ttu-id="322e3-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="322e3-189">user;QueryEntity</span></span> |<span data-ttu-id="322e3-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="322e3-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="322e3-191">1</span><span class="sxs-lookup"><span data-stu-id="322e3-191">1</span></span> |<span data-ttu-id="322e3-192">1</span><span class="sxs-lookup"><span data-stu-id="322e3-192">1</span></span> |<span data-ttu-id="322e3-193">538</span><span class="sxs-lookup"><span data-stu-id="322e3-193">538</span></span> |<span data-ttu-id="322e3-194">633</span><span class="sxs-lookup"><span data-stu-id="322e3-194">633</span></span> |<span data-ttu-id="322e3-195">100</span><span class="sxs-lookup"><span data-stu-id="322e3-195">100</span></span> |<span data-ttu-id="322e3-196">3</span><span class="sxs-lookup"><span data-stu-id="322e3-196">3</span></span> |<span data-ttu-id="322e3-197">3</span><span class="sxs-lookup"><span data-stu-id="322e3-197">3</span></span> |<span data-ttu-id="322e3-198">100</span><span class="sxs-lookup"><span data-stu-id="322e3-198">100</span></span> |
| <span data-ttu-id="322e3-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="322e3-199">20140522T1100</span></span> |<span data-ttu-id="322e3-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="322e3-200">user;UpdateEntity</span></span> |<span data-ttu-id="322e3-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="322e3-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="322e3-202">1</span><span class="sxs-lookup"><span data-stu-id="322e3-202">1</span></span> |<span data-ttu-id="322e3-203">1</span><span class="sxs-lookup"><span data-stu-id="322e3-203">1</span></span> |<span data-ttu-id="322e3-204">771</span><span class="sxs-lookup"><span data-stu-id="322e3-204">771</span></span> |<span data-ttu-id="322e3-205">217</span><span class="sxs-lookup"><span data-stu-id="322e3-205">217</span></span> |<span data-ttu-id="322e3-206">100</span><span class="sxs-lookup"><span data-stu-id="322e3-206">100</span></span> |<span data-ttu-id="322e3-207">9</span><span class="sxs-lookup"><span data-stu-id="322e3-207">9</span></span> |<span data-ttu-id="322e3-208">6</span><span class="sxs-lookup"><span data-stu-id="322e3-208">6</span></span> |<span data-ttu-id="322e3-209">100</span><span class="sxs-lookup"><span data-stu-id="322e3-209">100</span></span> |

<span data-ttu-id="322e3-210">Neste exemplo dos dados de métrica de minutos, a chave de partição usa o tempo de resolução minuto.</span><span class="sxs-lookup"><span data-stu-id="322e3-210">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="322e3-211">A chave de linha identifica o tipo de informação que é armazenado na linha, e isso é composto de duas partes de informações, o tipo de acesso e o tipo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="322e3-211">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="322e3-212">O tipo de acesso é um usuário ou sistema, onde o usuário refere-se a todas as solicitações de usuário para o serviço de armazenamento e o sistema refere-se às solicitações feitas pela análise de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-212">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="322e3-213">O tipo de solicitação é tudo que nesse caso é uma linha de resumo, ou ele identifica a API específica, como QueryEntity ou UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="322e3-213">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="322e3-214">Os dados de exemplo acima mostram todos os registros de um minuto (iniciando às 11h00), para o número de solicitações de QueryEntities mais o número de solicitações de QueryEntity mais o número de solicitações de UpdateEntity adicionam até sete, que é o total mostrado na linha user:All.</span><span class="sxs-lookup"><span data-stu-id="322e3-214">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="322e3-215">Da mesma forma, você pode derivar a latência média de ponta a ponta 104.4286 na linha user:All ao calcular ((143.8 * 5) + 3 + 9)/7.</span><span class="sxs-lookup"><span data-stu-id="322e3-215">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="322e3-216">Considere configurar alertas no Portal clássico do Azure na página de Monitorar para que as Métricas de armazenamento possam notificá-lo automaticamente de todas as alterações importantes no comportamento dos seus serviços de armazenamento. Se você usar uma ferramenta de Gerenciador de armazenamento para baixar esses dados de métricas em um formato delimitado, você pode usar o Microsoft Excel para analisar os dados.</span><span class="sxs-lookup"><span data-stu-id="322e3-216">You should consider setting up alerts in the Azure Classic Portal on the Monitor page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="322e3-217">Confira a postagem do blog [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) (Gerenciadores de armazenamento do Microsoft Azure) para obter uma lista das ferramentas disponíveis do gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-217">See the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="322e3-218">Acessando dados de métrica programaticamente</span><span class="sxs-lookup"><span data-stu-id="322e3-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="322e3-219">A listagem a seguir mostra o código C# de exemplo, que acessa a métrica de minutos para um intervalo de minutos e exibe os resultados em uma janela de console.</span><span class="sxs-lookup"><span data-stu-id="322e3-219">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="322e3-220">Ele usa a biblioteca de armazenamento do Azure versão 4, o que inclui a classe CloudAnalyticsClient que simplifica o acesso às tabelas de métricas no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="322e3-220">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="322e3-221">Quais taxas você provoca quando habilita a métrica de armazenamento?</span><span class="sxs-lookup"><span data-stu-id="322e3-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="322e3-222">Gravar solicitações para criar entidades de tabela para métricas são cobradas de acordo com as taxas padrão aplicáveis a todas as operações de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="322e3-222">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="322e3-223">Solicitações de leitura e exclusão por um cliente para dados de métrica também são faturáveis em taxas padrão.</span><span class="sxs-lookup"><span data-stu-id="322e3-223">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="322e3-224">Se você configurou uma política de retenção de dados, que não seja cobrado quando o armazenamento do Azure excluir dados de métricas antigos.</span><span class="sxs-lookup"><span data-stu-id="322e3-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="322e3-225">No entanto, se você excluir dados de análise, sua conta será cobrada para as operações de exclusão.</span><span class="sxs-lookup"><span data-stu-id="322e3-225">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="322e3-226">A capacidade usada pelas tabelas de métricas também é faturável. Você pode usar o seguinte para estimar a quantidade de capacidade usada para armazenar dados de métricas:</span><span class="sxs-lookup"><span data-stu-id="322e3-226">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="322e3-227">Se cada hora de um serviço utiliza todas as APIs de cada serviço, então aproximadamente 148KB de dados serão armazenados nas tabelas de transações de métricas a cada hora se você tiver habilitado o serviço e o resumo de nível de API.</span><span class="sxs-lookup"><span data-stu-id="322e3-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="322e3-228">Se cada hora de um serviço utiliza todas as APIs de cada serviço, então cerca de 12KB de dados serão armazenados nas tabelas de transação de métricas a cada hora se você tiver habilitado apenas o resumo do nível de serviço.</span><span class="sxs-lookup"><span data-stu-id="322e3-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="322e3-229">A tabela de capacidade para blobs tem duas linhas adicionadas por dia (fornecida pelo usuário que optou pelos logs). Isso implica que todos os dias o tamanho dessa tabela aumenta em até aproximadamente 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="322e3-229">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="322e3-230">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="322e3-230">Next steps:</span></span>
[<span data-ttu-id="322e3-231">Habilitando o armazenamento de análise de log e acessando os dados de log</span><span class="sxs-lookup"><span data-stu-id="322e3-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
