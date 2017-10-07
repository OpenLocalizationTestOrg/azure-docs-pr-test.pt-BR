---
title: "aaaAdd um atraso na lógica de aplicativos | Microsoft Docs"
description: "Visão geral da saudação atraso e o atraso-até ações e como toouse-los com um aplicativo do Azure lógica."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Introdução ao Olá atraso e o atraso-até ações
Usando o atraso de saudação e "atraso-até" ações, você pode concluir a cenários de fluxo de trabalho.

Por exemplo, você pode:

* Aguarde até que um dia da semana toosend um status de atualização por email.
* Fluxo de trabalho do atraso Olá até que uma chamada HTTP tem toofinish de tempo antes de reiniciar e recuperar resultados de saudação.

tooget iniciado usando a ação de atraso de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Use as ações de atraso de saudação
Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico. [Saiba mais sobre ações](connectors-overview.md).

Aqui está uma sequência de exemplo de como um atraso de toouse etapa em um aplicativo lógico:

1. Depois de adicionar um gatilho, clique em **nova etapa** tooadd uma ação.
2. Procurar **atraso** toobring as ações de atraso de saudação. Neste exemplo, escolheremos **Atrasar**.
   
    ![Ações atrasar](./media/connectors-native-delay/using-action-1.png)
3. Conclua qualquer atraso de Olá Olá ação propriedades tooconfigure.
   
    ![Configuração de atraso](./media/connectors-native-delay/using-action-2.png)
4. Clique em **salvar** toopublish e ativar o aplicativo de lógica de saudação.

## <a name="action-details"></a>Detalhes da ação
gatilho de recorrência Olá tem Olá seguintes propriedades que podem ser configuradas.

### <a name="delay-action"></a>Ação atrasar
Execute este Olá atrasos de ação para um determinado intervalo de tempo.
Um * significa que é um campo obrigatório.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| Contagem* |count |número de saudação do toodelay de unidades de tempo |
| Unidade* |unit |unidade de saudação de tempo: `Second`, `Minute`, `Hour`, ou`Day` |

<br>

### <a name="delay-until-action"></a>Ação atrasar até
Essa ação atrasa Olá seja executada até que uma data/hora especificada.
Um * significa que é um campo obrigatório.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| Ano* |timestamp |Olá ano toodelay até (GMT) |
| Mês* |timestamp |Olá mês toodelay até (GMT) |
| Dia* |timestamp |Olá toodelay dia até (GMT) |

<br>

## <a name="next-steps"></a>Próximas etapas
Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).

