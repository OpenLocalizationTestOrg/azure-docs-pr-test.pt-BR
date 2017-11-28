---
title: "Cenário: Disparar aplicativos lógicos com o Azure Functions e Barramento de Serviço do Azure | Microsoft Docs"
description: "Crie uma função para disparar um aplicativo lógico usando o Azure Functions e o Barramento de Serviço do Azure"
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
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="a5bfd-103">Cenário: Disparar um aplicativo lógico usando o Azure Functions e o Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="a5bfd-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="a5bfd-104">Você pode usar as Azure Functions para criar um gatilho para um aplicativo lógico quando você precisa implantar um ouvinte ou uma tarefa de execução longa.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="a5bfd-105">Por exemplo, você pode criar uma função que escutaria em uma fila e acionaria imediatamente um aplicativo lógico como um gatilho de envio.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="a5bfd-106">Compilar o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="a5bfd-106">Build the logic app</span></span>
<span data-ttu-id="a5bfd-107">Neste exemplo, você terá uma função em execução para cada aplicativo lógico que precisa ser disparado.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="a5bfd-108">Primeiro, crie um aplicativo lógico com um gatilho de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="a5bfd-109">A função chama esse ponto de extremidade sempre que uma mensagem da fila é recebida.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="a5bfd-110">Crie um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-110">Create a logic app.</span></span>
2. <span data-ttu-id="a5bfd-111">Selecione o gatilho **Manual – Quando uma solicitação HTTP é recebida**.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="a5bfd-112">Opcionalmente, você pode especificar um esquema JSON para usar com a mensagem da fila usando uma ferramenta como [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="a5bfd-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="a5bfd-113">Cole o esquema no gatilho.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="a5bfd-114">Os esquemas ajudam o designer a entender a forma dos dados e movimentar as propriedades com mais facilidade pelo fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="a5bfd-115">Adicione as etapas adicionais que você deseja que ocorram após uma mensagem da fila ser recebida.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="a5bfd-116">Por exemplo, envie um email por meio do Office 365.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="a5bfd-117">Salve o aplicativo lógico para gerar a URL de retorno de chamada do gatilho para esse aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="a5bfd-118">A URL aparecerá no cartão do gatilho.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-118">The URL appears on the trigger card.</span></span>

![A URL de retorno de chamada aparece no cartão do gatilho][1]

## <a name="build-the-function"></a><span data-ttu-id="a5bfd-120">Compilar a função</span><span class="sxs-lookup"><span data-stu-id="a5bfd-120">Build the function</span></span>
<span data-ttu-id="a5bfd-121">Em seguida, crie uma função que atuará como o gatilho e ouvirá a fila.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="a5bfd-122">Abra o [Portal do Azure Functions](https://functions.azure.com/signin), escolha **Nova Função** e selecione o modelo **ServiceBusQueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![portal das Azure Functions][2]
2. <span data-ttu-id="a5bfd-124">Configure a conexão com a fila do Barramento de Serviço, que usará o ouvinte de `OnMessageReceive()` do SDK do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="a5bfd-125">Grave uma função básica para chamar o ponto de extremidade do aplicativo lógico (criado anteriormente) usando a mensagem da fila como gatilho.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="a5bfd-126">Aqui está um exemplo completo de uma função.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-126">Here's a full example of a function.</span></span> <span data-ttu-id="a5bfd-127">O exemplo usa um tipo de conteúdo de mensagem `application/json`, mas você pode alterar isso conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="a5bfd-128">Para testar, adicionar uma mensagem na fila por meio de uma ferramenta como o [Explorer do Barramento de Serviço](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="a5bfd-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="a5bfd-129">Veja o aplicativo lógico disparar imediatamente após a função receber a mensagem.</span><span class="sxs-lookup"><span data-stu-id="a5bfd-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
