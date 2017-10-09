---
title: "uso de dados de aaaAnalyze na análise de Log | Microsoft Docs"
description: "Use o painel de uso de saudação na análise de Log tooview quantos dados estão sendo enviados toohello serviço de análise de Log e solução de problemas que grandes quantidades de dados estão sendo enviadas."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Analisar o uso de dados no Log Analytics
Análise de log inclui informações sobre a quantidade de saudação de dados coletados, computadores envia dados saudação e Olá diferentes tipos de dados enviados.  Saudação de uso **uso de análise de Log** quantidade de saudação toosee painel de dados enviados toohello serviço de análise de Log. painel Olá mostra quantos dados são coletados por cada solução e a quantidade de dados os computadores estão enviando.

## <a name="understand-hello-usage-dashboard"></a>Entender o painel de uso de saudação
Olá **uso de análise de Log** painel exibe o saudação informações a seguir:

- Volume de dados
    - Volume de dados ao longo do tempo (com base em seu escopo de tempo atual)
    - Volume de dados por solução
    - Dados não associados a um computador
- Computadores
    - Computadores enviando dados
    - Computadores sem dados nas últimas 24 horas
- Ofertas
    - Nós Insight e de Análise
    - Nós de automação e controle
    - Nós de segurança
- Desempenho
    - Tempo gasto dados toocollect e índice
- Lista de consultas

![painel de uso](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork com dados de uso
1. Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com) usando sua assinatura do Azure.
2. Em Olá **Hub** menu, clique em **mais serviços** e, na lista de saudação de recursos, digite **análise de Log**. Como começar a digitar, Olá filtros de lista com base em sua entrada. Clique em **Log Analytics**.  
    ![Hub do Azure](./media/log-analytics-usage/hub.png)
3. Olá **análise de Log** painel mostra uma lista dos espaços de trabalho. Selecione um espaço de trabalho.
4. Em Olá *espaço de trabalho* painel, clique em **uso de análise de Log**.
5. Em Olá **uso de análise de Log** painel, clique em **tempo: últimas 24 horas** toochange intervalo de tempo de saudação.  
    ![intervalo de tempo](./media/log-analytics-usage/time.png)
6. Folhas categoria de uso de saudação de exibição que mostram áreas de seu interesse. Escolha uma folha e, em seguida, clique em um item tooview mais detalhes em [pesquisa de Log](log-analytics-log-searches.md).  
    ![folha de uso de dados de exemplo](./media/log-analytics-usage/blade.png)
7. No painel de pesquisa de Log hello, examine os resultados de saudação que são retornados da pesquisa de saudação.  
    ![pesquisa de log de uso de exemplo](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Criar um alerta quando a coleta de dados for maior que a esperada
Esta seção descreve como toocreate um alerta se:
- O volume de dados excede uma quantidade definida.
- Volume de dados é previsto tooexceed um período especificado.

Os [alertas](log-analytics-alerts-creating.md) do Log Analytics usam consultas de pesquisa. Olá consulta a seguir tem um resultado quando há mais de 100 GB de dados coletados no hello últimas 24 horas:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Olá consulta a seguir usa uma simple toopredict fórmula quando mais de 100 GB de dados será enviado em um dia: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert em um volume de dados diferentes, alteração Olá 100 na Olá consultas toohello número GB deseja tooalert no.

Usar Olá etapas descritas [criar uma regra de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notificado quando a coleta de dados é maior do que o esperado.

Ao criar o alerta Olá para consulta de primeira hello, quando há mais de 100 GB de dados em 24 horas, defina o:
- **Nome** muito*volume de dados maior que 100 GB em 24 horas*
- **Severidade** muito*aviso*
- **Consulta de pesquisa** muito`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Janela de tempo** muito*24 horas*.
- **Frequência de alerta** toobe uma hora, como dados de uso de saudação atualiza somente uma vez por hora.
- **Gerar alerta com base em** toobe *número de resultados*
- **Número de resultados** toobe *maior que 0*

Usar Olá etapas descritas [adicionar regras de tooalert ações](log-analytics-alerts-actions.md) configurar uma ação de email, webhook ou runbook para regra de alerta de saudação.

Quando criar alerta Olá para consulta de segundo hello, quando ele está previsto que haja mais de 100 GB de dados em 24 horas, definir o:
- **Nome** muito*volume de dados esperado toogreater de 100 GB em 24 horas*
- **Severidade** muito*aviso*
- **Consulta de pesquisa** muito`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Janela de tempo** muito*3 horas*.
- **Frequência de alerta** toobe uma hora, como dados de uso de saudação atualiza somente uma vez por hora.
- **Gerar alerta com base em** toobe *número de resultados*
- **Número de resultados** toobe *maior que 0*

Quando você receber um alerta, use as etapas de Olá Olá seguinte seção tootroubleshoot por que o uso é maior do que o esperado.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Solução de problemas por uso acima do esperado
Painel de uso de saudação ajuda a tooidentify por uso (e, portanto, o custo) é maior do que você espera.

O uso aumenta devido a uma ou mais das seguintes causas:
- Mais dados do que o esperado enviados tooLog análise
- Nós mais do que o esperado na enviando dados tooLog análise

### <a name="check-if-there-is-more-data-than-expected"></a>Verificar se há mais dados do que é esperado 
Há duas seções principais da página de uso de saudação que ajudam a identificar o que está causando Olá toobe de maioria dos dados coletado.

Olá *volume de dados ao longo do tempo* gráfico mostra o total do volume de dados enviados hello e computadores Olá enviando Olá a maioria dos dados. Olá gráfico na parte superior da saudação permite que você toosee se o uso geral de dados está aumentando, restantes estável ou decrescente. lista de saudação de computadores mostra os computadores de saudação 10 enviando Olá a maioria dos dados.

Olá *volume de dados por solução* gráfico mostra o volume de saudação de dados que são enviados por cada solução e soluções Olá enviando Olá a maioria dos dados. gráfico de saudação na parte superior da saudação mostra volume total de saudação de dados que são enviados por cada solução ao longo do tempo. Essas informações permite que você tooidentify se uma solução está enviando mais dados sobre Olá mesmo valor de dados, ou menos dados ao longo do tempo. saudação de lista de soluções mostra soluções Olá 10 enviando Olá a maioria dos dados. 

Esses dois gráficos mostram todos os dados. Alguns dados são faturáveis, e outros são gratuitos. toofocus apenas nos dados que faturáveis, modificar a consulta de saudação em tooinclude de página de pesquisa Olá `IsBillable=true`.  

![gráficos de volume de dados](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Examinar Olá *volume de dados ao longo do tempo* gráfico. soluções de saudação toosee e tipos de dados que estão enviando Olá a maioria dos dados para um computador específico, clique no nome de saudação do computador hello. Clique no nome de saudação do primeiro o computador na lista de Olá Olá.

Em Olá captura de tela a seguir, Olá *gerenciamento de Log / desempenho* tipo de dados está enviando Olá maioria dos dados para o computador de saudação. 

![volume de dados para um computador](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Em seguida, volte toohello *uso* painel e examine Olá *volume de dados por solução* gráfico. computadores de saudação toosee enviando Olá a maioria dos dados para uma solução, clique no nome de saudação de solução de saudação na lista de saudação. Clique no nome da saudação de solução de saudação primeiro na lista de saudação. 

Olá captura de tela a seguir, ele confirma que Olá *acmetomcat* computador está enviando Olá maioria dos dados para a solução de gerenciamento de Log hello.

![volume de dados para uma solução](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

Se necessário, execute análises adicionais tooidentify grandes volumes dentro de um tipo de dados ou solução. As consultas de exemplo incluem:

+ Solução de **Segurança**
  - `Type=SecurityEvent | measure count() by EventID`
+ Solução do **Gerenciamento de log**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ Tipo de dados de **Desempenho**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ Tipo de dados de **Evento**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ Tipo de dados **Syslog**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ Tipo de dados **AzureDiagnostics**
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Use Olá etapas tooreduce Olá volume de logs são coletados a seguir:

| Origem do alto volume de dados | Como o volume de dados tooreduce |
| -------------------------- | ------------------------- |
| Eventos de segurança            | Selecione [eventos de segurança mínima ou comuns](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/) <br> Olá segurança auditoria política toocollect necessitado apenas eventos de alteração. Em particular, examine Olá necessidade toocollect eventos <br> - [auditoria de plataforma de filtragem](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [auditoria de registro](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [auditoria de sistema de arquivos](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [auditoria de objeto kernel](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [auditoria de manipulação de identificador](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [auditoria de armazenamento removível](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| Contadores de desempenho       | Altere a [configuração do contador de desempenho](log-analytics-data-sources-performance-counters.md) para: <br> -Reduza a frequência de saudação de coleção <br> - Reduzir o número de contadores de desempenho |
| Logs de eventos                 | Altere a [configuração de log de eventos](log-analytics-data-sources-windows-events.md) para: <br> -Reduza o número de saudação dos logs de eventos coletados <br> - Coletar somente níveis de eventos necessários. Por exemplo, não colete eventos de nível *informações* |
| syslog                     | Altere a [configuração do syslog](log-analytics-data-sources-syslog.md) para: <br> -Reduza o número de saudação de recursos coletados <br> - Coletar somente níveis de eventos necessários. Por exemplo, não coletar eventos de nível *Informações* e *Depurar* |
| AzureDiagnostics           | Altere a coleção de logs do recurso para: <br> -Reduza o número de saudação de recursos enviar logs tooLog análise <br> - Coletar somente os logs necessários |
| Dados de computadores que não precisam de solução de saudação da solução | Use [solução direcionamento](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect dados apenas necessários grupos de computadores. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Verifique se há mais nós do que o esperado
Se você estiver usando Olá *por nó (OMS)* preço, em seguida, você é cobrado baseado no número de saudação de nós e soluções usadas. Você pode ver quantos nós de cada oferta estão sendo usados no hello *ofertas* seção do painel de uso de saudação.

![painel de uso](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Clique em **ver tudo...**  lista completa de saudação de tooview de computadores enviando dados para a oferta de saudação selecionada.

Use [solução direcionamento](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect dados apenas necessários grupos de computadores.


## <a name="next-steps"></a>Próximas etapas
* Consulte [pesquisas de Log na análise de Log](log-analytics-log-searches.md) toolearn como toouse Olá a pesquisa de idioma. Você pode usar consultas de pesquisa tooperform análise adicional nos dados de uso de saudação.
* Usar Olá etapas descritas [criar uma regra de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notificado quando um critério de pesquisa é atingido
* Use [solução direcionamento](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect dados apenas necessários grupos de computadores
* Selecione [eventos de segurança mínima ou comuns](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)
* Altere a [configuração do contador de desempenho](log-analytics-data-sources-performance-counters.md)
* Altere a [configuração de log de eventos](log-analytics-data-sources-windows-events.md)
* Altere a [configuração do syslog](log-analytics-data-sources-syslog.md)
