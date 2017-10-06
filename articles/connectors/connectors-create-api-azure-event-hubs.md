---
title: "aaaSet o monitor de eventos com Hubs de eventos do Azure para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar eventos de tooreceive de fluxos de dados e enviar eventos para os aplicativos lógicos do Azure com Hubs de eventos do Azure"
services: logic-apps
keywords: fluxo de dados, monitor de eventos, hubs de eventos
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>Monitorar, receber e enviar eventos com o conector de Hubs de eventos Olá

tooset backup de um monitor de eventos para que seu aplicativo lógico pode detectar eventos, receber eventos e enviar eventos, conecte-se tooan [Hub de eventos do Azure](https://azure.microsoft.com/services/event-hubs) do seu aplicativo lógico. Saiba mais sobre [Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Requisitos

* Você tem toohave um [namespace de Hubs de eventos e Hub de eventos](../event-hubs/event-hubs-create.md) no Azure. Saiba [como toocreate um namespace de Hubs de eventos e o Hub de eventos](../event-hubs/event-hubs-create.md). 

* toouse [qualquer conector](https://docs.microsoft.com/azure/connectors/apis-list) em seu aplicativo lógico, você tem toocreate um lógica de aplicativo pela primeira vez. Saiba [como um aplicativo de lógica de toocreate](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Verifique as permissões de namespace de Hubs de eventos e localizar a cadeia de caracteres de conexão Olá

Para tooaccess de aplicativo sua lógica de qualquer serviço, você tem toocreate um [ *conexão* ](./connectors-overview.md) entre sua lógica aplicativo hello serviço e, se ainda não o fez. Essa conexão autoriza seus dados de tooaccess lógica do aplicativo.
Para sua tooaccess de aplicativo lógica seu Hub de eventos, você tem toohave **gerenciar** permissões e a cadeia de caracteres de conexão de saudação para seu namespace de Hubs de eventos.

toocheck as permissões e a cadeia de conexão do get hello, siga estas etapas.

1.  Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure"). 

2.  Vá Hubs de eventos tooyour *namespace*, não Olá Hub de eventos específico. Na folha de namespace hello, em **configurações**, escolha **políticas de acesso compartilhado**. Em **Declarações**, verifique se você tem permissões de **Gerenciamento** para esse namespace.

    ![Gerenciar permissões para seu namespace do Hub de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  cadeia de conexão toocopy Olá para o namespace de Hubs de eventos hello, escolha **RootManageSharedAccessKey**. Tooyour próxima primária chave de cadeia de caracteres de conexão, escolha o botão de cópia de saudação.

    ![Copie a cadeia de conexão do namespace dos Hubs de Eventos](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm se a cadeia de conexão está associada com seu namespace de Hubs de eventos ou com um Hub de eventos específico, verifique cadeia de caracteres de conexão de saudação de saudação `EntityPath` parâmetro. Se você encontrar esse parâmetro, cadeia de caracteres de conexão de saudação é para um Hub de eventos específico "entidade" e não é Olá toouse de cadeia de caracteres correto com seu aplicativo lógico.

4.  Agora, quando você for solicitado a fornecer credenciais depois de adicionar um aplicativo Hubs de eventos do gatilho ou ação tooyour lógica, você pode conectar tooyour namespace de Hubs de eventos. Dê um nome de sua conexão, digite a cadeia de caracteres de conexão de saudação que você copiou e escolha **criar**.

    ![Insira a cadeia de conexão para o namespace dos Hubs de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Depois de criar sua conexão, o nome de conexão de saudação deve aparecer em Olá gatilho de Hubs de evento ou ação. 
    Você pode continuar com hello outras etapas em seu aplicativo de lógica.

    ![Conexão do namespace dos Hubs de Eventos criado](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Iniciar o fluxo de trabalho quando seu Hub de Eventos receber novos eventos

Um [*gatilho*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia um fluxo de trabalho em seu aplicativo lógico. Para iniciar um fluxo de trabalho quando novos eventos são enviados tooyour Hub de eventos, siga estas etapas para adicionar o gatilho Olá que detecta esse evento.

1.  Em Olá [portal do Azure](https://portal.azure.com "portal do Azure"), vá tooyour aplicativo de lógica existente ou criar um aplicativo em branco lógica.

2.  Na caixa de pesquisa Olá Olá Designer de lógica do aplicativo, insira `event hubs` para seu filtro. Selecione esse gatilho: **quando os eventos estiverem disponíveis no Hub de Eventos**

    ![Selecionar o gatilho quando seu Hub de Eventos receber novos eventos](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Se você ainda não tiver um namespace de Hubs de eventos de tooyour de conexão, será solicitado que você toocreate agora essa conexão. Dê um nome de sua conexão e insira a cadeia de caracteres de conexão de saudação para seu namespace de Hubs de eventos. 
    Se necessário, saiba [como toofind sua cadeia de caracteres de conexão](#permissions-connection-string).

    ![Insira a cadeia de conexão para o namespace dos Hubs de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Depois de criar conexão hello, Olá configurações para Olá **quando um evento em disponíveis em um Hub de eventos** gatilho aparecem.

    ![Configurações do gatilho quando seu Hub de Eventos receber novos eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Insira ou selecione o nome Olá Olá Hub de eventos que você deseja toomonitor. Selecione a frequência de saudação e intervalo de frequência você deseja toocheck Olá Hub de eventos.

    > [!TIP]
    > toooptionally selecionar um grupo de consumidores para ler eventos, escolha **Mostrar opções avançadas**. 

    ![Especifique o Hub de Evento ou grupo de consumidores](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    Você agora configurou um gatilho toostart um fluxo de trabalho para seu aplicativo lógico. 
    Seu aplicativo lógica verifica Olá especificado Hub de eventos com base em agendamento Olá que você definir. 
    Se seu aplicativo encontrar novos eventos no hello Hub de eventos, o gatilho Olá executa outras ações ou disparadores em seu aplicativo de lógica.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Enviar eventos tooyour Hub de eventos do aplicativo lógica

Uma [*ação*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa executada pelo fluxo de trabalho do aplicativo lógico. Depois de adicionar um aplicativo de lógica do gatilho tooyour, você pode adicionar operações de tooperform uma ação com dados gerados por que o disparador. toosend um tooyour evento Hub de eventos do seu aplicativo lógico, siga estas etapas.

1.  No Designer de Aplicativo Lógico, no gatilho de seu aplicativo lógico, escolha **Nova etapa** > **Adicionar uma ação**.

    ![Escolha "Nova etapa", em seguida, "Adicionar uma ação"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    Agora você pode localizar e selecionar uma ação tooperform. 
    Embora você possa selecionar qualquer ação, neste exemplo, queremos que eventos de toosend de ação do hello Hubs de eventos.

2.  Na caixa de pesquisa hello, digite `event hubs` para seu filtro.
Selecione esta ação: **Enviar evento**

    ![Selecione a ação "Hubs de eventos - Enviar evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Insira os detalhes de saudação necessária para evento hello, como nome Olá Olá Hub de eventos onde você deseja que o evento de saudação toosend. Insira os detalhes opcionais sobre o evento hello, como conteúdo para o evento.

    > [!TIP]
    > toooptionally especificar a partição do Hub de eventos Olá onde toosend Olá eventos, escolha **Mostrar opções avançadas**. 

    ![Insira o nome do Hub de Eventos e detalhes opcionais do evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Salve suas alterações.

    ![Salve seu aplicativo lógico](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    Você configurou agora um toosend de eventos de ação de seu aplicativo lógico. 

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/eventhubs/). 

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder a perguntas e veja que outros usuários de aplicativos do Azure lógicos estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp melhorar a lógica de aplicativos e conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos lógicos](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Próximas etapas

*  [Encontrar outros conectores de Aplicativos Lógicos do Azure](./apis-list.md)