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
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="d653b-103">Cenário: Disparar um aplicativo lógico usando o Azure Functions e o Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="d653b-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="d653b-104">Você pode usar funções do Azure toocreate um gatilho para um aplicativo de lógica quando precisar toodeploy um ouvinte ou uma tarefa demorada.</span><span class="sxs-lookup"><span data-stu-id="d653b-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="d653b-105">Por exemplo, você pode criar uma função que escutaria em uma fila e acionaria imediatamente um aplicativo lógico como um gatilho de envio.</span><span class="sxs-lookup"><span data-stu-id="d653b-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="d653b-106">Criar aplicativo de lógica de saudação</span><span class="sxs-lookup"><span data-stu-id="d653b-106">Build hello logic app</span></span>
<span data-ttu-id="d653b-107">Neste exemplo, você tem uma função em execução para cada aplicativo lógico que precisa toobe disparado.</span><span class="sxs-lookup"><span data-stu-id="d653b-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="d653b-108">Primeiro, crie um aplicativo lógico com um gatilho de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="d653b-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="d653b-109">função Hello chama esse ponto de extremidade sempre que uma mensagem da fila é recebida.</span><span class="sxs-lookup"><span data-stu-id="d653b-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="d653b-110">Crie um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d653b-110">Create a logic app.</span></span>
2. <span data-ttu-id="d653b-111">Selecione Olá **Manual - após o recebimento de uma solicitação HTTP** gatilho.</span><span class="sxs-lookup"><span data-stu-id="d653b-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="d653b-112">Opcionalmente, você pode especificar um toouse de esquema JSON com a mensagem da fila de saudação usando uma ferramenta como [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="d653b-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="d653b-113">Cole o esquema de saudação gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="d653b-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="d653b-114">Esquemas compreender designer Olá forma Olá das propriedades de dados e fluxo de hello mais facilmente por meio do fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d653b-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="d653b-115">Adicione as etapas adicionais que você deseja toooccur depois que uma mensagem da fila é recebida.</span><span class="sxs-lookup"><span data-stu-id="d653b-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="d653b-116">Por exemplo, envie um email por meio do Office 365.</span><span class="sxs-lookup"><span data-stu-id="d653b-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="d653b-117">Salve Olá lógica aplicativo toogenerate Olá URL de retorno de chamada para o aplicativo de lógica de toothis Olá gatilho.</span><span class="sxs-lookup"><span data-stu-id="d653b-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="d653b-118">Olá URL aparece no cartão de gatilho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d653b-118">hello URL appears on hello trigger card.</span></span>

![URL de retorno de chamada de saudação aparece no cartão de gatilho Olá][1]

## <a name="build-hello-function"></a><span data-ttu-id="d653b-120">Criar função hello</span><span class="sxs-lookup"><span data-stu-id="d653b-120">Build hello function</span></span>
<span data-ttu-id="d653b-121">Em seguida, você deve criar uma função que age como gatilho hello e toohello fila de escuta.</span><span class="sxs-lookup"><span data-stu-id="d653b-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="d653b-122">Em Olá [portal do Azure funções](https://functions.azure.com/signin), selecione **nova função**e, em seguida, selecione Olá **ServiceBusQueueTrigger - C#** modelo.</span><span class="sxs-lookup"><span data-stu-id="d653b-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![portal das Azure Functions][2]
2. <span data-ttu-id="d653b-124">Configurar Olá conexão toohello barramento de serviço fila, que usa Olá SDK do Azure Service Bus `OnMessageReceive()` ouvinte.</span><span class="sxs-lookup"><span data-stu-id="d653b-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="d653b-125">Escreva um função básica toocall Olá lógica aplicativo ponto de extremidade (criado anteriormente) usando a mensagem de saudação do fila como um disparador.</span><span class="sxs-lookup"><span data-stu-id="d653b-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="d653b-126">Aqui está um exemplo completo de uma função.</span><span class="sxs-lookup"><span data-stu-id="d653b-126">Here's a full example of a function.</span></span> <span data-ttu-id="d653b-127">exemplo Hello usa um `application/json` tipo de conteúdo da mensagem, mas você pode alterar esse tipo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d653b-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="d653b-128">tootest, adicionar uma mensagem da fila por meio de uma ferramenta como [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="d653b-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="d653b-129">Consulte Olá lógica aplicativo dispara imediatamente após a função hello recebe a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d653b-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
