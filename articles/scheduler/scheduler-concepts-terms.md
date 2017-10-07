---
title: aaaScheduler entidades, termos e conceitos | Microsoft Docs
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
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="1993a-104">Conceitos, terminologia e hierarquia de entidades do Agendador</span><span class="sxs-lookup"><span data-stu-id="1993a-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="1993a-105">Hierarquia de entidade do Agendador</span><span class="sxs-lookup"><span data-stu-id="1993a-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="1993a-106">Olá tabela a seguir descreve Olá principais recursos expostos ou usados por Olá API do Agendador:</span><span class="sxs-lookup"><span data-stu-id="1993a-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="1993a-107">Recurso</span><span class="sxs-lookup"><span data-stu-id="1993a-107">Resource</span></span> | <span data-ttu-id="1993a-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="1993a-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1993a-109">**Coleção de trabalhos**</span><span class="sxs-lookup"><span data-stu-id="1993a-109">**Job collection**</span></span> |<span data-ttu-id="1993a-110">Uma coleção de trabalho contém um grupo de trabalho e mantém as configurações, cotas e limites que são compartilhados pelos trabalhos dentro da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="1993a-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="1993a-111">Uma coleção de trabalhos é criada por um proprietário de assinatura e agrupa os trabalhos com base em limites de uso ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1993a-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="1993a-112">Ela é restrita tooone região.</span><span class="sxs-lookup"><span data-stu-id="1993a-112">It’s constrained tooone region.</span></span> <span data-ttu-id="1993a-113">Também permite imposição Olá das cotas de uso de saudação tooconstrain de todos os trabalhos na coleção.</span><span class="sxs-lookup"><span data-stu-id="1993a-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="1993a-114">cotas de saudação incluem MaxJobs e MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="1993a-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="1993a-115">**Trabalho**</span><span class="sxs-lookup"><span data-stu-id="1993a-115">**Job**</span></span> |<span data-ttu-id="1993a-116">Um trabalho define uma única ação recorrente com estratégias simples ou complexas para execução.</span><span class="sxs-lookup"><span data-stu-id="1993a-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="1993a-117">As ações podem incluir solicitações HTTP, de fila de armazenamento, de barramento de serviço ou de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1993a-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="1993a-118">**Histórico de trabalho**</span><span class="sxs-lookup"><span data-stu-id="1993a-118">**Job history**</span></span> |<span data-ttu-id="1993a-119">Um histórico de trabalho representa os detalhes para a execução de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="1993a-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="1993a-120">Ele contém o êxito versus a falha, bem como os detalhes da resposta.</span><span class="sxs-lookup"><span data-stu-id="1993a-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="1993a-121">Gerenciamento de entidade do Agendador</span><span class="sxs-lookup"><span data-stu-id="1993a-121">Scheduler entity management</span></span>
<span data-ttu-id="1993a-122">Em um nível alto, Agendador hello e API de gerenciamento do serviço de saudação expõem Olá operações nos recursos de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="1993a-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="1993a-123">Recurso</span><span class="sxs-lookup"><span data-stu-id="1993a-123">Capability</span></span> | <span data-ttu-id="1993a-124">Descrição e endereço de URI</span><span class="sxs-lookup"><span data-stu-id="1993a-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="1993a-125">**Gerenciamento de coleção de trabalhos**</span><span class="sxs-lookup"><span data-stu-id="1993a-125">**Job collection management**</span></span> |<span data-ttu-id="1993a-126">GET, PUT e DELETE dão suporte para criar e modificar coleções e trabalhos Olá nele contidos.</span><span class="sxs-lookup"><span data-stu-id="1993a-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="1993a-127">Uma coleção de trabalhos é um contêiner para trabalhos e mapeia tooquotas e configurações compartilhadas.</span><span class="sxs-lookup"><span data-stu-id="1993a-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="1993a-128">Os exemplos de cotas, descritos a seguir, são o número máximo de trabalhos e o menor intervalo de recorrência.</span><span class="sxs-lookup"><span data-stu-id="1993a-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="1993a-129">PUT e DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="1993a-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="1993a-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="1993a-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="1993a-131">**Gerenciamento de trabalhos**</span><span class="sxs-lookup"><span data-stu-id="1993a-131">**Job management**</span></span> |<span data-ttu-id="1993a-132">GET, PUT, POST, PATCH e DELETE dão suporte para criar e modificar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="1993a-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="1993a-133">Todos os trabalhos devem pertencer a coleção de trabalhos de tooa que já existe, portanto não há nenhuma criação implícita.</span><span class="sxs-lookup"><span data-stu-id="1993a-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="1993a-134">**Gerenciamento de histórico de trabalho**</span><span class="sxs-lookup"><span data-stu-id="1993a-134">**Job history management**</span></span> |<span data-ttu-id="1993a-135">Suporte de GET para busca de 60 dias do histórico de execução do trabalho, tais como, tempo decorrido do trabalho e resultados de execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="1993a-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="1993a-136">Adiciona suporte ao parâmetro de cadeia de caracteres consulta para filtrar com base no estado e status.</span><span class="sxs-lookup"><span data-stu-id="1993a-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="1993a-137">Tipos de trabalho</span><span class="sxs-lookup"><span data-stu-id="1993a-137">Job types</span></span>
<span data-ttu-id="1993a-138">Existem vários tipos de trabalhos: trabalhos HTTP (incluindo trabalhos HTTPS que oferecem suporte a SSL), trabalhos de fila de armazenamento, trabalhos de fila do barramento de serviço e trabalhos de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1993a-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="1993a-139">Trabalhos de HTTP são ideais se você tiver um ponto de extremidade de uma carga de trabalho ou serviço existente.</span><span class="sxs-lookup"><span data-stu-id="1993a-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="1993a-140">Você pode usar o armazenamento trabalhos toopost mensagens toostorage filas, portanto esses trabalhos são ideais para cargas de trabalho que usam filas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1993a-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="1993a-141">Da mesma forma, os trabalhos de barramento de serviço são ideais para as cargas de trabalho que usam tópicos e filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1993a-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="1993a-142">entidade de "trabalho" Hello em detalhes</span><span class="sxs-lookup"><span data-stu-id="1993a-142">hello "job" entity in detail</span></span>
<span data-ttu-id="1993a-143">Em um nível básico, um trabalho agendado tem várias partes:</span><span class="sxs-lookup"><span data-stu-id="1993a-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="1993a-144">Olá tooperform ação quando o trabalho do temporizador hello é acionado</span><span class="sxs-lookup"><span data-stu-id="1993a-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="1993a-145">Trabalho de saudação do toorun de tempo de saudação (opcional)</span><span class="sxs-lookup"><span data-stu-id="1993a-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="1993a-146">(Opcional) Quando e com que frequência trabalho de saudação toorepeat</span><span class="sxs-lookup"><span data-stu-id="1993a-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="1993a-147">(Opcional) Toofire uma ação se a ação primária Olá falhar</span><span class="sxs-lookup"><span data-stu-id="1993a-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="1993a-148">Internamente, um trabalho agendado também contém os dados fornecidos pelo sistema, como o próximo tempo de execução agendada hello.</span><span class="sxs-lookup"><span data-stu-id="1993a-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="1993a-149">saudação de código a seguir fornece um exemplo completo de um trabalho agendado.</span><span class="sxs-lookup"><span data-stu-id="1993a-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="1993a-150">Os detalhes são fornecidos nas seções seguintes.</span><span class="sxs-lookup"><span data-stu-id="1993a-150">Details are provided in subsequent sections.</span></span>

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
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
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

<span data-ttu-id="1993a-151">Conforme visto no trabalho agendado de exemplo de hello acima, uma definição de trabalho tem várias partes:</span><span class="sxs-lookup"><span data-stu-id="1993a-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="1993a-152">Hora de início ("startTime")</span><span class="sxs-lookup"><span data-stu-id="1993a-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="1993a-153">Ação ("action"), que inclui a ação de erro ("errorAction")</span><span class="sxs-lookup"><span data-stu-id="1993a-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="1993a-154">Recorrência ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="1993a-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="1993a-155">Estado ("state")</span><span class="sxs-lookup"><span data-stu-id="1993a-155">State (“state”)</span></span>  
* <span data-ttu-id="1993a-156">Status ("status")</span><span class="sxs-lookup"><span data-stu-id="1993a-156">Status (“status”)</span></span>  
* <span data-ttu-id="1993a-157">Política de novas tentativas ("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="1993a-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="1993a-158">Vamos examinar cada um em detalhes:</span><span class="sxs-lookup"><span data-stu-id="1993a-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="1993a-159">startTime</span><span class="sxs-lookup"><span data-stu-id="1993a-159">startTime</span></span>
<span data-ttu-id="1993a-160">Olá "startTime" é hora de início de saudação e permite Olá chamador toospecify um fuso horário de deslocamento na transmissão de saudação em [formato ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="1993a-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="1993a-161">action e errorAction</span><span class="sxs-lookup"><span data-stu-id="1993a-161">action and errorAction</span></span>
<span data-ttu-id="1993a-162">Olá "ação" hello ação invocada em cada ocorrência e descreve um tipo de invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="1993a-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="1993a-163">ação de saudação é o que será executado em Olá fornecido agenda.</span><span class="sxs-lookup"><span data-stu-id="1993a-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="1993a-164">O agendador dá suporte a ações HTTP, de fila de armazenamento, de tópico do barramento de serviço e de fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1993a-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="1993a-165">Olá no exemplo hello acima é uma ação HTTP.</span><span class="sxs-lookup"><span data-stu-id="1993a-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="1993a-166">Abaixo está um exemplo de uma ação de fila de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="1993a-166">Below is an example of a storage queue action:</span></span>

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

<span data-ttu-id="1993a-167">A seguir, um exemplo de uma ação de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1993a-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="1993a-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="1993a-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="1993a-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="1993a-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="1993a-170">A seguir, um exemplo de uma ação de fila do barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="1993a-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="1993a-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="1993a-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="1993a-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="1993a-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="1993a-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="1993a-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="1993a-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="1993a-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="1993a-175">Olá "errorAction" é o manipulador de erro hello, ação de saudação invocada quando ocorre falha na ação principal hello.</span><span class="sxs-lookup"><span data-stu-id="1993a-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="1993a-176">Você pode usar essa variável toocall um ponto de extremidade de tratamento de erros ou enviar uma notificação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1993a-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="1993a-177">Isso pode ser usado para alcançar um ponto de extremidade secundário no caso de Olá que Olá primário não está disponível (por exemplo, no caso de saudação de um desastre no site do ponto de extremidade Olá) ou pode ser usado para notificar um ponto de extremidade de tratamento de erros.</span><span class="sxs-lookup"><span data-stu-id="1993a-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="1993a-178">Saudação de ação primária, uma ação de erro Olá pode ser lógica simples ou composta com base em outras ações.</span><span class="sxs-lookup"><span data-stu-id="1993a-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="1993a-179">toolearn como toocreate um token SAS, consulte muito[criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="1993a-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="1993a-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="1993a-180">recurrence</span></span>
<span data-ttu-id="1993a-181">A recorrência tem várias partes:</span><span class="sxs-lookup"><span data-stu-id="1993a-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="1993a-182">Frequência: uma por minuto, hora, dia, semana, mês, ano</span><span class="sxs-lookup"><span data-stu-id="1993a-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="1993a-183">Intervalo: Intervalo na Olá atribuído a frequência de recorrência Olá</span><span class="sxs-lookup"><span data-stu-id="1993a-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="1993a-184">Agenda prescrita: especificar minutos, horas, dias da semana, meses e dias do mês Olá recorrência</span><span class="sxs-lookup"><span data-stu-id="1993a-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="1993a-185">Contagem: contagem de ocorrências</span><span class="sxs-lookup"><span data-stu-id="1993a-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="1993a-186">Hora de término: nenhum trabalho será executado após Olá especificado a hora de término</span><span class="sxs-lookup"><span data-stu-id="1993a-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="1993a-187">Um trabalho é recorrente se tiver um objeto recorrente especificado em sua definição JSON.</span><span class="sxs-lookup"><span data-stu-id="1993a-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="1993a-188">Se a contagem e o endTime estiverem especificados, a regra de conclusão de saudação que ocorre primeiro é cumprida.</span><span class="sxs-lookup"><span data-stu-id="1993a-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="1993a-189">state</span><span class="sxs-lookup"><span data-stu-id="1993a-189">state</span></span>
<span data-ttu-id="1993a-190">estado de saudação do trabalho de saudação é um dos quatro valores: habilitado, desabilitado, concluído ou com falha.</span><span class="sxs-lookup"><span data-stu-id="1993a-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="1993a-191">Você pode colocar ou PATCH trabalhos isso como tooupdate-los toohello habilitado ou desabilitado de estado.</span><span class="sxs-lookup"><span data-stu-id="1993a-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="1993a-192">Se um trabalho foi concluído ou com falha, que é um estado final não pode ser atualizado (embora o trabalho de saudação ainda pode ser excluído).</span><span class="sxs-lookup"><span data-stu-id="1993a-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="1993a-193">Um exemplo de propriedade de estado de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1993a-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="1993a-194">Trabalhos concluídos e com falha são excluídos após 60 dias.</span><span class="sxs-lookup"><span data-stu-id="1993a-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="1993a-195">status</span><span class="sxs-lookup"><span data-stu-id="1993a-195">status</span></span>
<span data-ttu-id="1993a-196">Após o início de um trabalho do Agendador, serão retornadas informações sobre o status atual de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1993a-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="1993a-197">Este objeto não é configurável pelo usuário hello – ele é definido pelo sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="1993a-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="1993a-198">No entanto, ele é incluído no hello objeto de trabalho (em vez de um recurso vinculado separado) para que possa obter status de saudação de um trabalho facilmente.</span><span class="sxs-lookup"><span data-stu-id="1993a-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="1993a-199">Status do trabalho inclui o tempo de saudação do hello execução anterior (se houver), Olá hora da próxima execução agendada hello (para trabalhos em andamento) e contagem de execução de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1993a-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="1993a-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="1993a-200">retryPolicy</span></span>
<span data-ttu-id="1993a-201">Se um trabalho do Agendador falhar, é possível toospecify um toodetermine de política de repetição se e como a ação de saudação é repetida.</span><span class="sxs-lookup"><span data-stu-id="1993a-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="1993a-202">Isso é determinado pelo Olá **retryType** objeto — está definido muito**nenhum** se não houver nenhuma política de repetição, como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="1993a-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="1993a-203">Defina-o muito**fixa** se houver uma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="1993a-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="1993a-204">tooset uma política de repetição, duas configurações adicionais podem ser especificadas: um intervalo de repetição (**retryInterval**) e o número de tentativas de saudação (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="1993a-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="1993a-205">intervalo de repetição Hello, especificado com hello **retryInterval** de objeto, é o intervalo de saudação entre repetições.</span><span class="sxs-lookup"><span data-stu-id="1993a-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="1993a-206">O valor padrão é de 30 segundos, seu valor configurável mínimo é de 15 segundos e o valor máximo é de 18 meses.</span><span class="sxs-lookup"><span data-stu-id="1993a-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="1993a-207">Os trabalhos em coleções de trabalhos gratuitas têm um valor mínimo configurável de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="1993a-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="1993a-208">Ele é definido no formato ISO 8601 de saudação.</span><span class="sxs-lookup"><span data-stu-id="1993a-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="1993a-209">Da mesma forma, o valor de saudação do número de saudação de novas tentativas for especificado com hello **retryCount** objeto; é Olá número de vezes que uma nova tentativa será feita.</span><span class="sxs-lookup"><span data-stu-id="1993a-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="1993a-210">O valor padrão é 4 e o valor máximo é 20\.</span><span class="sxs-lookup"><span data-stu-id="1993a-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="1993a-211">Ambos **retryInterval** e **retryCount** são opcionais.</span><span class="sxs-lookup"><span data-stu-id="1993a-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="1993a-212">Eles recebem seus valores padrão se **retryType** está definido muito**fixa** e nenhum valor for especificado explicitamente.</span><span class="sxs-lookup"><span data-stu-id="1993a-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="1993a-213">Consulte também</span><span class="sxs-lookup"><span data-stu-id="1993a-213">See also</span></span>
 [<span data-ttu-id="1993a-214">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="1993a-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="1993a-215">Começar a usar o Agendador no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="1993a-216">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="1993a-217">Como toobuild complexo agenda e recorrência avançadas com o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="1993a-218">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="1993a-219">Referência de cmdlets do PowerShell do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="1993a-220">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="1993a-221">Limites, padrões e códigos de erro do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="1993a-222">Autenticação de saída do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="1993a-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

