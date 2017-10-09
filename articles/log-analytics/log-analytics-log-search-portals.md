---
title: "aaaPortals para criar e editar consultas de log na análise de Log do Azure | Microsoft Docs"
description: "Este artigo descreve os portais de saudação que você pode usar no Azure Log Analytics toocreate e editar pesquisas de log."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portais para criar e editar consultas de log no Azure Log Analytics

> [!NOTE]
> Este artigo descreve os portais no Azure Log Analytics usando Olá nova linguagem de consulta.  Você pode saber mais sobre a nova linguagem de saudação e obter Olá procedimento tooupgrade seu espaço de trabalho em [atualizar sua pesquisa de log de toonew de espaço de trabalho do Azure Log Analytics](log-analytics-log-search-upgrade.md).  
>
> Se o espaço de trabalho não tiver sido atualizado toohello nova linguagem de consulta, você deve referir-se muito[localizar os dados usando pesquisas de log na análise de Log](log-analytics-log-searches.md) para obter informações sobre a versão atual de saudação do portal de pesquisa de Log de saudação.

Você pode usar pesquisas de log em uma variedade de dados de análise de Log de tooretrieve locais do espaço de trabalho de saudação.  Para realmente criar e editar consultas Além disso tooworking interativamente com retornou dados no entanto, você tem duas opções são descritas abaixo.  

## <a name="log-search-portal"></a>Portal de pesquisa de logs
portal de pesquisa de Log de saudação é acessível Olá portal do Azure ou o portal do OMS hello.  Ele é adequado para criar consultas básicas que podem ser criadas em uma única linha.  portal de pesquisa de Log de saudação pode ser usado sem iniciar um portal externo, e você pode usá-lo tooperform uma variedade de funções com pesquisas de log, incluindo a criação de regras de alerta, criar grupos de computadores e exportando Olá resultados de consulta de saudação.  

portal de pesquisa de Log de saudação fornece vários recursos para edição de consulta Olá sem ter um conhecimento completo da linguagem de consulta de saudação.  Você pode obter um resumo desses recursos em [criar pesquisas de log na análise de Log do Azure usando o portal de pesquisa de Log de saudação](log-analytics-log-search-log-search-portal.md).


![Portal de Pesquisa de Logs](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Portal Análise Avançada
portal de análise avançada de saudação é um portal dedicado que fornece a funcionalidade avançada não está disponível no portal de pesquisa de Log de saudação.  Recursos incluem a capacidade de saudação tooedit uma consulta em várias linhas, executar seletivamente o código, Intellisense sensível ao contexto e análise inteligente.  portal de análise avançada de saudação é mais adequado para a criação de consultas complexas que são o salva como uma pesquisa de log ou copiadas e coladas em outros elementos de análise de Log.  Inicie o portal do Advanced Analytics Olá de um link no portal de pesquisa de Log de saudação.

![Portal Análise Avançada](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Devido a seus recursos avançados, normalmente você usará portal de análise avançada hello como a principal ferramenta para criar e editar consultas.  Depois de determinar que consulta Olá funciona conforme o esperado, em seguida, copie e cole-o em outro lugar, como o portal de pesquisa de Log de saudação ou Designer de exibição.  Como Olá Advanced Analytics portal oferece suporte a consultas com várias linhas no entanto, é necessário seguir de saudação tootake em consideração ao copiar uma consulta desse portal.

- Comentários devem ser removidos da consulta Olá antes que ele foi copiado e colado em outro local.  Você pode comentar uma linha, precedendo-a de duas barras (//).  Quando você cola uma consulta de várias linhas em uma única linha, quebras de linha são removidas.  Se os comentários são incluídos, todos os caracteres após o primeiro comentário de saudação são considerados parte do comentário de saudação.


## <a name="next-steps"></a>Próximas etapas

- Percorrer um tutorial sobre como usar o hello [portal de pesquisa de Log](log-analytics-log-search-log-search-portal.md) ou hello [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) toocreate consultas.
- Check-out de um [tutorial sobre como escrever consultas](https://go.microsoft.com/fwlink/?linkid=856078) usando Olá nova linguagem de consulta.
