---
title: "aaaConfigure diagnóstico do Azure toosend dados tooApplication Insights | Microsoft Docs"
description: "Atualize Olá diagnóstico do Azure configuração pública toosend dados tooApplication Insights."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="1e63f-103">Enviar dados de diagnóstico de serviço de nuvem, Máquina Virtual ou do Service Fabric tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="1e63f-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="1e63f-104">Serviços de nuvem, máquinas virtuais, conjuntos de escala de máquinas virtuais e Service Fabric saudação de uso de todos os dados de toocollect de extensão de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e63f-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="1e63f-105">Diagnóstico do Azure envia dados tooAzure tabelas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1e63f-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="1e63f-106">No entanto, você também pode pipe todos ou um subconjunto Olá tooother de locais de dados usando a extensão de diagnóstico do Azure 1.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1e63f-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="1e63f-107">Este artigo descreve como dados toosend Olá tooApplication de extensão de diagnóstico do Azure Insights.</span><span class="sxs-lookup"><span data-stu-id="1e63f-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="1e63f-108">Explicação da configuração do Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="1e63f-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="1e63f-109">Olá Coletores de extensão 1.5 introduzida o diagnóstico do Azure, que são locais adicionais, onde você pode enviar dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="1e63f-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="1e63f-110">Exemplo de configuração de um coletor para o Application Insights:</span><span class="sxs-lookup"><span data-stu-id="1e63f-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="1e63f-111">Olá **coletor** *nome* atributo é um valor de cadeia de caracteres que identifica exclusivamente o coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e63f-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="1e63f-112">Olá **ApplicationInsights** elemento Especifica a chave de instrumentação da saudação onde Olá dados de diagnóstico do Azure é enviado do recurso do Application insights.</span><span class="sxs-lookup"><span data-stu-id="1e63f-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="1e63f-113">Se você não tiver um recurso existente do Application Insights, consulte [criar um novo recurso do Application Insights](../application-insights/app-insights-create-new-resource.md) para obter mais informações sobre como criar um recurso e obter a chave de instrumentação hello.</span><span class="sxs-lookup"><span data-stu-id="1e63f-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="1e63f-114">Se você estiver desenvolvendo um Serviço de Nuvem com o Azure SDK 2.8 e posterior, essa chave de instrumentação é preenchida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1e63f-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="1e63f-115">valor Olá baseia-se a saudação **APPINSIGHTS_INSTRUMENTATIONKEY** configuração de serviço ao empacotar um projeto de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="1e63f-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="1e63f-116">Consulte [problemas de serviço de nuvem Use Application Insights com o diagnóstico do Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="1e63f-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="1e63f-117">Olá **canais** elemento contém um ou mais **Channel** elementos.</span><span class="sxs-lookup"><span data-stu-id="1e63f-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="1e63f-118">Olá *nome* exclusivamente refere-se o atributo toothat canal.</span><span class="sxs-lookup"><span data-stu-id="1e63f-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="1e63f-119">Olá *loglevel* atributo permite que você especifique o nível de log Olá Olá canal permite.</span><span class="sxs-lookup"><span data-stu-id="1e63f-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="1e63f-120">Olá níveis de log disponíveis na ordem da maioria das informações de tooleast são:</span><span class="sxs-lookup"><span data-stu-id="1e63f-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="1e63f-121">Detalhado</span><span class="sxs-lookup"><span data-stu-id="1e63f-121">Verbose</span></span>
        - <span data-ttu-id="1e63f-122">Informações</span><span class="sxs-lookup"><span data-stu-id="1e63f-122">Information</span></span>
        - <span data-ttu-id="1e63f-123">Aviso</span><span class="sxs-lookup"><span data-stu-id="1e63f-123">Warning</span></span>
        - <span data-ttu-id="1e63f-124">Erro</span><span class="sxs-lookup"><span data-stu-id="1e63f-124">Error</span></span>
        - <span data-ttu-id="1e63f-125">Crítico</span><span class="sxs-lookup"><span data-stu-id="1e63f-125">Critical</span></span>

<span data-ttu-id="1e63f-126">Um canal atua como um filtro e permite que você tooselect log específico níveis toosend toohello destino coletor.</span><span class="sxs-lookup"><span data-stu-id="1e63f-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="1e63f-127">Por exemplo, você pode coletar logs detalhados e enviá-los toostorage, mas enviar somente coletor de toohello de erros.</span><span class="sxs-lookup"><span data-stu-id="1e63f-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="1e63f-128">Olá gráfico a seguir mostra essa relação.</span><span class="sxs-lookup"><span data-stu-id="1e63f-128">hello following graphic shows this relationship.</span></span>

![Configuração pública do Diagnóstico](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="1e63f-130">Olá gráfico a seguir resume os valores de configuração hello e como elas funcionam.</span><span class="sxs-lookup"><span data-stu-id="1e63f-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="1e63f-131">Você pode incluir vários coletores na configuração de saudação em diferentes níveis na hierarquia de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e63f-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="1e63f-132">Olá coletor no nível superior Olá atua como uma configuração global e hello um especificado em Olá individual elemento age como uma configuração global de toothat de substituição.</span><span class="sxs-lookup"><span data-stu-id="1e63f-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Configuração dos coletores de diagnóstico com o Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="1e63f-134">Exemplo de configuração completa do coletor</span><span class="sxs-lookup"><span data-stu-id="1e63f-134">Complete sink configuration example</span></span>
<span data-ttu-id="1e63f-135">Aqui está um exemplo completo de configuração pública Olá arquivo</span><span class="sxs-lookup"><span data-stu-id="1e63f-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="1e63f-136">envia todos os erros tooApplication Insights (especificado no hello **DiagnosticMonitorConfiguration** nó)</span><span class="sxs-lookup"><span data-stu-id="1e63f-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="1e63f-137">também envia logs detalhados de nível para Olá Logs de aplicativo (especificado no hello **Logs** nó).</span><span class="sxs-lookup"><span data-stu-id="1e63f-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="1e63f-138">Configuração anterior do hello, Olá linhas a seguir têm Olá significados a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e63f-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="1e63f-139">Enviar todos os dados de saudação que estão sendo coletados pelo diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="1e63f-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="1e63f-140">Enviar somente logs toohello Application Insights coletor de erros</span><span class="sxs-lookup"><span data-stu-id="1e63f-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="1e63f-141">Enviar logs de aplicativo detalhado tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="1e63f-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="1e63f-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="1e63f-142">Limitations</span></span>

- <span data-ttu-id="1e63f-143">**Os canais só registro o tipo e não contadores de desempenho.**</span><span class="sxs-lookup"><span data-stu-id="1e63f-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="1e63f-144">Se você especificar um canal com um elemento contador de desempenho, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="1e63f-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="1e63f-145">**nível de log Olá para um canal não pode exceder o nível de log Olá para o que está sendo coletado pelo diagnóstico do Azure.**</span><span class="sxs-lookup"><span data-stu-id="1e63f-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="1e63f-146">Por exemplo, você não pode coletar erros do Log de aplicativo no elemento de Logs hello e tente toosend logs detalhados toohello Application Insight coletor.</span><span class="sxs-lookup"><span data-stu-id="1e63f-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="1e63f-147">Olá *scheduledTransferLogLevelFilter* atributo sempre deve coletar igual ou mais logs de saudação logs que você estão tentando toosend tooa coletor.</span><span class="sxs-lookup"><span data-stu-id="1e63f-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="1e63f-148">**Você não pode enviar dados blob coletados pelo diagnóstico do Azure extensão tooApplication Insights.**</span><span class="sxs-lookup"><span data-stu-id="1e63f-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="1e63f-149">Por exemplo, nada especificado em Olá *diretórios* nó.</span><span class="sxs-lookup"><span data-stu-id="1e63f-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="1e63f-150">Despejos de memória Olá real despejo de memória é enviado tooblob armazenamento e apenas uma notificação que Olá despejo de memória foi gerada é enviada tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="1e63f-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e63f-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e63f-151">Next Steps</span></span>
* <span data-ttu-id="1e63f-152">Saiba como muito[exibir suas informações de diagnóstico do Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1e63f-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="1e63f-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable Olá extensão de diagnóstico do Azure para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1e63f-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="1e63f-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable Olá extensão de diagnóstico do Azure para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e63f-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
