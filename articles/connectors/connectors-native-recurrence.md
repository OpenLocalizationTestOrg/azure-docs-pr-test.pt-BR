---
title: "gatilho de recorrência Olá aaaAdd em aplicativos lógicos | Microsoft Docs"
description: "Visão geral de gatilho de recorrência Olá e como toouse com um aplicativo do Azure lógica."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Introdução ao gatilho de recorrência Olá
Usando o gatilho de recorrência hello, você pode criar fluxos de trabalho poderosos na nuvem hello.

Por exemplo, você pode:

* Agende um fluxo de trabalho toorun um procedimento armazenado SQL diariamente.
* Um resumo de todos os tweets dentro Olá última semana sobre um determinado hashtag de email.

tooget iniciado usando o gatilho de recorrência de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Usar um gatilho de recorrência
Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico. [Saiba mais sobre gatilhos](connectors-overview.md).

Aqui está uma sequência de exemplo de como tooset backup uma recorrência disparar em um aplicativo de lógica:

1. Adicionar Olá **recorrência** disparador como primeira etapa Olá em um aplicativo de lógica.
2. Preencha os parâmetros Olá Olá intervalo de recorrência.

Olá lógica aplicativo agora inicia uma execução depois de cada intervalo de tempo.

![Gatilho HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Detalhes do gatilho
gatilho de recorrência Olá tem Olá propriedades que você pode configurar a seguir.

Ele dispara um aplicativo lógico depois de um intervalo de tempo especificado.
Um * significa que é um campo obrigatório.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| Frequência* |frequência |unidade de saudação de tempo: `Second`, `Minute`, `Hour`, `Day`, ou `Year`. |
| Intervalo* |intervalo |intervalo de saudação do hello atribuído a frequência de recorrência de saudação. |
| Fuso horário |timeZone |Se uma hora de início for fornecida sem uma diferença UTC, este fuso horário será usado. |
| Hora de início |startTime |hora de início de saudação em [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Próximas etapas
Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).

