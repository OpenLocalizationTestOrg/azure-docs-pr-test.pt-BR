---
title: "conector de aaaWebhook para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como ações de webhook toouse e gatilhos tooperform como filtro de matriz de aplicativos lógicos"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Introdução ao conector de webhook Olá

Com a ação de webhook hello e gatilho, você pode iniciar, pausar e retomar fluxos tooperform essas tarefas:

* Disparar de um [Hub de Eventos do Azure](https://github.com/logicappsio/EventHubAPI) assim que um item é recebido
* Aguardar uma aprovação antes de continuar um fluxo de trabalho

Saiba mais sobre [como toocreate APIs personalizadas que dão suporte a um webhook](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Use o gatilho de webhook Olá

Um [*gatilho*](connectors-overview.md) é um evento que inicia um fluxo de trabalho do aplicativo lógico. Um gatilho de webhook é baseado em evento e não depende de sondagem para novos itens. Como Olá [gatilho solicitação](connectors-native-reqres.md), Olá lógica aplicativo dispara Olá instantânea que um evento ocorra. gatilho de webhook Olá registra um *URL de retorno de chamada* tooa serviço e usa esse aplicativo de lógica de saudação do URL toofire como necessário.

Aqui está um exemplo que mostra como tooset um HTTP gatilho Olá Designer de lógica do aplicativo. Olá etapas pressupõem que você já implantou ou está acessando uma API que segue Olá [webhook se inscrever e cancelar a assinatura padrão em aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Olá inscrever-se a chamada é feita sempre que um aplicativo lógico é salvo com um novo webhook ou alternou de tooenabled desabilitado. Olá cancelar a assinatura de chamada é feita quando um gatilho de webhook aplicativo lógica é removido e salvo ou alternou de toodisabled habilitado.

**gatilho de webhook Olá tooadd**

1. Adicionar Olá **HTTP Webhook** disparador como primeira etapa Olá em um aplicativo de lógica.
2. Preencha os parâmetros Olá Olá webhook se inscrever e cancelar a assinatura de chamadas.

   Esta etapa segue Olá mesmo padrão como Olá [ação HTTP](connectors-native-http.md) formato.

     ![Gatilho de HTTP](./media/connectors-native-webhook/using-trigger.png)

3. Adicione pelo menos uma ação.
4. Clique em **salvar** toopublish Olá lógica aplicativo. Saudação de chamadas essa etapa assinar ponto de extremidade com hello retorno de chamada URL necessário tootrigger esse aplicativo lógico.
5. Olá sempre que o serviço faz um `HTTP POST` toohello URL de retorno de chamada, Olá lógica aplicativo acionado e inclui todos os dados passados para a solicitação de saudação.

## <a name="use-hello-webhook-action"></a>Use a ação de webhook Olá

Um [ *ação* ](connectors-overview.md) é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. Uma ação de webhook registra um *URL de retorno de chamada* com um serviço e aguarda até que a URL de saudação é chamado antes de continuar. Olá ["Enviar Email de aprovação"](connectors-create-api-office365-outlook.md) é um exemplo de um conector que segue este padrão. Você pode estender esse padrão para qualquer serviço por meio de ação de webhook hello. 

Aqui está um exemplo que mostra como tooset a uma ação de webhook em Olá Designer de lógica do aplicativo. Essas etapas pressupõem que você já implantou ou está acessando uma API que segue Olá [webhook se inscrever e cancelar a assinatura padrão usado em aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Olá inscrever-se a chamada é feita quando um aplicativo lógico executa a ação de webhook hello. Olá cancelar a assinatura de chamada é feita quando uma execução é cancelada durante a espera por uma resposta ou antes de lógica de saudação aplicativo expire.

**tooadd uma ação de webhook**

1. Escolha **Nova Etapa** > **Adicionar uma ação**.

2. Na caixa de pesquisa hello, digite "webhook" toofind Olá **HTTP Webhook** ação.

    ![Selecionar ação de consulta](./media/connectors-native-webhook/using-action-1.png)

3. Preencher os parâmetros Olá Olá webhook se inscrever e cancelar a assinatura de chamadas

   Esta etapa segue Olá mesmo padrão como Olá [ação HTTP](connectors-native-http.md) formato.

     ![Concluir ação de consulta](./media/connectors-native-webhook/using-action-2.png)
   
   Em tempo de execução, Olá lógica aplicativo chamadas Olá assinar o ponto de extremidade depois de atingir essa etapa.

4. Clique em **salvar** toopublish Olá lógica aplicativo.

## <a name="technical-details"></a>Detalhes técnicos

Aqui estão mais detalhes sobre Olá gatilhos e ações que webhook oferece suporte.

## <a name="webhook-triggers"></a>Gatilhos de Webhook

| Ação | Descrição |
| --- | --- |
| Webhook HTTP |Assine um serviço de tooa de URL de retorno de chamada pode chamar o aplicativo hello URL toofire lógico conforme necessário. |

### <a name="trigger-details"></a>Detalhes do gatilho

#### <a name="http-webhook"></a>Webhook HTTP

Assine um serviço de tooa de URL de retorno de chamada pode chamar o aplicativo hello URL toofire lógico conforme necessário.
Um * significa que o campo é obrigatório.

| Nome de exibição | Nome da Propriedade | Descrição |
| --- | --- | --- |
| Método de Assinatura* |estático |Método HTTP toouse para solicitação de inscrição |
| URI da Assinatura* |uri |URI HTTP toouse para solicitação de inscrição |
| Método de Cancelamento da Assinatura* |estático |Toouse de método HTTP para a solicitação de cancelamento de assinatura |
| URI do Cancelamento da Assinatura* |uri |URI HTTP toouse para solicitação de cancelamento de assinatura |
| Corpo da Assinatura |corpo |Corpo da solicitação HTTP da assinatura |
| Cabeçalhos da Assinatura |headers |Cabeçalhos da solicitação HTTP da assinatura |
| Autenticação da Assinatura |Autenticação |Toouse de autenticação de HTTP para inscrever-se. [Consulte o conector HTTP](connectors-native-http.md#authentication) para obter detalhes |
| Corpo do Cancelamento da Assinatura |corpo |Corpo da solicitação HTTP do cancelamento da assinatura |
| Cabeçalhos do Cancelamento da Assinatura |headers |Cabeçalhos da solicitação HTTP do cancelamento da assinatura |
| Autenticação do Cancelamento da Assinatura |Autenticação |Toouse de autenticação de HTTP para Cancelar assinatura. [Consulte o conector HTTP](connectors-native-http.md#authentication) para obter detalhes |

**Detalhes da saída**

Solicitação de webhook

| Nome da Propriedade | Tipo de Dados | Descrição |
| --- | --- | --- |
| headers |objeto |Cabeçalhos da solicitação de webhook |
| corpo |objeto |Objeto da solicitação de webhook |
| Código de status |int |Código de status da solicitação de webhook |

## <a name="webhook-actions"></a>Ações de Webhook

| Ação | Descrição |
| --- | --- |
| Webhook HTTP |Assine um serviço de tooa de URL de retorno de chamada pode chamar hello URL tooresume uma etapa do fluxo de trabalho conforme necessário. |

### <a name="action-details"></a>Detalhes da ação

#### <a name="http-webhook"></a>Webhook HTTP

Assine um serviço de tooa de URL de retorno de chamada pode chamar hello URL tooresume uma etapa do fluxo de trabalho conforme necessário.
Um * significa que o campo é obrigatório.

| Nome de exibição | Nome da Propriedade | Descrição |
| --- | --- | --- |
| Método de Assinatura* |estático |Método HTTP toouse para solicitação de inscrição |
| URI da Assinatura* |uri |URI HTTP toouse para solicitação de inscrição |
| Método de Cancelamento da Assinatura* |estático |Toouse de método HTTP para a solicitação de cancelamento de assinatura |
| URI do Cancelamento da Assinatura* |uri |URI HTTP toouse para solicitação de cancelamento de assinatura |
| Corpo da Assinatura |corpo |Corpo da solicitação HTTP da assinatura |
| Cabeçalhos da Assinatura |headers |Cabeçalhos da solicitação HTTP da assinatura |
| Autenticação da Assinatura |Autenticação |Toouse de autenticação de HTTP para inscrever-se. [Consulte o conector HTTP](connectors-native-http.md#authentication) para obter detalhes |
| Corpo do Cancelamento da Assinatura |corpo |Corpo da solicitação HTTP do cancelamento da assinatura |
| Cabeçalhos do Cancelamento da Assinatura |headers |Cabeçalhos da solicitação HTTP do cancelamento da assinatura |
| Autenticação do Cancelamento da Assinatura |Autenticação |Toouse de autenticação de HTTP para Cancelar assinatura. [Consulte o conector HTTP](connectors-native-http.md#authentication) para obter detalhes |

**Detalhes da saída**

Solicitação de webhook

| Nome da Propriedade | Tipo de Dados | Descrição |
| --- | --- | --- |
| headers |objeto |Cabeçalhos da solicitação de webhook |
| corpo |objeto |Objeto da solicitação de webhook |
| Código de status |int |Código de status da solicitação de webhook |

## <a name="next-steps"></a>Próximas etapas

* [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)
* [Localizar outros conectores](apis-list.md)