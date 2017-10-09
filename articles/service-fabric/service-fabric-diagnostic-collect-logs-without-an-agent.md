---
title: "logs de aaaCollect diretamente de uma malha de serviço do Azure processo do serviço | Microsoft Azure"
description: "Descreve os aplicativos podem enviar logs diretamente local central tooa, como informações de aplicativo do Azure ou Elasticsearch, sem depender de agente de diagnóstico do Azure do Service Fabric."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Coletar logs diretamente de um processo do serviço Azure Service Fabric
## <a name="in-process-log-collection"></a>Coleta de logs no processo
Coletar o aplicativo registra em log usando [extensão de diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) é uma boa opção para **Azure Service Fabric** serviços se Olá conjunto de log origens e destinos é pequeno, não altere muitas vezes e há é um mapeamento direto entre as origens de saudação e seus destinos. Caso contrário, uma alternativa é toohave serviços enviar os logs diretamente local central tooa. Esse processo é conhecido como **coleta de logs no processo** e tem várias vantagens potenciais:

* *Fácil Configuração e implantação*

    * configuração de saudação da coleta de dados de diagnóstico é apenas parte da configuração do serviço de saudação. É fácil tooalways manter "sincronizado" com hello-rest do aplicativo hello.
    * A configuração por aplicativo ou por serviço é facilmente realizável.
        * Coleta de log com base em agente normalmente requer uma implantação separada e a configuração do agente de diagnóstico hello, que é uma tarefa administrativa adicional e uma fonte de erros em potencial. Geralmente, há apenas uma instância do agente de saudação permitido por máquina virtual (nó) e configuração do agente Olá é compartilhada entre todos os aplicativos e serviços em execução nesse nó. 

* *Flexibilidade*
   
    * aplicativo Hello pode enviar dados Olá sempre que ele precisa toogo, enquanto há uma biblioteca de cliente que oferece suporte ao sistema de armazenamento de dados Olá direcionado. Novos destinos podem ser adicionados conforme desejado.
    * Regras de captura complexa, filtragem e agregação de dados podem ser implementadas.
    * Coleta de log com base em agente geralmente é limitada pelo Coletores de dados de saudação que Olá agent dá suporte a. Alguns agentes são extensíveis.

* *Contexto e acessar dados de aplicativo toointernal*
   
    * subsistema de diagnóstico Olá em execução no processo de aplicativo/serviço Olá facilmente pode aumentar rastreamentos Olá com informações contextuais.
    * Com a coleção de log com base em agente dados saudação devem ser enviados tooan agent por meio de um mecanismo de comunicação entre processos, como o rastreamento de eventos do Windows. Esse mecanismo pode impor limitações adicionais.

É possível toocombine e se beneficiam de ambos os métodos de coleção. Na verdade, talvez seja melhor solução Olá para muitos aplicativos. Coleção com base em agente é uma solução natural para coletar o cluster inteiro de toohello relacionados de logs e nós de cluster individuais. É uma maneira muito mais confiável, que coleta de log em processo, problemas de inicialização do serviço de toodiagnose e falhas. Além disso, com muitos serviços em execução dentro de um cluster do Service Fabric, cada serviço fazer sua própria coleção de log em processo resulta em várias conexões de saída do cluster hello. Grande número de conexões de saída é uma sobrecarga para o subsistema de rede hello e de destino de log hello. Um agente como [ **diagnóstico do Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) pode coletar dados de vários serviços e enviar dados por meio de algumas conexões, melhorando a taxa de transferência. 

Neste artigo, mostramos como tooset um processo de-log coleção usando [ **biblioteca de código-fonte aberto EventFlow**](https://github.com/Azure/diagnostics-eventflow). Outras bibliotecas podem ser usadas para Olá mesmo propósito, mas EventFlow tem benefício de saudação de projetados especificamente para em processo log coleta e toosupport serviços do Service Fabric. Usamos [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) como destino de log hello. Outros destinos, como [ **Hubs de eventos** ](https://azure.microsoft.com/services/event-hubs/) ou [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) também têm suporte. É apenas uma questão de instalar o pacote do NuGet apropriado e configurando o destino de Olá no arquivo de configuração EventFlow Olá. Para obter mais informações sobre destinos de log diferente do Application Insights, consulte [EventFlow documentação](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>Adicionar projeto de serviço EventFlow biblioteca tooa Service Fabric
EventFlow binários estão disponíveis como um conjunto de pacotes do NuGet. tooadd EventFlow tooa projeto do serviço do Service Fabric, clique com botão direito Olá no hello Gerenciador de soluções e escolha "Pacotes de gerenciar NuGet". Alternar o guia de "Procurar" toohello e procure "`Diagnostics.EventFlow`":

![Pacotes do EventFlow NuGet no Gerenciador de pacotes do NuGet do Visual Studio da interface do usuário][1]

serviço de saudação hospedagem EventFlow deve incluir pacotes apropriados dependendo da origem de saudação e de destino para os logs de aplicativo hello. Adicione Olá pacotes a seguir: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (toocapture dados de classe de EventSource do serviço hello e de EventSources padrão como *serviços do Microsoft-ServiceFabric* e *ServiceFabric-Microsoft-atores*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (vamos toosend Olá logs tooan Azure Application Insights recurso)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (permite a inicialização do pipeline de EventFlow Olá da configuração de serviço do Service Fabric e reporta os problemas com o envio de dados de diagnóstico como relatórios de integridade da malha do serviço)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`o pacote requer tootarget de projeto de serviço de saudação do .NET Framework 4.6 ou mais recente. Verifique se que você configurou o framework de destino apropriado Olá nas propriedades do projeto antes de instalar este pacote. 

Depois que todos os hello pacotes estão instalados, Olá próxima etapa é tooconfigure e habilitar EventFlow no serviço de saudação.

## <a name="configuring-and-enabling-log-collection"></a>Configurar e habilitar a coleta de logs
Pipeline EventFlow, responsável pelo envio de logs Olá, é criado a partir de uma especificação armazenada em um arquivo de configuração. `Microsoft.Diagnostics.EventFlow.ServiceFabric`pacote instala um arquivo de configuração inicial do EventFlow em `PackageRoot\Config` pasta da solução. nome do arquivo Hello é `eventFlowConfig.json`. Esse arquivo de configuração precisa toobe modificado toocapture dados do serviço de padrão de saudação `EventSource` classe e envia dados tooApplication Insights service.

> [!NOTE]
> Vamos supor que você esteja familiarizado com **Azure Application Insights** serviço e se você tem um recurso do Application Insights que você planeje toouse toomonitor seu serviço de malha do serviço. Se você precisar de mais informações, veja [Criar um recurso do Application Insights](../application-insights/app-insights-create-new-resource.md).

Olá abrir `eventFlowConfig.json` no editor de saudação e alterar seu conteúdo, conforme mostrado abaixo. Certifique-se de nome de ServiceEventSource de saudação de tooreplace e a chave de instrumentação do Application Insights toocomments de acordo com. 

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

> [!NOTE]
> nome de saudação do ServiceEventSource do serviço é o valor de saudação do hello propriedade Name de saudação `EventSourceAttribute` aplicada toohello ServiceEventSource classe. Ele é especificado em Olá `ServiceEventSource.cs` arquivo, que faz parte do código de serviço hello. Por exemplo, em Olá seguir Olá nome do trecho de saudação ServiceEventSource é *MyCompany-Application1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Observe que o arquivo `eventFlowConfig.json` faz parte do pacote de configuração de serviço. Arquivo de toothis de alterações pode ser incluído no completo ou configuração-somente atualizações de serviço hello, assunto tooService malha atualização verificações de integridade e reversão automática se houver falha na atualização. Para saber mais, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).

Olá última etapa é o pipeline de EventFlow tooinstantiate no código de inicialização do serviço, localizado em `Program.cs` arquivo. Em Olá adições a seguir exemplo EventFlow relacionadas são marcadas com comentários começando com `****`:

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

## <a name="verification"></a>Verificação
Iniciar o serviço e observar Olá depuração janela de saída no Visual Studio. Depois de iniciado o serviço hello, você deve começar a ver evidências de que o serviço está enviando registros de "Telemetria do Application Insights". Abra um navegador da web e navegue tooyour vá Application Insights recursos. Abra a guia "Pesquisar" (na parte superior de saudação da folha de "Visão geral" hello padrão). Após um pequeno atraso você deve começar a ver os rastreamentos no portal do Application Insights hello:

![Portal do Application Insights mostrando logs de um aplicativo do Service Fabric][2]

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre o diagnóstico e monitoramento de um serviço da Malha de Serviço](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [Documentação de EventFlow](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
