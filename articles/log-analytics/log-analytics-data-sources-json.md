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
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Coletando fontes de dados JSON personalizadas com hello agente do OMS para Linux em análise de Log
Fontes de dados JSON personalizadas podem ser coletadas para análise de Log usando a saudação do agente do OMS para Linux.  Essas fontes de dados personalizados podem ser scripts simples retornando JSON, assim como [curl](https://curl.haxx.se/) ou um dos [mais de 300 plug-ins do FluentD](http://www.fluentd.org/plugins/all). Este artigo descreve a configuração de Olá necessária para este conjunto de dados.

> [!NOTE]
> O Agente do OMS para Linux v1.1.0-217+ é necessário para dados JSON personalizados

## <a name="configuration"></a>Configuração

### <a name="configure-input-plugin"></a>Configurar plug-in de entrada

Adicionar dados JSON toocollect na análise de Log, `oms.api.` toohello início de uma marca de FluentD em um plug-in de entrada.

Por exemplo, a seguir temos um arquivo de configuração separado `exec-json.conf` em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Isso usa o plug-in do hello FluentD `exec` toorun um comando de ondulação a cada 30 segundos.  saída de Hello desse comando é coletada pelo plug-in de saída JSON hello.

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
arquivo de configuração de saudação adicionado em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` exigirá toohave sua propriedade alterada com hello comando a seguir.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Configurar o plug-in de saída 
Adicionar Olá seguinte saída plug-in Configuração toohello principal configuração em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou como um arquivo de configuração separados são colocados em`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Reiniciar o Agente do OMS para Linux
Reinicie o hello agente do OMS para Linux service com hello comando a seguir.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Saída
Olá dados serão coletados na análise de Log com um tipo de registro de `<FLUENTD_TAG>_CL`.

Por exemplo, Olá marca personalizada `tag oms.api.tomcat` na análise de Log com um tipo de registro de `tomcat_CL`.  Você pode recuperar todos os registros desse tipo com hello pesquisa de log a seguir.

    Type=tomcat_CL

Fontes de dados JSON aninhados têm suporte, mas são indexadas sem se basear no campo pai. Por exemplo, Olá dados JSON a seguir é retornado de uma pesquisa de análise de Log como `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções. 
 