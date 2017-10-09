---
title: aaaIIS registra em Log Analytics | Microsoft Docs
description: "O IIS (Serviços de Informações da Internet) armazena a atividade do usuário em arquivos de log que podem ser coletados pelo Log Analytics.  Este artigo descreve como tooconfigure coleta de logs do IIS e os detalhes de registros de saudação criado no repositório do OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Logs do IIS no Log Analytics
O IIS (Serviços de Informações da Internet) armazena a atividade do usuário em arquivos de log que podem ser coletados pelo Log Analytics.  

![Logs IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Configurando logs do IIS
O Log Analytics coleta entradas de arquivos de log criados pelo IIS, por isso você deve [configurar o IIS para o registro em log](https://technet.microsoft.com/library/hh831775.aspx).

O Log Analytics só oferece suporte a arquivos de log do IIS armazenados em formato W3C e não oferece suporte a campos personalizados ou a registro em Log Avançado do IIS.  
O Log Analytics não coleta logs no formato nativo IIS ou NCSA.

Configurar logs do IIS na análise de Log de saudação [menu dados nas configurações de análise de Log](log-analytics-data-sources.md#configuring-data-sources).  Não há nenhuma outra configuração necessária além da seleção de **Collect W3C format IIS log files**(Coletar arquivos de log do IIS no formato W3C).

É recomendável que, quando você habilita a coleta de log do IIS, você deve configurar configuração de substituição de log do IIS Olá em cada servidor.

## <a name="data-collection"></a>Coleta de dados
O Log Analytics coleta as entradas de log do IIS de cada fonte conectada a cada 15 minutos, aproximadamente.  agente Olá registra seu lugar em cada log de eventos de coleta.  Se agente Olá ficar offline, em seguida, análise de Log coleta eventos de onde parou, mesmo se os eventos foram criados durante a saudação agent estava offline.

## <a name="iis-log-record-properties"></a>Propriedades de registro de log do IIS
Registros de log do IIS têm um tipo de **W3CIISLog** e têm propriedades de saudação em Olá a tabela a seguir:

| Propriedade | Descrição |
|:--- |:--- |
| Computador |Nome do computador Olá Olá evento foi coletado do. |
| cIP |Endereço IP do cliente de saudação. |
| csMethod |Método de solicitação hello como GET ou POST. |
| csReferer |Site que Olá usuário seguiu um link de site atual toohello. |
| csUserAgent |Tipo de navegador do cliente hello. |
| csUserName |Nome da saudação autenticou o usuário que acessou o servidor de saudação. Os usuários anônimos são indicados por um hífen. |
| csUriStem |Destino da solicitação de saudação como uma página da web. |
| csUriQuery |Consulta, se houver, que o cliente Olá tentava tooperform. |
| ManagementGroupName |Nome do grupo de gerenciamento de saudação para agentes do Operations Manager.  Para outros agentes, ele é AOI-\<ID do espaço de trabalho\> |
| RemoteIPCountry |País do endereço IP de saudação do cliente hello. |
| RemoteIPLatitude |Latitude do endereço IP do cliente hello. |
| RemoteIPLongitude |Longitude do endereço IP do cliente hello. |
| scStatus |Código de status HTTP. |
| scSubStatus |Código de erro de substatus. |
| scWin32Status |Código de status do Windows. |
| sIP |Endereço IP do servidor de web hello. |
| SourceSystem |OpsMgr |
| sPort |No cliente de saudação do servidor de saudação conectada à. |
| sSiteName |Nome do site do IIS hello. |
| TimeGenerated |Data e hora da entrada de saudação foi registrada. |
| TimeTaken |Solicitação do comprimento de saudação do tooprocess de tempo em milissegundos. |

## <a name="log-searches-with-iis-logs"></a>Pesquisas de log com logs do IIS
Olá, tabela a seguir fornece exemplos de diferentes de consultas de log que recuperam registros de log do IIS.

| Consultar | Descrição |
|:--- |:--- |
| Type=W3CIISLog |Todos os registros de log do IIS. |
| Type=W3CIISLog scStatus=500 |Todos os registros de log do IIS com um status de retorno de 500. |
| Type=W3CIISLog &#124; Measure count() by cIP |Contagem das entradas do log do IIS por endereço IP do cliente. |
| Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |Contagem de IIS entradas no log por URL de saudação host www.contoso.com. |
| Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |Total de bytes recebidos por cada computador com IIS. |

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.

> | Consultar | Descrição |
|:--- |:--- |
| W3CIISLog |Todos os registros de log do IIS. |
| W3CIISLog &#124; where scStatus==500 |Todos os registros de log do IIS com um status de retorno de 500. |
| W3CIISLog &#124; summarize count() by cIP |Contagem das entradas do log do IIS por endereço IP do cliente. |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |Contagem de IIS entradas no log por URL de saudação host www.contoso.com. |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |Total de bytes recebidos por cada computador com IIS. |

## <a name="next-steps"></a>Próximas etapas
* Configurar análise de Log toocollect outros [fontes de dados](log-analytics-data-sources.md) para análise.
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.
* Configure alertas em análise de Log tooproactively notificá-lo de condições importantes encontradas nos logs do IIS.
