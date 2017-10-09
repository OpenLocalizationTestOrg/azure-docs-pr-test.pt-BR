---
title: "aaaScenario - aplicativos de lógica de gatilho com funções do Azure e o Azure Service Bus | Microsoft Docs"
description: "Criar um aplicativo de lógica de uma função tootrigger usando funções do Azure e o Azure Service Bus"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Cenário: Disparar um aplicativo lógico usando o Azure Functions e o Barramento de Serviço do Azure

Você pode usar funções do Azure toocreate um gatilho para um aplicativo de lógica quando precisar toodeploy um ouvinte ou uma tarefa demorada. Por exemplo, você pode criar uma função que escutaria em uma fila e acionaria imediatamente um aplicativo lógico como um gatilho de envio.

## <a name="build-hello-logic-app"></a>Criar aplicativo de lógica de saudação
Neste exemplo, você tem uma função em execução para cada aplicativo lógico que precisa toobe disparado. Primeiro, crie um aplicativo lógico com um gatilho de solicitação HTTP. função Hello chama esse ponto de extremidade sempre que uma mensagem da fila é recebida.  

1. Crie um aplicativo lógico.
2. Selecione Olá **Manual - após o recebimento de uma solicitação HTTP** gatilho.
   Opcionalmente, você pode especificar um toouse de esquema JSON com a mensagem da fila de saudação usando uma ferramenta como [jsonschema.net](http://jsonschema.net). Cole o esquema de saudação gatilho hello. Esquemas compreender designer Olá forma Olá das propriedades de dados e fluxo de hello mais facilmente por meio do fluxo de trabalho de saudação.
2. Adicione as etapas adicionais que você deseja toooccur depois que uma mensagem da fila é recebida. Por exemplo, envie um email por meio do Office 365.  
3. Salve Olá lógica aplicativo toogenerate Olá URL de retorno de chamada para o aplicativo de lógica de toothis Olá gatilho. Olá URL aparece no cartão de gatilho de saudação.

![URL de retorno de chamada de saudação aparece no cartão de gatilho Olá][1]

## <a name="build-hello-function"></a>Criar função hello
Em seguida, você deve criar uma função que age como gatilho hello e toohello fila de escuta.

1. Em Olá [portal do Azure funções](https://functions.azure.com/signin), selecione **nova função**e, em seguida, selecione Olá **ServiceBusQueueTrigger - C#** modelo.
   
    ![portal das Azure Functions][2]
2. Configurar Olá conexão toohello barramento de serviço fila, que usa Olá SDK do Azure Service Bus `OnMessageReceive()` ouvinte.
3. Escreva um função básica toocall Olá lógica aplicativo ponto de extremidade (criado anteriormente) usando a mensagem de saudação do fila como um disparador. Aqui está um exemplo completo de uma função. exemplo Hello usa um `application/json` tipo de conteúdo da mensagem, mas você pode alterar esse tipo conforme necessário.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest, adicionar uma mensagem da fila por meio de uma ferramenta como [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer). Consulte Olá lógica aplicativo dispara imediatamente após a função hello recebe a mensagem de saudação.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
