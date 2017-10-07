---
title: "ações de solicitação e resposta aaaUse | Microsoft Docs"
description: "Visão geral de gatilho de solicitação e resposta hello e ação em um aplicativo do Azure lógica"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a>Começar com os componentes de solicitação e resposta Olá
Com componentes Olá de solicitação e resposta em um aplicativo da lógica, você pode responder em tempo real tooevents.

Por exemplo, você pode:

* Responda tooan solicitação HTTP com dados de um banco de dados no local por meio de um aplicativo lógico.
* Dispare um aplicativo lógico de um evento de webhook externo.
* Chamar um aplicativo lógico com uma ação de solicitação e resposta de dentro de outro aplicativo lógico.

tooget iniciado usando ações de solicitação e resposta de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-request-trigger"></a>Use Olá gatilho de solicitação HTTP
Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico. [Saiba mais sobre gatilhos](connectors-overview.md).

Aqui está uma sequência de exemplo de como tooset um HTTP solicitar em Olá Designer de lógica do aplicativo.

1. Adicionar gatilho Olá **solicitar - quando HTTP de uma solicitação é recebida** em seu aplicativo de lógica. Opcionalmente, você pode fornecer um esquema JSON (usando uma ferramenta como [JSONSchema.net](http://jsonschema.net)) para o corpo da solicitação hello. Isso permite que os tokens de designer toogenerate Olá para as propriedades na solicitação HTTP de saudação.
2. Adicione outra ação para que você pode salvar o aplicativo de lógica de saudação.
3. Depois de salvar o aplicativo de lógica de hello, você pode obter URL de solicitação HTTP de saudação do cartão de solicitação de saudação.
4. Um HTTP POST (você pode usar uma ferramenta como [carteiro](https://www.getpostman.com/)) gatilhos de URL toohello Olá aplicativo lógico.

> [!NOTE]
> Se você não definir uma ação de resposta, um `202 ACCEPTED` resposta é retornada imediatamente toohello chamador. Você pode usar o hello resposta ação toocustomize uma resposta.
> 
> 

![Gatilho de resposta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>Use Olá ação de resposta HTTP
Olá ação de resposta HTTP só é válida quando você usá-lo em um fluxo de trabalho que é disparado por uma solicitação HTTP. Se você não definir uma ação de resposta, um `202 ACCEPTED` resposta é retornada imediatamente toohello chamador.  Você pode adicionar uma ação de resposta em qualquer etapa do fluxo de trabalho de saudação. Olá lógica aplicativo mantém apenas solicitação de entrada hello aberto por um minuto por uma resposta.  Após um minuto, se nenhuma resposta foi enviada do fluxo de trabalho da saudação (e existe uma ação de resposta na definição de saudação), um `504 GATEWAY TIMEOUT` é retornado toohello chamador.

Aqui está como tooadd uma ação de resposta HTTP:

1. Selecione Olá **nova etapa** botão.
2. Escolha **Adicionar uma ação**.
3. Na caixa de pesquisa de ação hello, digite **resposta** Olá toolist ação de resposta.
   
    ![Selecione a ação de resposta Olá](./media/connectors-native-reqres/using-action-1.png)
4. Adicione quaisquer parâmetros que são necessários para a mensagem de resposta HTTP hello.
   
    ![Ação de resposta Olá concluída](./media/connectors-native-reqres/using-action-2.png)
5. Clique o canto superior esquerdo de saudação de saudação da barra de ferramentas toosave e sua lógica aplicativo salvará os dois e publicar (Ativar).

## <a name="request-trigger"></a>Gatilho de solicitação
Aqui estão os detalhes de saudação disparador Olá que oferece suporte a esse conector. Há um único gatilho de solicitação.

| Gatilho | Descrição |
| --- | --- |
| Solicitação |Ocorre quando uma solicitação HTTP é recebida |

## <a name="response-action"></a>Ação de resposta
Aqui estão os detalhes de saudação para ação Olá que oferece suporte a esse conector. Há uma única ação de resposta que pode ser usada apenas quando acompanhada por um gatilho de solicitação.

| Ação | Descrição |
| --- | --- |
| Resposta |Retorna que uma resposta toohello correlacionado a solicitação HTTP |

### <a name="trigger-and-action-details"></a>Detalhes de gatilho e da ação
Olá tabelas a seguir descrevem os campos de entrada hello para Olá trigger e action e Olá detalhes de saída correspondente.

#### <a name="request-trigger"></a>Gatilho de solicitação
a seguir Olá é um campo de entrada para o disparador de saudação de uma solicitação HTTP de entrada.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| Esquema JSON |schema |esquema JSON Olá Olá HTTP do corpo da solicitação |

<br>

**Detalhes de saída**

Olá seguem detalhes de saída de solicitação de saudação.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| headers |objeto |Cabeçalhos da solicitação |
| Corpo |objeto |Objeto da solicitação |

#### <a name="response-action"></a>Ação de resposta
Olá seguem campos de entrada para Olá ação de resposta HTTP. Um * significa que é um campo obrigatório.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| Código de status* |statusCode |Olá, código de status HTTP |
| Cabeçalhos |headers |Um objeto JSON de qualquer tooinclude de cabeçalhos de resposta |
| Corpo |body |corpo da resposta Olá |

## <a name="next-steps"></a>Próximas etapas
Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).

