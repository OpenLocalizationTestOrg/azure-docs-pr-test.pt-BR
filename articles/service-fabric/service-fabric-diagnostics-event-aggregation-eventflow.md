---
title: "Agregação de eventos do serviço de malha com EventFlow de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre a agregação e a coleta de eventos utilizando EventFlow para monitoramento e diagnóstico de clusters do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a>Agregação e coleta de eventos usando EventFlow

[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) pode encaminhar eventos de um nó tooone ou mais destinos de monitoramentos. Porque ele está incluído como um pacote do NuGet em seu projeto de serviço, configuração e código EventFlow viajam com serviço hello, eliminando o problema de configuração por nó Olá mencionado anteriormente sobre o diagnóstico do Azure. EventFlow é executado em seu processo de serviço e se conecta diretamente saídas toohello configurado. Devido à conexão direta de Olá, EventFlow funciona para o Azure, contêiner e implantações de serviço local. Tenha cuidado se você executar EventFlow em cenários de alta densidade, como em um contêiner, pois cada pipeline EventFlow faz uma conexão externa. Então, se você hospedar vários processos, obterá várias conexões de saída! Isso não é uma preocupação quanto para aplicativos do Service Fabric, porque todas as réplicas de um `ServiceType` executar no hello mesmo processo, e isso limita o número de saudação de conexões de saída. EventFlow também oferece filtragem de eventos, para que somente os eventos de saudação que correspondem ao filtro especificado Olá são enviados.

## <a name="setting-up-eventflow"></a>Configuração do EventFlow

EventFlow binários estão disponíveis como um conjunto de pacotes do NuGet. tooadd EventFlow tooa projeto do serviço do Service Fabric, clique com botão direito Olá no hello Gerenciador de soluções e escolha "Pacotes de gerenciar NuGet". Alternar o guia de "Procurar" toohello e procure "`Diagnostics.EventFlow`":

![Pacotes do EventFlow NuGet no Gerenciador de pacotes do NuGet do Visual Studio da interface do usuário](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

Você verá uma lista de vários pacotes, rotulados como "Entradas" e "Saídas". O EventFlow dá suporte a vários provedores de log e analisadores diferentes. serviço de saudação hospedagem EventFlow deve incluir pacotes apropriados dependendo da origem de saudação e de destino para os logs de aplicativo hello. Além do pacote ServiceFabric core toohello, também é necessário pelo menos uma entrada e saída configurada. Para o exemplo, você pode adicionar Olá pacotes toosent EventSource eventos tooApplication informações a seguir:

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture dados de classe de EventSource do serviço hello e de EventSources padrão como *serviços do Microsoft-ServiceFabric* e *ServiceFabric-Microsoft-atores*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(vamos toosend Olá logs tooan Azure Application Insights recurso)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(permite a inicialização do pipeline de EventFlow Olá da configuração de serviço do Service Fabric e reporta os problemas com o envio de dados de diagnóstico como relatórios de integridade da malha do serviço)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`o pacote requer tootarget de projeto de serviço de saudação do .NET Framework 4.6 ou mais recente. Verifique se que você configurou o framework de destino apropriado Olá nas propriedades do projeto antes de instalar este pacote.

Depois que todos os hello pacotes estão instalados, Olá próxima etapa é tooconfigure e habilitar EventFlow no serviço de saudação.

## <a name="configuring-and-enabling-log-collection"></a>Configurar e habilitar a coleta de logs
pipeline de EventFlow Olá responsável pelo envio de logs de saudação é criada de uma especificação armazenada em um arquivo de configuração. Olá `Microsoft.Diagnostics.EventFlow.ServiceFabric` pacote instala um arquivo de configuração inicial do EventFlow em `PackageRoot\Config` pasta de solução, chamada `eventFlowConfig.json`. Esse arquivo de configuração precisa toobe modificado toocapture dados do serviço de padrão de saudação `EventSource` classe e outras entradas tooconfigure e enviar dados toohello apropriado local.

Aqui está um exemplo *eventFlowConfig.json* com base em pacotes do NuGet Olá mencionados acima:
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

nome de saudação do ServiceEventSource do serviço é o valor de saudação do hello propriedade Name de saudação `EventSourceAttribute` aplicada toohello ServiceEventSource classe. Ele é especificado em Olá `ServiceEventSource.cs` arquivo, que faz parte do código de serviço hello. Por exemplo, em Olá seguir Olá nome do trecho de saudação ServiceEventSource é *MyCompany-Application1-Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Observe que o arquivo `eventFlowConfig.json` faz parte do pacote de configuração de serviço. Arquivo de toothis de alterações pode ser incluído no completo ou configuração-somente atualizações de serviço hello, assunto tooService malha atualização verificações de integridade e reversão automática se houver falha na atualização. Para saber mais, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).

Olá *filtros* seção de configuração de saudação permite que você toofurther personalizar informações Olá contínuo toogo por meio de saudação EventFlow pipeline toohello saídas, permitindo que você toodrop incluir determinadas informações ou alterar Olá estrutura de dados de evento de saudação. Para saber mais sobre filtragem, confira [Filtros EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).

Olá última etapa é o pipeline de EventFlow tooinstantiate no código de inicialização do serviço, localizado em `Program.cs` arquivo:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

nome Hello passado como parâmetro de saudação do hello `CreatePipeline` método hello `ServiceFabricDiagnosticsPipelineFactory` é nome de saudação do hello *entidade integridade* que representa o pipeline de coleta de log Olá EventFlow. Esse nome é usado se encontrar EventFlow e erro e reporta isso por meio de saudação subsistema de integridade da malha do serviço.

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>Usando as configurações de malha do serviço e aplicativo parâmetros tooin eventFlowConfig

EventFlow oferece suporte a configurações de malha do serviço e aplicativo incorretos tooconfigure EventFlow. Você pode consultar os parâmetros de configuração de malha tooService usando essa sintaxe especial para valores:

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`é o nome de saudação de saudação seção de configuração de malha do serviço, e `<setting-name>` é a configuração Olá fornecendo valor Olá que serão usada tooconfigure uma configuração de EventFlow. tooread mais informações sobre como toodo, ir muito[suporte para parâmetros de aplicativos e configurações do Service Fabric](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Verificação

Iniciar o serviço e observar Olá depuração janela de saída no Visual Studio. Depois de iniciado o serviço hello, você deve começar a ver evidências de que o serviço está enviando registros de saída toohello que você configurou. Navegue tooyour plataforma de análise e à visualização do evento e confirme se os logs foram iniciados tooshow up (pode levar alguns minutos).

## <a name="next-steps"></a>Próximas etapas

* [Visualização e Análise de Eventos com o Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Visualização com o OMS e Análise de Eventos](service-fabric-diagnostics-event-analysis-oms.md)
* [Documentação de EventFlow](https://github.com/Azure/diagnostics-eventflow)