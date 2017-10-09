---
title: "dados de aaaCollect de CollectD na análise de Log do OMS | Microsoft Docs"
description: "CollectD é um daemon do Linux de software livre que coleta periodicamente dados de aplicativos e informações de nível de sistema.  Este artigo fornece informações sobre a coleta de dados do CollectD no Log Analytics."
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
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Coletar dados do CollectD em agentes do Linux no Log Analytics
O [CollectD](https://collectd.org/) é um daemon do Linux de software livre que coleta periodicamente métricas de desempenho de aplicativos e informações de nível de sistema. Aplicativos de exemplo incluem Nginx, Olá Máquina Virtual Java (JVM) e do MySQL Server. Este artigo fornece informações sobre a coleta de dados de desempenho do CollectD no Log Analytics.

Uma lista completa de plug-ins disponíveis pode ser encontrada na [Tabela de Plug-ins](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Visão geral do CollectD](media/log-analytics-data-sources-collectd/overview.png)

Olá CollectD configuração a seguir está incluída no hello agente do OMS para Linux tooroute CollectD dados toohello agente do OMS para Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Além disso, se usando um versões collectD antes 5.5 usar Olá seguinte configuração em vez disso.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

configuração de CollectD Olá usa o padrão de saudação`write_http` dados métrica de desempenho do toosend de plug-in pela porta 26000 tooOMS agente para Linux. 

> [!NOTE]
> Essa porta pode ser configurado tooa personalizadas se necessário.

Olá agente do OMS para Linux também escuta na porta 26000 CollectD métricas e converte-os tooOMS métricas de esquema. Olá, a seguir é hello agente do OMS para Linux configuração `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Versões com suporte
- O Log Analytics dá suporte atualmente às versões 4.8 e superiores do CollectD.
- O Agente do OMS para Linux v1.1.0-217 ou superior é necessário para coleta de métrica do CollectD.


## <a name="configuration"></a>Configuração
Olá seguem coleção de tooconfigure etapas básicas de CollectD dados na análise de Log.

1. Configure CollectD toosend dados toohello agente do OMS para Linux usando o plug-in do hello write_http.  
2. Configure hello agente do OMS para Linux toolisten para Olá CollectD dados na porta apropriada hello.
3. Reinicie o CollectD e o Agente do OMS para Linux.

### <a name="configure-collectd-tooforward-data"></a>Configurar CollectD tooforward dados 

1. tooroute CollectD dados toohello agente do OMS para Linux, `oms.conf` necessidades toobe adicionado o diretório de configuração do tooCollectD. destino de saudação do arquivo depende Olá distribuição de Linux de sua máquina.

    Se o diretório de configuração CollectD está localizado em /etc/collectd.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Se o diretório de configuração CollectD está localizado em /etc/collectd/collectd.conf.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Para versões CollectD antes 5.5 terá marcas de saudação toomodify `oms.conf` como mostrado acima.
    >

2. Copie o diretório de configuração omsagent collectd.conf toohello desejado do espaço de trabalho.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Reinicie o CollectD e o agente do OMS para Linux com hello comandos a seguir.

    sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>Métricas de CollectD tooLog conversão do esquema de análise
toomaintain um modelo familiar entre as métricas de infraestrutura já coletados pelo agente do OMS para Linux e hello novas métricas coletadas pelo CollectD Olá mapeamento de esquema a seguir é usado:

| Campo Métrica do CollectD | Campo Log Analytics |
|:--|:--|
| host | Computador |
| plug-in | Nenhum |
| plugin_instance | Nome da Instância<br>Se **plugin_instance** é *null*, então InstanceName="*_Total*" |
| type | ObjectName |
| type_instance | CounterName<br>Se **type_instance** é *null*, então CounterName=**blank** |
| dsnames[] | CounterName |
| dstypes | Nenhum |
| values[] | CounterValue |

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções. 
* Use [campos personalizados](log-analytics-custom-fields.md) tooparse dados de registros de syslog em campos individuais.

