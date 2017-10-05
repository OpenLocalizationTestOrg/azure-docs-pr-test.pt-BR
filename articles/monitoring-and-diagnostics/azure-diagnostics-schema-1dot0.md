---
title: "Esquema de configuração do Diagnóstico do Azure 1.0 | Microsoft Docs"
description: "Relevante APENAS se você estiver usando o SDK do Azure 2.4 e abaixo com Máquinas Virtuais do Azure, conjuntos de dimensionamento de máquinas virtuais, Service Fabric ou Serviços de Nuvem."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="0b274-103">Esquema de Configuração do Azure Diagnostics 1.0</span><span class="sxs-lookup"><span data-stu-id="0b274-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="0b274-104">Diagnóstico do Azure é o componente usado para coletar contadores de desempenho e outras estatísticas de Máquinas Virtuais do Azure, Conjuntos de Escala de Máquina Virtual, Service Fabric e Serviços de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="0b274-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="0b274-105">Esta página só é relevante se você estiver usando um desses serviços.</span><span class="sxs-lookup"><span data-stu-id="0b274-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="0b274-106">O Diagnóstico do Azure é usado com outros produtos de diagnóstico da Microsoft, como Azure Monitor, Application Insights e Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0b274-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="0b274-107">O arquivo de configuração do Diagnóstico do Azure define os valores que são usados para inicializar o Monitor de Diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="0b274-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="0b274-108">Esse arquivo é usado para inicializar as definições de configuração de diagnóstico quando o monitor de diagnóstico é iniciado.</span><span class="sxs-lookup"><span data-stu-id="0b274-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="0b274-109">Por padrão, o arquivo de esquema de configuração do Diagnóstico do Azure é instalado no diretório `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas`.</span><span class="sxs-lookup"><span data-stu-id="0b274-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="0b274-110">Substitua `<version>` pela versão instalada do [SDK do Azure](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0b274-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="0b274-111">O arquivo de configuração de diagnóstico é normalmente usado com tarefas de inicialização que exigem a coleta prévia de dados de diagnóstico no processo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="0b274-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="0b274-112">Para obter mais informações sobre como usar o Diagnóstico do Azure, consulte [Coletar dados do log usando o Diagnóstico do Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="0b274-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="0b274-113">Exemplo do arquivo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0b274-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="0b274-114">O exemplo a seguir mostra um arquivo de configuração de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="0b274-114">The following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="0b274-115">Namespace DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="0b274-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="0b274-116">O namespace XML para o arquivo de configuração de diagnóstico é:</span><span class="sxs-lookup"><span data-stu-id="0b274-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="0b274-117">Elementos de esquema</span><span class="sxs-lookup"><span data-stu-id="0b274-117">Schema Elements</span></span>  
 <span data-ttu-id="0b274-118">O arquivo de configuração de diagnóstico inclui os elementos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0b274-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="0b274-119">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="0b274-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="0b274-120">O elemento de nível superior do arquivo de configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="0b274-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="0b274-121">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-121">Attributes:</span></span>

|<span data-ttu-id="0b274-122">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-122">Attribute</span></span>  |<span data-ttu-id="0b274-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-123">Type</span></span>   |<span data-ttu-id="0b274-124">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0b274-124">Required</span></span>| <span data-ttu-id="0b274-125">Padrão</span><span class="sxs-lookup"><span data-stu-id="0b274-125">Default</span></span> | <span data-ttu-id="0b274-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="0b274-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="0b274-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="0b274-128">duration</span><span class="sxs-lookup"><span data-stu-id="0b274-128">duration</span></span>|<span data-ttu-id="0b274-129">Opcional</span><span class="sxs-lookup"><span data-stu-id="0b274-129">Optional</span></span> | <span data-ttu-id="0b274-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="0b274-130">PT1M</span></span>| <span data-ttu-id="0b274-131">Especifica o intervalo no qual o monitor de diagnóstico sonda em busca de alterações de configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="0b274-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="0b274-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="0b274-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-133">unsignedInt</span></span>|<span data-ttu-id="0b274-134">Opcional</span><span class="sxs-lookup"><span data-stu-id="0b274-134">Optional</span></span>| <span data-ttu-id="0b274-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="0b274-135">4000 MB.</span></span> <span data-ttu-id="0b274-136">Se você fornecer um valor, ele não deverá exceder esse valor</span><span class="sxs-lookup"><span data-stu-id="0b274-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="0b274-137">A quantidade total de armazenamento de sistema de arquivos alocado para todos os buffers de registro em log.</span><span class="sxs-lookup"><span data-stu-id="0b274-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="0b274-138">Elemento DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="0b274-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="0b274-139">Define a configuração de buffer para os logs gerados pela infraestrutura de diagnóstico subjacente.</span><span class="sxs-lookup"><span data-stu-id="0b274-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="0b274-140">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="0b274-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="0b274-141">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-141">Attributes:</span></span>

|<span data-ttu-id="0b274-142">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-142">Attribute</span></span>|<span data-ttu-id="0b274-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-143">Type</span></span>|<span data-ttu-id="0b274-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="0b274-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0b274-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-146">unsignedInt</span></span>|<span data-ttu-id="0b274-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-147">Optional.</span></span> <span data-ttu-id="0b274-148">Especifica a quantidade máxima de armazenamento do sistema de arquivos disponível para os dados especificados.</span><span class="sxs-lookup"><span data-stu-id="0b274-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="0b274-149">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-149">The default is 0.</span></span>|  
|<span data-ttu-id="0b274-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="0b274-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="0b274-151">string</span><span class="sxs-lookup"><span data-stu-id="0b274-151">string</span></span>|<span data-ttu-id="0b274-152">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-152">Optional.</span></span> <span data-ttu-id="0b274-153">Especifica o nível de severidade mínimo para as entradas de log transferidas.</span><span class="sxs-lookup"><span data-stu-id="0b274-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0b274-154">O valor padrão é **Indefinido**.</span><span class="sxs-lookup"><span data-stu-id="0b274-154">The default value is **Undefined**.</span></span> <span data-ttu-id="0b274-155">Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="0b274-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0b274-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0b274-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0b274-157">duration</span><span class="sxs-lookup"><span data-stu-id="0b274-157">duration</span></span>|<span data-ttu-id="0b274-158">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-158">Optional.</span></span> <span data-ttu-id="0b274-159">Especifica o intervalo entre as transferências agendadas de dados, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="0b274-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="0b274-160">O padrão é PT0S.</span><span class="sxs-lookup"><span data-stu-id="0b274-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="0b274-161">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="0b274-161">Logs Element</span></span>  
 <span data-ttu-id="0b274-162">Define a configuração de buffer para logs básicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b274-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="0b274-163">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="0b274-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="0b274-164">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-164">Attributes:</span></span>  

|<span data-ttu-id="0b274-165">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-165">Attribute</span></span>|<span data-ttu-id="0b274-166">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-166">Type</span></span>|<span data-ttu-id="0b274-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0b274-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-169">unsignedInt</span></span>|<span data-ttu-id="0b274-170">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-170">Optional.</span></span> <span data-ttu-id="0b274-171">Especifica a quantidade máxima de armazenamento do sistema de arquivos disponível para os dados especificados.</span><span class="sxs-lookup"><span data-stu-id="0b274-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="0b274-172">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-172">The default is 0.</span></span>|  
|<span data-ttu-id="0b274-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="0b274-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="0b274-174">string</span><span class="sxs-lookup"><span data-stu-id="0b274-174">string</span></span>|<span data-ttu-id="0b274-175">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-175">Optional.</span></span> <span data-ttu-id="0b274-176">Especifica o nível de severidade mínimo para as entradas de log transferidas.</span><span class="sxs-lookup"><span data-stu-id="0b274-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0b274-177">O valor padrão é **Indefinido**.</span><span class="sxs-lookup"><span data-stu-id="0b274-177">The default value is **Undefined**.</span></span> <span data-ttu-id="0b274-178">Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="0b274-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0b274-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0b274-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0b274-180">duration</span><span class="sxs-lookup"><span data-stu-id="0b274-180">duration</span></span>|<span data-ttu-id="0b274-181">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-181">Optional.</span></span> <span data-ttu-id="0b274-182">Especifica o intervalo entre as transferências agendadas de dados, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="0b274-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="0b274-183">O padrão é PT0S.</span><span class="sxs-lookup"><span data-stu-id="0b274-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="0b274-184">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="0b274-184">Directories Element</span></span>  
<span data-ttu-id="0b274-185">Define a configuração de buffer para logs baseados em arquivo que você pode definir.</span><span class="sxs-lookup"><span data-stu-id="0b274-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="0b274-186">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="0b274-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="0b274-187">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-187">Attributes:</span></span>  

|<span data-ttu-id="0b274-188">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-188">Attribute</span></span>|<span data-ttu-id="0b274-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-189">Type</span></span>|<span data-ttu-id="0b274-190">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0b274-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-192">unsignedInt</span></span>|<span data-ttu-id="0b274-193">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-193">Optional.</span></span> <span data-ttu-id="0b274-194">Especifica a quantidade máxima de armazenamento do sistema de arquivos disponível para os dados especificados.</span><span class="sxs-lookup"><span data-stu-id="0b274-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="0b274-195">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-195">The default is 0.</span></span>|  
|<span data-ttu-id="0b274-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0b274-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0b274-197">duration</span><span class="sxs-lookup"><span data-stu-id="0b274-197">duration</span></span>|<span data-ttu-id="0b274-198">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-198">Optional.</span></span> <span data-ttu-id="0b274-199">Especifica o intervalo entre as transferências agendadas de dados, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="0b274-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="0b274-200">O padrão é PT0S.</span><span class="sxs-lookup"><span data-stu-id="0b274-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="0b274-201">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="0b274-201">CrashDumps Element</span></span>  
 <span data-ttu-id="0b274-202">Define o diretório de despejos de falha.</span><span class="sxs-lookup"><span data-stu-id="0b274-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="0b274-203">Elemento pai: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="0b274-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="0b274-204">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-204">Attributes:</span></span>  

|<span data-ttu-id="0b274-205">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-205">Attribute</span></span>|<span data-ttu-id="0b274-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-206">Type</span></span>|<span data-ttu-id="0b274-207">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-208">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="0b274-208">**container**</span></span>|<span data-ttu-id="0b274-209">string</span><span class="sxs-lookup"><span data-stu-id="0b274-209">string</span></span>|<span data-ttu-id="0b274-210">O nome do contêiner para onde o conteúdo do diretório será transferido.</span><span class="sxs-lookup"><span data-stu-id="0b274-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="0b274-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="0b274-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-212">unsignedInt</span></span>|<span data-ttu-id="0b274-213">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-213">Optional.</span></span> <span data-ttu-id="0b274-214">Especifica o tamanho máximo do diretório em megabytes.</span><span class="sxs-lookup"><span data-stu-id="0b274-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="0b274-215">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="0b274-216">Elemento FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="0b274-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="0b274-217">Define o diretório de log de solicitação com falha.</span><span class="sxs-lookup"><span data-stu-id="0b274-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="0b274-218">Elemento pai [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="0b274-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="0b274-219">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-219">Attributes:</span></span>  

|<span data-ttu-id="0b274-220">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-220">Attribute</span></span>|<span data-ttu-id="0b274-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-221">Type</span></span>|<span data-ttu-id="0b274-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-223">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="0b274-223">**container**</span></span>|<span data-ttu-id="0b274-224">string</span><span class="sxs-lookup"><span data-stu-id="0b274-224">string</span></span>|<span data-ttu-id="0b274-225">O nome do contêiner para onde o conteúdo do diretório será transferido.</span><span class="sxs-lookup"><span data-stu-id="0b274-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="0b274-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="0b274-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-227">unsignedInt</span></span>|<span data-ttu-id="0b274-228">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-228">Optional.</span></span> <span data-ttu-id="0b274-229">Especifica o tamanho máximo do diretório em megabytes.</span><span class="sxs-lookup"><span data-stu-id="0b274-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="0b274-230">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="0b274-231">Elemento IISLogs</span><span class="sxs-lookup"><span data-stu-id="0b274-231">IISLogs Element</span></span>  
 <span data-ttu-id="0b274-232">Define o diretório de log do IIS.</span><span class="sxs-lookup"><span data-stu-id="0b274-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="0b274-233">Elemento pai [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="0b274-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="0b274-234">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-234">Attributes:</span></span>  

|<span data-ttu-id="0b274-235">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-235">Attribute</span></span>|<span data-ttu-id="0b274-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-236">Type</span></span>|<span data-ttu-id="0b274-237">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-238">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="0b274-238">**container**</span></span>|<span data-ttu-id="0b274-239">string</span><span class="sxs-lookup"><span data-stu-id="0b274-239">string</span></span>|<span data-ttu-id="0b274-240">O nome do contêiner para onde o conteúdo do diretório será transferido.</span><span class="sxs-lookup"><span data-stu-id="0b274-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="0b274-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="0b274-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-242">unsignedInt</span></span>|<span data-ttu-id="0b274-243">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-243">Optional.</span></span> <span data-ttu-id="0b274-244">Especifica o tamanho máximo do diretório em megabytes.</span><span class="sxs-lookup"><span data-stu-id="0b274-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="0b274-245">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="0b274-246">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="0b274-246">DataSources Element</span></span>  
 <span data-ttu-id="0b274-247">Define zero ou mais diretórios de log adicionais.</span><span class="sxs-lookup"><span data-stu-id="0b274-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="0b274-248">Elemento pai: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="0b274-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="0b274-249">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="0b274-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="0b274-250">Define o diretório de arquivos de log a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="0b274-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="0b274-251">Elemento pai: [elemento DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="0b274-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="0b274-252">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-252">Attributes:</span></span>

|<span data-ttu-id="0b274-253">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-253">Attribute</span></span>|<span data-ttu-id="0b274-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-254">Type</span></span>|<span data-ttu-id="0b274-255">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-256">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="0b274-256">**container**</span></span>|<span data-ttu-id="0b274-257">string</span><span class="sxs-lookup"><span data-stu-id="0b274-257">string</span></span>|<span data-ttu-id="0b274-258">O nome do contêiner para onde o conteúdo do diretório será transferido.</span><span class="sxs-lookup"><span data-stu-id="0b274-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="0b274-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="0b274-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-260">unsignedInt</span></span>|<span data-ttu-id="0b274-261">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-261">Optional.</span></span> <span data-ttu-id="0b274-262">Especifica o tamanho máximo do diretório em megabytes.</span><span class="sxs-lookup"><span data-stu-id="0b274-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="0b274-263">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="0b274-264">Elemento Absolute</span><span class="sxs-lookup"><span data-stu-id="0b274-264">Absolute Element</span></span>  
 <span data-ttu-id="0b274-265">Define um caminho absoluto do diretório a ser monitorado com opção de expansão de ambiente.</span><span class="sxs-lookup"><span data-stu-id="0b274-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="0b274-266">Elemento pai: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="0b274-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="0b274-267">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-267">Attributes:</span></span>  

|<span data-ttu-id="0b274-268">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-268">Attribute</span></span>|<span data-ttu-id="0b274-269">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-269">Type</span></span>|<span data-ttu-id="0b274-270">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-271">**path**</span><span class="sxs-lookup"><span data-stu-id="0b274-271">**path**</span></span>|<span data-ttu-id="0b274-272">string</span><span class="sxs-lookup"><span data-stu-id="0b274-272">string</span></span>|<span data-ttu-id="0b274-273">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0b274-273">Required.</span></span> <span data-ttu-id="0b274-274">O caminho absoluto para o diretório a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="0b274-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="0b274-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="0b274-275">**expandEnvironment**</span></span>|<span data-ttu-id="0b274-276">Booliano</span><span class="sxs-lookup"><span data-stu-id="0b274-276">boolean</span></span>|<span data-ttu-id="0b274-277">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0b274-277">Required.</span></span> <span data-ttu-id="0b274-278">Se definido como **true**, as variáveis de ambiente no caminho serão expandidas.</span><span class="sxs-lookup"><span data-stu-id="0b274-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="0b274-279">Elemento LocalResource</span><span class="sxs-lookup"><span data-stu-id="0b274-279">LocalResource Element</span></span>  
 <span data-ttu-id="0b274-280">Define um caminho relativo para um recurso local indicado na definição do serviço.</span><span class="sxs-lookup"><span data-stu-id="0b274-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="0b274-281">Elemento pai: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="0b274-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="0b274-282">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-282">Attributes:</span></span>  

|<span data-ttu-id="0b274-283">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-283">Attribute</span></span>|<span data-ttu-id="0b274-284">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-284">Type</span></span>|<span data-ttu-id="0b274-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-286">**name**</span><span class="sxs-lookup"><span data-stu-id="0b274-286">**name**</span></span>|<span data-ttu-id="0b274-287">string</span><span class="sxs-lookup"><span data-stu-id="0b274-287">string</span></span>|<span data-ttu-id="0b274-288">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0b274-288">Required.</span></span> <span data-ttu-id="0b274-289">O nome do recurso local que contém o diretório a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="0b274-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="0b274-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="0b274-290">**relativePath**</span></span>|<span data-ttu-id="0b274-291">string</span><span class="sxs-lookup"><span data-stu-id="0b274-291">string</span></span>|<span data-ttu-id="0b274-292">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0b274-292">Required.</span></span> <span data-ttu-id="0b274-293">O caminho relativo a um recurso local a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="0b274-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="0b274-294">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="0b274-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="0b274-295">Define o caminho para coleta do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="0b274-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="0b274-296">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="0b274-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="0b274-297">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-297">Attributes:</span></span>  

|<span data-ttu-id="0b274-298">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-298">Attribute</span></span>|<span data-ttu-id="0b274-299">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-299">Type</span></span>|<span data-ttu-id="0b274-300">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0b274-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-302">unsignedInt</span></span>|<span data-ttu-id="0b274-303">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-303">Optional.</span></span> <span data-ttu-id="0b274-304">Especifica a quantidade máxima de armazenamento do sistema de arquivos disponível para os dados especificados.</span><span class="sxs-lookup"><span data-stu-id="0b274-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="0b274-305">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-305">The default is 0.</span></span>|  
|<span data-ttu-id="0b274-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0b274-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0b274-307">duration</span><span class="sxs-lookup"><span data-stu-id="0b274-307">duration</span></span>|<span data-ttu-id="0b274-308">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-308">Optional.</span></span> <span data-ttu-id="0b274-309">Especifica o intervalo entre as transferências agendadas de dados, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="0b274-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="0b274-310">O padrão é PT0S.</span><span class="sxs-lookup"><span data-stu-id="0b274-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="0b274-311">Elemento PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="0b274-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="0b274-312">Define o contador de desempenho a ser coletado.</span><span class="sxs-lookup"><span data-stu-id="0b274-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="0b274-313">Elemento pai: [elemento PerformanceCounters](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="0b274-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="0b274-314">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-314">Attributes:</span></span>  

|<span data-ttu-id="0b274-315">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-315">Attribute</span></span>|<span data-ttu-id="0b274-316">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-316">Type</span></span>|<span data-ttu-id="0b274-317">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="0b274-318">**counterSpecifier**</span></span>|<span data-ttu-id="0b274-319">string</span><span class="sxs-lookup"><span data-stu-id="0b274-319">string</span></span>|<span data-ttu-id="0b274-320">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0b274-320">Required.</span></span> <span data-ttu-id="0b274-321">O caminho para coleta do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="0b274-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="0b274-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="0b274-322">**sampleRate**</span></span>|<span data-ttu-id="0b274-323">duration</span><span class="sxs-lookup"><span data-stu-id="0b274-323">duration</span></span>|<span data-ttu-id="0b274-324">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0b274-324">Required.</span></span> <span data-ttu-id="0b274-325">A taxa de coleta do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="0b274-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="0b274-326">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="0b274-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="0b274-327">Define os logs de eventos a serem monitorados.</span><span class="sxs-lookup"><span data-stu-id="0b274-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="0b274-328">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="0b274-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="0b274-329">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-329">Attributes:</span></span>

|<span data-ttu-id="0b274-330">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-330">Attribute</span></span>|<span data-ttu-id="0b274-331">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-331">Type</span></span>|<span data-ttu-id="0b274-332">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0b274-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0b274-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="0b274-334">unsignedInt</span></span>|<span data-ttu-id="0b274-335">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-335">Optional.</span></span> <span data-ttu-id="0b274-336">Especifica a quantidade máxima de armazenamento do sistema de arquivos disponível para os dados especificados.</span><span class="sxs-lookup"><span data-stu-id="0b274-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="0b274-337">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="0b274-337">The default is 0.</span></span>|  
|<span data-ttu-id="0b274-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="0b274-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="0b274-339">string</span><span class="sxs-lookup"><span data-stu-id="0b274-339">string</span></span>|<span data-ttu-id="0b274-340">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-340">Optional.</span></span> <span data-ttu-id="0b274-341">Especifica o nível de severidade mínimo para as entradas de log transferidas.</span><span class="sxs-lookup"><span data-stu-id="0b274-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0b274-342">O valor padrão é **Indefinido**.</span><span class="sxs-lookup"><span data-stu-id="0b274-342">The default value is **Undefined**.</span></span> <span data-ttu-id="0b274-343">Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="0b274-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0b274-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0b274-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0b274-345">duration</span><span class="sxs-lookup"><span data-stu-id="0b274-345">duration</span></span>|<span data-ttu-id="0b274-346">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0b274-346">Optional.</span></span> <span data-ttu-id="0b274-347">Especifica o intervalo entre as transferências agendadas de dados, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="0b274-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="0b274-348">O padrão é PT0S.</span><span class="sxs-lookup"><span data-stu-id="0b274-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="0b274-349">Elemento DataSource</span><span class="sxs-lookup"><span data-stu-id="0b274-349">DataSource Element</span></span>  
 <span data-ttu-id="0b274-350">Define o log de eventos a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="0b274-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="0b274-351">Elemento pai: [elemento WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="0b274-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="0b274-352">Atributos:</span><span class="sxs-lookup"><span data-stu-id="0b274-352">Attributes:</span></span>

|<span data-ttu-id="0b274-353">Atributo</span><span class="sxs-lookup"><span data-stu-id="0b274-353">Attribute</span></span>|<span data-ttu-id="0b274-354">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b274-354">Type</span></span>|<span data-ttu-id="0b274-355">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b274-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0b274-356">**name**</span><span class="sxs-lookup"><span data-stu-id="0b274-356">**name**</span></span>|<span data-ttu-id="0b274-357">string</span><span class="sxs-lookup"><span data-stu-id="0b274-357">string</span></span>|<span data-ttu-id="0b274-358">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="0b274-358">Required.</span></span> <span data-ttu-id="0b274-359">Uma expressão XPath que especifica o log para coleta.</span><span class="sxs-lookup"><span data-stu-id="0b274-359">An XPath expression specifying the log to collect.</span></span>|  
