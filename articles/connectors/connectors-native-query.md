---
title: "ação de consulta Olá aaaAdd em aplicativos lógicos | Microsoft Docs"
description: "Visão geral de ação de consulta Olá para executar ações como a matriz de filtro."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Introdução à ação de consulta Olá
Usando a ação de consulta hello, você pode trabalhar com lotes e matrizes tooaccomplish os fluxos de trabalho:

* Criar uma tarefa para todos os registros de alta prioridade a partir de um banco de dados.
* Salvar todos os anexos em PDF dos emails em um blob do Azure.

tooget iniciado usando a ação de consulta de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Use a ação de consulta de saudação
Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico. [Saiba mais sobre ações](connectors-overview.md).  

ação de consulta Olá atualmente tem uma operação, chamada de matriz de filtro hello, que é exposta no designer de saudação. Isso permite que você tooquery uma matriz e retornar um conjunto de resultados filtrados.

Veja como é possível adicioná-lo em um aplicativo lógico:

1. Selecione Olá **nova etapa** botão.
2. Escolha **Adicionar uma ação**.
3. Na caixa de pesquisa de ação hello, digite **filtro** Olá toolist **matriz de filtro** ação.
   
    ![Selecionar ação de consulta Olá](./media/connectors-native-query/using-action-1.png)
4. Selecione um toofilter de matriz. (hello seguinte captura de tela mostra Olá matriz de resultados de uma pesquisa do Twitter.)
5. Crie uma condição tooevaluate em cada item. (Olá captura de tela a seguir filtra tweets de usuários que têm mais de 100 seguidores.)
   
    ![Ação de consulta Olá concluída](./media/connectors-native-query/using-action-2.png)
   
    ação de saudação produzirá uma nova matriz que contém somente os resultados que atendam aos requisitos de filtro de saudação.
6. Clique o canto superior esquerdo de saudação de saudação da barra de ferramentas toosave e sua lógica aplicativo salvará os dois e publicar (Ativar).

## <a name="query-action"></a>Ação de consulta
Aqui estão os detalhes de saudação para ação Olá que oferece suporte a esse conector. conector de saudação tem uma ação possível.

| Ação | Descrição |
| --- | --- |
| Filtrar matriz |Avalia uma condição para cada item em uma matriz e retorna resultados Olá |

## <a name="action-details"></a>Detalhes da ação
ação de consulta Olá vem com uma ação possível. Olá tabelas a seguir descrevem hello necessárias e os campos de entrada opcionais para ação hello e Olá correspondente saída detalhes associados usando a ação de saudação.

### <a name="filter-array"></a>Filtrar matriz
Olá seguem campos de entrada para a ação de saudação, que faz uma solicitação HTTP de saída.
Um * significa que é um campo obrigatório.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| De* |Da |Olá matriz toofilter |
| Condição* |onde |Olá tooevaluate condição para cada item |

<br>

### <a name="output-details"></a>Detalhes de saída
Olá seguem detalhes de saída de hello resposta HTTP.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Matriz filtrada |array |Uma matriz que contém um objeto para cada resultado filtrado |

## <a name="next-steps"></a>Próximas etapas
Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).

