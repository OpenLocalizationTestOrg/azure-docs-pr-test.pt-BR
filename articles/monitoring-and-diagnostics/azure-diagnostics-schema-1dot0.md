---
title: "aaaAzure esquema de configuração do diagnóstico 1.0 | Microsoft Docs"
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="2bedc-103">Esquema de Configuração do Azure Diagnostics 1.0</span><span class="sxs-lookup"><span data-stu-id="2bedc-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="2bedc-104">Diagnóstico do Azure é Olá componente usado toocollect os contadores de desempenho e outras estatísticas de máquinas virtuais do Azure, conjuntos de escala de máquina Virtual, serviço de malha e serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2bedc-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="2bedc-105">Esta página só é relevante se você estiver usando um desses serviços.</span><span class="sxs-lookup"><span data-stu-id="2bedc-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="2bedc-106">O Diagnóstico do Azure é usado com outros produtos de diagnóstico da Microsoft, como Azure Monitor, Application Insights e Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bedc-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="2bedc-107">arquivo de configuração de diagnóstico do Azure Olá define os valores que são usados tooinitialize Olá Monitor de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2bedc-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="2bedc-108">Esse arquivo é definições de configuração de diagnóstico de tooinitialize usada quando inicia do monitor de diagnósticos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2bedc-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="2bedc-109">Por padrão, o arquivo de esquema de configuração de diagnóstico do Azure Olá é instalado toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span><span class="sxs-lookup"><span data-stu-id="2bedc-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="2bedc-110">Substituir `<version>` com versão de hello instalado do hello [SDK do Azure](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2bedc-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="2bedc-111">o arquivo de configuração de diagnóstico Olá normalmente é usado com tarefas de inicialização que exigem toobe de dados de diagnóstico coletada anteriormente no processo de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="2bedc-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="2bedc-112">Para obter mais informações sobre como usar o Diagnóstico do Azure, consulte [Coletar dados do log usando o Diagnóstico do Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="2bedc-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="2bedc-113">Exemplo de arquivo de configuração de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="2bedc-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="2bedc-114">saudação de exemplo a seguir mostra um arquivo de configuração de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="2bedc-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="2bedc-115">Namespace DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="2bedc-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="2bedc-116">Olá namespace XML para o arquivo de configuração de diagnóstico Olá é:</span><span class="sxs-lookup"><span data-stu-id="2bedc-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="2bedc-117">Elementos de esquema</span><span class="sxs-lookup"><span data-stu-id="2bedc-117">Schema Elements</span></span>  
 <span data-ttu-id="2bedc-118">arquivo de configuração de diagnóstico de saudação inclui Olá elementos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2bedc-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="2bedc-119">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="2bedc-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="2bedc-120">elemento de nível superior de saudação do arquivo de configuração de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="2bedc-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="2bedc-121">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-121">Attributes:</span></span>

|<span data-ttu-id="2bedc-122">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-122">Attribute</span></span>  |<span data-ttu-id="2bedc-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-123">Type</span></span>   |<span data-ttu-id="2bedc-124">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2bedc-124">Required</span></span>| <span data-ttu-id="2bedc-125">Padrão</span><span class="sxs-lookup"><span data-stu-id="2bedc-125">Default</span></span> | <span data-ttu-id="2bedc-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="2bedc-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="2bedc-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="2bedc-128">duration</span><span class="sxs-lookup"><span data-stu-id="2bedc-128">duration</span></span>|<span data-ttu-id="2bedc-129">Opcional</span><span class="sxs-lookup"><span data-stu-id="2bedc-129">Optional</span></span> | <span data-ttu-id="2bedc-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="2bedc-130">PT1M</span></span>| <span data-ttu-id="2bedc-131">Especifica o intervalo de saudação em pesquisas de monitor de diagnóstico que Olá para alterações de configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2bedc-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="2bedc-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="2bedc-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-133">unsignedInt</span></span>|<span data-ttu-id="2bedc-134">Opcional</span><span class="sxs-lookup"><span data-stu-id="2bedc-134">Optional</span></span>| <span data-ttu-id="2bedc-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="2bedc-135">4000 MB.</span></span> <span data-ttu-id="2bedc-136">Se você fornecer um valor, ele não deverá exceder esse valor</span><span class="sxs-lookup"><span data-stu-id="2bedc-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="2bedc-137">Olá total de armazenamento do sistema de arquivos alocado para todos os buffers de log.</span><span class="sxs-lookup"><span data-stu-id="2bedc-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="2bedc-138">Elemento DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="2bedc-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="2bedc-139">Define a configuração de buffer de saudação para logs de saudação que são gerados pela infraestrutura de diagnóstico subjacente hello.</span><span class="sxs-lookup"><span data-stu-id="2bedc-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="2bedc-140">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="2bedc-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="2bedc-141">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-141">Attributes:</span></span>

|<span data-ttu-id="2bedc-142">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-142">Attribute</span></span>|<span data-ttu-id="2bedc-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-143">Type</span></span>|<span data-ttu-id="2bedc-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="2bedc-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="2bedc-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-146">unsignedInt</span></span>|<span data-ttu-id="2bedc-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-147">Optional.</span></span> <span data-ttu-id="2bedc-148">Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.</span><span class="sxs-lookup"><span data-stu-id="2bedc-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="2bedc-149">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-149">hello default is 0.</span></span>|  
|<span data-ttu-id="2bedc-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="2bedc-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="2bedc-151">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-151">string</span></span>|<span data-ttu-id="2bedc-152">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-152">Optional.</span></span> <span data-ttu-id="2bedc-153">Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="2bedc-154">valor padrão de saudação é **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="2bedc-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="2bedc-155">Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="2bedc-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="2bedc-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="2bedc-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="2bedc-157">duration</span><span class="sxs-lookup"><span data-stu-id="2bedc-157">duration</span></span>|<span data-ttu-id="2bedc-158">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-158">Optional.</span></span> <span data-ttu-id="2bedc-159">Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="2bedc-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="2bedc-160">padrão de saudação é PT0S.</span><span class="sxs-lookup"><span data-stu-id="2bedc-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="2bedc-161">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="2bedc-161">Logs Element</span></span>  
 <span data-ttu-id="2bedc-162">Define a configuração de buffer de saudação para logs básicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bedc-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="2bedc-163">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="2bedc-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="2bedc-164">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-164">Attributes:</span></span>  

|<span data-ttu-id="2bedc-165">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-165">Attribute</span></span>|<span data-ttu-id="2bedc-166">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-166">Type</span></span>|<span data-ttu-id="2bedc-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="2bedc-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-169">unsignedInt</span></span>|<span data-ttu-id="2bedc-170">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-170">Optional.</span></span> <span data-ttu-id="2bedc-171">Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.</span><span class="sxs-lookup"><span data-stu-id="2bedc-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="2bedc-172">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-172">hello default is 0.</span></span>|  
|<span data-ttu-id="2bedc-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="2bedc-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="2bedc-174">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-174">string</span></span>|<span data-ttu-id="2bedc-175">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-175">Optional.</span></span> <span data-ttu-id="2bedc-176">Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="2bedc-177">valor padrão de saudação é **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="2bedc-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="2bedc-178">Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="2bedc-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="2bedc-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="2bedc-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="2bedc-180">duration</span><span class="sxs-lookup"><span data-stu-id="2bedc-180">duration</span></span>|<span data-ttu-id="2bedc-181">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-181">Optional.</span></span> <span data-ttu-id="2bedc-182">Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="2bedc-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="2bedc-183">padrão de saudação é PT0S.</span><span class="sxs-lookup"><span data-stu-id="2bedc-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="2bedc-184">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="2bedc-184">Directories Element</span></span>  
<span data-ttu-id="2bedc-185">Define a configuração de buffer de saudação para logs baseados em arquivo que você pode definir.</span><span class="sxs-lookup"><span data-stu-id="2bedc-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="2bedc-186">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="2bedc-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="2bedc-187">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-187">Attributes:</span></span>  

|<span data-ttu-id="2bedc-188">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-188">Attribute</span></span>|<span data-ttu-id="2bedc-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-189">Type</span></span>|<span data-ttu-id="2bedc-190">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="2bedc-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-192">unsignedInt</span></span>|<span data-ttu-id="2bedc-193">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-193">Optional.</span></span> <span data-ttu-id="2bedc-194">Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.</span><span class="sxs-lookup"><span data-stu-id="2bedc-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="2bedc-195">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-195">hello default is 0.</span></span>|  
|<span data-ttu-id="2bedc-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="2bedc-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="2bedc-197">duration</span><span class="sxs-lookup"><span data-stu-id="2bedc-197">duration</span></span>|<span data-ttu-id="2bedc-198">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-198">Optional.</span></span> <span data-ttu-id="2bedc-199">Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="2bedc-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="2bedc-200">padrão de saudação é PT0S.</span><span class="sxs-lookup"><span data-stu-id="2bedc-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="2bedc-201">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="2bedc-201">CrashDumps Element</span></span>  
 <span data-ttu-id="2bedc-202">Define o diretório de despejos de falhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="2bedc-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="2bedc-203">Elemento pai: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="2bedc-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="2bedc-204">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-204">Attributes:</span></span>  

|<span data-ttu-id="2bedc-205">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-205">Attribute</span></span>|<span data-ttu-id="2bedc-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-206">Type</span></span>|<span data-ttu-id="2bedc-207">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-208">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="2bedc-208">**container**</span></span>|<span data-ttu-id="2bedc-209">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-209">string</span></span>|<span data-ttu-id="2bedc-210">nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="2bedc-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="2bedc-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-212">unsignedInt</span></span>|<span data-ttu-id="2bedc-213">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-213">Optional.</span></span> <span data-ttu-id="2bedc-214">Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.</span><span class="sxs-lookup"><span data-stu-id="2bedc-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="2bedc-215">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="2bedc-216">Elemento FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="2bedc-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="2bedc-217">Define o diretório de log de solicitação com falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="2bedc-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="2bedc-218">Elemento pai [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="2bedc-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="2bedc-219">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-219">Attributes:</span></span>  

|<span data-ttu-id="2bedc-220">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-220">Attribute</span></span>|<span data-ttu-id="2bedc-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-221">Type</span></span>|<span data-ttu-id="2bedc-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-223">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="2bedc-223">**container**</span></span>|<span data-ttu-id="2bedc-224">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-224">string</span></span>|<span data-ttu-id="2bedc-225">nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="2bedc-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="2bedc-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-227">unsignedInt</span></span>|<span data-ttu-id="2bedc-228">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-228">Optional.</span></span> <span data-ttu-id="2bedc-229">Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.</span><span class="sxs-lookup"><span data-stu-id="2bedc-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="2bedc-230">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="2bedc-231">Elemento IISLogs</span><span class="sxs-lookup"><span data-stu-id="2bedc-231">IISLogs Element</span></span>  
 <span data-ttu-id="2bedc-232">Define o diretório de log do IIS de saudação.</span><span class="sxs-lookup"><span data-stu-id="2bedc-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="2bedc-233">Elemento pai [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="2bedc-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="2bedc-234">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-234">Attributes:</span></span>  

|<span data-ttu-id="2bedc-235">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-235">Attribute</span></span>|<span data-ttu-id="2bedc-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-236">Type</span></span>|<span data-ttu-id="2bedc-237">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-238">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="2bedc-238">**container**</span></span>|<span data-ttu-id="2bedc-239">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-239">string</span></span>|<span data-ttu-id="2bedc-240">nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="2bedc-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="2bedc-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-242">unsignedInt</span></span>|<span data-ttu-id="2bedc-243">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-243">Optional.</span></span> <span data-ttu-id="2bedc-244">Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.</span><span class="sxs-lookup"><span data-stu-id="2bedc-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="2bedc-245">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="2bedc-246">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="2bedc-246">DataSources Element</span></span>  
 <span data-ttu-id="2bedc-247">Define zero ou mais diretórios de log adicionais.</span><span class="sxs-lookup"><span data-stu-id="2bedc-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="2bedc-248">Elemento pai: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="2bedc-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="2bedc-249">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="2bedc-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="2bedc-250">Define o diretório de saudação do toomonitor de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="2bedc-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="2bedc-251">Elemento pai: [elemento DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="2bedc-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="2bedc-252">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-252">Attributes:</span></span>

|<span data-ttu-id="2bedc-253">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-253">Attribute</span></span>|<span data-ttu-id="2bedc-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-254">Type</span></span>|<span data-ttu-id="2bedc-255">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-256">**contêiner**</span><span class="sxs-lookup"><span data-stu-id="2bedc-256">**container**</span></span>|<span data-ttu-id="2bedc-257">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-257">string</span></span>|<span data-ttu-id="2bedc-258">nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="2bedc-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="2bedc-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-260">unsignedInt</span></span>|<span data-ttu-id="2bedc-261">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-261">Optional.</span></span> <span data-ttu-id="2bedc-262">Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.</span><span class="sxs-lookup"><span data-stu-id="2bedc-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="2bedc-263">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="2bedc-264">Elemento Absolute</span><span class="sxs-lookup"><span data-stu-id="2bedc-264">Absolute Element</span></span>  
 <span data-ttu-id="2bedc-265">Define um caminho absoluto do hello diretório toomonitor com expansão de ambiente opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="2bedc-266">Elemento pai: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="2bedc-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="2bedc-267">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-267">Attributes:</span></span>  

|<span data-ttu-id="2bedc-268">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-268">Attribute</span></span>|<span data-ttu-id="2bedc-269">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-269">Type</span></span>|<span data-ttu-id="2bedc-270">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-271">**path**</span><span class="sxs-lookup"><span data-stu-id="2bedc-271">**path**</span></span>|<span data-ttu-id="2bedc-272">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-272">string</span></span>|<span data-ttu-id="2bedc-273">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2bedc-273">Required.</span></span> <span data-ttu-id="2bedc-274">Olá caminho absoluto toohello diretório toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2bedc-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="2bedc-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="2bedc-275">**expandEnvironment**</span></span>|<span data-ttu-id="2bedc-276">Booliano</span><span class="sxs-lookup"><span data-stu-id="2bedc-276">boolean</span></span>|<span data-ttu-id="2bedc-277">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2bedc-277">Required.</span></span> <span data-ttu-id="2bedc-278">Se definir muito**true**, variáveis de ambiente no caminho de saudação são expandidas.</span><span class="sxs-lookup"><span data-stu-id="2bedc-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="2bedc-279">Elemento LocalResource</span><span class="sxs-lookup"><span data-stu-id="2bedc-279">LocalResource Element</span></span>  
 <span data-ttu-id="2bedc-280">Define um recurso de local relativo tooa caminho definido na definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="2bedc-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="2bedc-281">Elemento pai: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="2bedc-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="2bedc-282">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-282">Attributes:</span></span>  

|<span data-ttu-id="2bedc-283">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-283">Attribute</span></span>|<span data-ttu-id="2bedc-284">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-284">Type</span></span>|<span data-ttu-id="2bedc-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-286">**name**</span><span class="sxs-lookup"><span data-stu-id="2bedc-286">**name**</span></span>|<span data-ttu-id="2bedc-287">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-287">string</span></span>|<span data-ttu-id="2bedc-288">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2bedc-288">Required.</span></span> <span data-ttu-id="2bedc-289">nome de saudação do recurso de local de Olá que contém a saudação diretório toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2bedc-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="2bedc-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="2bedc-290">**relativePath**</span></span>|<span data-ttu-id="2bedc-291">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-291">string</span></span>|<span data-ttu-id="2bedc-292">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2bedc-292">Required.</span></span> <span data-ttu-id="2bedc-293">Olá toomonitor do caminho relativo toohello recurso local.</span><span class="sxs-lookup"><span data-stu-id="2bedc-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="2bedc-294">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="2bedc-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="2bedc-295">Define toocollect de contador de desempenho do hello caminho toohello.</span><span class="sxs-lookup"><span data-stu-id="2bedc-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="2bedc-296">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="2bedc-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="2bedc-297">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-297">Attributes:</span></span>  

|<span data-ttu-id="2bedc-298">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-298">Attribute</span></span>|<span data-ttu-id="2bedc-299">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-299">Type</span></span>|<span data-ttu-id="2bedc-300">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="2bedc-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-302">unsignedInt</span></span>|<span data-ttu-id="2bedc-303">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-303">Optional.</span></span> <span data-ttu-id="2bedc-304">Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.</span><span class="sxs-lookup"><span data-stu-id="2bedc-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="2bedc-305">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-305">hello default is 0.</span></span>|  
|<span data-ttu-id="2bedc-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="2bedc-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="2bedc-307">duration</span><span class="sxs-lookup"><span data-stu-id="2bedc-307">duration</span></span>|<span data-ttu-id="2bedc-308">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-308">Optional.</span></span> <span data-ttu-id="2bedc-309">Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="2bedc-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="2bedc-310">padrão de saudação é PT0S.</span><span class="sxs-lookup"><span data-stu-id="2bedc-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="2bedc-311">Elemento PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="2bedc-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="2bedc-312">Define Olá toocollect de contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="2bedc-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="2bedc-313">Elemento pai: [elemento PerformanceCounters](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="2bedc-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="2bedc-314">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-314">Attributes:</span></span>  

|<span data-ttu-id="2bedc-315">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-315">Attribute</span></span>|<span data-ttu-id="2bedc-316">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-316">Type</span></span>|<span data-ttu-id="2bedc-317">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="2bedc-318">**counterSpecifier**</span></span>|<span data-ttu-id="2bedc-319">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-319">string</span></span>|<span data-ttu-id="2bedc-320">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2bedc-320">Required.</span></span> <span data-ttu-id="2bedc-321">Olá toocollect de contador de desempenho do caminho toohello.</span><span class="sxs-lookup"><span data-stu-id="2bedc-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="2bedc-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="2bedc-322">**sampleRate**</span></span>|<span data-ttu-id="2bedc-323">duration</span><span class="sxs-lookup"><span data-stu-id="2bedc-323">duration</span></span>|<span data-ttu-id="2bedc-324">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2bedc-324">Required.</span></span> <span data-ttu-id="2bedc-325">taxa de saudação no qual Olá contador de desempenho deve ser coletado.</span><span class="sxs-lookup"><span data-stu-id="2bedc-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="2bedc-326">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="2bedc-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="2bedc-327">Define Olá toomonitor de logs de eventos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="2bedc-328">Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="2bedc-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="2bedc-329">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-329">Attributes:</span></span>

|<span data-ttu-id="2bedc-330">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-330">Attribute</span></span>|<span data-ttu-id="2bedc-331">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-331">Type</span></span>|<span data-ttu-id="2bedc-332">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2bedc-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="2bedc-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="2bedc-334">unsignedInt</span></span>|<span data-ttu-id="2bedc-335">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-335">Optional.</span></span> <span data-ttu-id="2bedc-336">Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.</span><span class="sxs-lookup"><span data-stu-id="2bedc-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="2bedc-337">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="2bedc-337">hello default is 0.</span></span>|  
|<span data-ttu-id="2bedc-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="2bedc-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="2bedc-339">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-339">string</span></span>|<span data-ttu-id="2bedc-340">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-340">Optional.</span></span> <span data-ttu-id="2bedc-341">Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="2bedc-342">valor padrão de saudação é **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="2bedc-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="2bedc-343">Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="2bedc-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="2bedc-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="2bedc-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="2bedc-345">duration</span><span class="sxs-lookup"><span data-stu-id="2bedc-345">duration</span></span>|<span data-ttu-id="2bedc-346">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2bedc-346">Optional.</span></span> <span data-ttu-id="2bedc-347">Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="2bedc-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="2bedc-348">padrão de saudação é PT0S.</span><span class="sxs-lookup"><span data-stu-id="2bedc-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="2bedc-349">Elemento DataSource</span><span class="sxs-lookup"><span data-stu-id="2bedc-349">DataSource Element</span></span>  
 <span data-ttu-id="2bedc-350">Define Olá toomonitor de log de eventos.</span><span class="sxs-lookup"><span data-stu-id="2bedc-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="2bedc-351">Elemento pai: [elemento WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="2bedc-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="2bedc-352">Atributos:</span><span class="sxs-lookup"><span data-stu-id="2bedc-352">Attributes:</span></span>

|<span data-ttu-id="2bedc-353">Atributo</span><span class="sxs-lookup"><span data-stu-id="2bedc-353">Attribute</span></span>|<span data-ttu-id="2bedc-354">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bedc-354">Type</span></span>|<span data-ttu-id="2bedc-355">Descrição</span><span class="sxs-lookup"><span data-stu-id="2bedc-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2bedc-356">**name**</span><span class="sxs-lookup"><span data-stu-id="2bedc-356">**name**</span></span>|<span data-ttu-id="2bedc-357">string</span><span class="sxs-lookup"><span data-stu-id="2bedc-357">string</span></span>|<span data-ttu-id="2bedc-358">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2bedc-358">Required.</span></span> <span data-ttu-id="2bedc-359">Uma expressão XPath especificando Olá toocollect de log.</span><span class="sxs-lookup"><span data-stu-id="2bedc-359">An XPath expression specifying hello log toocollect.</span></span>|  
