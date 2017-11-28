---
title: "Armazenar e exibir dados de diagnóstico no Armazenamento do Azure | Microsoft Docs"
description: "Obter dados de diagnóstico do Azure no Armazenamento do Azure e exibi-los"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="f235d-103">Armazenar e exibir dados de diagnóstico no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f235d-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="f235d-104">Os dados de diagnóstico não são armazenados permanentemente, a menos que sejam transferidos para o emulador de armazenamento do Microsoft Azure ou para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f235d-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="f235d-105">Quando estiverem no armazenamento, eles poderão ser exibidos com uma das várias ferramentas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f235d-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="f235d-106">Especificar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f235d-106">Specify a storage account</span></span>
<span data-ttu-id="f235d-107">Especifique a conta de armazenamento que você deseja usar no arquivo ServiceConfiguration.cscfg.</span><span class="sxs-lookup"><span data-stu-id="f235d-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="f235d-108">As informações da conta são definidas como uma cadeia de conexão em uma definição de configuração.</span><span class="sxs-lookup"><span data-stu-id="f235d-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="f235d-109">O exemplo a seguir mostra a cadeia de conexão padrão criada para um novo projeto do serviço de nuvem no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f235d-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="f235d-110">Você pode alterar essa cadeia de caracteres de conexão para fornecer informações de conta para uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f235d-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="f235d-111">Dependendo do tipo de dados de diagnóstico que estejam sendo coletados, o diagnóstico do Azure usará o serviço Blob ou o serviço Tabela.</span><span class="sxs-lookup"><span data-stu-id="f235d-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="f235d-112">A tabela a seguir mostra as fontes de dados persistentes e seu formato.</span><span class="sxs-lookup"><span data-stu-id="f235d-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="f235d-113">Fonte de dados</span><span class="sxs-lookup"><span data-stu-id="f235d-113">Data source</span></span> | <span data-ttu-id="f235d-114">Formato de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f235d-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="f235d-115">Logs do Azure</span><span class="sxs-lookup"><span data-stu-id="f235d-115">Azure logs</span></span> |<span data-ttu-id="f235d-116">Tabela</span><span class="sxs-lookup"><span data-stu-id="f235d-116">Table</span></span> |
| <span data-ttu-id="f235d-117">Logs do IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="f235d-117">IIS 7.0 logs</span></span> |<span data-ttu-id="f235d-118">Blob</span><span class="sxs-lookup"><span data-stu-id="f235d-118">Blob</span></span> |
| <span data-ttu-id="f235d-119">Logs de infraestrutura do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="f235d-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="f235d-120">Tabela</span><span class="sxs-lookup"><span data-stu-id="f235d-120">Table</span></span> |
| <span data-ttu-id="f235d-121">Logs de Rastreamento de Solicitação com Falha</span><span class="sxs-lookup"><span data-stu-id="f235d-121">Failed Request Trace logs</span></span> |<span data-ttu-id="f235d-122">Blob</span><span class="sxs-lookup"><span data-stu-id="f235d-122">Blob</span></span> |
| <span data-ttu-id="f235d-123">Log de eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="f235d-123">Windows Event logs</span></span> |<span data-ttu-id="f235d-124">Tabela</span><span class="sxs-lookup"><span data-stu-id="f235d-124">Table</span></span> |
| <span data-ttu-id="f235d-125">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="f235d-125">Performance counters</span></span> |<span data-ttu-id="f235d-126">Tabela</span><span class="sxs-lookup"><span data-stu-id="f235d-126">Table</span></span> |
| <span data-ttu-id="f235d-127">Despejos de falhas</span><span class="sxs-lookup"><span data-stu-id="f235d-127">Crash dumps</span></span> |<span data-ttu-id="f235d-128">Blob</span><span class="sxs-lookup"><span data-stu-id="f235d-128">Blob</span></span> |
| <span data-ttu-id="f235d-129">Logs de erros personalizados</span><span class="sxs-lookup"><span data-stu-id="f235d-129">Custom error logs</span></span> |<span data-ttu-id="f235d-130">Blob</span><span class="sxs-lookup"><span data-stu-id="f235d-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="f235d-131">Transferir dados de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="f235d-131">Transfer diagnostic data</span></span>
<span data-ttu-id="f235d-132">Para o SDK 2.5 e posterior, a solicitação para transferir dados de diagnóstico pode ocorrer por meio do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="f235d-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="f235d-133">Você pode transferir os dados de diagnóstico em intervalos agendados, como especificado na configuração.</span><span class="sxs-lookup"><span data-stu-id="f235d-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="f235d-134">Para o SDK 2.4 e anterior, você pode solicitar a transferência dos dados de diagnóstico por meio do arquivo de configuração, bem como programaticamente.</span><span class="sxs-lookup"><span data-stu-id="f235d-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="f235d-135">A abordagem programática também permite fazer transferências sob demanda.</span><span class="sxs-lookup"><span data-stu-id="f235d-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f235d-136">Quando você transfere dados de diagnóstico para uma conta de armazenamento do Azure, incorre em custos para os recursos de armazenamento usados pelos dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f235d-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="f235d-137">Armazenar dados de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="f235d-137">Store diagnostic data</span></span>
<span data-ttu-id="f235d-138">Os dados de log são armazenados no armazenamento de Blob ou de Tabela com os seguintes nomes:</span><span class="sxs-lookup"><span data-stu-id="f235d-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="f235d-139">**Tabelas**</span><span class="sxs-lookup"><span data-stu-id="f235d-139">**Tables**</span></span>

* <span data-ttu-id="f235d-140">**WadLogsTable** - logs escritos em código usando o ouvinte de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="f235d-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="f235d-141">**WADDiagnosticInfrastructureLogsTable** - monitor de diagnóstico e alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="f235d-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="f235d-142">**WADDirectoriesTable** – diretórios que o monitor de diagnóstico está monitorando.</span><span class="sxs-lookup"><span data-stu-id="f235d-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="f235d-143">Isso inclui logs do IIS, logs de solicitação do IIS com falha e diretórios personalizados.</span><span class="sxs-lookup"><span data-stu-id="f235d-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="f235d-144">O local do arquivo de log de blob é especificado no campo Container e o nome do blob está no campo RelativePath.</span><span class="sxs-lookup"><span data-stu-id="f235d-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="f235d-145">O campo AbsolutePath indica o local e o nome do arquivo como existia na máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f235d-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="f235d-146">**WADPerformanceCountersTable** – contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="f235d-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="f235d-147">**WADWindowsEventLogsTable** – logs de Eventos do Windows.</span><span class="sxs-lookup"><span data-stu-id="f235d-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="f235d-148">**Blobs**</span><span class="sxs-lookup"><span data-stu-id="f235d-148">**Blobs**</span></span>

* <span data-ttu-id="f235d-149">**wad-control-container** – (somente para o SDK 2.4 e anteriores) contém os arquivos de configuração XML que controlam o diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="f235d-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="f235d-150">**wad-iis-failedreqlogfiles** – contém informações de logs de solicitação com falha do IIS.</span><span class="sxs-lookup"><span data-stu-id="f235d-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="f235d-151">**wad-iis-logfiles** – contém informações sobre logs do IIS.</span><span class="sxs-lookup"><span data-stu-id="f235d-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="f235d-152">**"custom"** – um contêiner personalizado com base na configuração de diretórios que são monitorados pelo monitor de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f235d-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="f235d-153">O nome desse contêiner de blob será especificado em WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="f235d-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="f235d-154">Ferramentas para exibir dados de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="f235d-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="f235d-155">Várias ferramentas estão disponíveis para exibir os dados depois de serem transferidos para o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f235d-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="f235d-156">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f235d-156">For example:</span></span>

* <span data-ttu-id="f235d-157">Gerenciador de Servidores no Visual Studio – Se tiver instalado as Ferramentas do Azure para o Microsoft Visual Studio, será possível usar o nó do Armazenamento do Azure no Gerenciador de Servidores para exibir os dados de tabela e de blob somente leitura de suas contas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f235d-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="f235d-158">Você pode exibir dados de conta do emulador de armazenamento local e também de contas de armazenamento que você criou para o Azure.</span><span class="sxs-lookup"><span data-stu-id="f235d-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="f235d-159">Para obter mais informações, veja [Procurando e gerenciando recursos de armazenamento com o Gerenciador de Servidores](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="f235d-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="f235d-160">[Gerenciamento de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo que permite trabalhar facilmente com os dados de Armazenamento do Azure no Windows, OSX e Linux.</span><span class="sxs-lookup"><span data-stu-id="f235d-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="f235d-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) inclui o Gerenciador de Diagnóstico do Azure que permite exibir, baixar e gerenciar os dados de diagnósticos coletados pelos aplicativos em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="f235d-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f235d-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f235d-162">Next Steps</span></span>
[<span data-ttu-id="f235d-163">Rastrear o fluxo em um aplicativo de Serviços de Nuvem com o Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="f235d-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

