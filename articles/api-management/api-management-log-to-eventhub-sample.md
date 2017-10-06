---
title: aaaMonitor APIs com gerenciamento de API do Azure, os Hubs de eventos e Runscope | Microsoft Docs
description: "Aplicativo de exemplo demonstra a política de log para eventhub Olá por conexão gerenciamento de API do Azure, os Hubs de eventos do Azure e Runscope para HTTP, logs e monitoramento"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Monitorar suas APIs com o Gerenciamento de API do Azure, Hubs de Eventos e Runscope
Olá [serviço de gerenciamento de API](api-management-key-concepts.md) fornece muitos recursos tooenhance Olá processamento de solicitações enviadas de HTTP tooyour API HTTP. Olá no entanto, a existência de saudação solicitações e respostas são transitórias. Olá solicitação é feita e ela flui através de serviço de gerenciamento de API Olá backend do tooyour API. Sua API processa a solicitação de saudação e uma resposta flui através de consumidor toohello API. Olá serviço de gerenciamento de API mantém algumas estatísticas importantes sobre Olá APIs para exibição no painel do portal do publicador hello, mas Além disso, detalhes de saudação serão excluídos.

Usando Olá [log-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [política](api-management-howto-policies.md) em Olá serviço de gerenciamento de API pode enviar todos os detalhes do tooan de solicitação e resposta Olá [Hub de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md). Há uma variedade de motivos pelos quais você pode querer toogenerate eventos de mensagens HTTP enviadas tooyour APIs. Alguns exemplos incluem trilha de auditoria de atualizações, análise de uso, alerta de exceção e integrações de terceiros.   

Este artigo demonstra como toocapture Olá toda solicitação e resposta de mensagem HTTP, enviá-lo tooan Hub de eventos e, em seguida, esse serviço de terceiros tooa de mensagem que fornece HTTP log e monitoramento dos serviços de retransmissão.

## <a name="why-send-from-api-management-service"></a>Por que enviar do serviço Gerenciamento de API?
É possível toowrite HTTP middleware que conecte API HTTP estruturas toocapture solicitações e respostas HTTP e alimentam o registro e monitoramento de sistemas. Olá desvantagem toothis consiste Olá HTTP middleware precisa toobe integrado a API de back-end hello e deve coincidir com a plataforma de saudação do hello API. Se houver várias APIs cada um deles deve implantar Olá middleware. Normalmente, há motivos pelos quais as APIs de back-end não podem ser atualizadas.

Usando Olá toointegrate de serviço de gerenciamento de API do Azure com a infraestrutura de log fornece uma solução centralizada e independente de plataforma. Também é escalonável, em parte devido toohello [georeplicação](api-management-howto-deploy-multi-region.md) recursos de gerenciamento de API do Azure.

## <a name="why-send-tooan-azure-event-hub"></a>Por que enviar tooan Hub de eventos do Azure?
É um tooask razoável, por que criar uma política de Hubs de eventos específico tooAzure? Há muitos lugares diferentes em que eu possa querer toolog Minhas solicitações. Por que não basta enviar Olá diretamente solicitações destino final toohello?  Essa é uma opção. No entanto, ao fazer o registro em log solicitações de um serviço de gerenciamento de API, é necessário tooconsider como mensagens de log afetará o desempenho de saudação do hello API. Os aumentos graduais na carga podem ser tratados aumentando as instâncias disponíveis dos componentes do sistema ou aproveitando a replicação geográfica. No entanto, curtos picos no tráfego podem causar solicitações toobe significativamente atrasada se a infra-estrutura de toologging solicitações iniciar tooslow sob carga.

Olá Hubs de eventos do Azure é projetado tooingress grandes volumes de dados, com capacidade para lidar com um número muito maior de eventos que número de saudação do HTTP solicita a maioria dos processos APIs. Olá Hub de eventos atua como um tipo de buffer sofisticado entre sua API serviço e hello infraestrutura de gerenciamento que armazenar e processar mensagens de saudação. Isso garante que o desempenho de API não sofrerão devido a infraestrutura de log toohello.  

Quando dados saudação passou tooan Hub de eventos, ele é persistente e aguardará tooprocess de consumidores do Hub de eventos-lo. Olá Hub de eventos, não importa como ele será processado, apenas importantes sobre como verificar se a mensagem será entregue com êxito.     

Hubs de eventos tem grupos de consumidores de toomultiple Olá capacidade toostream eventos. Isso permite que toobe eventos processado por sistemas completamente diferentes. Isso permite que o suporte a vários cenários de integração sem colocar os atrasos de adição Olá de processamento de solicitação de API Olá no serviço de gerenciamento de API hello como apenas um evento precisa toobe gerado na.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Mensagens de aplicativo/http de toosend uma política
Um Hub de Eventos aceita dados de evento como uma cadeia de caracteres simples. conteúdo de saudação dessa cadeia de caracteres são completamente o tooyou. toopackage capaz de toobe até uma solicitação HTTP e enviá-la tooEvent Hubs precisamos tooformat cadeia de caracteres de saudação com informações de solicitação ou resposta hello. Em situações como essa, se houver um formato existente que pode ser reutilizado, em seguida, pode não temos toowrite nosso própria análise de código. Inicialmente, considerado usando Olá [HAR](http://www.softwareishard.com/blog/har-12-spec/) para enviar solicitações e respostas HTTP. No entanto, esse formato é otimizado para armazenar uma sequência de solicitações HTTP em um formato baseado em JSON. Continha um número de elementos obrigatórios que mais complexidade desnecessária para cenário de saudação de passar a mensagem de saudação HTTP conexão hello.  

Uma opção alternativa foi Olá toouse `application/http` tipo de mídia, conforme descrito na especificação de saudação HTTP [7230 RFC](http://tools.ietf.org/html/rfc7230). Esse tipo de mídia usa Olá exatamente o mesmo formato que é usado tooactually enviar mensagens de HTTP conexão hello, mas a mensagem de saudação do inteiro pode ser colocada no corpo de saudação da outra solicitação HTTP. Em nosso caso vamos apenas corpo de saudação toouse como tooEvent de toosend nossa mensagem Hubs. Convenientemente, há um analisador que existe em [cliente do Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotecas que podem analisar esse formato e convertê-la em Olá nativo `HttpRequestMessage` e `HttpResponseMessage` objetos.

toocreate capaz de toobe essa mensagem precisamos tootake aproveitar com base em c# [expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx) no gerenciamento de API do Azure. Aqui está a política Olá que envia um tooAzure de mensagem de solicitação HTTP Hubs de eventos.

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a>Declaração de política
Existem alguns itens específicos sobre essa expressão de política que vale a pena mencionar. política de log para eventhub Olá tem um atributo chamado id de agente que se refere a toohello nome do agente de log que foi criado no hello serviço de gerenciamento de API. Olá detalhes de como toosetup um agente de Hub de eventos no serviço de gerenciamento de API Olá pode ser encontrado no documento hello [como toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure](api-management-howto-log-event-hubs.md). atributo segundo Olá é um parâmetro opcional que instrui o qual mensagem de saudação do toostore de partição em Hubs de eventos. Hubs de eventos usam partições tooenable scalabilty e exigem um mínimo de dois. Olá ordenados de entrega de mensagens é garantida apenas dentro de uma partição. Se não podemos instruir o Hub de eventos na mensagem de saudação de tooplace qual partição, ele usará um algoritmo de round-robin toodistribute Olá de carga. No entanto, que podem causar alguns dos nossos toobe de mensagens processada fora de ordem.  

### <a name="partitions"></a>Partições
tooensure nossas mensagens são entregues tooconsumers em ordem e aproveitar o recurso de distribuição de carga de saudação de partições, escolhi partição tooone de mensagens de solicitação do toosend HTTP e HTTP resposta mensagens tooa segunda partição. Isso garantirá uma distribuição de carga uniforme e que todas as solicitações e respostas sejam consumidas na ordem. É possível que um toobe resposta consumido antes de solicitação correspondente hello, mas já que não é um problema porque temos um mecanismo diferente para correlacionar solicitações tooresponses e sabemos que solicitações vêm sempre antes de respostas.

### <a name="http-payloads"></a>Cargas HTTP
Depois de criar hello `requestLine` verificamos toosee se o corpo da solicitação Olá deve ser truncado. corpo da solicitação de saudação é truncado tooonly 1024. Isso pode ser aumentado, porém mensagens individuais do Hub de eventos são too256KB limitado, portanto, é provável que algumas mensagens HTTP agências será não caber em uma única mensagem. Ao fazer o registro em log e análise de uma quantidade significativa de informações podem ser derivadas de apenas a linha de solicitação HTTP hello e cabeçalhos. Além disso, muitas solicitações de API retornam somente os corpos de pequenos e perda de saudação do valor de informações truncando corpos grandes é mínima em redução de toohello de comparação de transferência, processamento e armazenamento custos tookeep todo o conteúdo do corpo. Uma observação final sobre processamento Olá corpo é que precisamos toopass `true` toohello como<string>método () porque ler o conteúdo do corpo hello, mas foi também deseja Olá API back-end toobe tooread capaz de saudação corpo. Ao passar true toothis método fazemos o hello corpo toobe em buffer para que ele possa ser lido pela segunda vez. Isso é importante toobe atento se você tiver uma API que não o upload de arquivos muito grandes ou usa a sondagem longa. Nesses casos, seria melhor tooavoid ler o corpo da saudação em todos os.   

### <a name="http-headers"></a>Cabeçalhos HTTP
Cabeçalhos HTTP podem ser simplesmente transferidos por em formato de mensagem de saudação em um formato de par chave/valor simples. Escolhemos toostrip determinados segurança confidenciais campos, tooavoid desnecessariamente vazamento de informações de credencial. É improvável que as chaves da API e outras credenciais sejam usadas para fins de análise. Se desejamos toodo análise no usuário hello e produto em particular Olá eles estão usando, foi possível obter que Olá `context` do objeto e adicionar mensagem toohello.     

### <a name="message-metadata"></a>Metadados da mensagem
Ao criar o hub de eventos do hello mensagem completa toosend toohello, a primeira linha de saudação não é parte da saudação `application/http` mensagem. Olá primeira linha é metadados adicionais que consiste em se a mensagem de saudação é uma mensagem de solicitação ou resposta e uma id de mensagem que é usado toocorrelate solicita tooresponses. id de mensagem de saudação é criada usando outra política que tem esta aparência:

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Poderíamos criar mensagem de solicitação hello, armazenada que em uma variável até Olá resposta foi retornada e simplesmente enviada Olá solicitação e resposta como uma única mensagem. No entanto, envio de resposta e solicitação Olá independentemente e usando um toocorrelate de id de mensagem Olá dois, obtemos um pouco mais flexibilidade no tamanho da mensagem de saudação, Olá capacidade tootake aproveitar várias partições mantendo hello e ordem de mensagem solicitação será exibida em nosso painel log antecipadamente. Também pode haver alguns cenários em que uma resposta válida nunca é enviada para o hub de eventos toohello, possivelmente devido a erro de solicitação fatal tooa no serviço de gerenciamento de API hello, mas ainda teremos um registro de solicitação de saudação.

mensagem de HTTP de resposta Olá política toosend Olá parece muito semelhante solicitação de toohello e portanto Olá concluir configuração da política tem esta aparência:

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

Olá `set-variable` política cria um valor que é acessível por ambos os Olá `log-to-eventhub` política no hello `<inbound>` seção e hello `<outbound>` seção.  

## <a name="receiving-events-from-event-hubs"></a>Recebendo eventos dos Hubs de Eventos
Eventos do Hub de eventos do Azure são recebidos usando Olá [protocolo AMQP](http://www.amqp.org/). equipe do barramento de serviço do Microsoft Hello fez cliente Olá toomake disponíveis de bibliotecas consumindo eventos mais fácil. Há duas abordagens diferentes de suporte, um está sendo um *consumidor direto* e Olá outros usando Olá `EventProcessorHost` classe. Exemplos dessas duas abordagens podem ser encontrados no hello [guia de programação de Hubs de evento](../event-hubs/event-hubs-programming-guide.md). é a versão curta Olá das diferenças hello, `Direct Consumer` lhe dá controle total e hello `EventProcessorHost` realiza-parte do trabalho Olá para você mas faz algumas suposições sobre como você processará os eventos.  

### <a name="eventprocessorhost"></a>EventProcessorHost
Neste exemplo, usaremos Olá `EventProcessorHost` para manter a simplicidade, porém ele pode não Olá melhor opção para esse cenário específico. `EventProcessorHost`Olá difícil trabalho de certificar-se de que você não tem tooworry sobre threading problemas dentro de uma classe de processador de determinado evento. No entanto, em nosso cenário, estamos simplesmente converter o formato de tooanother de mensagem de saudação e passá-lo ao longo do serviço de tooanother usando um método assíncrono. Não há necessidade de atualizar o estado compartilhado e, portanto, nenhum risco de ter problemas de threading. Na maioria dos cenários, `EventProcessorHost` provavelmente é Olá melhor opção e é certamente opção mais fácil de saudação.     

### <a name="ieventprocessor"></a>IEventProcessor
conceito de saudação central ao usar `EventProcessorHost` é toocreate um uma implementação de saudação `IEventProcessor` interface que contém o método hello `ProcessEventAsync`. essência Olá desse método é mostrada aqui:

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

Uma lista de objetos EventData são passados para o método hello e estamos iterar pela lista. bytes de saudação de cada método são analisadas em um objeto Mensagemhttp e esse objeto é passado a instância de tooan do IHttpMessageProcessor.

### <a name="httpmessage"></a>HttpMessage
Olá `HttpMessage` instância contém três partes de dados:

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

Olá `HttpMessage` instância contém um `MessageId` GUID que nos permite solicitação de saudação HTTP tooconnect toohello resposta HTTP correspondente e um valor booleano de valor que identifica se o objeto Olá contém uma instância de uma HttpRequestMessage e HttpResponseMessage. Usando Olá criado nas classes HTTP de `System.Net.Http`, foi tootake capaz de aproveitar Olá `application/http` análise de código que está incluído no `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Olá `HttpMessage` instância é então encaminhada tooimplementation de `IHttpMessageProcessor` que é uma interface que criei recebimento de saudação toodecouple e interpretação de evento de saudação do Hub de eventos do Azure e hello real de processamento dele.

## <a name="forwarding-hello-http-message"></a>Encaminhamento de mensagens HTTP de saudação
Para este exemplo, decidi seria interessante toopush Olá solicitação HTTP sobre muito[Runscope](http://www.runscope.com). O Runscope é um serviço baseado em nuvem especializado em depuração, registro em log e monitoramento de HTTP. Eles têm uma camada gratuita, portanto, é fácil tootry e nos permite solicitações HTTP toosee Olá no fluxo em tempo real por meio de nosso serviço de gerenciamento de API.

Olá `IHttpMessageProcessor` implementação parecida com esta,

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

Foi tootake capaz de aproveitar um [biblioteca de cliente existente para Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) que torna mais fácil toopush `HttpRequestMessage` e `HttpResponseMessage` instâncias backup em seus serviços. Em ordem tooaccess Olá API Runscope você precisará de uma conta e uma chave de API. Instruções sobre como obter uma chave de API pode ser encontrado no hello [criando aplicativos tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.

## <a name="complete-sample"></a>Exemplo completo
Olá [código-fonte](https://github.com/darrelmiller/ApimEventProcessor) e testes de exemplo hello no GitHub. Você precisará de um [serviço de gerenciamento de API](api-management-get-started.md), [um Hub de eventos conectado](api-management-howto-log-event-hubs.md)e um [conta de armazenamento](../storage/common/storage-create-storage-account.md) exemplo hello de toorun por conta própria.   

exemplo Hello é apenas um aplicativo de Console simples que escuta para eventos do Hub de eventos, converte-os em uma `HttpRequestMessage` e `HttpResponseMessage` objetos e, em seguida, encaminha-os em toohello Runscope API.

Olá imagem animada a seguir, você pode ver uma solicitação seja feita tooan API no hello Portal do desenvolvedor, Olá Console aplicativo mostrando Olá recebimento de mensagem, processada e encaminhados e hello, em seguida, a solicitação e resposta aparecendo no hello tráfego Runscope Inspetor de propriedades.

![Demonstração de solicitação que está sendo encaminhada tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Resumo
Serviço de gerenciamento de API do Azure fornece um local ideal toocapture Olá HTTP o tráfego entre períodos tooand de suas APIs. Os Hubs de Eventos do Azure são uma solução escalonável de baixo custo para capturar esse tráfego e mantê-lo em sistemas de processamento secundários para registro em log, monitoramento e outras análise sofisticadas. Conectando too3rd sistemas como Runscope é um simples como algumas dezenas linhas de código de monitoramento de tráfego de terceiros.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Hubs de Eventos do Azure
  * [Introdução aos Hubs de Eventos do Azure](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Receber mensagens com EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guia de programação dos Hubs de Eventos](../event-hubs/event-hubs-programming-guide.md)
* Saiba mais sobre a integração do Gerenciamento de API e Hubs de eventos
  * [Como toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure](api-management-howto-log-event-hubs.md)
  * [Referência de entidade do agente](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [referência de política de log ao hub de eventos](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
