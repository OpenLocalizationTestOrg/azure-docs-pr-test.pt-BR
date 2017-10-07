---
title: armazenamento de blob aaaUse para IIS e a tabela de armazenamento para eventos no Azure Log Analytics | Microsoft Docs
description: "Análise de log pode ler logs Olá para serviços do Azure que gravam o armazenamento de diagnóstico tootable ou gravados tooblob armazenamento de logs do IIS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="f1860-103">Usar o armazenamento de blobs do Azure para IIS e armazenamento de tabelas do Azure para eventos com o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f1860-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="f1860-104">Análise de log pode ler os logs de saudação para Olá serviços que gravam diagnóstico tootable armazenamento ou o IIS registra tooblob escrito armazenamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1860-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="f1860-105">Clusters do Service Fabric (visualização)</span><span class="sxs-lookup"><span data-stu-id="f1860-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="f1860-106">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="f1860-106">Virtual Machines</span></span>
* <span data-ttu-id="f1860-107">Funções Web/de Trabalho</span><span class="sxs-lookup"><span data-stu-id="f1860-107">Web/Worker Roles</span></span>

<span data-ttu-id="f1860-108">Antes que o Log Analytics possa coletar dados para esses recursos, o diagnóstico do Azure deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="f1860-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="f1860-109">Depois que os diagnósticos são habilitados, você pode usar o portal do Azure de saudação ou PowerShell configurar logs de saudação do toocollect de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="f1860-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="f1860-110">Diagnóstico do Azure é uma extensão do Azure que permite que você toocollect dados de diagnóstico de uma função de trabalho, a função web ou a máquina virtual em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="f1860-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="f1860-111">dados de saudação são armazenados em uma conta de armazenamento do Azure e, em seguida, podem ser coletados pela análise de Log.</span><span class="sxs-lookup"><span data-stu-id="f1860-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="f1860-112">Para análise de Log toocollect esses logs de diagnóstico do Azure, Olá logs devem estar no hello locais a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1860-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="f1860-113">Tipo de Log</span><span class="sxs-lookup"><span data-stu-id="f1860-113">Log Type</span></span> | <span data-ttu-id="f1860-114">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="f1860-114">Resource Type</span></span> | <span data-ttu-id="f1860-115">Local</span><span class="sxs-lookup"><span data-stu-id="f1860-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1860-116">Logs IIS</span><span class="sxs-lookup"><span data-stu-id="f1860-116">IIS logs</span></span> |<span data-ttu-id="f1860-117">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="f1860-117">Virtual Machines</span></span> <br> <span data-ttu-id="f1860-118">Funções da Web</span><span class="sxs-lookup"><span data-stu-id="f1860-118">Web roles</span></span> <br> <span data-ttu-id="f1860-119">Funções de trabalho</span><span class="sxs-lookup"><span data-stu-id="f1860-119">Worker roles</span></span> |<span data-ttu-id="f1860-120">wad-iis-logfiles (Armazenamento de Blobs)</span><span class="sxs-lookup"><span data-stu-id="f1860-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="f1860-121">syslog</span><span class="sxs-lookup"><span data-stu-id="f1860-121">Syslog</span></span> |<span data-ttu-id="f1860-122">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="f1860-122">Virtual Machines</span></span> |<span data-ttu-id="f1860-123">LinuxsyslogVer2v0 (Armazenamento de Tabelas)</span><span class="sxs-lookup"><span data-stu-id="f1860-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="f1860-124">Eventos operacionais do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="f1860-125">Nós do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-125">Service Fabric nodes</span></span> |<span data-ttu-id="f1860-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="f1860-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="f1860-127">Eventos dos Reliable Actors do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="f1860-128">Nós do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-128">Service Fabric nodes</span></span> |<span data-ttu-id="f1860-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="f1860-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="f1860-130">Arquitetura de Serviços Confiáveis do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="f1860-131">Nós do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-131">Service Fabric nodes</span></span> |<span data-ttu-id="f1860-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="f1860-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="f1860-133">Log de eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="f1860-133">Windows Event logs</span></span> |<span data-ttu-id="f1860-134">Nós do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="f1860-135">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="f1860-135">Virtual Machines</span></span> <br> <span data-ttu-id="f1860-136">Funções da Web</span><span class="sxs-lookup"><span data-stu-id="f1860-136">Web roles</span></span> <br> <span data-ttu-id="f1860-137">Funções de trabalho</span><span class="sxs-lookup"><span data-stu-id="f1860-137">Worker roles</span></span> |<span data-ttu-id="f1860-138">WADWindowsEventLogsTable (Armazenamento de Tabelas)</span><span class="sxs-lookup"><span data-stu-id="f1860-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="f1860-139">Logs do ETW do Windows</span><span class="sxs-lookup"><span data-stu-id="f1860-139">Windows ETW logs</span></span> |<span data-ttu-id="f1860-140">Nós do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="f1860-141">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="f1860-141">Virtual Machines</span></span> <br> <span data-ttu-id="f1860-142">Funções da Web</span><span class="sxs-lookup"><span data-stu-id="f1860-142">Web roles</span></span> <br> <span data-ttu-id="f1860-143">Funções de trabalho</span><span class="sxs-lookup"><span data-stu-id="f1860-143">Worker roles</span></span> |<span data-ttu-id="f1860-144">WADETWEventTable (Armazenamento de Tabelas)</span><span class="sxs-lookup"><span data-stu-id="f1860-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="f1860-145">Atualmente, não há suporte para logs do IIS nos sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1860-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="f1860-146">Para máquinas virtuais, você tem opção de saudação da instalação Olá [agente de análise de Log](log-analytics-azure-vm-extension.md) em suas ideias adicionais de tooenable de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f1860-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="f1860-147">Além de logs do IIS capaz de tooanalyze toobeing e Logs de eventos, você pode executar análises adicionais, incluindo controle de alterações de configuração, avaliação de SQL e avaliação de atualização.</span><span class="sxs-lookup"><span data-stu-id="f1860-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="f1860-148">Habilitar os diagnósticos do Azure em uma máquina virtual para coleta de log de eventos e log do IIS</span><span class="sxs-lookup"><span data-stu-id="f1860-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="f1860-149">Saudação de uso seguindo o procedimento tooenable diagnósticos do Azure em uma máquina virtual para Log de eventos e o IIS usando o portal do Microsoft Azure Olá de coleção de log.</span><span class="sxs-lookup"><span data-stu-id="f1860-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="f1860-150">tooenable diagnósticos do Azure em uma máquina virtual com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1860-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="f1860-151">Instale Olá VM Agent ao criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f1860-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="f1860-152">Se já existir uma máquina virtual de saudação, verifique se esse Olá que VM Agent já está instalado.</span><span class="sxs-lookup"><span data-stu-id="f1860-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="f1860-153">Em Olá portal do Azure, navegue toohello virtual machine, selecione **configuração opcional**, em seguida, **diagnóstico** e defina **Status** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="f1860-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="f1860-154">Após a conclusão, Olá VM tem a extensão de diagnóstico do Azure Olá instalado e em execução.</span><span class="sxs-lookup"><span data-stu-id="f1860-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="f1860-155">Essa extensão é responsável por coletar seus dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f1860-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="f1860-156">Habilite o monitoramento e configure o log de eventos em uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="f1860-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="f1860-157">Você pode habilitar o diagnóstico no hello nível da VM.</span><span class="sxs-lookup"><span data-stu-id="f1860-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="f1860-158">Diagnóstico de tooenable e, em seguida, configurar o log de eventos, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1860-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="f1860-159">Selecione Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f1860-159">Select hello VM.</span></span>
   2. <span data-ttu-id="f1860-160">Clique em **Monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="f1860-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="f1860-161">Clique em **Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="f1860-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="f1860-162">Saudação de conjunto **Status** muito**ON**.</span><span class="sxs-lookup"><span data-stu-id="f1860-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="f1860-163">Selecione cada log de diagnóstico que você deseja toocollect.</span><span class="sxs-lookup"><span data-stu-id="f1860-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="f1860-164">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1860-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="f1860-165">Habilitar diagnóstico do Azure em uma função web para coleta de eventos e log do IIS</span><span class="sxs-lookup"><span data-stu-id="f1860-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="f1860-166">Consulte também[como tooEnable diagnóstico em um serviço de nuvem](../cloud-services/cloud-services-dotnet-diagnostics.md) para etapas gerais sobre como habilitar o diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1860-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="f1860-167">instruções de saudação abaixo usam essas informações e personalizá-lo para uso com a análise de Log.</span><span class="sxs-lookup"><span data-stu-id="f1860-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="f1860-168">Com o diagnóstico do Azure habilitado:</span><span class="sxs-lookup"><span data-stu-id="f1860-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="f1860-169">Logs do IIS são armazenados por padrão, com dados de log transferidos no intervalo de transferência de scheduledTransferPeriod hello.</span><span class="sxs-lookup"><span data-stu-id="f1860-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="f1860-170">Logs de eventos do Windows não são transferidos por padrão.</span><span class="sxs-lookup"><span data-stu-id="f1860-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="f1860-171">Diagnóstico de tooenable</span><span class="sxs-lookup"><span data-stu-id="f1860-171">tooenable diagnostics</span></span>
<span data-ttu-id="f1860-172">tooenable Logs de eventos do Windows ou toochange Olá scheduledTransferPeriod, configure o diagnóstico do Azure usando o arquivo de configuração do hello XML (Diagnostics. wadcfg), conforme mostrado no [etapa 4: criar o arquivo de configuração de diagnóstico e instalar Olá extensão](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="f1860-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="f1860-173">Olá seguinte arquivo de configuração de exemplo coleta Logs do IIS e todos os eventos de saudação aplicativos e logs do sistema:</span><span class="sxs-lookup"><span data-stu-id="f1860-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="f1860-174">Certifique-se de que seu ConfigurationSettings Especifica uma conta de armazenamento, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f1860-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="f1860-175">Olá **AccountName** e **AccountKey** valores são encontrados na Olá portal do Azure no painel de conta de armazenamento hello, em gerenciar chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="f1860-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="f1860-176">protocolo de saudação para cadeia de caracteres de conexão Olá deve ser **https**.</span><span class="sxs-lookup"><span data-stu-id="f1860-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="f1860-177">Depois que a configuração de diagnóstico atualizada Olá é aplicada tooyour serviço de nuvem e está gravando diagnóstico tooAzure armazenamento, e em seguida, você está pronto tooconfigure análise de Log.</span><span class="sxs-lookup"><span data-stu-id="f1860-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="f1860-178">Usar os logs de toocollect portal do Azure de saudação do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f1860-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="f1860-179">Você pode usar logs de Olá Olá tooconfigure portal do Azure Log Analytics toocollect para Olá serviços do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1860-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="f1860-180">Clusters do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-180">Service Fabric clusters</span></span>
* <span data-ttu-id="f1860-181">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="f1860-181">Virtual Machines</span></span>
* <span data-ttu-id="f1860-182">Funções Web/de Trabalho</span><span class="sxs-lookup"><span data-stu-id="f1860-182">Web/Worker Roles</span></span>

<span data-ttu-id="f1860-183">No portal do Azure de Olá, navegar espaço de trabalho de análise de Log tooyour e executar Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1860-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="f1860-184">Clique em *Logs das contas de armazenamento*</span><span class="sxs-lookup"><span data-stu-id="f1860-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="f1860-185">Clique em Olá *adicionar* tarefa</span><span class="sxs-lookup"><span data-stu-id="f1860-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="f1860-186">Selecionar conta de armazenamento Olá que contém os logs de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="f1860-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="f1860-187">Essa conta pode ser uma conta de armazenamento clássica ou uma conta de armazenamento do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f1860-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="f1860-188">Selecione Olá tipo de dados que você deseja toocollect logs para</span><span class="sxs-lookup"><span data-stu-id="f1860-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="f1860-189">Opções de saudação são Logs do IIS; Eventos; Syslog (Linux); Logs do ETW; Eventos do serviço do Fabric</span><span class="sxs-lookup"><span data-stu-id="f1860-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="f1860-190">valor de saudação de origem é preenchido automaticamente com base em hello, tipo de dados e não podem ser alterados</span><span class="sxs-lookup"><span data-stu-id="f1860-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="f1860-191">Clique em configuração de saudação toosave Okey</span><span class="sxs-lookup"><span data-stu-id="f1860-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="f1860-192">Repita as etapas 2 a 6 para tipos de dados e contas de armazenamento adicional que você deseja toocollect de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="f1860-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="f1860-193">Em aproximadamente 30 minutos, você está toosee capaz de dados da conta de armazenamento Olá na análise de Log.</span><span class="sxs-lookup"><span data-stu-id="f1860-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="f1860-194">Você verá apenas os dados gravados toostorage depois Olá configuração é aplicada.</span><span class="sxs-lookup"><span data-stu-id="f1860-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="f1860-195">Análise de log não lê dados preexistentes Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f1860-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="f1860-196">portal de saudação não valida que Olá origem existe na conta de armazenamento hello ou se novos dados está sendo gravados.</span><span class="sxs-lookup"><span data-stu-id="f1860-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="f1860-197">Habilitar o diagnóstico do Azure em uma máquina virtual para coleta de log de eventos e log do IIS usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1860-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="f1860-198">Olá Use as etapas em [tooindex de análise de Log de configuração de diagnóstico do Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread do diagnóstico do Azure que é gravado tootable armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f1860-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="f1860-199">Usando o Azure PowerShell você pode especificar mais precisamente os eventos de saudação que são gravados tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f1860-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="f1860-200">Para obter mais informações, consulte [Habilitando o diagnóstico em Máquinas Virtuais do Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f1860-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="f1860-201">Você pode habilitar e atualizar o diagnóstico do Azure usando Olá script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="f1860-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="f1860-202">Você também pode usar esse script com uma configuração de log personalizada.</span><span class="sxs-lookup"><span data-stu-id="f1860-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="f1860-203">Modificar a conta de armazenamento Olá script tooset Olá, nome do serviço e nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f1860-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="f1860-204">script Hello usa cmdlets para máquinas virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="f1860-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="f1860-205">Examine Olá exemplo de script a seguir, copiá-lo, modifique conforme necessário, salve o exemplo hello como um arquivo de script do PowerShell e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="f1860-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="f1860-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1860-206">Next steps</span></span>
* <span data-ttu-id="f1860-207">[Coletar logs e métricas para serviços do Azure](log-analytics-azure-storage.md) para serviços do Azure com suporte.</span><span class="sxs-lookup"><span data-stu-id="f1860-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="f1860-208">[Habilitar soluções](log-analytics-add-solutions.md) tooprovide ideias sobre dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1860-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="f1860-209">[Usar consultas de pesquisa](log-analytics-log-searches.md) tooanalyze dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1860-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
