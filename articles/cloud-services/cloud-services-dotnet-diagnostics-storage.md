---
title: "aaaStore e exibir dados de diagnóstico no armazenamento do Azure | Microsoft Docs"
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
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="40bfa-103">Armazenar e exibir dados de diagnóstico no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="40bfa-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="40bfa-104">Dados de diagnóstico não são armazenados permanentemente, a menos que você transferir emulador de armazenamento do Microsoft Azure toohello ou tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="40bfa-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="40bfa-105">Quando estiverem no armazenamento, eles poderão ser exibidos com uma das várias ferramentas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="40bfa-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="40bfa-106">Especificar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="40bfa-106">Specify a storage account</span></span>
<span data-ttu-id="40bfa-107">Você especificar conta de armazenamento de saudação que você deseja toouse no arquivo ServiceConfiguration cscfg hello.</span><span class="sxs-lookup"><span data-stu-id="40bfa-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="40bfa-108">informações de conta de saudação são definidas como uma cadeia de caracteres de conexão em uma definição de configuração.</span><span class="sxs-lookup"><span data-stu-id="40bfa-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="40bfa-109">Olá, exemplo a seguir mostra cadeia de conexão padrão Olá criada para um novo projeto de serviço de nuvem no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="40bfa-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="40bfa-110">Você pode alterar esses informações de conta de tooprovide da cadeia de conexão para uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="40bfa-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="40bfa-111">Dependendo do tipo de saudação de dados de diagnóstico que está sendo coletados, o diagnóstico do Azure usa o serviço de Blob hello ou serviço de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="40bfa-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="40bfa-112">Olá tabela a seguir mostra as fontes de dados de saudação que são mantidas e seu formato.</span><span class="sxs-lookup"><span data-stu-id="40bfa-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="40bfa-113">Fonte de dados</span><span class="sxs-lookup"><span data-stu-id="40bfa-113">Data source</span></span> | <span data-ttu-id="40bfa-114">Formato de armazenamento</span><span class="sxs-lookup"><span data-stu-id="40bfa-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="40bfa-115">Logs do Azure</span><span class="sxs-lookup"><span data-stu-id="40bfa-115">Azure logs</span></span> |<span data-ttu-id="40bfa-116">Tabela</span><span class="sxs-lookup"><span data-stu-id="40bfa-116">Table</span></span> |
| <span data-ttu-id="40bfa-117">Logs do IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="40bfa-117">IIS 7.0 logs</span></span> |<span data-ttu-id="40bfa-118">Blob</span><span class="sxs-lookup"><span data-stu-id="40bfa-118">Blob</span></span> |
| <span data-ttu-id="40bfa-119">Logs de infraestrutura do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="40bfa-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="40bfa-120">Tabela</span><span class="sxs-lookup"><span data-stu-id="40bfa-120">Table</span></span> |
| <span data-ttu-id="40bfa-121">Logs de Rastreamento de Solicitação com Falha</span><span class="sxs-lookup"><span data-stu-id="40bfa-121">Failed Request Trace logs</span></span> |<span data-ttu-id="40bfa-122">Blob</span><span class="sxs-lookup"><span data-stu-id="40bfa-122">Blob</span></span> |
| <span data-ttu-id="40bfa-123">Log de eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="40bfa-123">Windows Event logs</span></span> |<span data-ttu-id="40bfa-124">Tabela</span><span class="sxs-lookup"><span data-stu-id="40bfa-124">Table</span></span> |
| <span data-ttu-id="40bfa-125">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="40bfa-125">Performance counters</span></span> |<span data-ttu-id="40bfa-126">Tabela</span><span class="sxs-lookup"><span data-stu-id="40bfa-126">Table</span></span> |
| <span data-ttu-id="40bfa-127">Despejos de falhas</span><span class="sxs-lookup"><span data-stu-id="40bfa-127">Crash dumps</span></span> |<span data-ttu-id="40bfa-128">Blob</span><span class="sxs-lookup"><span data-stu-id="40bfa-128">Blob</span></span> |
| <span data-ttu-id="40bfa-129">Logs de erros personalizados</span><span class="sxs-lookup"><span data-stu-id="40bfa-129">Custom error logs</span></span> |<span data-ttu-id="40bfa-130">Blob</span><span class="sxs-lookup"><span data-stu-id="40bfa-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="40bfa-131">Transferir dados de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="40bfa-131">Transfer diagnostic data</span></span>
<span data-ttu-id="40bfa-132">2.5 do SDK e posterior, dados de diagnóstico Olá solicitação tootransfer podem ocorrer por meio do arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="40bfa-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="40bfa-133">Você pode transferir dados de diagnóstico em intervalos agendados, como especificado na configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="40bfa-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="40bfa-134">Para SDK 2.4 e anterior pode solicitar dados de diagnóstico tootransfer hello como programaticamente por meio do arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="40bfa-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="40bfa-135">abordagem programática Olá permite transferências sob demanda de toodo.</span><span class="sxs-lookup"><span data-stu-id="40bfa-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40bfa-136">Quando você transfere dados de diagnóstico tooan conta de armazenamento do Azure, incorre em custos Olá para recursos de armazenamento que usa os dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="40bfa-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="40bfa-137">Armazenar dados de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="40bfa-137">Store diagnostic data</span></span>
<span data-ttu-id="40bfa-138">Dados de log são armazenados no armazenamento de BLOBs ou tabelas com hello nomes a seguir:</span><span class="sxs-lookup"><span data-stu-id="40bfa-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="40bfa-139">**Tabelas**</span><span class="sxs-lookup"><span data-stu-id="40bfa-139">**Tables**</span></span>

* <span data-ttu-id="40bfa-140">**WadLogsTable** - Logs escritos em código usando o ouvinte de rastreamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="40bfa-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="40bfa-141">**WADDiagnosticInfrastructureLogsTable** - monitor de diagnóstico e alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="40bfa-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="40bfa-142">**WADDirectoriesTable** – diretórios de monitor de diagnóstico que hello está monitorando.</span><span class="sxs-lookup"><span data-stu-id="40bfa-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="40bfa-143">Isso inclui logs do IIS, logs de solicitação do IIS com falha e diretórios personalizados.</span><span class="sxs-lookup"><span data-stu-id="40bfa-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="40bfa-144">local Olá Olá blob do arquivo de log especificado no campo de contêiner de saudação e nome de saudação do blob Olá é no campo RelativePath de saudação.</span><span class="sxs-lookup"><span data-stu-id="40bfa-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="40bfa-145">campo AbsolutePath de saudação indica Olá local e o nome do arquivo hello como existia na máquina virtual do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="40bfa-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="40bfa-146">**WADPerformanceCountersTable** – contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="40bfa-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="40bfa-147">**WADWindowsEventLogsTable** – logs de Eventos do Windows.</span><span class="sxs-lookup"><span data-stu-id="40bfa-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="40bfa-148">**Blobs**</span><span class="sxs-lookup"><span data-stu-id="40bfa-148">**Blobs**</span></span>

* <span data-ttu-id="40bfa-149">**wad-control-container** – (somente para o SDK 2.4 e anterior) contém arquivos de configuração XML de saudação que controla Olá diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="40bfa-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="40bfa-150">**wad-iis-failedreqlogfiles** – contém informações de logs de solicitação com falha do IIS.</span><span class="sxs-lookup"><span data-stu-id="40bfa-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="40bfa-151">**wad-iis-logfiles** – contém informações sobre logs do IIS.</span><span class="sxs-lookup"><span data-stu-id="40bfa-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="40bfa-152">**"custom"** – um contêiner personalizado com base na configuração dos diretórios que são monitorados pelo monitor de diagnóstico hello.</span><span class="sxs-lookup"><span data-stu-id="40bfa-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="40bfa-153">Olá nome desse contêiner de blob será especificado em WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="40bfa-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="40bfa-154">Dados de diagnóstico de tooview de ferramentas</span><span class="sxs-lookup"><span data-stu-id="40bfa-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="40bfa-155">Várias ferramentas são dados de saudação tooview disponível depois que ele toostorage transferido.</span><span class="sxs-lookup"><span data-stu-id="40bfa-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="40bfa-156">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="40bfa-156">For example:</span></span>

* <span data-ttu-id="40bfa-157">Gerenciador de servidores no Visual Studio - se você tiver instalado as ferramentas do Azure Olá para Microsoft Visual Studio, você pode usar nó de armazenamento do Azure Olá no Gerenciador de servidores tooview dados somente leitura blob e tabela de suas contas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="40bfa-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="40bfa-158">Você pode exibir dados de conta do emulador de armazenamento local e também de contas de armazenamento que você criou para o Azure.</span><span class="sxs-lookup"><span data-stu-id="40bfa-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="40bfa-159">Para obter mais informações, veja [Procurando e gerenciando recursos de armazenamento com o Gerenciador de Servidores](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="40bfa-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="40bfa-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Linux, Windows e OSX.</span><span class="sxs-lookup"><span data-stu-id="40bfa-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="40bfa-161">[O estúdio de gerenciamento do Azure](http://www.cerebrata.com/products/azure-management-studio/introduction) inclui o Azure Diagnostics Manager que permite que você tooview, baixar e gerenciar dados de diagnóstico de Olá coletados pelos aplicativos Olá em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="40bfa-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40bfa-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40bfa-162">Next Steps</span></span>
[<span data-ttu-id="40bfa-163">Fluxo de saudação do rastreamento em um aplicativo de serviços de nuvem com o diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="40bfa-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

