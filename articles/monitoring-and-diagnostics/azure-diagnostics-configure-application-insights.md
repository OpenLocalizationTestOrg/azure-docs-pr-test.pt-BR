---
title: "Configurar o Diagnóstico do Azure para enviar dados ao Application Insights | Microsoft Docs"
description: "Atualize a configuração pública do Diagnóstico do Azure para enviar dados ao Application Insights."
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
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="c56ee-103">Enviar dados de diagnóstico do Serviço de Nuvem, da máquina virtual ou do Service Fabric ao Application Insights</span><span class="sxs-lookup"><span data-stu-id="c56ee-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="c56ee-104">Serviços de nuvem, máquinas virtuais, conjuntos de dimensionamento de máquinas virtuais e o Service Fabric usam a extensão do Diagnóstico do Azure para coletar dados.</span><span class="sxs-lookup"><span data-stu-id="c56ee-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="c56ee-105">O Diagnóstico do Azure envia dados às tabelas do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c56ee-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="c56ee-106">No entanto, também é possível redirecionar todos os dados, ou um subconjunto deles, para outros locais usando a extensão do Diagnóstico do Azure 1.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c56ee-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="c56ee-107">Este artigo descreve como enviar dados da extensão do Diagnóstico do Azure para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c56ee-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="c56ee-108">Explicação da configuração do Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c56ee-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="c56ee-109">A extensão do Diagnóstico do Azure 1.5 introduziu coletores, que são locais adicionais para os quais você pode enviar dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c56ee-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="c56ee-110">Exemplo de configuração de um coletor para o Application Insights:</span><span class="sxs-lookup"><span data-stu-id="c56ee-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="c56ee-111">O atributo **Sink** *name* é um valor de cadeia de caracteres que identifica exclusivamente o coletor.</span><span class="sxs-lookup"><span data-stu-id="c56ee-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="c56ee-112">O elemento **ApplicationInsights** especifica a chave de instrumentação do recurso do Application Insights para onde os dados do Diagnóstico do Azure são enviados.</span><span class="sxs-lookup"><span data-stu-id="c56ee-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="c56ee-113">Se você não tiver um recurso existente do Application Insights, confira [Criar um novo recurso do Application Insights](../application-insights/app-insights-create-new-resource.md) para saber mais sobre como criar um recurso e obter a chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="c56ee-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="c56ee-114">Se você estiver desenvolvendo um Serviço de Nuvem com o Azure SDK 2.8 e posterior, essa chave de instrumentação é preenchida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c56ee-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="c56ee-115">O valor tem base na configuração do serviço **APPINSIGHTS_INSTRUMENTATIONKEY** ao empacotar o projeto de Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="c56ee-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="c56ee-116">Confira [Usar o Application Insights com o Diagnóstico do Azure para solucionar problemas do Serviço de Nuvem](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="c56ee-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="c56ee-117">O elemento **Channels** contém um ou mais elementos **Channel**.</span><span class="sxs-lookup"><span data-stu-id="c56ee-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="c56ee-118">O atributo *name* refere-se exclusivamente a esse canal.</span><span class="sxs-lookup"><span data-stu-id="c56ee-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="c56ee-119">O atributo *loglevel* permite que você especifique o nível de log permitido pelo canal.</span><span class="sxs-lookup"><span data-stu-id="c56ee-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="c56ee-120">Os níveis de log disponíveis, organizados do que contém mais para o que contém menos informações, são:</span><span class="sxs-lookup"><span data-stu-id="c56ee-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="c56ee-121">Detalhado</span><span class="sxs-lookup"><span data-stu-id="c56ee-121">Verbose</span></span>
        - <span data-ttu-id="c56ee-122">Informações</span><span class="sxs-lookup"><span data-stu-id="c56ee-122">Information</span></span>
        - <span data-ttu-id="c56ee-123">Aviso</span><span class="sxs-lookup"><span data-stu-id="c56ee-123">Warning</span></span>
        - <span data-ttu-id="c56ee-124">Erro</span><span class="sxs-lookup"><span data-stu-id="c56ee-124">Error</span></span>
        - <span data-ttu-id="c56ee-125">Crítico</span><span class="sxs-lookup"><span data-stu-id="c56ee-125">Critical</span></span>

<span data-ttu-id="c56ee-126">Um canal funciona como um filtro e permite que você selecione níveis de log específicos para enviar ao coletor de destino.</span><span class="sxs-lookup"><span data-stu-id="c56ee-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="c56ee-127">Por exemplo, você poderia coletar logs detalhados e enviá-los ao armazenamento, mas enviar apenas os Erros ao coletor.</span><span class="sxs-lookup"><span data-stu-id="c56ee-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="c56ee-128">O gráfico a seguir mostra essa relação.</span><span class="sxs-lookup"><span data-stu-id="c56ee-128">The following graphic shows this relationship.</span></span>

![Configuração pública do Diagnóstico](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="c56ee-130">O gráfico a seguir resume os valores de configuração e como eles funcionam.</span><span class="sxs-lookup"><span data-stu-id="c56ee-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="c56ee-131">Você pode incluir vários coletores na configuração em diferentes níveis na hierarquia.</span><span class="sxs-lookup"><span data-stu-id="c56ee-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="c56ee-132">O coletor no nível superior atua como uma configuração global, e o especificado no elemento individual atua como uma substituição daquela configuração global.</span><span class="sxs-lookup"><span data-stu-id="c56ee-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Configuração dos coletores de diagnóstico com o Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="c56ee-134">Exemplo de configuração completa do coletor</span><span class="sxs-lookup"><span data-stu-id="c56ee-134">Complete sink configuration example</span></span>
<span data-ttu-id="c56ee-135">Veja um exemplo completo do arquivo de configuração pública que</span><span class="sxs-lookup"><span data-stu-id="c56ee-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="c56ee-136">envia todos os erros ao Application Insights (especificado no nó **DiagnosticMonitorConfiguration**)</span><span class="sxs-lookup"><span data-stu-id="c56ee-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="c56ee-137">também envia logs de nível Detalhado para os Logs do Aplicativo (especificado no nó **Logs**).</span><span class="sxs-lookup"><span data-stu-id="c56ee-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
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
<span data-ttu-id="c56ee-138">Na configuração anterior, as linhas a seguir apresentam estes significados:</span><span class="sxs-lookup"><span data-stu-id="c56ee-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="c56ee-139">Enviar todos os dados que estão sendo coletados pelo Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="c56ee-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="c56ee-140">Enviar somente logs de erro para o coletor do Application Insights</span><span class="sxs-lookup"><span data-stu-id="c56ee-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="c56ee-141">Enviar logs de aplicativo Detalhados para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="c56ee-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="c56ee-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="c56ee-142">Limitations</span></span>

- <span data-ttu-id="c56ee-143">**Os canais só registro o tipo e não contadores de desempenho.**</span><span class="sxs-lookup"><span data-stu-id="c56ee-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="c56ee-144">Se você especificar um canal com um elemento contador de desempenho, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="c56ee-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="c56ee-145">**O nível de log para um canal não pode exceder o nível de log do que está sendo coletado pelo Diagnóstico do Azure**</span><span class="sxs-lookup"><span data-stu-id="c56ee-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="c56ee-146">Por exemplo: não é possível coletar erros do Log de Aplicativo no elemento Logs e tentar enviar logs Detalhados ao coletor do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c56ee-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="c56ee-147">O atributo *scheduledTransferLogLevelFilter* sempre deve coletar uma quantidade igual ou maior de logs que a quantidade de logs que você está tentando enviar para um coletor.</span><span class="sxs-lookup"><span data-stu-id="c56ee-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="c56ee-148">**Não é possível enviar dados de blob coletados pela extensão do Diagnóstico do Azure ao Application Insights.**</span><span class="sxs-lookup"><span data-stu-id="c56ee-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="c56ee-149">Por exemplo, qualquer coisa especificada no nó *Diretórios*.</span><span class="sxs-lookup"><span data-stu-id="c56ee-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="c56ee-150">No caso de Despejos de Memória, o despejo de memória real é enviado ao armazenamento de blobs, e somente uma notificação da geração do despejo é enviada ao Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c56ee-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c56ee-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c56ee-151">Next Steps</span></span>
* <span data-ttu-id="c56ee-152">Saiba como [exibir as informações de diagnóstico do Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c56ee-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="c56ee-153">Use o [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) para habilitar a extensão do Diagnóstico do Azure para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c56ee-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="c56ee-154">Use o [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para habilitar a extensão do Diagnóstico do Azure para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c56ee-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
