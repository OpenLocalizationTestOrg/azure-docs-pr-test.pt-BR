---
title: "aaaLearn como toouse Olá conector MQ em aplicativos do Azure lógica | Microsoft Docs"
description: "Conectar-se tooan no local ou servidor do Azure MQ de toobrowse de fluxo de trabalho de aplicativo sua lógica, receber e enviar mensagens tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Conecte-se tooan servidor IBM MQ de aplicativos lógicos usando Olá MQ conector 

O Conector Microsoft para MQ envia e recupera mensagens armazenadas em um servidor MQ local ou no Azure. Esse conector inclui um cliente Microsoft MQ para se comunicar com um servidor MQ IBM remoto em uma rede TCP/IP. Este documento é um conector MQ starter guia toouse hello. É recomendável começar navegando em uma única mensagem em uma fila e, em seguida, tentar Olá outras ações.    

conector MQ Olá inclui Olá ações a seguir. Não há nenhum gatilho.

-   Procurar uma única mensagem sem excluir a mensagem de saudação do hello IBM MQ Server
-   Procurar um lote de mensagens sem excluir mensagens de saudação do hello IBM MQ Server
-   Uma única mensagem de recebimento e excluir a mensagem de saudação do hello IBM MQ Server
-   Receber um lote de mensagens e excluir mensagens de saudação da saudação IBM MQ Server
-   Enviar uma única mensagem toohello IBM MQ Server 

## <a name="prerequisites"></a>Pré-requisitos

* Se usar um servidor do local MQ, [instalar o gateway de dados local Olá](../logic-apps/logic-apps-gateway-install.md) em um servidor dentro de sua rede. Se Olá MQ Server está publicamente disponível ou disponível no Azure, em seguida, Olá data gateway não está usado ou necessárias.

    > [!NOTE]
    > servidor de saudação onde Olá Gateway de dados local está instalado também deve ter .net Framework 4.6 instalado para Olá MQ conector toofunction.

* Criar hello recursos do Azure para gateway de dados local Olá - [configurar a conexão de gateway de dados Olá](../logic-apps/logic-apps-gateway-connection.md).

* Versões do IBM WebSphere MQ oficialmente com suporte:
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>Criar um aplicativo lógico

1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**. 
2. Digite hello **nome**, como MQTestApp, **assinatura**, **grupo de recursos**, e **local** (usar Olá local onde hello conexão de Gateway de dados local está configurado). Selecione **Pin toodashboard**e selecione **criar**.  
![Criar Aplicativo Lógico](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>Adicionar um gatilho

> [!NOTE]
> Olá MQ conector não tem todos os gatilhos. Assim, use outra toostart de gatilho seu aplicativo lógico, como Olá **recorrência** gatilho. 

1. Olá **lógica aplicativos Designer** é aberta, selecione **recorrência** na lista de saudação de gatilhos comuns.
2. Selecione **editar** dentro Olá gatilho de recorrência. 
3. Saudação de conjunto **frequência** muito**dia**e conjunto hello **intervalo** muito**7**. 

## <a name="browse-a-single-message"></a>Procurar uma única mensagem
1. Selecione **+ Nova etapa** e selecione **Adicionar uma ação**.
2. Na caixa de pesquisa hello, digite `mq`e, em seguida, selecione **MQ - procurar mensagem**.  
![Procurar mensagem](media/connectors-create-api-mq/Browse_message.png)

3. Se não houver uma conexão MQ existente, em seguida, crie conexão hello:  

    1. Selecione **conectar por meio do gateway de dados local**e insira as propriedades de saudação do servidor MQ.  
    Para **Server**, você pode inserir nome do servidor de saudação MQ ou Inserir endereço IP hello seguido por um número de porta de dois-pontos e hello. 
    2. Olá **gateway** suspensa lista as conexões de gateway existentes que foram configuradas. Selecione seu gateway.
    3. Selecione **Criar** quando terminar. A conexão tem a aparência a seguir toohello semelhante:   
    ![Propriedades da Conexão](media/connectors-create-api-mq/Connection_Properties.png)

4. Nas propriedades de ação de saudação, você pode:  

    * Saudação de uso **fila** propriedade tooaccess um nome de outra fila que está definida na conexão Olá
    * Saudação de uso **MessageId**, **CorrelationId**, **GroupId**e toobrowse outras propriedades de uma mensagem com base nas propriedades da mensagem MQ diferentes Olá
    * Definir **IncludeInfo** muito**True** tooinclude informações de mensagem adicionais na saída de hello. Ou, defina-o muito**False** toonot incluir informações adicionais de mensagem na saída de hello.
    * Insira um **Timeout** toodetermine valor toowait quanto para tooarrive uma mensagem em uma fila vazia. Se nada for inserido, mensagem de saudação do primeiro na fila de saudação é recuperada e não há nenhum tempo gasto aguardando tooappear uma mensagem.  
    ![Procurar propriedades de mensagem](media/connectors-create-api-mq/Browse_message_Props.png)

5. **Salve** suas alterações e, em seguida, **execute** seu aplicativo lógico:  
![Salvar e Executar](media/connectors-create-api-mq/Save_Run.png)

6. Depois de alguns segundos, etapas Olá Olá executar são mostradas, e você pode examinar a saída de hello. Selecione Olá marca de seleção verde toosee detalhes de cada etapa. Selecione **consulte saídas brutas** toosee obter detalhes adicionais sobre Olá dados de saída.  
![Procurar saída de mensagem](media/connectors-create-api-mq/Browse_message_output.png)  

    Saída bruta:  
    ![Procurar saída bruta de mensagem](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Olá quando **IncludeInfo** opção é definida tootrue, Olá saída a seguir será exibida:  
![Procurar informações de inclusão da mensagem](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>Procurar várias mensagens
Olá **procurar mensagens** ação inclui um **BatchSize** tooindicate opção quantas mensagens devem ser retornadas da fila de saudação.  Se **BatchSize** não tem nenhuma entrada, todas as mensagens são retornadas. Olá retornado a saída é uma matriz de mensagens.

1. Ao adicionar Olá **procurar mensagens** ação, a conexão de primeira Olá configurado é selecionada por padrão. Selecione **alterar conexão** toocreate uma nova conexão, ou selecione uma conexão diferente.

2. saída de Hello da procurar mensagens mostra:  
![Saída de Procurar mensagens](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>Receber uma única mensagem
Olá **receber mensagem** ação tem Olá mesmo entradas e saídas como Olá **procurar mensagem** ação. Ao usar **receber mensagem**, mensagem de saudação é excluída da fila de saudação.

## <a name="receive-multiple-messages"></a>Receber várias mensagens
Olá **receber mensagens** ação tem Olá mesmo entradas e saídas como Olá **procurar mensagens** ação. Ao usar **receber mensagens**, mensagens de saudação são excluídas da fila de saudação.

Se não houver nenhuma mensagem na fila de saudação ao fazer uma pesquisa ou receive, Olá falhar com hello saída a seguir:  
![Erro MQ Nenhuma Mensagem](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>Enviar uma mensagem
1. Ao adicionar Olá **enviar mensagem** ação, a conexão de primeira Olá configurado é selecionada por padrão. Selecione **alterar conexão** toocreate uma nova conexão, ou selecione uma conexão diferente. Olá válido **tipos de mensagem** são **datagrama**, **resposta**, ou **solicitação**.  
![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)

2. Olá saída de enviar mensagem hello seguinte aparência:  
![Send Msg Output](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/mq/).

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).
