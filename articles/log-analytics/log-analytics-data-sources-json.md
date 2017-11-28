---
title: "dados JSON personalizado de aaaCollecting na análise de Log do OMS | Microsoft Docs"
description: "Fontes de dados JSON personalizadas podem ser coletadas para análise de Log usando a saudação do agente do OMS para Linux.  Essas fontes de dados personalizados podem ser scripts simples retornando JSON, assim como curl ou um dos mais de 300 plug-ins do FluentD. Este artigo descreve a configuração de Olá necessária para este conjunto de dados."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="a9588-105">Coletando fontes de dados JSON personalizadas com hello agente do OMS para Linux em análise de Log</span><span class="sxs-lookup"><span data-stu-id="a9588-105">Collecting custom JSON data sources with hello OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="a9588-106">Fontes de dados JSON personalizadas podem ser coletadas para análise de Log usando a saudação do agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="a9588-106">Custom JSON data sources can be collected into Log Analytics using hello OMS Agent for Linux.</span></span>  <span data-ttu-id="a9588-107">Essas fontes de dados personalizados podem ser scripts simples retornando JSON, assim como [curl](https://curl.haxx.se/) ou um dos [mais de 300 plug-ins do FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="a9588-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="a9588-108">Este artigo descreve a configuração de Olá necessária para este conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="a9588-108">This article describes hello configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="a9588-109">O Agente do OMS para Linux v1.1.0-217+ é necessário para dados JSON personalizados</span><span class="sxs-lookup"><span data-stu-id="a9588-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="a9588-110">Configuração</span><span class="sxs-lookup"><span data-stu-id="a9588-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="a9588-111">Configurar plug-in de entrada</span><span class="sxs-lookup"><span data-stu-id="a9588-111">Configure input plugin</span></span>

<span data-ttu-id="a9588-112">Adicionar dados JSON toocollect na análise de Log, `oms.api.` toohello início de uma marca de FluentD em um plug-in de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9588-112">toocollect JSON data in Log Analytics, add `oms.api.` toohello start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="a9588-113">Por exemplo, a seguir temos um arquivo de configuração separado `exec-json.conf` em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="a9588-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="a9588-114">Isso usa o plug-in do hello FluentD `exec` toorun um comando de ondulação a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="a9588-114">This uses hello FluentD plugin `exec` toorun a curl command every 30 seconds.</span></span>  <span data-ttu-id="a9588-115">saída de Hello desse comando é coletada pelo plug-in de saída JSON hello.</span><span class="sxs-lookup"><span data-stu-id="a9588-115">hello output from this command is collected by hello JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="a9588-116">arquivo de configuração de saudação adicionado em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` exigirá toohave sua propriedade alterada com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9588-116">hello configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require toohave its ownership changed with hello following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="a9588-117">Configurar o plug-in de saída</span><span class="sxs-lookup"><span data-stu-id="a9588-117">Configure output plugin</span></span> 
<span data-ttu-id="a9588-118">Adicionar Olá seguinte saída plug-in Configuração toohello principal configuração em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou como um arquivo de configuração separados são colocados em`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="a9588-118">Add hello following output plugin configuration toohello main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="a9588-119">Reiniciar o Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="a9588-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="a9588-120">Reinicie o hello agente do OMS para Linux service com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9588-120">Restart hello OMS Agent for Linux service with hello following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="a9588-121">Saída</span><span class="sxs-lookup"><span data-stu-id="a9588-121">Output</span></span>
<span data-ttu-id="a9588-122">Olá dados serão coletados na análise de Log com um tipo de registro de `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="a9588-122">hello data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="a9588-123">Por exemplo, Olá marca personalizada `tag oms.api.tomcat` na análise de Log com um tipo de registro de `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="a9588-123">For example, hello custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="a9588-124">Você pode recuperar todos os registros desse tipo com hello pesquisa de log a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9588-124">You could retrieve all records of this type with hello following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="a9588-125">Fontes de dados JSON aninhados têm suporte, mas são indexadas sem se basear no campo pai.</span><span class="sxs-lookup"><span data-stu-id="a9588-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="a9588-126">Por exemplo, Olá dados JSON a seguir é retornado de uma pesquisa de análise de Log como `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="a9588-126">For example, hello following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="a9588-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a9588-127">Next steps</span></span>
* <span data-ttu-id="a9588-128">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="a9588-128">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
 