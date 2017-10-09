---
title: aaaScheduled eventos para VMs do Windows no Azure | Microsoft Docs
description: "Eventos agendados usando o serviço de metadados do Azure Olá para em suas máquinas virtuais do Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a>Serviço de Metadados do Azure: Eventos Agendados (versão prévia) para VMs do Windows

> [!NOTE] 
> Visualizações são feitas tooyou disponível em condição de saudação concordar toohello termos de uso. Para obter mais informações, consulte [Termos de Uso Complementares do Microsoft Azure para Visualizações do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Eventos agendados é uma saudação subserviços em hello Azure metadados de serviço. Ele responsável por identificar informações sobre eventos futuros (por exemplo, reiniciar) para que seu aplicativo possa se preparar para eles e limitar a interrupção. Estão disponíveis para todos os tipos de Máquina Virtual do Azure, incluindo PaaS e IaaS. Eventos agendados dá toominimize Olá efeito um evento de suas tarefas tooperform preventivas de tempo de máquina Virtual. 

Os eventos agendados estão disponíveis para Linux e VMs do Windows. Para saber mais sobre os Eventos Agendados no Linux, confira [Eventos agendados para VMs do Linux](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Por que Eventos Agendados?

Com os eventos agendados, você pode adotar medidas impacto de saudação do toolimit de plataforma intiated manutenção ou ações iniciadas pelo usuário em seu serviço. 

Cargas de trabalho de várias instâncias, que usam o estado da replicação técnicas toomaintain, podem ser vulnerável toooutages acontecendo em várias instâncias. Tais interrupções podem resultar em tarefas caras (por exemplo, recompilação de índices) ou até mesmo na perda de uma réplica. 

Em muitos casos, hello geral disponibilidade do serviço pode ser melhorada pela execução de uma sequência de desligamento normal como concluídas (ou cancelamento) transações em andamento, reatribuindo tarefas tooother VMs no cluster hello (failover manual) ou removendo Olá Máquina virtual de um pool de Balanceador de carga de rede. 

Há casos onde notificando um administrador sobre um evento futuro ou registro em log um evento ajudar a melhorar a facilidade de manutenção de saudação de aplicativos hospedados na nuvem hello.

Casos de uso do Azure Metadata Service superfícies agendado eventos no seguinte hello:
-   Manutenção iniciada na plataforma (por exemplo, distribuição do sistema operacional do Host)
-   Chamadas iniciadas pelo usuário (por exemplo, o usuário reinicia ou reimplanta uma VM)


## <a name="hello-basics"></a>Noções básicas de saudação  

Serviço de metadados do Azure expõe informações sobre a execução de máquinas virtuais usando um ponto de extremidade de REST podem ser acessados no hello VM. informações de saudação estão disponíveis por meio de um IP não roteável para que ele não é exposto fora Olá VM.

### <a name="scope"></a>Escopo
Eventos agendados são tooall da superfície máquinas virtuais em um serviço de nuvem ou tooall máquinas virtuais em um conjunto de disponibilidade. Como resultado, você deve verificar Olá `Resources` campo Olá evento tooidentify que máquinas virtuais serão toobe afetado. 

### <a name="discovering-hello-endpoint"></a>Descobrir ponto de extremidade Olá
No caso de Olá onde uma máquina Virtual é criada em uma rede Virtual (VNet), o serviço de metadados de hello está disponível de um IP não roteável estático, `169.254.169.254`.
Se Olá Máquina Virtual não é criado em uma rede Virtual, casos de padrão de saudação para serviços de nuvem e VMs clássicas, lógica adicional é necessário toodiscover toouse de ponto de extremidade de saudação. Consulte toothis exemplo toolearn como muito[descobrir o ponto de extremidade do hello host](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Controle de versão 
Olá serviço de metadados de instância é com controle de versão. As versões são obrigatórias e Olá a versão atual é `2017-03-01`.

> [!NOTE] 
> Versões anteriores de visualização de eventos agendados suportados {mais recente} como Olá api-version. Esse formato não é mais suportado e será substituído em Olá futuras.

### <a name="using-headers"></a>Uso de cabeçalhos
Quando você consulta Olá Metadata Service, você deve fornecer o cabeçalho Olá `Metadata: true` solicitação de saudação tooensure não foi redirecionada acidentalmente.

### <a name="enabling-scheduled-events"></a>Habilitar Eventos Agendados
Olá primeira vez que você faz uma solicitação para eventos agendados, Azure implicitamente habilita Olá recurso em sua máquina Virtual. Como resultado, você deve esperar uma resposta atrasada em sua primeira chamada do backup tootwo minutos.

### <a name="user-initiated-maintenance"></a>Manutenção iniciada pelo usuário
Manutenção de máquinas virtuais por meio de saudação portal do Azure, API, CLI, iniciada pelo usuário ou o PowerShell resulta em um evento agendado. Isso permite que você tootest lógica de preparação de manutenção de saudação em seu aplicativo e permite tooprepare seu aplicativo para manutenção iniciada pelo usuário.

Reiniciar uma máquina virtual agendará um evento com tipo `Reboot`. Reimplantar uma máquina virtual agendará um evento com tipo `Redeploy`.

> [!NOTE] 
> No momento, no máximo 10 operações de manutenção iniciadas pelo usuário podem ser agendadas simultaneamente. Esse limite será aliviado antes da disponibilidade geral de Eventos Agendados.

> [!NOTE] 
> A manutenção iniciada pelo usuário que resulta em Eventos Agendados no momento não é configurável. A capacidade de configuração está prevista para uma versão futura.

## <a name="using-hello-api"></a>Usando a API de saudação

### <a name="query-for-events"></a>Consulta de eventos
Você pode consultar eventos agendados simplesmente fazendo Olá seguinte chamada:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Uma resposta contém uma matriz de eventos agendados. Uma matriz vazia significa que não há eventos agendados no momento.
No caso de Olá onde há eventos agendados, resposta Olá contém uma matriz de eventos: 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Propriedades do evento
|Propriedade  |  Descrição |
| - | - |
| EventId | Identificador global exclusivo para esse evento. <br><br> Exemplo: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | Impacto desse evento. <br><br> Valores: <br><ul><li> `Freeze`: Olá Máquina Virtual é agendado toopause por alguns segundos. Olá CPU está suspenso, mas não há nenhum impacto na memória, arquivos abertos ou conexões de rede. <li>`Reboot`: Olá Máquina Virtual está agendada para reinicialização (a memória não persistente é perdida). <li>`Redeploy`: Olá Máquina Virtual é agendado toomove tooanother nó (efêmeros discos são perdidos). |
| ResourceType | Tipo de recurso que esse evento impacta. <br><br> Valores: <ul><li>`VirtualMachine`|
| Recursos| Lista de recursos que esse evento impacta. Isso é garantido toocontain máquinas de no máximo uma [domínio de atualização](manage-availability.md), mas não pode conter todas as máquinas no hello UD. <br><br> Exemplo: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Status do evento | Status desse evento. <br><br> Valores: <ul><li>`Scheduled`: Esse evento é agendado toostart depois de tempo de saudação especificado no hello `NotBefore` propriedade.<li>`Started`: esse evento foi iniciado.</ul> Não `Completed` ou status semelhante já é fornecido; evento Olá não será retornado quando o evento de saudação é concluído.
| NotBefore| Tempo após o qual esse evento poderá começar. <br><br> Exemplo: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Agendamento do evento
Cada evento é agendado uma quantidade mínima de tempo em Olá futuro com base no tipo de evento. Esse tempo é refletido na propriedades `NotBefore` de um evento. 

|EventType  | Aviso mínimo |
| - | - |
| Congelamento| 15 minutos |
| Reboot | 15 minutos |
| Reimplantar | 10 minutos |

### <a name="starting-an-event"></a>Como iniciar um evento 

Depois que você tem conhecimento de um evento futuro e concluiu sua lógica de desligamento normal, você pode aprovar eventos pendentes Olá fazendo uma `POST` chamar o serviço de metadados toohello com hello `EventId`. Isso indica tooAzure que ele pode diminuir notificação mínimo Olá tempo (quando for possível). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Confirmar um evento permite Olá evento tooproceed para todos os `Resources` no evento hello, não apenas Olá máquina virtual que reconhece o evento hello. Portanto, você pode escolher tooelect uma confirmação de saudação do líder toocoordinate, que pode ser tão simple quanto a primeira máquina Olá em Olá `Resources` campo.


## <a name="powershell-sample"></a>Exemplo do PowerShell 

Olá exemplos de consultas a seguir Olá metadados de serviço para eventos agendados e aprova a cada evento pendente.

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a>Exemplo de C\# 

Olá exemplo a seguir é de um cliente simple que se comunica com o serviço de metadados de saudação.

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

Eventos agendados podem ser representados usando Olá estruturas de dados a seguir:

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

Olá exemplos de consultas a seguir Olá metadados de serviço para eventos agendados e aprova a cada evento pendente.

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a>Exemplo de Python 

Olá exemplos de consultas a seguir Olá metadados de serviço para eventos agendados e aprova a cada evento pendente.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Próximas etapas 

- Leia mais sobre Olá APIs disponíveis no hello [o serviço de metadados de instância](instance-metadata-service.md).
- Saiba mais sobre a [manutenção planejada para máquinas virtuais do Windows no Azure](planned-maintenance.md).

