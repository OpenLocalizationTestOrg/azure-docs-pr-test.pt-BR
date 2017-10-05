---
title: Conceitos, termos e entidades do Agendador | Microsoft Docs
description: "Conceitos, terminologia e hierarquia de entidades do Agendador do Azure, incluindo trabalhos e coleções de trabalhos.  Fornece um exemplo completo de um trabalho agendado."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="35c53-104">Conceitos, terminologia e hierarquia de entidades do Agendador</span><span class="sxs-lookup"><span data-stu-id="35c53-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="35c53-105">Hierarquia de entidade do Agendador</span><span class="sxs-lookup"><span data-stu-id="35c53-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="35c53-106">A tabela a seguir descreve os principais recursos expostos ou usados pela API do Agendador:</span><span class="sxs-lookup"><span data-stu-id="35c53-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="35c53-107">Recurso</span><span class="sxs-lookup"><span data-stu-id="35c53-107">Resource</span></span> | <span data-ttu-id="35c53-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="35c53-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="35c53-109">**Coleção de trabalhos**</span><span class="sxs-lookup"><span data-stu-id="35c53-109">**Job collection**</span></span> |<span data-ttu-id="35c53-110">Uma coleção de trabalhos contém um grupo de trabalhos e mantém as configurações, cotas e limites que são compartilhados pelos trabalhos dentro da coleção.</span><span class="sxs-lookup"><span data-stu-id="35c53-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="35c53-111">Uma coleção de trabalhos é criada por um proprietário de assinatura e agrupa os trabalhos com base em limites de uso ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="35c53-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="35c53-112">Ele é restrito a uma região.</span><span class="sxs-lookup"><span data-stu-id="35c53-112">It’s constrained to one region.</span></span> <span data-ttu-id="35c53-113">Ele também permite a imposição de cotas para restringir o uso de todos os trabalhos na coleção.</span><span class="sxs-lookup"><span data-stu-id="35c53-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="35c53-114">As cotas incluem MaxJobs e MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="35c53-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="35c53-115">**Trabalho**</span><span class="sxs-lookup"><span data-stu-id="35c53-115">**Job**</span></span> |<span data-ttu-id="35c53-116">Um trabalho define uma única ação recorrente com estratégias simples ou complexas para execução.</span><span class="sxs-lookup"><span data-stu-id="35c53-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="35c53-117">As ações podem incluir solicitações HTTP, de fila de armazenamento, de barramento de serviço ou de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="35c53-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="35c53-118">**Histórico de trabalho**</span><span class="sxs-lookup"><span data-stu-id="35c53-118">**Job history**</span></span> |<span data-ttu-id="35c53-119">Um histórico de trabalho representa os detalhes para a execução de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="35c53-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="35c53-120">Ele contém o êxito versus a falha, bem como os detalhes da resposta.</span><span class="sxs-lookup"><span data-stu-id="35c53-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="35c53-121">Gerenciamento de entidade do Agendador</span><span class="sxs-lookup"><span data-stu-id="35c53-121">Scheduler entity management</span></span>
<span data-ttu-id="35c53-122">Em um alto nível, o Agendador e a API de gerenciamento do serviço expõem as seguintes operações nos recursos:</span><span class="sxs-lookup"><span data-stu-id="35c53-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="35c53-123">Recurso</span><span class="sxs-lookup"><span data-stu-id="35c53-123">Capability</span></span> | <span data-ttu-id="35c53-124">Descrição e endereço de URI</span><span class="sxs-lookup"><span data-stu-id="35c53-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="35c53-125">**Gerenciamento de coleção de trabalhos**</span><span class="sxs-lookup"><span data-stu-id="35c53-125">**Job collection management**</span></span> |<span data-ttu-id="35c53-126">GET, PUT e DELETE dão suporte para criar e modificar as coleções e os trabalhos nelas contidos.</span><span class="sxs-lookup"><span data-stu-id="35c53-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="35c53-127">Uma coleção de trabalhos é um contêiner para trabalhos, com o mapeamento para cotas e configurações compartilhadas.</span><span class="sxs-lookup"><span data-stu-id="35c53-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="35c53-128">Os exemplos de cotas, descritos a seguir, são o número máximo de trabalhos e o menor intervalo de recorrência.</span><span class="sxs-lookup"><span data-stu-id="35c53-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="35c53-129">PUT e DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="35c53-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="35c53-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="35c53-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="35c53-131">**Gerenciamento de trabalhos**</span><span class="sxs-lookup"><span data-stu-id="35c53-131">**Job management**</span></span> |<span data-ttu-id="35c53-132">GET, PUT, POST, PATCH e DELETE dão suporte para criar e modificar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="35c53-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="35c53-133">Todos os trabalhos devem pertencer a uma coleção de trabalhos que já existe, para que não haja criação implícita.</span><span class="sxs-lookup"><span data-stu-id="35c53-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="35c53-134">**Gerenciamento de histórico de trabalho**</span><span class="sxs-lookup"><span data-stu-id="35c53-134">**Job history management**</span></span> |<span data-ttu-id="35c53-135">Suporte de GET para busca de 60 dias do histórico de execução do trabalho, tais como, tempo decorrido do trabalho e resultados de execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="35c53-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="35c53-136">Adiciona suporte ao parâmetro de cadeia de caracteres consulta para filtrar com base no estado e status.</span><span class="sxs-lookup"><span data-stu-id="35c53-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="35c53-137">Tipos de trabalho</span><span class="sxs-lookup"><span data-stu-id="35c53-137">Job types</span></span>
<span data-ttu-id="35c53-138">Existem vários tipos de trabalhos: trabalhos HTTP (incluindo trabalhos HTTPS que oferecem suporte a SSL), trabalhos de fila de armazenamento, trabalhos de fila do barramento de serviço e trabalhos de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="35c53-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="35c53-139">Trabalhos de HTTP são ideais se você tiver um ponto de extremidade de uma carga de trabalho ou serviço existente.</span><span class="sxs-lookup"><span data-stu-id="35c53-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="35c53-140">Você pode usar os trabalhos de fila de armazenamento para postar mensagens em filas de armazenamento, portanto, esses trabalhos são ideais para cargas de trabalho que usam filas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="35c53-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="35c53-141">Da mesma forma, os trabalhos de barramento de serviço são ideais para as cargas de trabalho que usam tópicos e filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="35c53-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="35c53-142">A entidade "trabalho" em detalhes</span><span class="sxs-lookup"><span data-stu-id="35c53-142">The "job" entity in detail</span></span>
<span data-ttu-id="35c53-143">Em um nível básico, um trabalho agendado tem várias partes:</span><span class="sxs-lookup"><span data-stu-id="35c53-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="35c53-144">A ação a ser executada quando o temporizador do trabalho é disparado</span><span class="sxs-lookup"><span data-stu-id="35c53-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="35c53-145">(Opcional) O tempo para executar o trabalho</span><span class="sxs-lookup"><span data-stu-id="35c53-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="35c53-146">(Opcional) Quando e com que frequência repetir o trabalho</span><span class="sxs-lookup"><span data-stu-id="35c53-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="35c53-147">(Opcional) Uma ação a ser acionada, se a ação principal falhar</span><span class="sxs-lookup"><span data-stu-id="35c53-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="35c53-148">Internamente, um trabalho agendado também contém dados fornecidos pelo sistema, como o próximo tempo de execução agendado.</span><span class="sxs-lookup"><span data-stu-id="35c53-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="35c53-149">O código a seguir fornece um exemplo completo de um trabalho agendado.</span><span class="sxs-lookup"><span data-stu-id="35c53-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="35c53-150">Os detalhes são fornecidos nas seções seguintes.</span><span class="sxs-lookup"><span data-stu-id="35c53-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="35c53-151">Como visto no trabalho agendado no exemplo acima, uma definição de trabalho tem várias partes:</span><span class="sxs-lookup"><span data-stu-id="35c53-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="35c53-152">Hora de início ("startTime")</span><span class="sxs-lookup"><span data-stu-id="35c53-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="35c53-153">Ação ("action"), que inclui a ação de erro ("errorAction")</span><span class="sxs-lookup"><span data-stu-id="35c53-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="35c53-154">Recorrência ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="35c53-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="35c53-155">Estado ("state")</span><span class="sxs-lookup"><span data-stu-id="35c53-155">State (“state”)</span></span>  
* <span data-ttu-id="35c53-156">Status ("status")</span><span class="sxs-lookup"><span data-stu-id="35c53-156">Status (“status”)</span></span>  
* <span data-ttu-id="35c53-157">Política de novas tentativas ("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="35c53-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="35c53-158">Vamos examinar cada um em detalhes:</span><span class="sxs-lookup"><span data-stu-id="35c53-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="35c53-159">startTime</span><span class="sxs-lookup"><span data-stu-id="35c53-159">startTime</span></span>
<span data-ttu-id="35c53-160">O "startTime" é a hora de início e permite que o chamador especifique um deslocamento de fuso horário na rede no [formato ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="35c53-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="35c53-161">action e errorAction</span><span class="sxs-lookup"><span data-stu-id="35c53-161">action and errorAction</span></span>
<span data-ttu-id="35c53-162">A “ação” é a ação invocada em cada ocorrência e descreve um tipo de invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="35c53-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="35c53-163">A ação é o que será executado na agenda fornecida.</span><span class="sxs-lookup"><span data-stu-id="35c53-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="35c53-164">O agendador dá suporte a ações HTTP, de fila de armazenamento, de tópico do barramento de serviço e de fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="35c53-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="35c53-165">A ação no exemplo acima é uma ação de http.</span><span class="sxs-lookup"><span data-stu-id="35c53-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="35c53-166">Abaixo está um exemplo de uma ação de fila de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="35c53-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="35c53-167">A seguir, um exemplo de uma ação de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="35c53-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="35c53-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="35c53-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="35c53-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="35c53-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="35c53-170">A seguir, um exemplo de uma ação de fila do barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="35c53-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="35c53-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="35c53-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="35c53-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="35c53-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="35c53-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="35c53-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="35c53-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="35c53-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="35c53-175">"errorAction" é o manipulador de erro, a ação invocada quando ocorre falha na ação principal.</span><span class="sxs-lookup"><span data-stu-id="35c53-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="35c53-176">Você pode usar essa variável para chamar um ponto de extremidade de tratamento de erros ou enviar uma notificação do usuário.</span><span class="sxs-lookup"><span data-stu-id="35c53-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="35c53-177">Isso pode ser usado para atingir um ponto de extremidade secundário no caso em que o principal não está disponível (por exemplo, no caso de um desastre no site do ponto de extremidade) ou pode ser usado para notificar um ponto de extremidade de tratamento de erros.</span><span class="sxs-lookup"><span data-stu-id="35c53-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="35c53-178">Assim como a ação principal, a ação de erro pode ser simples ou composta lógica com base em outras ações.</span><span class="sxs-lookup"><span data-stu-id="35c53-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="35c53-179">Para saber como criar um token SAS, consulte [Criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="35c53-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="35c53-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="35c53-180">recurrence</span></span>
<span data-ttu-id="35c53-181">A recorrência tem várias partes:</span><span class="sxs-lookup"><span data-stu-id="35c53-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="35c53-182">Frequência: uma por minuto, hora, dia, semana, mês, ano</span><span class="sxs-lookup"><span data-stu-id="35c53-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="35c53-183">Intervalo: intervalo na frequência determinada para a recorrência</span><span class="sxs-lookup"><span data-stu-id="35c53-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="35c53-184">Agenda prescrita: especificar minutos, horas, dias da semana, meses e dias do mês da recorrência</span><span class="sxs-lookup"><span data-stu-id="35c53-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="35c53-185">Contagem: contagem de ocorrências</span><span class="sxs-lookup"><span data-stu-id="35c53-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="35c53-186">Hora de término: nenhum trabalho será executado após a hora de término especificada</span><span class="sxs-lookup"><span data-stu-id="35c53-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="35c53-187">Um trabalho é recorrente se tiver um objeto recorrente especificado em sua definição JSON.</span><span class="sxs-lookup"><span data-stu-id="35c53-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="35c53-188">Se count e endTime forem especificados, a regra de conclusão que ocorre primeiro será aplicada.</span><span class="sxs-lookup"><span data-stu-id="35c53-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="35c53-189">state</span><span class="sxs-lookup"><span data-stu-id="35c53-189">state</span></span>
<span data-ttu-id="35c53-190">O estado do trabalho é um dos quatro valores: habilitado, desabilitado, concluído ou com falha.</span><span class="sxs-lookup"><span data-stu-id="35c53-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="35c53-191">Você pode utilizar os recursos PUT ou PATCH nos trabalhos para atualizá-los para o estado habilitado ou desabilitado.</span><span class="sxs-lookup"><span data-stu-id="35c53-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="35c53-192">Se um trabalho tiver sido concluído ou estiver com falha, este é um estado final que não pode ser atualizado (embora o trabalho possa ser excluído).</span><span class="sxs-lookup"><span data-stu-id="35c53-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="35c53-193">A seguir está um exemplo da propriedade state:</span><span class="sxs-lookup"><span data-stu-id="35c53-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="35c53-194">Trabalhos concluídos e com falha são excluídos após 60 dias.</span><span class="sxs-lookup"><span data-stu-id="35c53-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="35c53-195">status</span><span class="sxs-lookup"><span data-stu-id="35c53-195">status</span></span>
<span data-ttu-id="35c53-196">Após o início de um trabalho do Agendador,  informações sobre o status atual do trabalho serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="35c53-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="35c53-197">Esse objeto não é configurável pelo usuário – ele é definido pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="35c53-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="35c53-198">No entanto, ele está incluído no objeto de trabalho (em vez de um recurso vinculado separado) para que qualquer um possa obter facilmente o status de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="35c53-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="35c53-199">O status do trabalho inclui o tempo de execução anterior (se houver), a hora da próxima execução agendada (para trabalhos em andamento) e a contagem de execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="35c53-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="35c53-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="35c53-200">retryPolicy</span></span>
<span data-ttu-id="35c53-201">Se um trabalho do Agendador falhar, é possível especificar uma política de repetição para determinar se e como a ação é repetida.</span><span class="sxs-lookup"><span data-stu-id="35c53-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="35c53-202">Isso é determinado pelo objeto **retryType** – será definido como **nenhum** se não houver nenhuma política de repetição, conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="35c53-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="35c53-203">Defina-o como **fixo** se houver uma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="35c53-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="35c53-204">Para definir uma política de nova tentativa, configurações adicionais de dois valores podem ser especificadas: um intervalo de nova tentativa (**retryInterval**) e o número de tentativas (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="35c53-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="35c53-205">Intervalo de nova tentativa, especificado com o objeto **retryInterval** , que é o intervalo entre as tentativas.</span><span class="sxs-lookup"><span data-stu-id="35c53-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="35c53-206">O valor padrão é de 30 segundos, seu valor configurável mínimo é de 15 segundos e o valor máximo é de 18 meses.</span><span class="sxs-lookup"><span data-stu-id="35c53-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="35c53-207">Os trabalhos em coleções de trabalhos gratuitas têm um valor mínimo configurável de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="35c53-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="35c53-208">Ele é definido no formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="35c53-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="35c53-209">Da mesma forma, o valor do número de tentativas é especificado com o objeto **retryCount** ; esse é o número de vezes que uma nova tentativa será feita.</span><span class="sxs-lookup"><span data-stu-id="35c53-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="35c53-210">O valor padrão é 4 e o valor máximo é 20\.</span><span class="sxs-lookup"><span data-stu-id="35c53-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="35c53-211">Ambos **retryInterval** e **retryCount** são opcionais.</span><span class="sxs-lookup"><span data-stu-id="35c53-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="35c53-212">Eles receberão seus valores padrão se **retryType** for definido como **fixo** e nenhum valor for especificado explicitamente.</span><span class="sxs-lookup"><span data-stu-id="35c53-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="35c53-213">Consulte também</span><span class="sxs-lookup"><span data-stu-id="35c53-213">See also</span></span>
 [<span data-ttu-id="35c53-214">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="35c53-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="35c53-215">Introdução à utilização do Agendador no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="35c53-216">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="35c53-217">Como criar agendas complexas e recorrência avançada com o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="35c53-218">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="35c53-219">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="35c53-220">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="35c53-221">Limites, padrões e códigos de erro do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="35c53-222">Autenticação de saída do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="35c53-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

