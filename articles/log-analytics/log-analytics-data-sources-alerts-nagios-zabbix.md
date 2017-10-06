---
title: "alertas de Nagios e Zabbix aaaCollect na análise de Log do OMS | Microsoft Docs"
description: "O Nagios e o Zabbix são ferramentas de monitoramento de software livre. Você pode coletar de alertas essas ferramentas para análise de Log na ordem tooanalyze-los junto com os alertas de outras fontes.  Este artigo descreve como tooconfigure Olá agente do OMS para Linux toocollect alertas desses sistemas."
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
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Coletar alertas do Nagios e do Zabbix no Log Analytics do Agente do OMS para Linux 
O [Nagios](https://www.nagios.org/) e o [Zabbix](http://www.zabbix.com/) são ferramentas de monitoramento de software livre.  Você pode coletar de alertas essas ferramentas para análise de Log na ordem tooanalyze-os junto com [alertas de outras fontes](log-analytics-alerts.md).  Este artigo descreve como tooconfigure Olá agente do OMS para Linux toocollect alertas desses sistemas.
 
## <a name="configure-alert-collection"></a>Configurar coleta de alertas

### <a name="configuring-nagios-alert-collection"></a>Configurar coleta de alertas do Nagios
Execute Olá seguindo as etapas em alertas de toocollect Olá Nagios server.

1. Usuário de saudação Grant **omsagent** arquivo de log do acesso de leitura toohello Nagios (ou seja, `/var/log/nagios/nagios.log`). Supondo que o arquivo nagios.log de saudação pertencem ao grupo Olá `nagios`, você pode adicionar usuário Olá **omsagent** toohello **nagios** grupo. 

    sudo usermod -a -G nagios omsagent

2.  Modificar o arquivo de configuração de saudação em (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Certifique-se de saudação entradas a seguir está presentes e sem comentários:  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. Reiniciar o daemon omsagent Olá

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Configurar coleta de alertas do Zabbix
toocollect alertas de um servidor Zabbix, você precisa toospecify um usuário e senha em *limpar texto*. Isso não é ideal, mas é recomendável que você crie Olá usuário e conceda permissões toomonitor onlu.

Execute Olá seguindo as etapas em alertas de toocollect Olá Nagios server.

1. Modificar o arquivo de configuração de saudação em (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Certifique-se de saudação entradas a seguir está presentes e sem comentários.  Alterar os toovalues Olá nome e senha de usuário para o seu ambiente Zabbix.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Reiniciar o daemon omsagent Olá

    sudo sh /opt/microsoft/omsagent/bin/service_control restart


## <a name="alert-records"></a>Registros de alerta
Você pode recuperar registros de alerta do Nagios e do Zabbix usando [pesquisas de logs](log-analytics-log-searches.md) no Log Analytics.

### <a name="nagios-alert-records"></a>Registros de alerta do Nagios

Registros de alerta coletados pelo Nagios têm **Type** definido como **Alert** e **SourceSystem** definido como **Nagios**.  Eles têm propriedades Olá no Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*Nagios* |
| AlertName |Nome do alerta de saudação. |
| AlertDescription | Descrição do alerta de saudação. |
| AlertState | Status do serviço de saudação ou host.<br><br>OK<br>AVISO<br>PARA CIMA<br>PARA BAIXO |
| HostName | Nome do host de saudação que criou o alerta de saudação. |
| PriorityNumber | Nível de prioridade de alerta de saudação. |
| StateType | tipo de saudação do estado de alerta de saudação.<br><br>SUAVE – problema que não foi verificado novamente.<br>GRAVE – problema que foi verificado novamente um número especificado de vezes.  |
| TimeGenerated |Alerta de saudação de data e hora foi criado. |


### <a name="zabbix-alert-records"></a>Registros de alerta do Zabbix
Registros de alerta coletados pelo Zabbix têm **Type** definido como **Alert** e **SourceSystem** definido como **Zabbix**.  Eles têm propriedades Olá no Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*Zabbix* |
| AlertName | Nome do alerta de saudação. |
| AlertPriority | Severidade do alerta de saudação.<br><br>não classificado<br>informações<br>Aviso<br>média<br>alto<br>desastre  |
| AlertState | Estado de alerta de saudação.<br><br>0 - estado é toodate.<br>1 – o estado é desconhecido.  |
| AlertTypeNumber | Especifica se o alerta pode ou não gerar vários eventos de problema.<br><br>0 - estado é toodate.<br>1 – o estado é desconhecido.    |
| Comentários | Comentários adicionais para o alerta. |
| HostName | Nome do host de saudação que criou o alerta de saudação. |
| PriorityNumber | Valor que indica a severidade do alerta de saudação.<br><br>0 – não classificado<br>1 – informações<br>2 – aviso<br>3 – média<br>4 – alta<br>5 – desastre |
| TimeGenerated |Alerta de saudação de data e hora foi criado. |
| TimeLastModified |Estado de saudação de data e hora de alerta de saudação última alteração. |


## <a name="next-steps"></a>Próximas etapas
* Aprenda sobre [alertas](log-analytics-alerts.md) no Log Analytics.
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções. 
