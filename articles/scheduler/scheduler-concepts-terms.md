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
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>Conceitos, terminologia e hierarquia de entidades do Agendador
## <a name="scheduler-entity-hierarchy"></a>Hierarquia de entidade do Agendador
Olá tabela a seguir descreve Olá principais recursos expostos ou usados por Olá API do Agendador:

| Recurso | Descrição |
| --- | --- |
| **Coleção de trabalhos** |Uma coleção de trabalho contém um grupo de trabalho e mantém as configurações, cotas e limites que são compartilhados pelos trabalhos dentro da coleção de saudação. Uma coleção de trabalhos é criada por um proprietário de assinatura e agrupa os trabalhos com base em limites de uso ou aplicativo. Ela é restrita tooone região. Também permite imposição Olá das cotas de uso de saudação tooconstrain de todos os trabalhos na coleção. cotas de saudação incluem MaxJobs e MaxRecurrence. |
| **Trabalho** |Um trabalho define uma única ação recorrente com estratégias simples ou complexas para execução. As ações podem incluir solicitações HTTP, de fila de armazenamento, de barramento de serviço ou de tópico do barramento de serviço. |
| **Histórico de trabalho** |Um histórico de trabalho representa os detalhes para a execução de um trabalho. Ele contém o êxito versus a falha, bem como os detalhes da resposta. |

## <a name="scheduler-entity-management"></a>Gerenciamento de entidade do Agendador
Em um nível alto, Agendador hello e API de gerenciamento do serviço de saudação expõem Olá operações nos recursos de saudação a seguir:

| Recurso | Descrição e endereço de URI |
| --- | --- |
| **Gerenciamento de coleção de trabalhos** |GET, PUT e DELETE dão suporte para criar e modificar coleções e trabalhos Olá nele contidos. Uma coleção de trabalhos é um contêiner para trabalhos e mapeia tooquotas e configurações compartilhadas. Os exemplos de cotas, descritos a seguir, são o número máximo de trabalhos e o menor intervalo de recorrência. <p>PUT e DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **Gerenciamento de trabalhos** |GET, PUT, POST, PATCH e DELETE dão suporte para criar e modificar trabalhos. Todos os trabalhos devem pertencer a coleção de trabalhos de tooa que já existe, portanto não há nenhuma criação implícita. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **Gerenciamento de histórico de trabalho** |Suporte de GET para busca de 60 dias do histórico de execução do trabalho, tais como, tempo decorrido do trabalho e resultados de execução do trabalho. Adiciona suporte ao parâmetro de cadeia de caracteres consulta para filtrar com base no estado e status. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>Tipos de trabalho
Existem vários tipos de trabalhos: trabalhos HTTP (incluindo trabalhos HTTPS que oferecem suporte a SSL), trabalhos de fila de armazenamento, trabalhos de fila do barramento de serviço e trabalhos de tópico do barramento de serviço. Trabalhos de HTTP são ideais se você tiver um ponto de extremidade de uma carga de trabalho ou serviço existente. Você pode usar o armazenamento trabalhos toopost mensagens toostorage filas, portanto esses trabalhos são ideais para cargas de trabalho que usam filas de armazenamento. Da mesma forma, os trabalhos de barramento de serviço são ideais para as cargas de trabalho que usam tópicos e filas do barramento de serviço.

## <a name="hello-job-entity-in-detail"></a>entidade de "trabalho" Hello em detalhes
Em um nível básico, um trabalho agendado tem várias partes:

* Olá tooperform ação quando o trabalho do temporizador hello é acionado  
* Trabalho de saudação do toorun de tempo de saudação (opcional)  
* (Opcional) Quando e com que frequência trabalho de saudação toorepeat  
* (Opcional) Toofire uma ação se a ação primária Olá falhar  

Internamente, um trabalho agendado também contém os dados fornecidos pelo sistema, como o próximo tempo de execução agendada hello.

saudação de código a seguir fornece um exemplo completo de um trabalho agendado. Os detalhes são fornecidos nas seções seguintes.

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

Conforme visto no trabalho agendado de exemplo de hello acima, uma definição de trabalho tem várias partes:

* Hora de início ("startTime")  
* Ação ("action"), que inclui a ação de erro ("errorAction")
* Recorrência ("recurrence")  
* Estado ("state")  
* Status ("status")  
* Política de novas tentativas ("retryPolicy")  

Vamos examinar cada um em detalhes:

## <a name="starttime"></a>startTime
Olá "startTime" é hora de início de saudação e permite Olá chamador toospecify um fuso horário de deslocamento na transmissão de saudação em [formato ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).

## <a name="action-and-erroraction"></a>action e errorAction
Olá "ação" hello ação invocada em cada ocorrência e descreve um tipo de invocação de serviço. ação de saudação é o que será executado em Olá fornecido agenda. O agendador dá suporte a ações HTTP, de fila de armazenamento, de tópico do barramento de serviço e de fila do barramento de serviço.

Olá no exemplo hello acima é uma ação HTTP. Abaixo está um exemplo de uma ação de fila de armazenamento:

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

A seguir, um exemplo de uma ação de tópico do barramento de serviço.

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

A seguir, um exemplo de uma ação de fila do barramento de serviço:

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

Olá "errorAction" é o manipulador de erro hello, ação de saudação invocada quando ocorre falha na ação principal hello. Você pode usar essa variável toocall um ponto de extremidade de tratamento de erros ou enviar uma notificação do usuário. Isso pode ser usado para alcançar um ponto de extremidade secundário no caso de Olá que Olá primário não está disponível (por exemplo, no caso de saudação de um desastre no site do ponto de extremidade Olá) ou pode ser usado para notificar um ponto de extremidade de tratamento de erros. Saudação de ação primária, uma ação de erro Olá pode ser lógica simples ou composta com base em outras ações. toolearn como toocreate um token SAS, consulte muito[criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="recurrence"></a>recurrence
A recorrência tem várias partes:

* Frequência: uma por minuto, hora, dia, semana, mês, ano  
* Intervalo: Intervalo na Olá atribuído a frequência de recorrência Olá  
* Agenda prescrita: especificar minutos, horas, dias da semana, meses e dias do mês Olá recorrência  
* Contagem: contagem de ocorrências  
* Hora de término: nenhum trabalho será executado após Olá especificado a hora de término  

Um trabalho é recorrente se tiver um objeto recorrente especificado em sua definição JSON. Se a contagem e o endTime estiverem especificados, a regra de conclusão de saudação que ocorre primeiro é cumprida.

## <a name="state"></a>state
estado de saudação do trabalho de saudação é um dos quatro valores: habilitado, desabilitado, concluído ou com falha. Você pode colocar ou PATCH trabalhos isso como tooupdate-los toohello habilitado ou desabilitado de estado. Se um trabalho foi concluído ou com falha, que é um estado final não pode ser atualizado (embora o trabalho de saudação ainda pode ser excluído). Um exemplo de propriedade de estado de saudação é o seguinte:

        "state": "disabled", // enabled, disabled, completed, or faulted
Trabalhos concluídos e com falha são excluídos após 60 dias.

## <a name="status"></a>status
Após o início de um trabalho do Agendador, serão retornadas informações sobre o status atual de saudação do trabalho de saudação. Este objeto não é configurável pelo usuário hello – ele é definido pelo sistema de saudação. No entanto, ele é incluído no hello objeto de trabalho (em vez de um recurso vinculado separado) para que possa obter status de saudação de um trabalho facilmente.

Status do trabalho inclui o tempo de saudação do hello execução anterior (se houver), Olá hora da próxima execução agendada hello (para trabalhos em andamento) e contagem de execução de saudação do trabalho de saudação.

## <a name="retrypolicy"></a>retryPolicy
Se um trabalho do Agendador falhar, é possível toospecify um toodetermine de política de repetição se e como a ação de saudação é repetida. Isso é determinado pelo Olá **retryType** objeto — está definido muito**nenhum** se não houver nenhuma política de repetição, como mostrado acima. Defina-o muito**fixa** se houver uma política de repetição.

tooset uma política de repetição, duas configurações adicionais podem ser especificadas: um intervalo de repetição (**retryInterval**) e o número de tentativas de saudação (**retryCount**).

intervalo de repetição Hello, especificado com hello **retryInterval** de objeto, é o intervalo de saudação entre repetições. O valor padrão é de 30 segundos, seu valor configurável mínimo é de 15 segundos e o valor máximo é de 18 meses. Os trabalhos em coleções de trabalhos gratuitas têm um valor mínimo configurável de 1 hora.  Ele é definido no formato ISO 8601 de saudação. Da mesma forma, o valor de saudação do número de saudação de novas tentativas for especificado com hello **retryCount** objeto; é Olá número de vezes que uma nova tentativa será feita. O valor padrão é 4 e o valor máximo é 20\. Ambos **retryInterval** e **retryCount** são opcionais. Eles recebem seus valores padrão se **retryType** está definido muito**fixa** e nenhum valor for especificado explicitamente.

## <a name="see-also"></a>Consulte também
 [O que é o Agendador?](scheduler-intro.md)

 [Começar a usar o Agendador no hello portal do Azure](scheduler-get-started-portal.md)

 [Planos e Cobrança no Agendador do Azure](scheduler-plans-billing.md)

 [Como toobuild complexo agenda e recorrência avançadas com o Agendador do Azure](scheduler-advanced-complexity.md)

 [Referência da API REST do Agendador do Azure](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Agendador do Azure](scheduler-powershell-reference.md)

 [Alta disponibilidade e confiabilidade do Agendador do Azure](scheduler-high-availability-reliability.md)

 [Limites, padrões e códigos de erro do Agendador do Azure](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Agendador do Azure](scheduler-outbound-authentication.md)

