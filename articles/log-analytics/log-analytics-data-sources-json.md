---
title: Coletar dados JSON personalizados no OMS Log Analytics | Microsoft Docs
description: "Fontes de dados JSON personalizados podem ser coletadas no Log Analytics usando o Agente do OMS para Linux.  Essas fontes de dados personalizados podem ser scripts simples retornando JSON, assim como curl ou um dos mais de 300 plug-ins do FluentD. Este artigo descreve a configuração necessária para essa coleta de dados."
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
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="74e15-105">Coletar fontes de dados JSON personalizados com o Agente do OMS para Linux em Log Analytics</span><span class="sxs-lookup"><span data-stu-id="74e15-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="74e15-106">Fontes de dados JSON personalizados podem ser coletadas no Log Analytics usando o Agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="74e15-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="74e15-107">Essas fontes de dados personalizados podem ser scripts simples retornando JSON, assim como [curl](https://curl.haxx.se/) ou um dos [mais de 300 plug-ins do FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="74e15-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="74e15-108">Este artigo descreve a configuração necessária para essa coleta de dados.</span><span class="sxs-lookup"><span data-stu-id="74e15-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="74e15-109">O Agente do OMS para Linux v1.1.0-217+ é necessário para dados JSON personalizados</span><span class="sxs-lookup"><span data-stu-id="74e15-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="74e15-110">Configuração</span><span class="sxs-lookup"><span data-stu-id="74e15-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="74e15-111">Configurar plug-in de entrada</span><span class="sxs-lookup"><span data-stu-id="74e15-111">Configure input plugin</span></span>

<span data-ttu-id="74e15-112">Para coletar dados JSON no Log Analytics, adicione `oms.api.` ao início de uma marcação FluentD em um plug-in de entrada.</span><span class="sxs-lookup"><span data-stu-id="74e15-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="74e15-113">Por exemplo, a seguir temos um arquivo de configuração separado `exec-json.conf` em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="74e15-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="74e15-114">Isso usa o plug-in FluentD `exec` para executar um comando curl a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="74e15-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="74e15-115">A saída desse comando é coletada pelo plug-in de saída do JSON.</span><span class="sxs-lookup"><span data-stu-id="74e15-115">The output from this command is collected by the JSON output plugin.</span></span>

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
<span data-ttu-id="74e15-116">O arquivo de configuração adicionado a `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` precisará ter sua propriedade alterada com o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="74e15-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="74e15-117">Configurar o plug-in de saída</span><span class="sxs-lookup"><span data-stu-id="74e15-117">Configure output plugin</span></span> 
<span data-ttu-id="74e15-118">Adicione a configuração de plug-in de saída a seguir à configuração principal em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou como um arquivo de configuração separado colocado em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="74e15-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="74e15-119">Reiniciar o Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="74e15-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="74e15-120">Reinicie o serviço Agente do OMS para Linux com o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="74e15-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="74e15-121">Saída</span><span class="sxs-lookup"><span data-stu-id="74e15-121">Output</span></span>
<span data-ttu-id="74e15-122">Os dados serão coletados no Log Analytics com um tipo de registro de `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="74e15-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="74e15-123">Por exemplo, a marcação personalizada `tag oms.api.tomcat` no Log Analytics com um tipo de registro de `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="74e15-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="74e15-124">Você pode recuperar todos os registros desse tipo com a pesquisa de logs a seguir.</span><span class="sxs-lookup"><span data-stu-id="74e15-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="74e15-125">Fontes de dados JSON aninhados têm suporte, mas são indexadas sem se basear no campo pai.</span><span class="sxs-lookup"><span data-stu-id="74e15-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="74e15-126">Por exemplo, os seguintes dados JSON são retornados de uma pesquisa do Log Analytics como `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="74e15-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="74e15-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74e15-127">Next steps</span></span>
* <span data-ttu-id="74e15-128">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) para analisar os dados coletados de fontes de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="74e15-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 