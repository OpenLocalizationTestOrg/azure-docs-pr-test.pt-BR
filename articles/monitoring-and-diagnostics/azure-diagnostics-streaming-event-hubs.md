---
title: "Transmitindo dados do Diagnóstico do Azure no afunilamento usando os Hubs de Eventos | Microsoft Docs"
description: "Configurando o Diagnóstico do Azure com os Hubs de Eventos de ponta a ponta, incluindo diretrizes para cenários comuns."
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
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="2bb34-103">Streaming de dados de Diagnóstico do Azure no afunilamento usando os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="2bb34-104">O Diagnóstico do Azure fornece maneiras flexíveis para coletar as métricas e os logs das VMs (máquinas virtuais) dos serviços de nuvem e para transferir os resultados para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb34-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="2bb34-105">A partir de março de 2016 (SDK 2.9), você poderá enviar o Diagnóstico para fontes de dados personalizadas e transferir dados do afunilamento em questão de segundos usando os [Hubs de Eventos do Azure](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="2bb34-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="2bb34-106">Entre os tipos de dados com suporte estão:</span><span class="sxs-lookup"><span data-stu-id="2bb34-106">Supported data types include:</span></span>

* <span data-ttu-id="2bb34-107">Eventos de ETW (Rastreamento de Eventos para Windows)</span><span class="sxs-lookup"><span data-stu-id="2bb34-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="2bb34-108">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="2bb34-108">Performance counters</span></span>
* <span data-ttu-id="2bb34-109">Logs de eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="2bb34-109">Windows event logs</span></span>
* <span data-ttu-id="2bb34-110">Logs de aplicativo</span><span class="sxs-lookup"><span data-stu-id="2bb34-110">Application logs</span></span>
* <span data-ttu-id="2bb34-111">Logs de infraestrutura do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb34-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="2bb34-112">Este artigo mostra como configurar completamente o Diagnóstico do Azure com os Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="2bb34-113">Também são fornecidas diretrizes para os seguintes cenários comuns:</span><span class="sxs-lookup"><span data-stu-id="2bb34-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="2bb34-114">Como personalizar os logs e as métricas que são enviados para os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="2bb34-115">Como alterar as configurações em cada ambiente</span><span class="sxs-lookup"><span data-stu-id="2bb34-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="2bb34-116">Como exibir dados de fluxo dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="2bb34-117">Como solucionar problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="2bb34-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="2bb34-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2bb34-118">Prerequisites</span></span>
<span data-ttu-id="2bb34-119">Há suporte para o recebimento de dados pelos Hubs de Eventos do Diagnóstico do Azure nos Serviços de Nuvem, em VMs, nos Conjuntos de Dimensionamento de Máquinas Virtuais e no Service Fabric a partir do SDK do Azure 2.9 e nas Ferramentas do Azure para Visual Studio correspondentes.</span><span class="sxs-lookup"><span data-stu-id="2bb34-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="2bb34-120">Extensão 1.6 do Diagnóstico do Azure (o[SDK do Azure para .NET 2.9 ou posterior](https://azure.microsoft.com/downloads/) resolve isso por padrão)</span><span class="sxs-lookup"><span data-stu-id="2bb34-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="2bb34-121">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2bb34-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="2bb34-122">As configurações existentes do Diagnóstico do Azure em um aplicativo usando um arquivo *.wadcfgx* e um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="2bb34-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="2bb34-123">Visual Studio: [Configurando o Diagnóstico para os Serviços de Nuvem e máquinas virtuais do Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="2bb34-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="2bb34-124">Windows PowerShell: [Habilitar o Diagnóstico nos Serviços de Nuvem do Azure usando o PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="2bb34-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="2bb34-125">Namespace de Hubs de Eventos provisionado de acordo com o artigo [Introdução aos Hubs de Evento](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="2bb34-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="2bb34-126">Conectar o Diagnóstico do Azure no coletor dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="2bb34-127">Por padrão, o Diagnóstico do Azure sempre envia logs e métricas para uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb34-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="2bb34-128">Um aplicativo também pode enviar dados para os Hubs de Eventos adicionando uma nova seção **Coletores** ao elemento **PublicConfig** / **WadCfg** do arquivo *.wadcfgx*.</span><span class="sxs-lookup"><span data-stu-id="2bb34-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="2bb34-129">No Visual Studio, o arquivo *.wadcfgx* é armazenado no seguinte caminho: **Projeto do Serviço de Nuvem** > **Funções** > **(RoleName)** > **arquivo diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="2bb34-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="2bb34-130">Neste exemplo, a URL do hub de eventos é definida no namespace totalmente qualificado do hub de eventos: namespace de hubs de eventos + "/" + nome do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="2bb34-131">A URL do hub de eventos é exibida no [Portal do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) , no painel Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="2bb34-132">O nome do **Coletor** pode ser definido como qualquer cadeia de caracteres válida, desde que o mesmo valor seja usado de maneira consistente no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="2bb34-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="2bb34-133">Pode haver outros coletores configurados nesta seção, como o *applicationInsights* .</span><span class="sxs-lookup"><span data-stu-id="2bb34-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="2bb34-134">O Diagnóstico do Azure permitirá a definição de um ou mais coletores, se cada coletor também for declarado na seção **PrivateConfig** .</span><span class="sxs-lookup"><span data-stu-id="2bb34-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="2bb34-135">O coletor do Hubs de Eventos também deve ser declarado e definido na seção **PrivateConfig** do arquivo de configuração *.wadcfgx* .</span><span class="sxs-lookup"><span data-stu-id="2bb34-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="2bb34-136">O valor `SharedAccessKeyName` deve ser compatível com uma chave de SAS (Assinatura de Acesso Compartilhado) e com uma política definida no namespace **Hubs de Eventos** .</span><span class="sxs-lookup"><span data-stu-id="2bb34-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="2bb34-137">Navegue até o painel Hubs de Eventos no [Portal do Azure](https://manage.windowsazure.com), clique na guia **Configurar** e configure uma política nomeada (por exemplo, "SendRule") que tenha permissões de *Envio* .</span><span class="sxs-lookup"><span data-stu-id="2bb34-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="2bb34-138">A **StorageAccount** também é declarada em **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="2bb34-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="2bb34-139">Não é necessário alterar os valores aqui se eles estiverem funcionando.</span><span class="sxs-lookup"><span data-stu-id="2bb34-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="2bb34-140">Neste exemplo, deixamos os valores vazios, o que é um sinal de que um ativo de downstream definirá os valores.</span><span class="sxs-lookup"><span data-stu-id="2bb34-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="2bb34-141">Por exemplo, o arquivo de configuração do ambiente *ServiceConfiguration.Cloud.cscfg* define as chaves e os nomes apropriados do ambiente.</span><span class="sxs-lookup"><span data-stu-id="2bb34-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="2bb34-142">A chave de SAS dos Hubs de Eventos é armazenada em texto sem formatação no arquivo *.wadcfgx* .</span><span class="sxs-lookup"><span data-stu-id="2bb34-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="2bb34-143">Muitas vezes, essa chave é verificada no controle do código-fonte ou está disponível como um ativo no servidor de build e, portanto, você deve protegê-la de maneira apropriada.</span><span class="sxs-lookup"><span data-stu-id="2bb34-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="2bb34-144">É recomendável usar uma chave de SAS com permissões do tipo *Somente envio* , de forma que um usuário mal-intencionado possa gravar no hub de eventos, mas não escutar nele nem gerenciá-lo.</span><span class="sxs-lookup"><span data-stu-id="2bb34-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="2bb34-145">Configurar o Diagnóstico do Azure para enviar logs e métricas para os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="2bb34-146">Como abordado anteriormente, todos os dados de diagnóstico padrão e personalizados, ou seja, as métricas e os logs, são automaticamente enviados para o Armazenamento do Azure em intervalos configurados.</span><span class="sxs-lookup"><span data-stu-id="2bb34-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="2bb34-147">Com os Hubs de Eventos e com qualquer coletor adicional, é possível especificar o envio de qualquer nó raiz ou folha na hierarquia para o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="2bb34-148">Isso inclui eventos de ETW, contadores de desempenho, logs de eventos do Windows e logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2bb34-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="2bb34-149">É importante considerar quantos pontos de dados devem ser transferidos para os Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="2bb34-150">Normalmente, os desenvolvedores transferem dados de caminhos recorrentes e de baixa latência, que devem ser consumidos e interpretados rapidamente.</span><span class="sxs-lookup"><span data-stu-id="2bb34-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="2bb34-151">Os sistemas que monitoram os alertas ou as regras de dimensionamento automático são exemplos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="2bb34-152">Um desenvolvedor também pode configurar um repositório de análise alternativo ou um repositório de pesquisa – por exemplo, o Stream Analytics do Azure, o Elasticsearch, um sistema de monitoramento personalizado ou um sistema de monitoramento favorito de outros usuários.</span><span class="sxs-lookup"><span data-stu-id="2bb34-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="2bb34-153">Veja a seguir alguns exemplos de configurações.</span><span class="sxs-lookup"><span data-stu-id="2bb34-153">The following are some example configurations.</span></span>

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

<span data-ttu-id="2bb34-154">No exemplo acima, o coletor é aplicado ao nó pai **PerformanceCounters** na hierarquia, o que significa que todos os **PerformanceCounters** filho serão enviados aos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

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

<span data-ttu-id="2bb34-155">No exemplo anterior, o coletor é aplicado a apenas três contadores: **Solicitações Enfileiradas**, **Solicitações Rejeitadas** e **% do Tempo do processador**.</span><span class="sxs-lookup"><span data-stu-id="2bb34-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="2bb34-156">O exemplo a seguir mostra como um desenvolvedor pode limitar a quantidade de dados enviados, a fim de definir as métricas essenciais que são usadas para a integridade deste serviço.</span><span class="sxs-lookup"><span data-stu-id="2bb34-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="2bb34-157">Neste exemplo, o coletor é aplicado aos logs e é filtrado apenas para o rastreamento de nível de erro.</span><span class="sxs-lookup"><span data-stu-id="2bb34-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="2bb34-158">Implantar e atualizar uma configuração de aplicativo e diagnóstico dos Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="2bb34-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="2bb34-159">O Visual Studio fornece o caminho mais fácil para implantar o aplicativo e a configuração do coletor de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="2bb34-160">Para exibir e editar o arquivo, abra o arquivo *.wadcfgx* no Visual Studio, edite e salve-o.</span><span class="sxs-lookup"><span data-stu-id="2bb34-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="2bb34-161">O caminho é **Projeto do Serviço de Nuvem** > **Funções** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="2bb34-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="2bb34-162">Neste ponto, todas as implantações e ações de atualização de implantações no Visual Studio, no Visual Studio Team System e em todos os comandos ou scripts que são baseados no MSBuild e usam o destino **/t:publish** incluem o *.wadcfgx* no processo de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="2bb34-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="2bb34-163">Além disso, as implantações e atualizações implantam o arquivo no Azure usando a extensão apropriada do agente de Diagnóstico do Azure em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="2bb34-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="2bb34-164">Depois de implantar o aplicativo e a configuração do Diagnóstico do Azure, você imediatamente verá a atividade no painel do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="2bb34-165">Isso indica que você está pronto para começar a ver os dados do afunilamento no cliente ouvinte ou na ferramenta de análise de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="2bb34-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="2bb34-166">Na figura a seguir, o painel Hub de Eventos mostra os envios íntegros dos dados de diagnóstico para o hub de eventos começando em algum momento depois das 23:00.</span><span class="sxs-lookup"><span data-stu-id="2bb34-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="2bb34-167">Ou seja, quando o aplicativo foi implantado com um arquivo *.wadcfgx* atualizado e o coletor foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2bb34-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="2bb34-168">Quando você faz atualizações no arquivo de configuração do Diagnóstico do Azure (.wadcfgx), é recomendável o envio por push das atualizações para todo o aplicativo, bem como a configuração usando a publicação do Visual Studio ou o script do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb34-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="2bb34-169">Exibir dados de caminhos recorrentes</span><span class="sxs-lookup"><span data-stu-id="2bb34-169">View hot-path data</span></span>
<span data-ttu-id="2bb34-170">Como discutido anteriormente, há muitos casos de uso sobre ouvir e processar os dados dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="2bb34-171">Uma abordagem simples é criar um pequeno aplicativo de console de teste para escutar o hub de eventos e imprimir a transmissão de saída.</span><span class="sxs-lookup"><span data-stu-id="2bb34-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="2bb34-172">Você pode colocar o código a seguir, que é explicado em mais detalhes na [Introdução aos Hubs de Evento](../event-hubs/event-hubs-csharp-ephcs-getstarted.md), em um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="2bb34-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="2bb34-173">Observe que o aplicativo de console deve incluir o [pacote NuGet do Host do Processador de Eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="2bb34-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="2bb34-174">Lembre-se de substituir os valores entre colchetes angulares na função **Main** pelos valores de seus recursos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="2bb34-175">Solucionar problemas dos coletores dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="2bb34-176">O hub de eventos não mostra a atividade de entrada ou saída de eventos conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="2bb34-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="2bb34-177">Verifique se o seu hub de eventos foi provisionado com êxito.</span><span class="sxs-lookup"><span data-stu-id="2bb34-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="2bb34-178">Todas as informações de conexão na seção **PrivateConfig** de *.wadcfgx* devem corresponder aos valores de seu recurso, como visto no portal.</span><span class="sxs-lookup"><span data-stu-id="2bb34-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="2bb34-179">Verifique se você tem uma política SAS definida ("SendRule", no exemplo) no portal e se a permissão de *Envio* foi concedida.</span><span class="sxs-lookup"><span data-stu-id="2bb34-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="2bb34-180">Depois de uma atualização, o hub de eventos não mostrará mais a atividade de entrada ou saída dos eventos.</span><span class="sxs-lookup"><span data-stu-id="2bb34-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="2bb34-181">Primeiro, verifique se as informações do hub de eventos e de configuração estão corretas, conforme explicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2bb34-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="2bb34-182">Às vezes, **PrivateConfig** é redefinida em uma atualização de implantação.</span><span class="sxs-lookup"><span data-stu-id="2bb34-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="2bb34-183">A solução recomendada é fazer todas as alterações em *.wadcfgx* no projeto e, depois, enviar uma atualização completa do aplicativo por push.</span><span class="sxs-lookup"><span data-stu-id="2bb34-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="2bb34-184">Se isso não for possível, verifique se a atualização do diagnóstico enviará por push uma **PrivateConfig** completa, que inclui a chave SAS.</span><span class="sxs-lookup"><span data-stu-id="2bb34-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="2bb34-185">Eu testei as sugestões, mas o hub de eventos ainda não está funcionando.</span><span class="sxs-lookup"><span data-stu-id="2bb34-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="2bb34-186">Tente examinar a tabela do Armazenamento do Azure que contém logs e erros do próprio Diagnóstico do Azure: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="2bb34-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="2bb34-187">Uma opção é usar uma ferramenta, como o [Gerenciador de Armazenamento do Azure](http://www.storageexplorer.com) , para se conectar a essa conta de armazenamento, exibir essa tabela e adicionar uma consulta por carimbo de data/hora nas últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="2bb34-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="2bb34-188">Você pode usar a ferramenta para exportar um arquivo .csv e abri-lo em um aplicativo, como o Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="2bb34-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="2bb34-189">O Excel facilita a pesquisa de cadeias de caracteres de cartão, como **EventHubs**, para ver qual erro é relatado.</span><span class="sxs-lookup"><span data-stu-id="2bb34-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="2bb34-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2bb34-190">Next steps</span></span>
<span data-ttu-id="2bb34-191">•    [Saiba mais sobre os Hubs de Eventos](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="2bb34-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="2bb34-192">Apêndice: Concluir o exemplo de arquivo de configuração do Diagnóstico do Azure (.wadcfgx)</span><span class="sxs-lookup"><span data-stu-id="2bb34-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="2bb34-193">O *ServiceConfiguration.Cloud.cscfg* complementar para este exemplo se parece com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="2bb34-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

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

<span data-ttu-id="2bb34-194">Configurações equivalentes baseada em Json para máquinas virtuais são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="2bb34-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="2bb34-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2bb34-195">Next steps</span></span>
<span data-ttu-id="2bb34-196">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="2bb34-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="2bb34-197">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2bb34-198">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="2bb34-199">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2bb34-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
