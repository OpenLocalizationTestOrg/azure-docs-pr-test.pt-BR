---
title: "dados de diagnóstico do Azure no afunilamento do hello usando Hubs de eventos de aaaStreaming | Microsoft Docs"
description: "Configurando diagnóstico do Azure com Hubs de eventos final tooend, incluindo diretrizes para cenários comuns."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="f30d0-103">Fluxo de dados de diagnóstico do Azure no afunilamento hello usando Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="f30d0-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="f30d0-104">Diagnóstico do Azure fornece maneiras flexíveis toocollect métricas e registra em log da nuvem de máquinas virtuais de serviços (VMs) e transferir resultados tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f30d0-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="f30d0-105">Iniciando no período de tempo de março de 2016 (SDK 2.9) hello, você pode enviar diagnóstico toocustom fontes de dados e transferir dados de afunilamento em segundos usando [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="f30d0-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="f30d0-106">Entre os tipos de dados com suporte estão:</span><span class="sxs-lookup"><span data-stu-id="f30d0-106">Supported data types include:</span></span>

* <span data-ttu-id="f30d0-107">Eventos de ETW (Rastreamento de Eventos para Windows)</span><span class="sxs-lookup"><span data-stu-id="f30d0-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="f30d0-108">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="f30d0-108">Performance counters</span></span>
* <span data-ttu-id="f30d0-109">Logs de eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="f30d0-109">Windows event logs</span></span>
* <span data-ttu-id="f30d0-110">Logs de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f30d0-110">Application logs</span></span>
* <span data-ttu-id="f30d0-111">Logs de infraestrutura do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="f30d0-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="f30d0-112">Este artigo mostra como o diagnóstico do Azure tooconfigure com Hubs de eventos de encerrar tooend.</span><span class="sxs-lookup"><span data-stu-id="f30d0-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="f30d0-113">Também são fornecidas diretrizes para Olá cenários comuns a seguir:</span><span class="sxs-lookup"><span data-stu-id="f30d0-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="f30d0-114">Como toocustomize Olá registra em log e métricas que sejam enviadas tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="f30d0-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="f30d0-115">Como as configurações de toochange em cada ambiente</span><span class="sxs-lookup"><span data-stu-id="f30d0-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="f30d0-116">Como os Hubs de eventos tooview fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="f30d0-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="f30d0-117">Como tootroubleshoot Olá conexão</span><span class="sxs-lookup"><span data-stu-id="f30d0-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="f30d0-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f30d0-118">Prerequisites</span></span>
<span data-ttu-id="f30d0-119">Há suporte para dados de receieving de Hubs de eventos do diagnóstico do Azure em serviços de nuvem, máquinas virtuais, conjuntos de escala de máquinas virtuais e Service Fabric partir hello Azure SDK 2.9 e Olá correspondente ferramentas do Azure para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f30d0-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="f30d0-120">Extensão 1.6 do Diagnóstico do Azure (o[SDK do Azure para .NET 2.9 ou posterior](https://azure.microsoft.com/downloads/) resolve isso por padrão)</span><span class="sxs-lookup"><span data-stu-id="f30d0-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="f30d0-121">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f30d0-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="f30d0-122">As configurações existentes do diagnóstico do Azure em um aplicativo usando um *.wadcfgx* de arquivo e um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f30d0-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="f30d0-123">Visual Studio: [Configurando o Diagnóstico para os Serviços de Nuvem e máquinas virtuais do Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="f30d0-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="f30d0-124">Windows PowerShell: [Habilitar o Diagnóstico nos Serviços de Nuvem do Azure usando o PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f30d0-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="f30d0-125">Namespace de Hubs de evento provisionado por artigo hello, [Introdução aos Hubs de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="f30d0-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="f30d0-126">Conecte-se o coletor de Hubs de tooEvent de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="f30d0-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="f30d0-127">Por padrão, o diagnóstico do Azure sempre envia logs e métricas tooan conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f30d0-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="f30d0-128">Um aplicativo também pode enviar dados tooEvent Hubs adicionando um novo **coletores** seção em Olá **PublicConfig** / **WadCfg** elemento de saudação *.wadcfgx* arquivo.</span><span class="sxs-lookup"><span data-stu-id="f30d0-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="f30d0-129">No Visual Studio, Olá *.wadcfgx* arquivo é armazenado no Olá que caminho a seguir: **projeto de serviço de nuvem** > **funções** > **( RoleName)** > **wadcfgx** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f30d0-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="f30d0-130">Neste exemplo, hub de eventos Olá URL é definida toohello totalmente qualificado de namespace de hub de eventos Olá: namespace de Hubs de eventos + "/" + nome de hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="f30d0-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="f30d0-131">hub de eventos Olá URL é exibido no hello [portal do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) no painel de Hubs de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f30d0-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="f30d0-132">Olá **coletor** nome pode ser definido a cadeia de caracteres válida tooany como hello mesmo valor é usado consistentemente em todo o arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f30d0-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="f30d0-133">Pode haver outros coletores configurados nesta seção, como o *applicationInsights* .</span><span class="sxs-lookup"><span data-stu-id="f30d0-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="f30d0-134">O diagnóstico do Azure permite que um ou mais coletores toobe definido se cada coletor também for declarado em Olá **PrivateConfig** seção.</span><span class="sxs-lookup"><span data-stu-id="f30d0-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="f30d0-135">Olá coletor de Hubs de eventos também deve ser declarado e definido em Olá **PrivateConfig** seção Olá *.wadcfgx* arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="f30d0-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="f30d0-136">Olá `SharedAccessKeyName` valor deve corresponder a uma chave de assinatura de acesso compartilhado (SAS) e a política que foi definida no hello **Hubs de eventos** namespace.</span><span class="sxs-lookup"><span data-stu-id="f30d0-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="f30d0-137">Procurar toohello painel de Hubs de eventos no hello [portal do Azure](https://manage.windowsazure.com), clique em Olá **configurar** guia e configurar uma regra nomeada (por exemplo, "SendRule") que tem *enviar* permissões.</span><span class="sxs-lookup"><span data-stu-id="f30d0-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="f30d0-138">Olá **StorageAccount** também é declarado em **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="f30d0-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="f30d0-139">Não é necessário toochange valores aqui se estão funcionando.</span><span class="sxs-lookup"><span data-stu-id="f30d0-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="f30d0-140">Neste exemplo, podemos deixe Olá valores vazios, que é um sinal de que um ativo de downstream definirá valores hello.</span><span class="sxs-lookup"><span data-stu-id="f30d0-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="f30d0-141">Por exemplo, Olá *ServiceConfiguration* arquivo de configuração de ambiente define nomes de ambiente apropriado hello e chaves.</span><span class="sxs-lookup"><span data-stu-id="f30d0-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="f30d0-142">chave de SAS de Hubs de evento de saudação é armazenada em texto sem formatação no hello *.wadcfgx* arquivo.</span><span class="sxs-lookup"><span data-stu-id="f30d0-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="f30d0-143">Normalmente, essa chave é verificada no controle do código toosource ou está disponível como um ativo no seu servidor de compilação, portanto, deve protegê-lo conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="f30d0-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="f30d0-144">Recomendamos que você use uma chave SAS com *apenas enviar* permissões para que um usuário mal-intencionado pode gravar toohello hub de eventos, mas não escutar tooit ou gerenciá-lo.</span><span class="sxs-lookup"><span data-stu-id="f30d0-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="f30d0-145">Configurar o diagnóstico do Azure toosend logs e métricas tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="f30d0-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="f30d0-146">Como discutido anteriormente, todos os dados de diagnóstico personalizado e padrão, ou seja, as métricas e os logs, é enviado automaticamente tooAzure armazenamento em intervalos de saudação configurado.</span><span class="sxs-lookup"><span data-stu-id="f30d0-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="f30d0-147">Com Hubs de eventos e qualquer coletor adicional, você pode especificar qualquer nó raiz ou folha em Olá hierarquia toobe enviado toohello hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="f30d0-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="f30d0-148">Isso inclui eventos de ETW, contadores de desempenho, logs de eventos do Windows e logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f30d0-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="f30d0-149">É importante tooconsider quantos pontos de dados, na verdade, devem ser transferidos tooEvent Hubs.</span><span class="sxs-lookup"><span data-stu-id="f30d0-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="f30d0-150">Normalmente, os desenvolvedores transferem dados de caminhos recorrentes e de baixa latência, que devem ser consumidos e interpretados rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f30d0-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="f30d0-151">Os sistemas que monitoram os alertas ou as regras de dimensionamento automático são exemplos.</span><span class="sxs-lookup"><span data-stu-id="f30d0-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="f30d0-152">Um desenvolvedor também pode configurar um repositório de análise alternativo ou um repositório de pesquisa – por exemplo, o Stream Analytics do Azure, o Elasticsearch, um sistema de monitoramento personalizado ou um sistema de monitoramento favorito de outros usuários.</span><span class="sxs-lookup"><span data-stu-id="f30d0-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="f30d0-153">Olá seguem alguns exemplos de configurações.</span><span class="sxs-lookup"><span data-stu-id="f30d0-153">hello following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="f30d0-154">Olá exemplo acima, coletor Olá é aplicado toohello pai **PerformanceCounters** nó na hierarquia de saudação, o que significa que todos os filhos **PerformanceCounters** tooEvent Hubs será enviado.</span><span class="sxs-lookup"><span data-stu-id="f30d0-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="f30d0-155">No exemplo anterior de saudação, o coletor de saudação está aplicada tooonly três contadores: **solicitações em fila**, **solicitações rejeitadas**, e **% tempo do processador**.</span><span class="sxs-lookup"><span data-stu-id="f30d0-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="f30d0-156">Olá exemplo a seguir mostra como um desenvolvedor pode limitar Olá dados enviados toobe Olá métricas críticas que são usadas para integridade do serviço.</span><span class="sxs-lookup"><span data-stu-id="f30d0-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="f30d0-157">Neste exemplo, o coletor de hello está aplicada toologs e é filtrado rastreamento de nível de tooerror somente.</span><span class="sxs-lookup"><span data-stu-id="f30d0-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="f30d0-158">Implantar e atualizar uma configuração de aplicativo e diagnóstico dos Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="f30d0-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="f30d0-159">Visual Studio fornece a aplicativo do hello mais fácil caminho toodeploy hello e configuração do coletor de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="f30d0-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="f30d0-160">arquivo de Olá tooview e editar, abrir Olá *.wadcfgx* de arquivo no Visual Studio, editá-lo e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="f30d0-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="f30d0-161">caminho de saudação é **projeto de serviço de nuvem** > **funções** > **(RoleName)** > **wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="f30d0-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="f30d0-162">Neste ponto, todos os implantação e implantação de atualização de ações no Visual Studio, o Visual Studio Team System e todos os comandos ou scripts que são baseadas no MSBuild e usam o hello **/t: publicar** destino incluem hello *.wadcfgx*  no processo de empacotamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="f30d0-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="f30d0-163">Além disso, as implantações e atualizações implantar Olá tooAzure de arquivo usando a extensão do agente de diagnóstico do Azure apropriada Olá em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="f30d0-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="f30d0-164">Depois de implantar o aplicativo hello e configuração de diagnóstico do Azure, você verá imediatamente atividade no painel de saudação do hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f30d0-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="f30d0-165">Isso indica que você está pronto toomove nos dados de caminho hot tooviewing Olá na ferramenta de cliente ou análise de ouvinte de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f30d0-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="f30d0-166">Olá figura a seguir, painel de Hubs de eventos Olá mostra envio Íntegro de diagnóstico dados toohello evento hub iniciando em algum momento depois de 11 PM.</span><span class="sxs-lookup"><span data-stu-id="f30d0-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="f30d0-167">Ou seja, quando Olá aplicativo foi implantado com atualizada *.wadcfgx* de arquivo e Olá coletor foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="f30d0-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="f30d0-168">Quando você fizer o arquivo de configuração de diagnóstico do Azure do atualizações toohello (.wadcfgx), é recomendável que você enviar por push Olá atualizações toohello todo o aplicativo, bem como a configuração de saudação usando a publicação do Visual Studio ou um script do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f30d0-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="f30d0-169">Exibir dados de caminhos recorrentes</span><span class="sxs-lookup"><span data-stu-id="f30d0-169">View hot-path data</span></span>
<span data-ttu-id="f30d0-170">Como discutido anteriormente, há muitos casos de uso para escuta tooand processamento de dados de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="f30d0-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="f30d0-171">Uma abordagem simple é toocreate um hub de eventos do teste pequena console aplicativo toolisten toohello e fluxo de saída de impressão hello.</span><span class="sxs-lookup"><span data-stu-id="f30d0-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="f30d0-172">Você pode colocar Olá código, que é explicado mais detalhadamente a seguir [Introdução aos Hubs de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), em um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="f30d0-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="f30d0-173">Observe que o aplicativo de console hello deve incluir Olá [pacote NuGet de Host de processador de evento](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="f30d0-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="f30d0-174">Lembre-se de valores de saudação tooreplace colchetes angulares em Olá **principal** função com valores para os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="f30d0-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="f30d0-175">Solucionar problemas dos coletores dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f30d0-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="f30d0-176">hub de eventos de saudação não mostra a atividade de evento de entrada ou saída conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="f30d0-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="f30d0-177">Verifique se o seu hub de eventos foi provisionado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f30d0-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="f30d0-178">Todas as informações de conexão em Olá **PrivateConfig** seção *.wadcfgx* devem corresponder a valores de saudação do recurso, como visto no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="f30d0-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="f30d0-179">Certifique-se de que você tenha uma SAS política definida ("SendRule" no exemplo hello) no portal de saudação e que *enviar* permissão é concedida.</span><span class="sxs-lookup"><span data-stu-id="f30d0-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="f30d0-180">Após uma atualização, o hub de eventos de saudação não mostra a atividade de eventos de entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="f30d0-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="f30d0-181">Primeiro, verifique se esse hub de eventos hello e informações de configuração estão correta, conforme explicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f30d0-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="f30d0-182">Às vezes, Olá **PrivateConfig** é redefinida em uma atualização de implantação.</span><span class="sxs-lookup"><span data-stu-id="f30d0-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="f30d0-183">Olá recomendado correção é toomake todas as alterações muito*.wadcfgx* em Olá projeto e, em seguida, enviar por push uma atualização completa do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f30d0-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="f30d0-184">Se isso não for possível, certifique-se de atualização diagnóstico Olá envia uma completa **PrivateConfig** que inclui a chave de SAS hello.</span><span class="sxs-lookup"><span data-stu-id="f30d0-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="f30d0-185">Tentativa de sugestões de saudação e hub de eventos Olá ainda não está funcionando.</span><span class="sxs-lookup"><span data-stu-id="f30d0-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="f30d0-186">Procure na tabela de armazenamento do Azure Olá que contém erros e logs de diagnóstico do Azure em si: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="f30d0-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="f30d0-187">Uma opção é toouse uma ferramenta como [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect conta de armazenamento toothis, exibir essa tabela e adicionar uma consulta para o carimbo de hora no hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f30d0-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="f30d0-188">Você pode usar a ferramenta de saudação tooexport um arquivo. csv e abri-lo em um aplicativo como o Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="f30d0-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="f30d0-189">Excel torna fácil toosearch para cadeias de caracteres de cartão, como **EventHubs**, toosee o erro é relatado.</span><span class="sxs-lookup"><span data-stu-id="f30d0-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f30d0-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f30d0-190">Next steps</span></span>
<span data-ttu-id="f30d0-191">•    [Saiba mais sobre os Hubs de Eventos](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="f30d0-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="f30d0-192">Apêndice: Concluir o exemplo de arquivo de configuração do Diagnóstico do Azure (.wadcfgx)</span><span class="sxs-lookup"><span data-stu-id="f30d0-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="f30d0-193">Olá complementar *ServiceConfiguration* para este exemplo semelhante ao seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="f30d0-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="f30d0-194">Configurações equivalentes baseada em Json para máquinas virtuais são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="f30d0-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
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
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="f30d0-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f30d0-195">Next steps</span></span>
<span data-ttu-id="f30d0-196">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="f30d0-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="f30d0-197">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f30d0-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="f30d0-198">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="f30d0-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="f30d0-199">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f30d0-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
