---
title: "dados de diagnóstico do Azure no afunilamento do hello usando Hubs de eventos de aaaStreaming | Microsoft Docs"
description: "Configurando diagnóstico do Azure com Hubs de eventos final tooend, incluindo diretrizes para cenários comuns."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Fluxo de dados de diagnóstico do Azure no afunilamento hello usando Hubs de eventos
Diagnóstico do Azure fornece maneiras flexíveis toocollect métricas e registra em log da nuvem de máquinas virtuais de serviços (VMs) e transferir resultados tooAzure armazenamento. Iniciando no período de tempo de março de 2016 (SDK 2.9) hello, você pode enviar diagnóstico toocustom fontes de dados e transferir dados de afunilamento em segundos usando [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/).

Entre os tipos de dados com suporte estão:

* Eventos de ETW (Rastreamento de Eventos para Windows)
* Contadores de desempenho
* Logs de eventos do Windows
* Logs de aplicativo
* Logs de infraestrutura do Diagnóstico do Azure

Este artigo mostra como o diagnóstico do Azure tooconfigure com Hubs de eventos de encerrar tooend. Também são fornecidas diretrizes para Olá cenários comuns a seguir:

* Como toocustomize Olá registra em log e métricas que sejam enviadas tooEvent Hubs
* Como as configurações de toochange em cada ambiente
* Como os Hubs de eventos tooview fluxo de dados
* Como tootroubleshoot Olá conexão  

## <a name="prerequisites"></a>Pré-requisitos
Há suporte para dados de receieving de Hubs de eventos do diagnóstico do Azure em serviços de nuvem, máquinas virtuais, conjuntos de escala de máquinas virtuais e Service Fabric partir hello Azure SDK 2.9 e Olá correspondente ferramentas do Azure para Visual Studio.

* Extensão 1.6 do Diagnóstico do Azure (o[SDK do Azure para .NET 2.9 ou posterior](https://azure.microsoft.com/downloads/) resolve isso por padrão)
* [Visual Studio 2013 ou posterior.](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* As configurações existentes do diagnóstico do Azure em um aplicativo usando um *.wadcfgx* de arquivo e um dos métodos a seguir de saudação:
  * Visual Studio: [Configurando o Diagnóstico para os Serviços de Nuvem e máquinas virtuais do Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell: [Habilitar o Diagnóstico nos Serviços de Nuvem do Azure usando o PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)
* Namespace de Hubs de evento provisionado por artigo hello, [Introdução aos Hubs de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>Conecte-se o coletor de Hubs de tooEvent de diagnóstico do Azure
Por padrão, o diagnóstico do Azure sempre envia logs e métricas tooan conta de armazenamento do Azure. Um aplicativo também pode enviar dados tooEvent Hubs adicionando um novo **coletores** seção em Olá **PublicConfig** / **WadCfg** elemento de saudação *.wadcfgx* arquivo. No Visual Studio, Olá *.wadcfgx* arquivo é armazenado no Olá que caminho a seguir: **projeto de serviço de nuvem** > **funções** > **( RoleName)** > **wadcfgx** arquivo.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

Neste exemplo, hub de eventos Olá URL é definida toohello totalmente qualificado de namespace de hub de eventos Olá: namespace de Hubs de eventos + "/" + nome de hub de eventos.  

hub de eventos Olá URL é exibido no hello [portal do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) no painel de Hubs de eventos de saudação.  

Olá **coletor** nome pode ser definido a cadeia de caracteres válida tooany como hello mesmo valor é usado consistentemente em todo o arquivo de configuração de saudação.

> [!NOTE]
> Pode haver outros coletores configurados nesta seção, como o *applicationInsights* . O diagnóstico do Azure permite que um ou mais coletores toobe definido se cada coletor também for declarado em Olá **PrivateConfig** seção.  
>
>

Olá coletor de Hubs de eventos também deve ser declarado e definido em Olá **PrivateConfig** seção Olá *.wadcfgx* arquivo de configuração.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

Olá `SharedAccessKeyName` valor deve corresponder a uma chave de assinatura de acesso compartilhado (SAS) e a política que foi definida no hello **Hubs de eventos** namespace. Procurar toohello painel de Hubs de eventos no hello [portal do Azure](https://manage.windowsazure.com), clique em Olá **configurar** guia e configurar uma regra nomeada (por exemplo, "SendRule") que tem *enviar* permissões. Olá **StorageAccount** também é declarado em **PrivateConfig**. Não é necessário toochange valores aqui se estão funcionando. Neste exemplo, podemos deixe Olá valores vazios, que é um sinal de que um ativo de downstream definirá valores hello. Por exemplo, Olá *ServiceConfiguration* arquivo de configuração de ambiente define nomes de ambiente apropriado hello e chaves.  

> [!WARNING]
> chave de SAS de Hubs de evento de saudação é armazenada em texto sem formatação no hello *.wadcfgx* arquivo. Normalmente, essa chave é verificada no controle do código toosource ou está disponível como um ativo no seu servidor de compilação, portanto, deve protegê-lo conforme apropriado. Recomendamos que você use uma chave SAS com *apenas enviar* permissões para que um usuário mal-intencionado pode gravar toohello hub de eventos, mas não escutar tooit ou gerenciá-lo.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Configurar o diagnóstico do Azure toosend logs e métricas tooEvent Hubs
Como discutido anteriormente, todos os dados de diagnóstico personalizado e padrão, ou seja, as métricas e os logs, é enviado automaticamente tooAzure armazenamento em intervalos de saudação configurado. Com Hubs de eventos e qualquer coletor adicional, você pode especificar qualquer nó raiz ou folha em Olá hierarquia toobe enviado toohello hub de eventos. Isso inclui eventos de ETW, contadores de desempenho, logs de eventos do Windows e logs de aplicativo.   

É importante tooconsider quantos pontos de dados, na verdade, devem ser transferidos tooEvent Hubs. Normalmente, os desenvolvedores transferem dados de caminhos recorrentes e de baixa latência, que devem ser consumidos e interpretados rapidamente. Os sistemas que monitoram os alertas ou as regras de dimensionamento automático são exemplos. Um desenvolvedor também pode configurar um repositório de análise alternativo ou um repositório de pesquisa – por exemplo, o Stream Analytics do Azure, o Elasticsearch, um sistema de monitoramento personalizado ou um sistema de monitoramento favorito de outros usuários.

Olá seguem alguns exemplos de configurações.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

Olá exemplo acima, coletor Olá é aplicado toohello pai **PerformanceCounters** nó na hierarquia de saudação, o que significa que todos os filhos **PerformanceCounters** tooEvent Hubs será enviado.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

No exemplo anterior de saudação, o coletor de saudação está aplicada tooonly três contadores: **solicitações em fila**, **solicitações rejeitadas**, e **% tempo do processador**.  

Olá exemplo a seguir mostra como um desenvolvedor pode limitar Olá dados enviados toobe Olá métricas críticas que são usadas para integridade do serviço.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

Neste exemplo, o coletor de hello está aplicada toologs e é filtrado rastreamento de nível de tooerror somente.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Implantar e atualizar uma configuração de aplicativo e diagnóstico dos Serviços de Nuvem
Visual Studio fornece a aplicativo do hello mais fácil caminho toodeploy hello e configuração do coletor de Hubs de eventos. arquivo de Olá tooview e editar, abrir Olá *.wadcfgx* de arquivo no Visual Studio, editá-lo e salvá-lo. caminho de saudação é **projeto de serviço de nuvem** > **funções** > **(RoleName)** > **wadcfgx**.  

Neste ponto, todos os implantação e implantação de atualização de ações no Visual Studio, o Visual Studio Team System e todos os comandos ou scripts que são baseadas no MSBuild e usam o hello **/t: publicar** destino incluem hello *.wadcfgx*  no processo de empacotamento de saudação. Além disso, as implantações e atualizações implantar Olá tooAzure de arquivo usando a extensão do agente de diagnóstico do Azure apropriada Olá em suas VMs.

Depois de implantar o aplicativo hello e configuração de diagnóstico do Azure, você verá imediatamente atividade no painel de saudação do hub de eventos de saudação. Isso indica que você está pronto toomove nos dados de caminho hot tooviewing Olá na ferramenta de cliente ou análise de ouvinte de saudação de sua escolha.  

Olá figura a seguir, painel de Hubs de eventos Olá mostra envio Íntegro de diagnóstico dados toohello evento hub iniciando em algum momento depois de 11 PM. Ou seja, quando Olá aplicativo foi implantado com atualizada *.wadcfgx* de arquivo e Olá coletor foi configurado corretamente.

![][0]  

> [!NOTE]
> Quando você fizer o arquivo de configuração de diagnóstico do Azure do atualizações toohello (.wadcfgx), é recomendável que você enviar por push Olá atualizações toohello todo o aplicativo, bem como a configuração de saudação usando a publicação do Visual Studio ou um script do Windows PowerShell.  
>
>

## <a name="view-hot-path-data"></a>Exibir dados de caminhos recorrentes
Como discutido anteriormente, há muitos casos de uso para escuta tooand processamento de dados de Hubs de eventos.

Uma abordagem simple é toocreate um hub de eventos do teste pequena console aplicativo toolisten toohello e fluxo de saída de impressão hello. Você pode colocar Olá código, que é explicado mais detalhadamente a seguir [Introdução aos Hubs de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), em um aplicativo de console.  

Observe que o aplicativo de console hello deve incluir Olá [pacote NuGet de Host de processador de evento](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Lembre-se de valores de saudação tooreplace colchetes angulares em Olá **principal** função com valores para os seus recursos.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Solucionar problemas dos coletores dos Hubs de Eventos
* hub de eventos de saudação não mostra a atividade de evento de entrada ou saída conforme esperado.

    Verifique se o seu hub de eventos foi provisionado com êxito. Todas as informações de conexão em Olá **PrivateConfig** seção *.wadcfgx* devem corresponder a valores de saudação do recurso, como visto no portal de saudação. Certifique-se de que você tenha uma SAS política definida ("SendRule" no exemplo hello) no portal de saudação e que *enviar* permissão é concedida.  
* Após uma atualização, o hub de eventos de saudação não mostra a atividade de eventos de entrada ou saída.

    Primeiro, verifique se esse hub de eventos hello e informações de configuração estão correta, conforme explicado anteriormente. Às vezes, Olá **PrivateConfig** é redefinida em uma atualização de implantação. Olá recomendado correção é toomake todas as alterações muito*.wadcfgx* em Olá projeto e, em seguida, enviar por push uma atualização completa do aplicativo. Se isso não for possível, certifique-se de atualização diagnóstico Olá envia uma completa **PrivateConfig** que inclui a chave de SAS hello.  
* Tentativa de sugestões de saudação e hub de eventos Olá ainda não está funcionando.

    Procure na tabela de armazenamento do Azure Olá que contém erros e logs de diagnóstico do Azure em si: **WADDiagnosticInfrastructureLogsTable**. Uma opção é toouse uma ferramenta como [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect conta de armazenamento toothis, exibir essa tabela e adicionar uma consulta para o carimbo de hora no hello últimas 24 horas. Você pode usar a ferramenta de saudação tooexport um arquivo. csv e abri-lo em um aplicativo como o Microsoft Excel. Excel torna fácil toosearch para cadeias de caracteres de cartão, como **EventHubs**, toosee o erro é relatado.  

## <a name="next-steps"></a>Próximas etapas
•    [Saiba mais sobre os Hubs de Eventos](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Apêndice: Concluir o exemplo de arquivo de configuração do Diagnóstico do Azure (.wadcfgx)
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

Olá complementar *ServiceConfiguration* para este exemplo semelhante ao seguinte hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

Configurações equivalentes baseada em Json para máquinas virtuais são as seguintes:
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](../event-hubs/event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
