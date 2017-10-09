---
title: "aaaWorkflow ações e gatilhos - os aplicativos lógicos do Azure | Microsoft Docs"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="9cac8-102">Ações do fluxo de trabalho e gatilhos para os Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="9cac8-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="9cac8-103">Os aplicativos lógicos são compostos por gatilhos e ações.</span><span class="sxs-lookup"><span data-stu-id="9cac8-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="9cac8-104">Há seis tipos de gatilhos.</span><span class="sxs-lookup"><span data-stu-id="9cac8-104">There are six types of triggers.</span></span> <span data-ttu-id="9cac8-105">Cada tipo tem um comportamento e interface diferentes.</span><span class="sxs-lookup"><span data-stu-id="9cac8-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="9cac8-106">Você também pode saber sobre outros detalhes examinando os detalhes de saudação do hello [linguagem de definição de fluxo de trabalho](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="9cac8-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="9cac8-107">Ler em toolearn mais informações sobre gatilhos e ações e como você pode usá-los toobuild lógica aplicativos tooimprove seus processos de negócios e fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="9cac8-108">Gatilhos</span><span class="sxs-lookup"><span data-stu-id="9cac8-108">Triggers</span></span>  

<span data-ttu-id="9cac8-109">Um gatilho Especifica chamadas de saudação que podem iniciar uma execução de fluxo de trabalho de aplicativo sua lógica.</span><span class="sxs-lookup"><span data-stu-id="9cac8-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="9cac8-110">Aqui estão duas maneiras diferentes de saudação tooinitiate uma execução do fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="9cac8-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="9cac8-111">Gatilho de sondagem</span><span class="sxs-lookup"><span data-stu-id="9cac8-111">A polling trigger</span></span>  

-   <span data-ttu-id="9cac8-112">Um disparador de envio - por chamada hello [API REST do serviço de fluxo de trabalho](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="9cac8-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="9cac8-113">Todos os gatilhos contêm estes elementos de alto nível:</span><span class="sxs-lookup"><span data-stu-id="9cac8-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="9cac8-114">Tipos de gatilho e suas entradas</span><span class="sxs-lookup"><span data-stu-id="9cac8-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="9cac8-115">Você pode usar estes tipos de gatilhos:</span><span class="sxs-lookup"><span data-stu-id="9cac8-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="9cac8-116">**Solicitar** \- torna o aplicativo de lógica de saudação um ponto de extremidade para você toocall</span><span class="sxs-lookup"><span data-stu-id="9cac8-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="9cac8-117">**Recorrência** \- é acionado com base em um agendamento definido</span><span class="sxs-lookup"><span data-stu-id="9cac8-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="9cac8-118">**HTTP** \- sonda um ponto de extremidade HTTP da Web.</span><span class="sxs-lookup"><span data-stu-id="9cac8-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="9cac8-119">ponto de extremidade Olá HTTP deve estar em conformidade tooa contrato específica de disparo \- usando um 202\-padrão assíncrono, ou retornando uma matriz</span><span class="sxs-lookup"><span data-stu-id="9cac8-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="9cac8-120">**ApiConnection** \- disparam sondagens como Olá HTTP, no entanto, se beneficia do hello [APIs gerenciada pela Microsoft](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="9cac8-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="9cac8-121">**HTTPWebhook** \- abre um ponto de extremidade, semelhante toohello gatilho Manual, no entanto, ele também chama tooa especificado tooregister de URL e cancelar o registro</span><span class="sxs-lookup"><span data-stu-id="9cac8-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="9cac8-122">**ApiConnectionWebhook** \- opera como Olá HTTPWebhook gatilho aproveitando Olá APIs gerenciada pela Microsoft</span><span class="sxs-lookup"><span data-stu-id="9cac8-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="9cac8-123">Cada tipo de gatilho tem um conjunto diferente de **entradas** que define seu comportamento.</span><span class="sxs-lookup"><span data-stu-id="9cac8-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="9cac8-124">Gatilho de solicitação</span><span class="sxs-lookup"><span data-stu-id="9cac8-124">Request trigger</span></span>  

<span data-ttu-id="9cac8-125">Esse gatilho serve como um ponto de extremidade que você chamar por meio de uma solicitação HTTP tooinvoke seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9cac8-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="9cac8-126">Um gatilho de solicitação é semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="9cac8-127">Há também uma propriedade opcional denominada **esquema**:</span><span class="sxs-lookup"><span data-stu-id="9cac8-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="9cac8-128">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-128">Element name</span></span>|<span data-ttu-id="9cac8-129">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-129">Required</span></span>|<span data-ttu-id="9cac8-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="9cac8-131">schema</span><span class="sxs-lookup"><span data-stu-id="9cac8-131">schema</span></span>|<span data-ttu-id="9cac8-132">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-132">No</span></span>|<span data-ttu-id="9cac8-133">Um esquema JSON que valida a solicitação de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="9cac8-134">Útil para ajudar a saber quais propriedades tooreference etapas subsequentes do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="9cac8-135">tooinvoke esse ponto de extremidade, você precisa Olá toocall *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="9cac8-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="9cac8-136">Consulte [API REST do Serviço do Fluxo de Trabalho](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="9cac8-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="9cac8-137">Gatilho de recorrência</span><span class="sxs-lookup"><span data-stu-id="9cac8-137">Recurrence trigger</span></span>  

<span data-ttu-id="9cac8-138">Um gatilho de Recorrência é aquele executado com base em um agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="9cac8-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="9cac8-139">Tal gatilho pode parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="9cac8-140">Como você pode ver, é uma maneira simples de toorun um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="9cac8-141">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-141">Element name</span></span>|<span data-ttu-id="9cac8-142">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-142">Required</span></span>|<span data-ttu-id="9cac8-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="9cac8-144">frequência</span><span class="sxs-lookup"><span data-stu-id="9cac8-144">frequency</span></span>|<span data-ttu-id="9cac8-145">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-145">Yes</span></span>|<span data-ttu-id="9cac8-146">Frequência hello gatilho é executado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-146">How often hello trigger executes.</span></span> <span data-ttu-id="9cac8-147">Use apenas um desses valores possíveis: segundo, minuto, hora, dia, semana, mês ou ano</span><span class="sxs-lookup"><span data-stu-id="9cac8-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="9cac8-148">intervalo</span><span class="sxs-lookup"><span data-stu-id="9cac8-148">interval</span></span>|<span data-ttu-id="9cac8-149">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-149">Yes</span></span>|<span data-ttu-id="9cac8-150">Intervalo de saudação atribuído a frequência de recorrência Olá</span><span class="sxs-lookup"><span data-stu-id="9cac8-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="9cac8-151">startTime</span><span class="sxs-lookup"><span data-stu-id="9cac8-151">startTime</span></span>|<span data-ttu-id="9cac8-152">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-152">No</span></span>|<span data-ttu-id="9cac8-153">Se um startTime for fornecido sem uma diferença UTC, o fuso horário será usado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="9cac8-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="9cac8-154">timeZone</span></span>|<span data-ttu-id="9cac8-155">não</span><span class="sxs-lookup"><span data-stu-id="9cac8-155">no</span></span>|<span data-ttu-id="9cac8-156">Se um startTime for fornecido sem uma diferença UTC, o fuso horário será usado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="9cac8-157">Você também pode agendar uma execução de gatilho toostart em algum momento no futuro de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="9cac8-158">Por exemplo, se você quiser toostart toda segunda-feira de relatório de uma semana você pode agendar Olá lógica aplicativo toostart toda segunda-feira, criando Olá gatilho a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cac8-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="9cac8-159">Gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="9cac8-159">HTTP trigger</span></span>  

<span data-ttu-id="9cac8-160">Gatilhos HTTP sondagem um ponto de extremidade especificado e verifique Olá resposta toodetermine se o fluxo de trabalho Olá deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="9cac8-161">objeto de entradas de saudação usa o conjunto de saudação de parâmetros necessários tooconstruct uma chamada HTTP:</span><span class="sxs-lookup"><span data-stu-id="9cac8-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="9cac8-162">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-162">Element name</span></span>|<span data-ttu-id="9cac8-163">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-163">Required</span></span>|<span data-ttu-id="9cac8-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-164">Description</span></span>|<span data-ttu-id="9cac8-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="9cac8-166">estático</span><span class="sxs-lookup"><span data-stu-id="9cac8-166">method</span></span>|<span data-ttu-id="9cac8-167">sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-167">yes</span></span>|<span data-ttu-id="9cac8-168">Pode ser uma saudação seguindo os métodos HTTP: GET, POST, PUT, DELETE, PATCH ou HEAD</span><span class="sxs-lookup"><span data-stu-id="9cac8-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="9cac8-169">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-169">String</span></span>|  
|<span data-ttu-id="9cac8-170">uri</span><span class="sxs-lookup"><span data-stu-id="9cac8-170">uri</span></span>|<span data-ttu-id="9cac8-171">sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-171">yes</span></span>|<span data-ttu-id="9cac8-172">Olá ponto de extremidade http ou https que é chamado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="9cac8-173">Máximo de 2 quilobytes.</span><span class="sxs-lookup"><span data-stu-id="9cac8-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="9cac8-174">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-174">String</span></span>|  
|<span data-ttu-id="9cac8-175">consultas</span><span class="sxs-lookup"><span data-stu-id="9cac8-175">queries</span></span>|<span data-ttu-id="9cac8-176">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-176">No</span></span>|<span data-ttu-id="9cac8-177">Um objeto que representa a URL do hello consulta parâmetros tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="9cac8-178">Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="9cac8-179">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-179">Object</span></span>|  
|<span data-ttu-id="9cac8-180">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-180">headers</span></span>|<span data-ttu-id="9cac8-181">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-181">No</span></span>|<span data-ttu-id="9cac8-182">Um objeto que representa cada um dos cabeçalhos de saudação toohello solicitação é enviada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="9cac8-183">Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="9cac8-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="9cac8-184">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-184">Object</span></span>|  
|<span data-ttu-id="9cac8-185">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-185">body</span></span>|<span data-ttu-id="9cac8-186">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-186">No</span></span>|<span data-ttu-id="9cac8-187">Um objeto que representa a carga de saudação que é enviada toohello de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9cac8-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="9cac8-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-188">Object</span></span>|  
|<span data-ttu-id="9cac8-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="9cac8-189">retryPolicy</span></span>|<span data-ttu-id="9cac8-190">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-190">No</span></span>|<span data-ttu-id="9cac8-191">Um objeto que permite que você personalize o comportamento de repetição de saudação erros 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="9cac8-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="9cac8-192">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-192">Object</span></span>|  
|<span data-ttu-id="9cac8-193">autenticação</span><span class="sxs-lookup"><span data-stu-id="9cac8-193">authentication</span></span>|<span data-ttu-id="9cac8-194">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-194">No</span></span>|<span data-ttu-id="9cac8-195">Método hello representa que Olá solicitação deve ser autenticado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="9cac8-196">Para obter detalhes sobre esse objeto, consulte [Autenticação de Saída do Agendador](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="9cac8-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="9cac8-197">Além do Agendador, há mais uma propriedade com suporte: `authority` por padrão, esse valor é `https://login.windows.net` quando não especificado, mas você pode usar um público diferente como `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="9cac8-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="9cac8-198">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-198">Object</span></span>|  
  
<span data-ttu-id="9cac8-199">gatilho HTTP Olá requer Olá API HTTP tooconform com toowork um padrão específico bem com seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9cac8-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="9cac8-200">Ele requer Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cac8-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="9cac8-201">Resposta</span><span class="sxs-lookup"><span data-stu-id="9cac8-201">Response</span></span>|<span data-ttu-id="9cac8-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="9cac8-203">Código de status</span><span class="sxs-lookup"><span data-stu-id="9cac8-203">Status code</span></span>|<span data-ttu-id="9cac8-204">Código de status 200 \(Okey\) toocause uma execução.</span><span class="sxs-lookup"><span data-stu-id="9cac8-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="9cac8-205">Qualquer outro código de status não provoca uma execução.</span><span class="sxs-lookup"><span data-stu-id="9cac8-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="9cac8-206">Repetir\-após o cabeçalho</span><span class="sxs-lookup"><span data-stu-id="9cac8-206">Retry\-after header</span></span>|<span data-ttu-id="9cac8-207">Número de segundos até que o aplicativo de lógica de saudação controla o ponto de extremidade Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="9cac8-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="9cac8-208">Cabeçalho do local</span><span class="sxs-lookup"><span data-stu-id="9cac8-208">Location header</span></span>|<span data-ttu-id="9cac8-209">Olá toocall de URL no próximo intervalo de sondagem hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="9cac8-210">Se não for especificado, a URL original Olá é usado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="9cac8-211">Aqui estão alguns exemplos de comportamentos diferentes para diferentes tipos de solicitações:</span><span class="sxs-lookup"><span data-stu-id="9cac8-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="9cac8-212">Código de resposta</span><span class="sxs-lookup"><span data-stu-id="9cac8-212">Response code</span></span>|<span data-ttu-id="9cac8-213">Repetir\-Após</span><span class="sxs-lookup"><span data-stu-id="9cac8-213">Retry\-After</span></span>|<span data-ttu-id="9cac8-214">Comportamento</span><span class="sxs-lookup"><span data-stu-id="9cac8-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="9cac8-215">200</span><span class="sxs-lookup"><span data-stu-id="9cac8-215">200</span></span>|<span data-ttu-id="9cac8-216">\(nenhum\)</span><span class="sxs-lookup"><span data-stu-id="9cac8-216">\(none\)</span></span>|<span data-ttu-id="9cac8-217">Não válido disparador, repetição\-após mecanismo Olá necessária, caso contrário nunca é sondagens para a próxima solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="9cac8-218">202</span><span class="sxs-lookup"><span data-stu-id="9cac8-218">202</span></span>|<span data-ttu-id="9cac8-219">60</span><span class="sxs-lookup"><span data-stu-id="9cac8-219">60</span></span>|<span data-ttu-id="9cac8-220">Não disparar o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="9cac8-221">próxima tentativa de saudação ocorre em um minuto.</span><span class="sxs-lookup"><span data-stu-id="9cac8-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="9cac8-222">200</span><span class="sxs-lookup"><span data-stu-id="9cac8-222">200</span></span>|<span data-ttu-id="9cac8-223">10</span><span class="sxs-lookup"><span data-stu-id="9cac8-223">10</span></span>|<span data-ttu-id="9cac8-224">Executar o fluxo de trabalho hello e verificar novamente para o conteúdo de mais de 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="9cac8-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="9cac8-225">400</span><span class="sxs-lookup"><span data-stu-id="9cac8-225">400</span></span>|<span data-ttu-id="9cac8-226">\(nenhum\)</span><span class="sxs-lookup"><span data-stu-id="9cac8-226">\(none\)</span></span>|<span data-ttu-id="9cac8-227">Solicitação incorreta, não execute o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="9cac8-228">Se não houver nenhum **política de repetição** definido, então a saudação padrão política é usada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="9cac8-229">Depois que o número de saudação de novas tentativas foi atingido, gatilho Olá não é mais válido.</span><span class="sxs-lookup"><span data-stu-id="9cac8-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="9cac8-230">500</span><span class="sxs-lookup"><span data-stu-id="9cac8-230">500</span></span>|<span data-ttu-id="9cac8-231">\(nenhum\)</span><span class="sxs-lookup"><span data-stu-id="9cac8-231">\(none\)</span></span>|<span data-ttu-id="9cac8-232">Erro de servidor, não são executados fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="9cac8-233">Se não houver nenhum **política de repetição** definido, então a saudação padrão política é usada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="9cac8-234">Depois que o número de saudação de novas tentativas foi atingido, gatilho Olá não é mais válido.</span><span class="sxs-lookup"><span data-stu-id="9cac8-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="9cac8-235">saídas de saudação de um gatilho HTTP se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="9cac8-236">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-236">Element name</span></span>|<span data-ttu-id="9cac8-237">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-237">Description</span></span>|<span data-ttu-id="9cac8-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="9cac8-239">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-239">headers</span></span>|<span data-ttu-id="9cac8-240">cabeçalhos de saudação de resposta de http hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-240">hello headers of hello http response.</span></span>|<span data-ttu-id="9cac8-241">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-241">Object</span></span>|  
|<span data-ttu-id="9cac8-242">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-242">body</span></span>|<span data-ttu-id="9cac8-243">corpo de saudação de resposta de http hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-243">hello body of hello http response.</span></span>|<span data-ttu-id="9cac8-244">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="9cac8-245">Gatilho de conexão da API</span><span class="sxs-lookup"><span data-stu-id="9cac8-245">API Connection trigger</span></span>  

<span data-ttu-id="9cac8-246">Olá API conexão gatilho é semelhante toohello HTTP em sua funcionalidade básica.</span><span class="sxs-lookup"><span data-stu-id="9cac8-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="9cac8-247">No entanto, os parâmetros de saudação para identificar a ação de saudação são diferentes.</span><span class="sxs-lookup"><span data-stu-id="9cac8-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="9cac8-248">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="9cac8-249">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-249">Element name</span></span>|<span data-ttu-id="9cac8-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-250">Required</span></span>|<span data-ttu-id="9cac8-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-251">Type</span></span>|<span data-ttu-id="9cac8-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-253">host</span><span class="sxs-lookup"><span data-stu-id="9cac8-253">host</span></span>|<span data-ttu-id="9cac8-254">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-254">Yes</span></span>||<span data-ttu-id="9cac8-255">Olá ApiApp hospedado gateway e id.</span><span class="sxs-lookup"><span data-stu-id="9cac8-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="9cac8-256">estático</span><span class="sxs-lookup"><span data-stu-id="9cac8-256">method</span></span>|<span data-ttu-id="9cac8-257">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-257">Yes</span></span>|<span data-ttu-id="9cac8-258">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-258">String</span></span>|<span data-ttu-id="9cac8-259">Pode ser uma saudação métodos HTTP a seguir: **obter**, **POST**, **colocar**, **excluir**, **PATCH**, ou  **CABEÇALHO**</span><span class="sxs-lookup"><span data-stu-id="9cac8-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="9cac8-260">consultas</span><span class="sxs-lookup"><span data-stu-id="9cac8-260">queries</span></span>|<span data-ttu-id="9cac8-261">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-261">No</span></span>|<span data-ttu-id="9cac8-262">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-262">Object</span></span>|<span data-ttu-id="9cac8-263">Toobe de parâmetros de consulta representa Olá adicionado toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="9cac8-264">Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="9cac8-265">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-265">headers</span></span>|<span data-ttu-id="9cac8-266">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-266">No</span></span>|<span data-ttu-id="9cac8-267">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-267">Object</span></span>|<span data-ttu-id="9cac8-268">Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="9cac8-269">Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="9cac8-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="9cac8-270">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-270">body</span></span>|<span data-ttu-id="9cac8-271">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-271">No</span></span>|<span data-ttu-id="9cac8-272">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-272">Object</span></span>|<span data-ttu-id="9cac8-273">Representa a carga de saudação que é enviada toohello de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9cac8-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="9cac8-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="9cac8-274">retryPolicy</span></span>|<span data-ttu-id="9cac8-275">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-275">No</span></span>|<span data-ttu-id="9cac8-276">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-276">Object</span></span>|<span data-ttu-id="9cac8-277">Permite a você o comportamento de repetição de saudação toocustomize erros 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="9cac8-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="9cac8-278">Autenticação</span><span class="sxs-lookup"><span data-stu-id="9cac8-278">authentication</span></span>|<span data-ttu-id="9cac8-279">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-279">No</span></span>|<span data-ttu-id="9cac8-280">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-280">Object</span></span>|<span data-ttu-id="9cac8-281">Método hello representa que Olá solicitação deve ser autenticado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="9cac8-282">Para obter detalhes sobre esse objeto, consulte [Autenticação de Saída do Agendador](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="9cac8-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="9cac8-283">Propriedades de saudação de host são:</span><span class="sxs-lookup"><span data-stu-id="9cac8-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="9cac8-284">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-284">Element name</span></span>|<span data-ttu-id="9cac8-285">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-285">Required</span></span>|<span data-ttu-id="9cac8-286">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="9cac8-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="9cac8-287">api runtimeUrl</span></span>|<span data-ttu-id="9cac8-288">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-288">Yes</span></span>|<span data-ttu-id="9cac8-289">ponto de extremidade de saudação do hello API gerenciada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="9cac8-290">nome da conexão</span><span class="sxs-lookup"><span data-stu-id="9cac8-290">connection name</span></span>||<span data-ttu-id="9cac8-291">Deve ser um parâmetro de referência tooa chamado `$connection` e é o nome da saudação de conexão de API Olá gerenciado que Olá usos de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="9cac8-292">saídas de saudação de um gatilho de conexão de API são:</span><span class="sxs-lookup"><span data-stu-id="9cac8-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="9cac8-293">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-293">Element name</span></span>|<span data-ttu-id="9cac8-294">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-294">Type</span></span>|<span data-ttu-id="9cac8-295">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="9cac8-296">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-296">headers</span></span>|<span data-ttu-id="9cac8-297">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-297">Object</span></span>|<span data-ttu-id="9cac8-298">cabeçalhos de saudação de resposta de http hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="9cac8-299">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-299">body</span></span>|<span data-ttu-id="9cac8-300">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-300">Object</span></span>|<span data-ttu-id="9cac8-301">corpo de saudação de resposta de http hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="9cac8-302">Gatilho HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="9cac8-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="9cac8-303">Aberturas de gatilho HTTPWebhook Olá um ponto de extremidade, gatilho manual de toohello semelhantes, mas Olá HTTPWebhook gatilho também chama tooa especificada URL tooregister e cancelar o registro.</span><span class="sxs-lookup"><span data-stu-id="9cac8-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="9cac8-304">Aqui está um exemplo de como um gatilho HTTPWebhook pode ser:</span><span class="sxs-lookup"><span data-stu-id="9cac8-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="9cac8-305">Muitas dessas seções são opcionais e comportamento Olá Olá Webhook depende de quais seções são fornecidas ou omitidas.</span><span class="sxs-lookup"><span data-stu-id="9cac8-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="9cac8-306">Propriedades de saudação de um Webhook são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9cac8-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="9cac8-307">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-307">Element name</span></span>|<span data-ttu-id="9cac8-308">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-308">Required</span></span>|<span data-ttu-id="9cac8-309">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="9cac8-310">assinar</span><span class="sxs-lookup"><span data-stu-id="9cac8-310">subscribe</span></span>|<span data-ttu-id="9cac8-311">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-311">No</span></span>|<span data-ttu-id="9cac8-312">saudação de solicitação que é chamada quando o gatilho de saudação é criado e executa o registro inicial Olá de saída.</span><span class="sxs-lookup"><span data-stu-id="9cac8-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="9cac8-313">cancelar assinatura</span><span class="sxs-lookup"><span data-stu-id="9cac8-313">unsubscribe</span></span>|<span data-ttu-id="9cac8-314">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-314">No</span></span>|<span data-ttu-id="9cac8-315">saudação de solicitação de saída quando Olá gatilho é excluído.</span><span class="sxs-lookup"><span data-stu-id="9cac8-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="9cac8-316">**Assinar** é Olá chamada que fez toostart tooevents de escuta de saída.</span><span class="sxs-lookup"><span data-stu-id="9cac8-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="9cac8-317">Essa chamada começa com saudação mesmo conjunto de parâmetros que Olá normais ações de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9cac8-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="9cac8-318">Esta chamada de saída é feita qualquer Olá tempo alterações de fluxo de trabalho de qualquer forma, por exemplo, sempre que as credenciais de saudação serão revertidas, ou alterar parâmetros de entrada do gatilho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="9cac8-319">toosupport chamar, há uma nova função: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="9cac8-320">Esta função retorna uma URL exclusiva para esse gatilho específico neste fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="9cac8-321">Ele representa o identificador exclusivo de saudação para pontos de extremidade de saudação que usam Olá serviço REST.</span><span class="sxs-lookup"><span data-stu-id="9cac8-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="9cac8-322">**Cancelar assinatura** é chamado quando uma operação apresenta o gatilho como inválido, incluindo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="9cac8-323">Excluir ou desabilitar o gatilho Olá</span><span class="sxs-lookup"><span data-stu-id="9cac8-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="9cac8-324">Excluir ou desabilitar o fluxo de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="9cac8-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="9cac8-325">Excluir ou desabilitar a assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="9cac8-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="9cac8-326">Olá lógica aplicativo chama automaticamente Olá cancelar a assinatura de ação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="9cac8-327">parâmetros de saudação toothis função são Olá mesmo como Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="9cac8-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="9cac8-328">Olá, saídas de gatilho de HTTPWebhook Olá são Olá conteúdo da solicitação de entrada hello:</span><span class="sxs-lookup"><span data-stu-id="9cac8-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="9cac8-329">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-329">Element name</span></span>|<span data-ttu-id="9cac8-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-330">Type</span></span>|<span data-ttu-id="9cac8-331">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="9cac8-332">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-332">headers</span></span>|<span data-ttu-id="9cac8-333">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-333">Object</span></span>|<span data-ttu-id="9cac8-334">cabeçalhos de saudação de solicitação de http hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="9cac8-335">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-335">body</span></span>|<span data-ttu-id="9cac8-336">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-336">Object</span></span>|<span data-ttu-id="9cac8-337">corpo de saudação de solicitação de http hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="9cac8-338">Limites de uma ação de webhook podem ser especificados em Olá exatamente como [limites assíncronos HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="9cac8-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="9cac8-339">Condições</span><span class="sxs-lookup"><span data-stu-id="9cac8-339">Conditions</span></span>  

<span data-ttu-id="9cac8-340">Para qualquer gatilho, você pode usar toodetermine de condições de uma ou mais se o fluxo de trabalho Olá deve ser executado ou não.</span><span class="sxs-lookup"><span data-stu-id="9cac8-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="9cac8-341">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="9cac8-342">Nesse caso, Olá gatilhos somente de relatório do fluxo de trabalho Olá `sendReports` parâmetro for definido tootrue.</span><span class="sxs-lookup"><span data-stu-id="9cac8-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="9cac8-343">Por fim, condições podem fazer referência a código de status de saudação do gatilho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="9cac8-344">Por exemplo, você poderia iniciar um fluxo de trabalho somente quando seu site retornasse um código de status 500, como a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cac8-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="9cac8-345">Quando qualquer expressão referencia o código de status de saudação do gatilho de saudação \(de qualquer forma\), Olá comportamento padrão \(gatilho apenas em 200 \(Okey\) \) é substituído.</span><span class="sxs-lookup"><span data-stu-id="9cac8-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="9cac8-346">Por exemplo, se você quiser tootrigger no código de status 200 e o código de status 201, ter tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` como sua condição.</span><span class="sxs-lookup"><span data-stu-id="9cac8-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="9cac8-347">Iniciar várias execuções para uma solicitação</span><span class="sxs-lookup"><span data-stu-id="9cac8-347">Start multiple runs for a request</span></span>

<span data-ttu-id="9cac8-348">tookick desativar várias execuções para uma única solicitação, `splitOn` é útil, por exemplo, quando você deseja toopoll um ponto de extremidade que pode ter vários novos itens entre os intervalos de sondagem.</span><span class="sxs-lookup"><span data-stu-id="9cac8-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="9cac8-349">Com `splitOn`, você especifica a propriedade hello dentro Olá carga de resposta que contém a matriz de saudação de itens, cada um dos quais você deseja toouse toostart uma execução de gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="9cac8-350">Por exemplo, imagine que você tem uma API que retorna Olá resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cac8-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="9cac8-351">Sua lógica de aplicativo só precisa conteúdo de linhas de saudação, portanto você pode construir seu gatilho semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="9cac8-352">Em seguida, na definição de fluxo de trabalho hello, `@triggerBody().name` retorna `mycoolrow` para Olá executado pela primeira vez, e `another row` para execução segundo hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="9cac8-353">Olá gatilho saídas aparência semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="9cac8-354">Portanto, se você usar `SplitOn`, não é possível obter propriedades de saudação que estão fora da matriz de hello, nesse caso, Olá `Status` campo.</span><span class="sxs-lookup"><span data-stu-id="9cac8-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="9cac8-355">Neste exemplo, usamos Olá `?` tooavoid do operador toobe capaz de uma falha se hello `Rows` propriedade não está presente.</span><span class="sxs-lookup"><span data-stu-id="9cac8-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="9cac8-356">Instância de execução única</span><span class="sxs-lookup"><span data-stu-id="9cac8-356">Single run instance</span></span>

<span data-ttu-id="9cac8-357">Você pode configurar os gatilhos que têm um incêndio de tooonly de propriedade de recorrência se tem concluído todas as execuções ativas.</span><span class="sxs-lookup"><span data-stu-id="9cac8-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="9cac8-358">Se uma recorrência agendada ocorrer enquanto houver uma execução em andamento, gatilho Olá ignora e aguarda até Olá próxima recorrência agendado intervalo toocheck novamente.</span><span class="sxs-lookup"><span data-stu-id="9cac8-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="9cac8-359">Você pode configurar essa configuração por meio de opções de operação hello:</span><span class="sxs-lookup"><span data-stu-id="9cac8-359">You can configure this setting through hello operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="9cac8-360">Tipos e entradas</span><span class="sxs-lookup"><span data-stu-id="9cac8-360">Types and inputs</span></span>  

<span data-ttu-id="9cac8-361">Há muitos tipos de ações, cada um com um comportamento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9cac8-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="9cac8-362">As ações de coleção podem conter muitas outras ações em si.</span><span class="sxs-lookup"><span data-stu-id="9cac8-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="9cac8-363">Ações padrão</span><span class="sxs-lookup"><span data-stu-id="9cac8-363">Standard actions</span></span>  

-   <span data-ttu-id="9cac8-364">**HTTP** esta ação chama um ponto de extremidade HTTP da Web.</span><span class="sxs-lookup"><span data-stu-id="9cac8-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="9cac8-365">**ApiConnection** \- essa ação se comporta como Olá ação HTTP, mas usa Olá APIs gerenciada pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9cac8-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="9cac8-366">**ApiConnectionWebhook** \- como HTTPWebhook, mas usa Olá APIs gerenciada pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9cac8-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="9cac8-367">**Resposta** \- esta ação define uma resposta para uma chamada de entrada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="9cac8-368">**Aguardar** \- esta ação simples aguarda um período fixo de tempo ou até uma hora específica.</span><span class="sxs-lookup"><span data-stu-id="9cac8-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="9cac8-369">**Fluxo de trabalho** \- esta ação representa um fluxo de trabalho aninhado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="9cac8-370">**Função** \- essa ação representa uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cac8-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="9cac8-371">Ações de coleção</span><span class="sxs-lookup"><span data-stu-id="9cac8-371">Collection actions</span></span>

-   <span data-ttu-id="9cac8-372">**Escopo** \- esta ação é um agrupamento lógico de outras ações.</span><span class="sxs-lookup"><span data-stu-id="9cac8-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="9cac8-373">**Condição** \- essa ação avalia uma expressão e executa a ramificação de resultado correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="9cac8-374">**ForEach** \- esta ação de loop itera uma matriz e executa as ações internas de cada item.</span><span class="sxs-lookup"><span data-stu-id="9cac8-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="9cac8-375">**Até** \- esta ação loop executa ações internas até que uma condição tootrue os resultados.</span><span class="sxs-lookup"><span data-stu-id="9cac8-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="9cac8-376">Cada tipo de ação tem um conjunto diferente de **entradas** que definem o comportamento de uma ação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="9cac8-377">Ação HTTP</span><span class="sxs-lookup"><span data-stu-id="9cac8-377">HTTP action</span></span>  

<span data-ttu-id="9cac8-378">Ações de HTTP chamar um ponto de extremidade especificado e verifique Olá resposta toodetermine se o fluxo de trabalho Olá deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="9cac8-379">Olá **entradas** objeto usa o conjunto de saudação de parâmetros necessários tooconstruct Olá HTTP chamada:</span><span class="sxs-lookup"><span data-stu-id="9cac8-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="9cac8-380">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-380">Element name</span></span>|<span data-ttu-id="9cac8-381">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-381">Required</span></span>|<span data-ttu-id="9cac8-382">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-382">Type</span></span>|<span data-ttu-id="9cac8-383">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-384">estático</span><span class="sxs-lookup"><span data-stu-id="9cac8-384">method</span></span>|<span data-ttu-id="9cac8-385">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-385">Yes</span></span>|<span data-ttu-id="9cac8-386">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-386">String</span></span>|<span data-ttu-id="9cac8-387">Pode ser uma saudação métodos HTTP a seguir: **obter**, **POST**, **colocar**, **excluir**, **PATCH**, ou  **CABEÇALHO**</span><span class="sxs-lookup"><span data-stu-id="9cac8-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="9cac8-388">uri</span><span class="sxs-lookup"><span data-stu-id="9cac8-388">uri</span></span>|<span data-ttu-id="9cac8-389">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-389">Yes</span></span>|<span data-ttu-id="9cac8-390">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-390">String</span></span>|<span data-ttu-id="9cac8-391">Olá ponto de extremidade http ou https que é chamado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="9cac8-392">O comprimento máximo é 2 quilobytes.</span><span class="sxs-lookup"><span data-stu-id="9cac8-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="9cac8-393">consultas</span><span class="sxs-lookup"><span data-stu-id="9cac8-393">queries</span></span>|<span data-ttu-id="9cac8-394">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-394">No</span></span>|<span data-ttu-id="9cac8-395">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-395">Object</span></span>|<span data-ttu-id="9cac8-396">Representa Olá consulta parâmetros tooadd toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="9cac8-397">Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="9cac8-398">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-398">headers</span></span>|<span data-ttu-id="9cac8-399">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-399">No</span></span>|<span data-ttu-id="9cac8-400">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-400">Object</span></span>|<span data-ttu-id="9cac8-401">Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="9cac8-402">Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="9cac8-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="9cac8-403">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-403">body</span></span>|<span data-ttu-id="9cac8-404">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-404">No</span></span>|<span data-ttu-id="9cac8-405">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-405">Object</span></span>|<span data-ttu-id="9cac8-406">Representa a carga de saudação que é enviada toohello de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9cac8-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="9cac8-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="9cac8-407">retryPolicy</span></span>|<span data-ttu-id="9cac8-408">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-408">No</span></span>|<span data-ttu-id="9cac8-409">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-409">Object</span></span>|<span data-ttu-id="9cac8-410">Permite que você personalize o comportamento de repetição de saudação erros 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="9cac8-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="9cac8-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="9cac8-411">operationsOptions</span></span>|<span data-ttu-id="9cac8-412">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-412">No</span></span>|<span data-ttu-id="9cac8-413">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-413">String</span></span>|<span data-ttu-id="9cac8-414">Define o conjunto de saudação do toooverride comportamentos especiais.</span><span class="sxs-lookup"><span data-stu-id="9cac8-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="9cac8-415">Autenticação</span><span class="sxs-lookup"><span data-stu-id="9cac8-415">authentication</span></span>|<span data-ttu-id="9cac8-416">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-416">No</span></span>|<span data-ttu-id="9cac8-417">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-417">Object</span></span>|<span data-ttu-id="9cac8-418">Método hello representa que Olá solicitação deve ser autenticado.</span><span class="sxs-lookup"><span data-stu-id="9cac8-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="9cac8-419">Para obter detalhes sobre esse objeto, consulte [Autenticação de Saída do Agendador](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="9cac8-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="9cac8-420">Além do agendador, há mais uma propriedade com suporte: `authority`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="9cac8-421">Por padrão, isto é `https://login.windows.net` quando não especificado, mas você pode usar um público diferente como`https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="9cac8-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="9cac8-422">As ações HTTP \(e as ações de Conexão da API\) têm suporte para as políticas de repetição.</span><span class="sxs-lookup"><span data-stu-id="9cac8-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="9cac8-423">Uma política de repetição se aplica a toointermittent falhas, caracterizadas como status do HTTP 408 429 e 5xx em exceções de conectividade de tooany de adição de códigos.</span><span class="sxs-lookup"><span data-stu-id="9cac8-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="9cac8-424">Essa política é descrita usando Olá *retryPolicy* objeto definido como mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="9cac8-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="9cac8-425">intervalo de repetição de saudação é especificado no formato de saudação ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="9cac8-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="9cac8-426">Esse intervalo tem um padrão e o valor mínimo de 20 segundos, enquanto o valor máximo de saudação é de uma hora.</span><span class="sxs-lookup"><span data-stu-id="9cac8-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="9cac8-427">saudação padrão e máximo de contagem de repetição é de quatro horas.</span><span class="sxs-lookup"><span data-stu-id="9cac8-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="9cac8-428">Se a definição de política de repetição de saudação não for especificada, um `fixed` estratégia é usada com valores de contagem e o intervalo de repetição padrão.</span><span class="sxs-lookup"><span data-stu-id="9cac8-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="9cac8-429">política de repetição de saudação toodisable, defina seu tipo muito`None`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="9cac8-430">Por exemplo, hello ação a seguir repete as notícias mais recentes do busca Olá duas vezes, se houver falhas intermitentes, para um total de execuções de três, com um atraso de 30 segundos entre cada tentativa de:</span><span class="sxs-lookup"><span data-stu-id="9cac8-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="9cac8-431">Padrões assíncronos</span><span class="sxs-lookup"><span data-stu-id="9cac8-431">Asynchronous patterns</span></span>

<span data-ttu-id="9cac8-432">Por padrão, todas as ações com base em HTTP oferece suporte a padrões de operação assíncrona padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="9cac8-433">Portanto, se o servidor remoto Olá indica que a solicitação Olá é aceita para processamento com um 202 \(aceito\) resposta, o mecanismo de aplicativos lógicos Olá mantém sondagem Olá URL especificado no cabeçalho de local da resposta Olá até atingir um terminal estado \(não\-resposta 202\).</span><span class="sxs-lookup"><span data-stu-id="9cac8-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="9cac8-434">comportamento assíncrono do toodisable Olá anteriormente descrito, defina um `DisableAsyncPattern` opção em entradas de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="9cac8-435">Nesse caso, a saída de hello da ação de saudação é baseada na resposta 202 inicial de saudação do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="9cac8-436">Limites Assíncronos</span><span class="sxs-lookup"><span data-stu-id="9cac8-436">Asynchronous Limits</span></span>

<span data-ttu-id="9cac8-437">Um padrão assíncrono pode ser limitado no intervalo de tempo específico de tooa sua duração.</span><span class="sxs-lookup"><span data-stu-id="9cac8-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="9cac8-438">Se o intervalo de tempo de saudação expira sem atingir um estado terminal, status de saudação de ação de saudação serão marcadas `Cancelled` com um código de `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="9cac8-439">tempo limite de limite de saudação é especificado no formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="9cac8-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="9cac8-440">Limites podem ser especificados com hello sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cac8-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="9cac8-441">Conexão da API</span><span class="sxs-lookup"><span data-stu-id="9cac8-441">API Connection</span></span>  

<span data-ttu-id="9cac8-442">A Conexão da API é uma ação que se refere a um conector gerenciado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9cac8-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="9cac8-443">Essa ação requer uma conexão válida do tooa de referência e informações sobre Olá API e os parâmetros necessários.</span><span class="sxs-lookup"><span data-stu-id="9cac8-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="9cac8-444">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="9cac8-444">Element name</span></span>|<span data-ttu-id="9cac8-445">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-445">Required</span></span>|<span data-ttu-id="9cac8-446">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-446">Type</span></span>|<span data-ttu-id="9cac8-447">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-448">host</span><span class="sxs-lookup"><span data-stu-id="9cac8-448">host</span></span>|<span data-ttu-id="9cac8-449">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-449">Yes</span></span>|<span data-ttu-id="9cac8-450">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-450">Object</span></span>|<span data-ttu-id="9cac8-451">Representa informações de conector hello como objeto de conexão de toohello de runtimeUrl e referência de saudação</span><span class="sxs-lookup"><span data-stu-id="9cac8-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="9cac8-452">estático</span><span class="sxs-lookup"><span data-stu-id="9cac8-452">method</span></span>|<span data-ttu-id="9cac8-453">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-453">Yes</span></span>|<span data-ttu-id="9cac8-454">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-454">String</span></span>|<span data-ttu-id="9cac8-455">Pode ser uma saudação métodos HTTP a seguir: **obter**, **POST**, **colocar**, **excluir**, **PATCH**, ou  **CABEÇALHO**</span><span class="sxs-lookup"><span data-stu-id="9cac8-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="9cac8-456">path</span><span class="sxs-lookup"><span data-stu-id="9cac8-456">path</span></span>|<span data-ttu-id="9cac8-457">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-457">Yes</span></span>|<span data-ttu-id="9cac8-458">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-458">String</span></span>|<span data-ttu-id="9cac8-459">caminho de saudação da operação de saudação API.</span><span class="sxs-lookup"><span data-stu-id="9cac8-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="9cac8-460">consultas</span><span class="sxs-lookup"><span data-stu-id="9cac8-460">queries</span></span>|<span data-ttu-id="9cac8-461">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-461">No</span></span>|<span data-ttu-id="9cac8-462">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-462">Object</span></span>|<span data-ttu-id="9cac8-463">Representa Olá consulta parâmetros tooadd toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="9cac8-464">Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="9cac8-465">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-465">headers</span></span>|<span data-ttu-id="9cac8-466">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-466">No</span></span>|<span data-ttu-id="9cac8-467">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-467">Object</span></span>|<span data-ttu-id="9cac8-468">Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="9cac8-469">Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="9cac8-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="9cac8-470">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-470">body</span></span>|<span data-ttu-id="9cac8-471">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-471">No</span></span>|<span data-ttu-id="9cac8-472">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-472">Object</span></span>|<span data-ttu-id="9cac8-473">Representa a carga de saudação que é enviada toohello de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9cac8-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="9cac8-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="9cac8-474">retryPolicy</span></span>|<span data-ttu-id="9cac8-475">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-475">No</span></span>|<span data-ttu-id="9cac8-476">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-476">Object</span></span>|<span data-ttu-id="9cac8-477">Permite que você personalize o comportamento de repetição de saudação erros 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="9cac8-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="9cac8-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="9cac8-478">operationsOptions</span></span>|<span data-ttu-id="9cac8-479">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-479">No</span></span>|<span data-ttu-id="9cac8-480">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-480">String</span></span>|<span data-ttu-id="9cac8-481">Define o conjunto de saudação do toooverride comportamentos especiais.</span><span class="sxs-lookup"><span data-stu-id="9cac8-481">Defines hello set of special behaviors toooverride.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="9cac8-482">Ação do webhook de Conexão da API</span><span class="sxs-lookup"><span data-stu-id="9cac8-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="9cac8-483">Limites de uma ação de webhook podem ser especificados em Olá exatamente como [limites assíncronos HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="9cac8-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="9cac8-484">Ação de resposta</span><span class="sxs-lookup"><span data-stu-id="9cac8-484">Response action</span></span>  

<span data-ttu-id="9cac8-485">Esse tipo de ação contém Olá carga de resposta inteira de uma solicitação HTTP e inclui um statusCode, corpo e cabeçalhos:</span><span class="sxs-lookup"><span data-stu-id="9cac8-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="9cac8-486">ação de resposta Olá tem restrições especiais que não se aplicam a tooother ações.</span><span class="sxs-lookup"><span data-stu-id="9cac8-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="9cac8-487">Especificamente:</span><span class="sxs-lookup"><span data-stu-id="9cac8-487">Specifically:</span></span>  
  
-   <span data-ttu-id="9cac8-488">Ações de resposta não podem ser paralelas em uma definição porque é necessária uma solicitação de entrada toohello resposta determinística.</span><span class="sxs-lookup"><span data-stu-id="9cac8-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="9cac8-489">Se uma ação de resposta é atingida depois de solicitação de entrada hello recebeu uma resposta, a ação de saudação é considerada falha \(conflito\), e como resultado, a saudação executar é `Failed`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="9cac8-490">Um fluxo de trabalho com ações de Resposta não pode ter um `splitOn` em seu gatilho porque uma chamada provoca muitas execuções.</span><span class="sxs-lookup"><span data-stu-id="9cac8-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="9cac8-491">Como resultado, isso deve ser validado quando o fluxo de saudação é PUT e causa uma solicitação incorreta.</span><span class="sxs-lookup"><span data-stu-id="9cac8-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="9cac8-492">Ação para aguardar</span><span class="sxs-lookup"><span data-stu-id="9cac8-492">Wait action</span></span>  

<span data-ttu-id="9cac8-493">Olá `wait` ação suspende a execução do fluxo de trabalho para o intervalo especificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="9cac8-494">Por exemplo, toowait 15 minutos, você pode usar este trecho de código:</span><span class="sxs-lookup"><span data-stu-id="9cac8-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="9cac8-495">Como alternativa, toowait até um momento específico, você pode usar este exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="9cac8-496">duração de espera de saudação pode ser especificada usando Olá **intervalo** objeto ou hello **até** objeto, mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="9cac8-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="9cac8-497">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-497">Name</span></span>|<span data-ttu-id="9cac8-498">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-498">Required</span></span>|<span data-ttu-id="9cac8-499">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-499">Type</span></span>|<span data-ttu-id="9cac8-500">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-501">intervalo</span><span class="sxs-lookup"><span data-stu-id="9cac8-501">interval</span></span>|<span data-ttu-id="9cac8-502">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-502">No</span></span>|<span data-ttu-id="9cac8-503">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-503">Object</span></span>|<span data-ttu-id="9cac8-504">com base na quantidade de tempo de duração de espera de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="9cac8-505">unidade do intervalo</span><span class="sxs-lookup"><span data-stu-id="9cac8-505">interval unit</span></span>|<span data-ttu-id="9cac8-506">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-506">Yes</span></span>|<span data-ttu-id="9cac8-507">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-507">String</span></span>|<span data-ttu-id="9cac8-508">Um destes intervalos: segundo, minuto, hora, dia, semana, mês, ano.</span><span class="sxs-lookup"><span data-stu-id="9cac8-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="9cac8-509">contagem do intervalo</span><span class="sxs-lookup"><span data-stu-id="9cac8-509">interval count</span></span>|<span data-ttu-id="9cac8-510">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-510">Yes</span></span>|<span data-ttu-id="9cac8-511">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-511">String</span></span>|<span data-ttu-id="9cac8-512">Duração com base em Olá fornecido unidade interna.</span><span class="sxs-lookup"><span data-stu-id="9cac8-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="9cac8-513">until</span><span class="sxs-lookup"><span data-stu-id="9cac8-513">until</span></span>|<span data-ttu-id="9cac8-514">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-514">No</span></span>|<span data-ttu-id="9cac8-515">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-515">Object</span></span>|<span data-ttu-id="9cac8-516">com base em um ponto no tempo de duração de espera de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="9cac8-517">until carimbo data/hora</span><span class="sxs-lookup"><span data-stu-id="9cac8-517">until timestamp</span></span>|<span data-ttu-id="9cac8-518">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-518">Yes</span></span>|<span data-ttu-id="9cac8-519">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-519">String</span></span>|<span data-ttu-id="9cac8-520">Cadeia de caracteres &#124; Olá pontual em UTC quando Olá espera expira.</span><span class="sxs-lookup"><span data-stu-id="9cac8-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="9cac8-521">Ação de consulta</span><span class="sxs-lookup"><span data-stu-id="9cac8-521">Query action</span></span>

<span data-ttu-id="9cac8-522">Olá `query` ação permite que uma matriz com base em uma condição de filtro.</span><span class="sxs-lookup"><span data-stu-id="9cac8-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="9cac8-523">Por exemplo, números de tooselect maiores que 2, você pode usar:</span><span class="sxs-lookup"><span data-stu-id="9cac8-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="9cac8-524">Olá saída de hello `query` ação é uma matriz com os elementos da matriz de entrada hello que satisfazem a condição de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="9cac8-525">Se nenhum valor satisfazer Olá `where` condição, hello, resultado é uma matriz vazia.</span><span class="sxs-lookup"><span data-stu-id="9cac8-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="9cac8-526">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-526">Name</span></span>|<span data-ttu-id="9cac8-527">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-527">Required</span></span>|<span data-ttu-id="9cac8-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-528">Type</span></span>|<span data-ttu-id="9cac8-529">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="9cac8-530">Da</span><span class="sxs-lookup"><span data-stu-id="9cac8-530">from</span></span>|<span data-ttu-id="9cac8-531">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-531">Yes</span></span>|<span data-ttu-id="9cac8-532">Matriz</span><span class="sxs-lookup"><span data-stu-id="9cac8-532">Array</span></span>|<span data-ttu-id="9cac8-533">matriz de origem Hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-533">hello source array.</span></span>|
|<span data-ttu-id="9cac8-534">onde</span><span class="sxs-lookup"><span data-stu-id="9cac8-534">where</span></span>|<span data-ttu-id="9cac8-535">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-535">Yes</span></span>|<span data-ttu-id="9cac8-536">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-536">String</span></span>|<span data-ttu-id="9cac8-537">Olá condição tooapply tooeach elemento de matriz de origem hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="9cac8-538">Ação selecionar</span><span class="sxs-lookup"><span data-stu-id="9cac8-538">Select action</span></span>

<span data-ttu-id="9cac8-539">Olá `select` ação permite que cada elemento de uma matriz de projeto em um novo valor.</span><span class="sxs-lookup"><span data-stu-id="9cac8-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="9cac8-540">Por exemplo, tooconvert uma matriz de números em uma matriz de objetos, você pode usar:</span><span class="sxs-lookup"><span data-stu-id="9cac8-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="9cac8-541">Olá saída de hello `select` ação é uma matriz que tem Olá cardinalidade mesmo como Olá a matriz de entrada, com cada elemento transformado conforme definida pelo Olá `select` propriedade.</span><span class="sxs-lookup"><span data-stu-id="9cac8-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="9cac8-542">Se a entrada de saudação é uma matriz vazia, a saída de hello também é uma matriz vazia.</span><span class="sxs-lookup"><span data-stu-id="9cac8-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="9cac8-543">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-543">Name</span></span>|<span data-ttu-id="9cac8-544">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-544">Required</span></span>|<span data-ttu-id="9cac8-545">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-545">Type</span></span>|<span data-ttu-id="9cac8-546">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="9cac8-547">Da</span><span class="sxs-lookup"><span data-stu-id="9cac8-547">from</span></span>|<span data-ttu-id="9cac8-548">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-548">Yes</span></span>|<span data-ttu-id="9cac8-549">Matriz</span><span class="sxs-lookup"><span data-stu-id="9cac8-549">Array</span></span>|<span data-ttu-id="9cac8-550">matriz de origem Hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-550">hello source array.</span></span>|
|<span data-ttu-id="9cac8-551">selecionar</span><span class="sxs-lookup"><span data-stu-id="9cac8-551">select</span></span>|<span data-ttu-id="9cac8-552">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-552">Yes</span></span>|<span data-ttu-id="9cac8-553">Qualquer</span><span class="sxs-lookup"><span data-stu-id="9cac8-553">Any</span></span>|<span data-ttu-id="9cac8-554">Olá projeção tooapply tooeach elemento de matriz de origem hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="9cac8-555">Ação para finalizar</span><span class="sxs-lookup"><span data-stu-id="9cac8-555">Terminate action</span></span>

<span data-ttu-id="9cac8-556">Olá terminar ação interrompe a execução de saudação fluxo de trabalho executar, anulando todas as ações em curso e ignorar as ações restantes.</span><span class="sxs-lookup"><span data-stu-id="9cac8-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="9cac8-557">Por exemplo, tooterminate uma execução com status **falha**, você pode usar o hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cac8-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="9cac8-558">Ações concluídas já não são afetadas por Olá encerrar a ação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="9cac8-559">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-559">Name</span></span>|<span data-ttu-id="9cac8-560">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-560">Required</span></span>|<span data-ttu-id="9cac8-561">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-561">Type</span></span>|<span data-ttu-id="9cac8-562">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="9cac8-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="9cac8-563">runStatus</span></span>|<span data-ttu-id="9cac8-564">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-564">Yes</span></span>|<span data-ttu-id="9cac8-565">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-565">String</span></span>|<span data-ttu-id="9cac8-566">destino de saudação status de execução.</span><span class="sxs-lookup"><span data-stu-id="9cac8-566">hello target run status.</span></span> <span data-ttu-id="9cac8-567">**Falha** ou **Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="9cac8-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="9cac8-568">runError</span><span class="sxs-lookup"><span data-stu-id="9cac8-568">runError</span></span>|<span data-ttu-id="9cac8-569">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-569">No</span></span>|<span data-ttu-id="9cac8-570">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-570">Object</span></span>|<span data-ttu-id="9cac8-571">detalhes do erro Hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-571">hello error details.</span></span> <span data-ttu-id="9cac8-572">Só há suporte para quando **runStatus** está definido muito**falha**.</span><span class="sxs-lookup"><span data-stu-id="9cac8-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="9cac8-573">código runError</span><span class="sxs-lookup"><span data-stu-id="9cac8-573">runError code</span></span>|<span data-ttu-id="9cac8-574">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-574">No</span></span>|<span data-ttu-id="9cac8-575">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-575">String</span></span>|<span data-ttu-id="9cac8-576">Olá executar código de erro.</span><span class="sxs-lookup"><span data-stu-id="9cac8-576">hello run error code.</span></span>|
|<span data-ttu-id="9cac8-577">mensagem runError</span><span class="sxs-lookup"><span data-stu-id="9cac8-577">runError message</span></span>|<span data-ttu-id="9cac8-578">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-578">No</span></span>|<span data-ttu-id="9cac8-579">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-579">String</span></span>|<span data-ttu-id="9cac8-580">Olá executar a mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="9cac8-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="9cac8-581">Ação para compor</span><span class="sxs-lookup"><span data-stu-id="9cac8-581">Compose action</span></span>

<span data-ttu-id="9cac8-582">Olá redigir ação permite que você construir um objeto arbitrário.</span><span class="sxs-lookup"><span data-stu-id="9cac8-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="9cac8-583">saída de saudação do hello compor a ação é Olá resultado da avaliação de suas entradas.</span><span class="sxs-lookup"><span data-stu-id="9cac8-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="9cac8-584">Por exemplo, você pode usar o hello compor saídas de toomerge ação várias ações:</span><span class="sxs-lookup"><span data-stu-id="9cac8-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="9cac8-585">Olá **redigir** ação pode ser usado tooconstruct qualquer saída, incluindo objetos, matrizes e qualquer outro tipo com suporte nativo aplicativos lógicos como XML e binário.</span><span class="sxs-lookup"><span data-stu-id="9cac8-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="9cac8-586">Ação tabela</span><span class="sxs-lookup"><span data-stu-id="9cac8-586">Table action</span></span>

<span data-ttu-id="9cac8-587">Olá `table` permite que você tooconvert uma matriz de itens em uma **CSV** ou **HTML** tabela.</span><span class="sxs-lookup"><span data-stu-id="9cac8-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="9cac8-588">Suponha que @triggerBody() seja</span><span class="sxs-lookup"><span data-stu-id="9cac8-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="9cac8-589">E permitir que a ação de saudação ser definida como</span><span class="sxs-lookup"><span data-stu-id="9cac8-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="9cac8-590">Olá acima produziria</span><span class="sxs-lookup"><span data-stu-id="9cac8-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="9cac8-591">ID</span><span class="sxs-lookup"><span data-stu-id="9cac8-591">id</span></span></th><th><span data-ttu-id="9cac8-592">name</span><span class="sxs-lookup"><span data-stu-id="9cac8-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="9cac8-593">0</span><span class="sxs-lookup"><span data-stu-id="9cac8-593">0</span></span></td><td><span data-ttu-id="9cac8-594">apples</span><span class="sxs-lookup"><span data-stu-id="9cac8-594">apples</span></span></td></tr><tr><td><span data-ttu-id="9cac8-595">1</span><span class="sxs-lookup"><span data-stu-id="9cac8-595">1</span></span></td><td><span data-ttu-id="9cac8-596">oranges</span><span class="sxs-lookup"><span data-stu-id="9cac8-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="9cac8-597">"</span><span class="sxs-lookup"><span data-stu-id="9cac8-597">"</span></span>

<span data-ttu-id="9cac8-598">Na tabela de saudação do toocustomize ordem, você pode especificar colunas Olá explicitamente.</span><span class="sxs-lookup"><span data-stu-id="9cac8-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="9cac8-599">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cac8-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="9cac8-600">Olá acima produziria</span><span class="sxs-lookup"><span data-stu-id="9cac8-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="9cac8-601">produce id</span><span class="sxs-lookup"><span data-stu-id="9cac8-601">produce id</span></span></th><th><span data-ttu-id="9cac8-602">description</span><span class="sxs-lookup"><span data-stu-id="9cac8-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="9cac8-603">0</span><span class="sxs-lookup"><span data-stu-id="9cac8-603">0</span></span></td><td><span data-ttu-id="9cac8-604">fresh apples</span><span class="sxs-lookup"><span data-stu-id="9cac8-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="9cac8-605">1</span><span class="sxs-lookup"><span data-stu-id="9cac8-605">1</span></span></td><td><span data-ttu-id="9cac8-606">fresh oranges</span><span class="sxs-lookup"><span data-stu-id="9cac8-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="9cac8-607">"</span><span class="sxs-lookup"><span data-stu-id="9cac8-607">"</span></span>

<span data-ttu-id="9cac8-608">Se hello `from` valor da propriedade é uma matriz vazia, a saída de hello é uma tabela vazia.</span><span class="sxs-lookup"><span data-stu-id="9cac8-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="9cac8-609">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-609">Name</span></span>|<span data-ttu-id="9cac8-610">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-610">Required</span></span>|<span data-ttu-id="9cac8-611">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-611">Type</span></span>|<span data-ttu-id="9cac8-612">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="9cac8-613">Da</span><span class="sxs-lookup"><span data-stu-id="9cac8-613">from</span></span>|<span data-ttu-id="9cac8-614">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-614">Yes</span></span>|<span data-ttu-id="9cac8-615">Matriz</span><span class="sxs-lookup"><span data-stu-id="9cac8-615">Array</span></span>|<span data-ttu-id="9cac8-616">matriz de origem Hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-616">hello source array.</span></span>|
|<span data-ttu-id="9cac8-617">formato</span><span class="sxs-lookup"><span data-stu-id="9cac8-617">format</span></span>|<span data-ttu-id="9cac8-618">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-618">Yes</span></span>|<span data-ttu-id="9cac8-619">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-619">String</span></span>|<span data-ttu-id="9cac8-620">Olá formato, ou **CSV** ou **HTML**.</span><span class="sxs-lookup"><span data-stu-id="9cac8-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="9cac8-621">colunas</span><span class="sxs-lookup"><span data-stu-id="9cac8-621">columns</span></span>|<span data-ttu-id="9cac8-622">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-622">No</span></span>|<span data-ttu-id="9cac8-623">Matriz</span><span class="sxs-lookup"><span data-stu-id="9cac8-623">Array</span></span>|<span data-ttu-id="9cac8-624">colunas de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-624">hello columns.</span></span> <span data-ttu-id="9cac8-625">Permite que a forma do toooverride saudação padrão da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="9cac8-626">cabeçalho de coluna</span><span class="sxs-lookup"><span data-stu-id="9cac8-626">column header</span></span>|<span data-ttu-id="9cac8-627">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-627">No</span></span>|<span data-ttu-id="9cac8-628">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-628">String</span></span>|<span data-ttu-id="9cac8-629">cabeçalho de saudação da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-629">hello header of hello column.</span></span>|
|<span data-ttu-id="9cac8-630">valor da coluna</span><span class="sxs-lookup"><span data-stu-id="9cac8-630">column value</span></span>|<span data-ttu-id="9cac8-631">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-631">Yes</span></span>|<span data-ttu-id="9cac8-632">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-632">String</span></span>|<span data-ttu-id="9cac8-633">valor de saudação da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="9cac8-634">Ação do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="9cac8-634">Workflow action</span></span>   

|<span data-ttu-id="9cac8-635">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-635">Name</span></span>|<span data-ttu-id="9cac8-636">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-636">Required</span></span>|<span data-ttu-id="9cac8-637">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-637">Type</span></span>|<span data-ttu-id="9cac8-638">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-639">id do host</span><span class="sxs-lookup"><span data-stu-id="9cac8-639">host id</span></span>|<span data-ttu-id="9cac8-640">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-640">Yes</span></span>|<span data-ttu-id="9cac8-641">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-641">String</span></span>|<span data-ttu-id="9cac8-642">ID do recurso de fluxo de trabalho de saudação que você deseja toocall Hello.</span><span class="sxs-lookup"><span data-stu-id="9cac8-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="9cac8-643">triggerName do host</span><span class="sxs-lookup"><span data-stu-id="9cac8-643">host triggerName</span></span>|<span data-ttu-id="9cac8-644">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-644">Yes</span></span>|<span data-ttu-id="9cac8-645">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-645">String</span></span>|<span data-ttu-id="9cac8-646">nome de saudação do gatilho de saudação que você deseja tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="9cac8-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="9cac8-647">consultas</span><span class="sxs-lookup"><span data-stu-id="9cac8-647">queries</span></span>|<span data-ttu-id="9cac8-648">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-648">No</span></span>|<span data-ttu-id="9cac8-649">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-649">Object</span></span>|<span data-ttu-id="9cac8-650">Representa Olá consulta parâmetros tooadd toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="9cac8-651">Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="9cac8-652">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-652">headers</span></span>|<span data-ttu-id="9cac8-653">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-653">No</span></span>|<span data-ttu-id="9cac8-654">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-654">Object</span></span>|<span data-ttu-id="9cac8-655">Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="9cac8-656">Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="9cac8-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="9cac8-657">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-657">body</span></span>|<span data-ttu-id="9cac8-658">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-658">No</span></span>|<span data-ttu-id="9cac8-659">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-659">Object</span></span>|<span data-ttu-id="9cac8-660">Representa a carga de saudação enviada toohello de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9cac8-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="9cac8-661">Uma verificação de acesso é feita no fluxo de trabalho Olá \(mais especificamente, o gatilho Olá\), ou seja, você precisará de acesso toohello de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="9cac8-662">Olá saídas de saudação `workflow` ação baseiam-se no que foi definido no hello `response` ação no fluxo de trabalho do hello filho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="9cac8-663">Se você não definiu nenhum `response` ação, em seguida, Olá saídas estão vazios.</span><span class="sxs-lookup"><span data-stu-id="9cac8-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="9cac8-664">Ação de função</span><span class="sxs-lookup"><span data-stu-id="9cac8-664">Function action</span></span>   

|<span data-ttu-id="9cac8-665">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-665">Name</span></span>|<span data-ttu-id="9cac8-666">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-666">Required</span></span>|<span data-ttu-id="9cac8-667">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-667">Type</span></span>|<span data-ttu-id="9cac8-668">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-669">Id de Função</span><span class="sxs-lookup"><span data-stu-id="9cac8-669">function id</span></span>|<span data-ttu-id="9cac8-670">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-670">Yes</span></span>|<span data-ttu-id="9cac8-671">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-671">String</span></span>|<span data-ttu-id="9cac8-672">ID de recurso de saudação do função hello que você deseja tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="9cac8-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="9cac8-673">estático</span><span class="sxs-lookup"><span data-stu-id="9cac8-673">method</span></span>|<span data-ttu-id="9cac8-674">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-674">No</span></span>|<span data-ttu-id="9cac8-675">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9cac8-675">String</span></span>|<span data-ttu-id="9cac8-676">Olá método HTTP usado tooinvoke função de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="9cac8-677">Por padrão, ele é `POST` quando não especificada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="9cac8-678">consultas</span><span class="sxs-lookup"><span data-stu-id="9cac8-678">queries</span></span>|<span data-ttu-id="9cac8-679">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-679">No</span></span>|<span data-ttu-id="9cac8-680">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-680">Object</span></span>|<span data-ttu-id="9cac8-681">Representa Olá consulta parâmetros tooadd toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="9cac8-682">Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9cac8-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="9cac8-683">headers</span><span class="sxs-lookup"><span data-stu-id="9cac8-683">headers</span></span>|<span data-ttu-id="9cac8-684">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-684">No</span></span>|<span data-ttu-id="9cac8-685">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-685">Object</span></span>|<span data-ttu-id="9cac8-686">Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="9cac8-687">Por exemplo, o idioma de saudação do tooset e o tipo em uma solicitação: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="9cac8-688">body</span><span class="sxs-lookup"><span data-stu-id="9cac8-688">body</span></span>|<span data-ttu-id="9cac8-689">Não</span><span class="sxs-lookup"><span data-stu-id="9cac8-689">No</span></span>|<span data-ttu-id="9cac8-690">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-690">Object</span></span>|<span data-ttu-id="9cac8-691">Representa a carga de saudação enviada toohello de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9cac8-691">Represents hello payload sent toohello endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="9cac8-692">Quando você salvar o aplicativo lógico de hello, podemos executar algumas verificações na função hello referenciada:</span><span class="sxs-lookup"><span data-stu-id="9cac8-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="9cac8-693">Você precisa de função de toohello toohave access.</span><span class="sxs-lookup"><span data-stu-id="9cac8-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="9cac8-694">Apenas o gatilho HTTP padrão ou gatilho de webhook JSON genérico é permitido.</span><span class="sxs-lookup"><span data-stu-id="9cac8-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="9cac8-695">Ele não deve ter nenhuma rota definida.</span><span class="sxs-lookup"><span data-stu-id="9cac8-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="9cac8-696">Apenas "função" e o nível de autorização "anônimo" é permitido.</span><span class="sxs-lookup"><span data-stu-id="9cac8-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="9cac8-697">URL do gatilho Olá é recuperado, armazenado em cache e usado em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="9cac8-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="9cac8-698">Portanto, se qualquer operação invalida URL Olá armazenado em cache, ação Olá falhará em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="9cac8-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="9cac8-699">toowork como alternativa, salve Olá aplicativo lógico novamente, fazer com que a lógica aplicativo tooretrieve e URL do gatilho de saudação do cache novamente.</span><span class="sxs-lookup"><span data-stu-id="9cac8-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="9cac8-700">Ações da coleção (escopos e loops)</span><span class="sxs-lookup"><span data-stu-id="9cac8-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="9cac8-701">Alguns tipos de ação podem conter ações em si.</span><span class="sxs-lookup"><span data-stu-id="9cac8-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="9cac8-702">Ações de referência em uma coleção podem ser referenciadas fora de coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="9cac8-703">Se você definiu `http` em um escopo, `@body('http')` ainda será válido em qualquer lugar em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="9cac8-704">As ações dentro de uma coleção podem `runAfter` apenas outras ações em Olá mesma coleção.</span><span class="sxs-lookup"><span data-stu-id="9cac8-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="9cac8-705">Ação de escopo</span><span class="sxs-lookup"><span data-stu-id="9cac8-705">Scope action</span></span>

<span data-ttu-id="9cac8-706">Olá `scope` ação permite que você logicamente agrupar ações em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9cac8-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="9cac8-707">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-707">Name</span></span>|<span data-ttu-id="9cac8-708">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-708">Required</span></span>|<span data-ttu-id="9cac8-709">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-709">Type</span></span>|<span data-ttu-id="9cac8-710">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-711">Ações</span><span class="sxs-lookup"><span data-stu-id="9cac8-711">actions</span></span>|<span data-ttu-id="9cac8-712">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-712">Yes</span></span>|<span data-ttu-id="9cac8-713">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-713">Object</span></span>|<span data-ttu-id="9cac8-714">Ações interna tooexecute dentro do escopo de saudação</span><span class="sxs-lookup"><span data-stu-id="9cac8-714">Inner actions tooexecute within hello scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="9cac8-715">Ação ForEach</span><span class="sxs-lookup"><span data-stu-id="9cac8-715">ForEach action</span></span>

<span data-ttu-id="9cac8-716">Esta ação de loop itera uma matriz e executa as ações internas de cada item.</span><span class="sxs-lookup"><span data-stu-id="9cac8-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="9cac8-717">Por padrão, o loop de foreach Olá é executado em paralelo (20 execuções em paralelo em um momento).</span><span class="sxs-lookup"><span data-stu-id="9cac8-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="9cac8-718">Você pode definir regras de execução usando Olá `operationOptions` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9cac8-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="9cac8-719">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-719">Name</span></span>|<span data-ttu-id="9cac8-720">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-720">Required</span></span>|<span data-ttu-id="9cac8-721">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-721">Type</span></span>|<span data-ttu-id="9cac8-722">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-723">Ações</span><span class="sxs-lookup"><span data-stu-id="9cac8-723">actions</span></span>|<span data-ttu-id="9cac8-724">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-724">Yes</span></span>|<span data-ttu-id="9cac8-725">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-725">Object</span></span>|<span data-ttu-id="9cac8-726">Ações interna tooexecute em loop Olá</span><span class="sxs-lookup"><span data-stu-id="9cac8-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="9cac8-727">foreach</span><span class="sxs-lookup"><span data-stu-id="9cac8-727">foreach</span></span>|<span data-ttu-id="9cac8-728">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-728">Yes</span></span>|<span data-ttu-id="9cac8-729">string</span><span class="sxs-lookup"><span data-stu-id="9cac8-729">string</span></span>|<span data-ttu-id="9cac8-730">Olá matriz tooiterate sobre</span><span class="sxs-lookup"><span data-stu-id="9cac8-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="9cac8-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="9cac8-731">operationOptions</span></span>|<span data-ttu-id="9cac8-732">não</span><span class="sxs-lookup"><span data-stu-id="9cac8-732">no</span></span>|<span data-ttu-id="9cac8-733">string</span><span class="sxs-lookup"><span data-stu-id="9cac8-733">string</span></span>|<span data-ttu-id="9cac8-734">Quaisquer opções de operação para o comportamento.</span><span class="sxs-lookup"><span data-stu-id="9cac8-734">Any operation options for behavior.</span></span> <span data-ttu-id="9cac8-735">Atualmente só dá suporte a `sequential` tooexecute iterações sequencialmente (o comportamento padrão é paralelo)</span><span class="sxs-lookup"><span data-stu-id="9cac8-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="9cac8-736">Ação Until</span><span class="sxs-lookup"><span data-stu-id="9cac8-736">Until action</span></span>

<span data-ttu-id="9cac8-737">Esta ação de loop executa ações internas até que uma condição tootrue os resultados.</span><span class="sxs-lookup"><span data-stu-id="9cac8-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="9cac8-738">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-738">Name</span></span>|<span data-ttu-id="9cac8-739">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-739">Required</span></span>|<span data-ttu-id="9cac8-740">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-740">Type</span></span>|<span data-ttu-id="9cac8-741">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-742">Ações</span><span class="sxs-lookup"><span data-stu-id="9cac8-742">actions</span></span>|<span data-ttu-id="9cac8-743">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-743">Yes</span></span>|<span data-ttu-id="9cac8-744">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-744">Object</span></span>|<span data-ttu-id="9cac8-745">Ações interna tooexecute em loop Olá</span><span class="sxs-lookup"><span data-stu-id="9cac8-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="9cac8-746">expressão</span><span class="sxs-lookup"><span data-stu-id="9cac8-746">expression</span></span>|<span data-ttu-id="9cac8-747">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-747">Yes</span></span>|<span data-ttu-id="9cac8-748">string</span><span class="sxs-lookup"><span data-stu-id="9cac8-748">string</span></span>|<span data-ttu-id="9cac8-749">Olá expressão tooevaluate após cada iteração</span><span class="sxs-lookup"><span data-stu-id="9cac8-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="9cac8-750">limite</span><span class="sxs-lookup"><span data-stu-id="9cac8-750">limit</span></span>|<span data-ttu-id="9cac8-751">sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-751">yes</span></span>|<span data-ttu-id="9cac8-752">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-752">Object</span></span>|<span data-ttu-id="9cac8-753">limites de saudação para loop Olá - pelo menos um limite devem ser definidos</span><span class="sxs-lookup"><span data-stu-id="9cac8-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="9cac8-754">count</span><span class="sxs-lookup"><span data-stu-id="9cac8-754">count</span></span>|<span data-ttu-id="9cac8-755">não</span><span class="sxs-lookup"><span data-stu-id="9cac8-755">no</span></span>|<span data-ttu-id="9cac8-756">int</span><span class="sxs-lookup"><span data-stu-id="9cac8-756">int</span></span>|<span data-ttu-id="9cac8-757">Olá limitar toohello o número de iterações que podem ser executadas</span><span class="sxs-lookup"><span data-stu-id="9cac8-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="9cac8-758">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="9cac8-758">timeout</span></span>|<span data-ttu-id="9cac8-759">não</span><span class="sxs-lookup"><span data-stu-id="9cac8-759">no</span></span>|<span data-ttu-id="9cac8-760">string</span><span class="sxs-lookup"><span data-stu-id="9cac8-760">string</span></span>|<span data-ttu-id="9cac8-761">Olá tempo limite de quanto tempo ele deve executar um loop.</span><span class="sxs-lookup"><span data-stu-id="9cac8-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="9cac8-762">Formato ISO 8601</span><span class="sxs-lookup"><span data-stu-id="9cac8-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="9cac8-763">Condições - Ação If</span><span class="sxs-lookup"><span data-stu-id="9cac8-763">Conditions - If Action</span></span>

<span data-ttu-id="9cac8-764">Olá `If` ação permite que você avalie uma condição e executar uma ramificação com base em se Olá avalia muito`true`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="9cac8-765">Nome</span><span class="sxs-lookup"><span data-stu-id="9cac8-765">Name</span></span>|<span data-ttu-id="9cac8-766">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9cac8-766">Required</span></span>|<span data-ttu-id="9cac8-767">Tipo</span><span class="sxs-lookup"><span data-stu-id="9cac8-767">Type</span></span>|<span data-ttu-id="9cac8-768">Descrição</span><span class="sxs-lookup"><span data-stu-id="9cac8-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="9cac8-769">Ações</span><span class="sxs-lookup"><span data-stu-id="9cac8-769">actions</span></span>|<span data-ttu-id="9cac8-770">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-770">Yes</span></span>|<span data-ttu-id="9cac8-771">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-771">Object</span></span>|<span data-ttu-id="9cac8-772">Ações interna tooexecute quando a expressão é avaliada muito`true`</span><span class="sxs-lookup"><span data-stu-id="9cac8-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="9cac8-773">expressão</span><span class="sxs-lookup"><span data-stu-id="9cac8-773">expression</span></span>|<span data-ttu-id="9cac8-774">Sim</span><span class="sxs-lookup"><span data-stu-id="9cac8-774">Yes</span></span>|<span data-ttu-id="9cac8-775">string</span><span class="sxs-lookup"><span data-stu-id="9cac8-775">string</span></span>|<span data-ttu-id="9cac8-776">Olá expressão tooevaluate</span><span class="sxs-lookup"><span data-stu-id="9cac8-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="9cac8-777">else</span><span class="sxs-lookup"><span data-stu-id="9cac8-777">else</span></span>|<span data-ttu-id="9cac8-778">não</span><span class="sxs-lookup"><span data-stu-id="9cac8-778">no</span></span>|<span data-ttu-id="9cac8-779">Objeto</span><span class="sxs-lookup"><span data-stu-id="9cac8-779">Object</span></span>|<span data-ttu-id="9cac8-780">Ações interna tooexecute quando a expressão é avaliada muito`false`</span><span class="sxs-lookup"><span data-stu-id="9cac8-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="9cac8-781">Olá tabela a seguir mostra exemplos de como as condições podem usar expressões em uma ação:</span><span class="sxs-lookup"><span data-stu-id="9cac8-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="9cac8-782">Valor JSON</span><span class="sxs-lookup"><span data-stu-id="9cac8-782">JSON value</span></span>|<span data-ttu-id="9cac8-783">Result</span><span class="sxs-lookup"><span data-stu-id="9cac8-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="9cac8-784">Qualquer valor que seria avaliado tootrue faz com que essa condição toopass.</span><span class="sxs-lookup"><span data-stu-id="9cac8-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="9cac8-785">Apenas as expressões boolianas têm suporte.</span><span class="sxs-lookup"><span data-stu-id="9cac8-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="9cac8-786">tooconvert outros tipos de tooBoolean, use funções `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="9cac8-787">Há suporte para as funções de comparação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-787">Comparison functions are supported.</span></span> <span data-ttu-id="9cac8-788">Por exemplo hello aqui, Olá ação será executada somente quando a saída de saudação do act1 é maior que o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cac8-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="9cac8-789">Funções lógicas também são suportado toocreate aninhados expressões Boolianas.</span><span class="sxs-lookup"><span data-stu-id="9cac8-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="9cac8-790">Nesse caso, a ação de saudação executa quando a saída de saudação do act1 está acima do limite de saudação ou abaixo de 100.</span><span class="sxs-lookup"><span data-stu-id="9cac8-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="9cac8-791">Você pode usar a matriz funções toocheck se uma matriz tem todos os itens.</span><span class="sxs-lookup"><span data-stu-id="9cac8-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="9cac8-792">Nesse caso, a ação de saudação executa quando Olá erros matriz está vazia.</span><span class="sxs-lookup"><span data-stu-id="9cac8-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="9cac8-793">Erro - não é uma condição válida porque @ é necessário para as condições.</span><span class="sxs-lookup"><span data-stu-id="9cac8-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="9cac8-794">Se uma condição for avaliada com êxito, a condição de saudação está marcada como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="9cac8-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="9cac8-795">Ações em qualquer Olá `actions` ou `else` objetos avaliar muito`Succeeded` quando executada e foi bem-sucedida, `Failed` quando executada e falha, ou `Skipped` quando essa ramificação não será executada.</span><span class="sxs-lookup"><span data-stu-id="9cac8-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cac8-796">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9cac8-796">Next steps</span></span>

[<span data-ttu-id="9cac8-797">API REST do Serviço de Fluxo de Trabalho</span><span class="sxs-lookup"><span data-stu-id="9cac8-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
