---
title: "aaaOptimizing de código do Azure no Visual Studio | Microsoft Docs"
description: "Saiba mais sobre como as ferramentas de otimização de código do Azure no Visual Studio ajudam a tornar o código mais robusto e com melhor desempenho."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Otimizando o código do Azure
Quando você estiver programando aplicativos que usam o Microsoft Azure, há algumas práticas de codificação que você deve seguir toohelp evitar problemas de escalabilidade do aplicativo, o comportamento e desempenho em um ambiente de nuvem. A Microsoft fornece uma ferramenta de análise de código do Azure que reconhece e identifica vários desses problemas comumente encontrados e ajuda a resolvê-los. Você pode baixar a ferramenta Olá no Visual Studio por meio do NuGet.

## <a name="azure-code-analysis-rules"></a>Regras de análise de código do Azure
ferramenta de análise de código do Azure Olá usa Olá tooautomatically sinalizador seu código do Azure quando ele encontra problemas conhecidos afetam o desempenho de regras a seguir. Os problemas detectados aparecem como avisos ou erros do compilador. Código correções ou sugestões tooresolve Olá aviso ou erro geralmente são fornecidos por meio de um ícone de lâmpada.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Evitar o uso do modo de estado de sessão padrão (em processo)
### <a name="id"></a>ID
AP0000

### <a name="description"></a>Descrição
Se você usar o modo de estado de sessão (em processo) saudação padrão para aplicativos em nuvem, você poderá perder o estado da sessão.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Por padrão, o modo de estado de sessão Olá especificado no arquivo Web. config de saudação estiver em processo. Além disso, se nenhuma entrada foi especificada no arquivo de configuração hello, modo de estado da sessão de saudação padrão tooin-process. modo do Hello em processo armazena o estado da sessão na memória no servidor de web hello. Quando uma instância é reiniciada ou uma nova instância é usada para balanceamento de carga ou o suporte a failover, o estado da sessão Olá armazenado na memória no servidor web de saudação não é salvos. Essa situação impede que o aplicativo hello sendo escalonável na nuvem hello.

O estado da sessão ASP.NET dá suporte a várias opções diferentes de armazenamento para dados de estado de sessão: InProc, StateServer, SQLServer, Personalizado e Desativado. É recomendável que você use dados de toohost de modo personalizado em um repositório externo do estado de sessão, como [provedor de estado de sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Solução
Uma solução recomendada é toostore estado da sessão em um serviço de cache gerenciado. Saiba como toouse [provedor de estado de sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore o estado da sessão. Você pode também armazenamento de estado de sessão em outros lugares tooensure que seu aplicativo é escalonável na nuvem hello. toolearn mais sobre as soluções alternativas, consulte [modos de estado de sessão](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>O método de execução não deve ser assíncrono
### <a name="id"></a>ID
AP1000

### <a name="description"></a>Descrição
Criar métodos assíncronos (como [await](https://msdn.microsoft.com/library/hh156528.aspx)) fora Olá [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método e, em seguida, chamar métodos de async saudação do [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Declarando Olá [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método como assíncronas faz com que o trabalho de saudação função tooenter um loop de reinicialização.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Chamando métodos assíncronos em Olá [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que a função de trabalho Olá nuvem service em tempo de execução toorecycle hello. Quando uma função de trabalho é iniciado, o todos a execução do programa ocorre dentro de saudação [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método. Olá existente [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que o trabalho de saudação toorestart de função. Quando o tempo de execução de função de trabalho Olá atinge o método assíncrono de hello, ele envia todas as operações depois de método assíncrono de saudação e, em seguida, retorna. Isso faz com que trabalho Olá função tooexit de saudação [ [ [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método e reinicie. Na próxima iteração de execução hello, função de trabalho Olá acertos Olá async método novamente e for reiniciado, fazendo com que o trabalho de saudação função toorecycle novamente.

### <a name="solution"></a>Solução
Colocar todas as operações assíncronas fora Olá [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método. Em seguida, chame o método assíncrono de saudação refatorado de dentro de saudação [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método, como RunAsync () .wait. ferramenta de análise de código do Azure Olá pode ajudá-lo a corrigir esse problema.

saudação de trecho de código a seguir demonstra Olá código para corrigir esse problema:

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Autenticação de assinatura de acesso compartilhado com barramento de serviço
### <a name="id"></a>ID
AP2000

### <a name="description"></a>Descrição
Use SAS (Assinatura de Acesso Compartilhado) para autenticação. ACS (Serviço de Controle de Acesso) está sendo preterido para autenticação do barramento de serviço.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Para mais segurança, o Active Directory do Azure está substituindo a autenticação do ACS pela autenticação SAS. Consulte [Active Directory do Azure é Olá futuras do ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) para obter informações sobre o plano de transição de saudação.

### <a name="solution"></a>Solução
Use autenticação de SAS em seus aplicativos. saudação de exemplo a seguir mostra como toouse uma tooaccess token SAS um serviço existente do barramento do namespace ou entidade.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Consulte Olá seguintes tópicos para obter mais informações.

* Para uma visão geral, consulte [Autenticação de assinatura de acesso compartilhado com barramento de serviço](https://msdn.microsoft.com/library/dn170477.aspx)
* [Como toouse compartilhado autenticação SAS com barramento de serviço](https://msdn.microsoft.com/library/dn205161.aspx)
* Para um projeto de exemplo, consulte [Usando SAS (Assinatura de Acesso Compartilhado) com assinaturas do barramento de serviço](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>Considere o uso de OnMessage método tooavoid "loop de recebimento"
### <a name="id"></a>ID
AP2002

### <a name="description"></a>Descrição
tooavoid entrar em um "loop de recebimento" hello chamada **OnMessage** método é a melhor solução para receber mensagens de saudação chamada **Receive** método. No entanto, se você precisar usar Olá **Receive** método e você especificar um tempo de espera do servidor não padrão, certifique-se de tempo de espera do servidor de saudação é de mais de um minuto.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Ao chamar **OnMessage**, cliente Olá inicia uma bomba de mensagem interno que monitora constantemente Olá fila ou assinatura. A bomba de mensagens contém um loop infinito que emite uma chamada tooreceive mensagens. Se a chamada de saudação expirar, ele emite uma chamada de novo. intervalo de tempo limite de saudação é determinado pelo valor de saudação do hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) propriedade Olá [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)que está sendo usado.

Olá vantagem de usar **OnMessage** comparados muito**Receive** é que os usuários não toomanually sondar mensagens, lidar com exceções, processar várias mensagens em paralelo e concluir Olá mensagens.

Se você chamar **Receive** sem usar o valor padrão, ser Olá se *ServerWaitTime* valor é a mais de um minuto. Configuração *ServerWaitTime* toomore de um minuto impede que o servidor de saudação tempo limite antes da mensagem de saudação totalmente é recebida.

### <a name="solution"></a>Solução
Consulte Olá exemplos de código para usos recomendados a seguir. Para obter mais detalhes, consulte o método [QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) e o método [QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

desempenho de saudação tooimprove de saudação infraestrutura de mensagens do Azure, consulte o padrão de design Olá [Primer de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).

Olá, a seguir é um exemplo de uso **OnMessage** tooreceive mensagens.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Olá, a seguir é um exemplo de uso **Receive** com o servidor de saudação tempo de espera.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Olá, a seguir é um exemplo de uso **Receive** tempo de espera com um servidor diferente do padrão.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Considere o uso de métodos assíncronos de barramento de serviço
### <a name="id"></a>ID
AP2003

### <a name="description"></a>Descrição
Use o desempenho de tooimprove de métodos de barramento de serviço assíncrono com mensagens orientadas.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Usar métodos assíncronos habilita a simultaneidade de programa do aplicativo como executar cada chamada de não bloquear o thread principal de saudação. Ao usar os métodos de mensagens do Barramento de Serviço, a execução de uma operação (enviar, receber, excluir, etc.) leva tempo. Esse tempo inclui o processamento de Olá da operação de saudação pelo Olá barramento de serviço na latência de toohello de adição de solicitação de saudação e resposta de saudação. número de saudação tooincrease de operações por vez, as operações devem ser executadas simultaneamente. Para obter mais informações, consulte muito[práticas recomendadas para desempenho melhorias usando o serviço de barramento de mensagens orientadas](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Solução
Consulte [QueueClient classe (. Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) para obter informações sobre como toouse Olá recomendado método assíncrono.

desempenho de saudação tooimprove de saudação infraestrutura de mensagens do Azure, consulte o padrão de design Olá [Primer de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Considerar o particionamento de tópicos e filas do barramento de serviço
### <a name="id"></a>ID
AP2004

### <a name="description"></a>Descrição
Particione filas e tópicos do barramento de serviço para um melhor desempenho com as mensagens do barramento de serviço.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Particionamento de tópicos e filas do barramento de serviço aumenta o desempenho taxa de transferência e disponibilidade do serviço porque hello taxa de transferência geral de uma fila ou tópico particionados não é mais limitada pelo desempenho de saudação de um único agente de mensagens ou repositório de mensagens. Além disso, uma falha temporária de um repositório de mensagens não torna uma fila ou tópico particionado indisponível. Para saber mais, confira [Particionamento de entidades de mensagens](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Solução
Olá seguindo o trecho de código mostra como toopartition entidades de mensagens.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Para obter mais informações, consulte [tópicos e filas do barramento de serviço particionado | Blog do Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) e check-out Olá [fila particionada do Microsoft Azure Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) exemplo.

## <a name="do-not-set-sharedaccessstarttime"></a>Não definir SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>Descrição
Você deve evitar usar SharedAccessStartTimeset toohello tooimmediately iniciar Olá política de acesso compartilhado de tempo atual. Você só precisa tooset essa propriedade se você quiser política de acesso compartilhado toostart hello mais tarde.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
A sincronização do relógio causa uma pequena diferença de hora entre os data centers. Por exemplo, você logicamente consideraria hora de início de saudação de configuração de uma política SAS de armazenamento como hello hora atual usando Now ou um método semelhante fará com que efeito de tootake Olá SAS política imediatamente. No entanto, diferenças de horários pequena de saudação entre data centers podem causar problemas com isso, já que algumas vezes de datacenter podem ser ligeiramente posteriores à hora de início do hello, enquanto outros antes que ele. Como resultado, Olá política da SAS pode expirar rapidamente (ou até mesmo imediatamente) se o tempo de vida de política de saudação é definido muito curto.

Para obter instruções sobre como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [apresentando tabela SAS (assinatura de acesso compartilhado) SAS de fila de Site e atualização tooBlob SAS - Blog de equipe de armazenamento do Microsoft Azure - início - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solução
Remova a instrução de saudação que define a hora de início Olá Olá compartilhado da política de acesso. ferramenta de análise de código do Azure Olá fornece uma correção para esse problema. Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design Olá [manobrista chave padrão](https://msdn.microsoft.com/library/dn568102.aspx).

saudação de trecho de código a seguir demonstra Olá código para corrigir esse problema.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>O tempo de expiração da Política de Acesso Compartilhado deve ser mais de cinco minutos
### <a name="id"></a>ID
AP3002

### <a name="description"></a>Descrição
Pode haver quanto um cinco minutos a diferença em relógios entre data centers em locais diferentes devido tooa condição conhecida como "pela defasagem horária". token da política SAS tooprevent Olá expirem antes da data planejada, defina toobe de tempo de expiração de saudação mais de cinco minutos.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Data centers em locais diferentes em torno de Olá, mundo sincronizem por um sinal de relógio. Como demora para locais de toodifferent de tootravel de sinal de relógio, pode ser uma variação de tempo entre data centers em locais geográficos diferentes embora supostamente tudo o que é sincronizado. Essa diferença de tempo pode afetar o acesso compartilhado política início tempo e expiração de intervalo de saudação. Portanto, tooensure política de acesso compartilhado entra em vigor imediatamente, não especifique a hora de início de saudação. Além disso, certifique-se de tempo de expiração de saudação é maior que o tempo limite inicial de tooprevent de 5 minutos.

Para obter mais informações sobre como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [apresentando tabela SAS (assinatura de acesso compartilhado) SAS de fila de Site e atualização tooBlob SAS - Blog de equipe de armazenamento do Microsoft Azure - início - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solução
Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design Olá [manobrista chave padrão](https://msdn.microsoft.com/library/dn568102.aspx).

a seguir Olá é um exemplo de não especificar uma hora de início da política de acesso compartilhado.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

a seguir Olá é um exemplo de especificar uma hora de início da política de acesso compartilhado com uma duração de expiração de política mais de cinco minutos.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Para obter mais informações, consulte [Criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Use CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>Descrição
Usando Olá [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) classe para projetos, como o site do Azure e serviços móveis do Azure não apresentam problemas de tempo de execução. Como prática recomendada, no entanto, é uma boa ideia toouse nuvem[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) como uma forma unificada de gerenciamento de configurações para todos os aplicativos de nuvem do Azure.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
CloudConfigurationManager lê o ambiente de aplicativo hello configuração arquivo toohello apropriado.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Solução
Refatorar o hello toouse de código [CloudConfigurationManager classe](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Um código para corrigir esse problema é fornecido pela ferramenta de análise de código do Azure hello.

saudação de trecho de código a seguir demonstra Olá código para corrigir esse problema. Substitua

`var settings = ConfigurationManager.AppSettings["mySettings"];`

por:

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Aqui está um exemplo de como toostore Olá configuração em um arquivo App. config ou Web. config. Adicione seção appSettings do hello configurações toohello saudação do arquivo de configuração. seguir Olá é Olá Web. config arquivo exemplo de código anterior hello.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Evitar o uso de cadeias de conexão embutidas em código
### <a name="id"></a>ID
AP4001

### <a name="description"></a>Descrição
Se você usar cadeias de caracteres de conexão embutidas e você precisa tooupdate-los mais tarde, você será toomake alterações tooyour código-fonte e recompilar o aplicativo hello. No entanto, se você armazenar suas cadeias de caracteres de conexão em um arquivo de configuração, você pode alterá-las posteriormente ao simplesmente atualizar o arquivo de configuração de saudação.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Codificar cadeias de caracteres de conexão é uma prática inadequada porque ele apresenta problemas quando precisam de cadeias de caracteres de conexão toobe alterada rapidamente. Além disso, se o projeto de saudação precisa toobe check-in de controle de toosource, cadeias de caracteres de conexão embutidas introduzem vulnerabilidades de segurança, como cadeias de caracteres de saudação podem ser exibidas no código-fonte hello.

### <a name="solution"></a>Solução
Armazenar cadeias de caracteres de conexão em arquivos de configuração de saudação ou ambientes do Azure.

* Para aplicativos autônomos, use as configurações de cadeia de caracteres de conexão de toostore App. config.
* Para aplicativos web hospedados no IIS, use cadeias de caracteres de conexão de toostore Web. config.
* Para aplicativos do ASP.NET vNext, use cadeias de caracteres de conexão do configuration.json toostore.

Para obter informações sobre como usar arquivos de configurações, como web.config ou app.config, consulte [Diretrizes de configuração Web do ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Para obter informações sobre como variáveis de ambiente do Azure funcionam, consulte [Sites do Azure: como as cadeias de aplicativo e cadeias de conexão funcionam](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Para obter informações sobre o armazenamento de cadeia de conexão no controle do código-fonte, consulte [Evitar colocar informações confidenciais, como cadeias de conexão em arquivos armazenados no repositório de código-fonte](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Usar arquivo de configuração de diagnóstico
### <a name="id"></a>ID
AP5000

### <a name="description"></a>Descrição
Em vez de configurar as configurações de diagnóstico em seu código, como usando Olá Microsoft.WindowsAzure.Diagnostics API de programação, você deve configurar as configurações de diagnóstico no arquivo Diagnostics wadcfg hello. (Ou diagnostics.wadcfgx se você usar o SDK 2.5 do Azure). Ao fazer isso, você pode alterar as configurações de diagnóstico sem ter que toorecompile seu código.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
2.5 do SDK do Azure (que usa o diagnóstico do Azure 1.3), o diagnóstico do Azure (WAD) podem ser configurados usando vários métodos diferentes: adicionando-blob de configuração toohello no armazenamento, usando o código obrigatório, configuração declarativa ou padrão de saudação configuração. No entanto, Olá preferencial maneira tooconfigure diagnóstico é toouse um arquivo de configuração XML (Diagnostics. wadcfg ou diagnositcs.wadcfgx SDK 2.5 e posterior) no projeto de aplicativo hello. Nessa abordagem, arquivo Diagnostics wadcfg Olá completamente define a configuração de saudação e seja atualizado e reimplantado à vontade. Combinação de uso Olá Olá wadcfg do arquivo de configuração com hello métodos programáticos de definir as configurações usando Olá [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)ou [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) classes podem gerar tooconfusion. Consulte [Inicializar ou alterar configuração de diagnóstico do Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) para obter mais informações.

A partir do WAD 1.3 (incluído no Azure SDK 2.5), já não diagnóstico de tooconfigure código toouse possíveis. Como resultado, você pode fornecer configuração Olá ao aplicar ou atualizar a extensão de diagnóstico de saudação.

### <a name="solution"></a>Solução
Use Olá diagnóstico designer toomove configurações de diagnóstico toohello diagnóstico configuração arquivo de configuração (diagnositcs.wadcfg ou diagnositcs.wadcfgx SDK 2.5 e posterior). Também é recomendável que você instale [2.5 do SDK do Azure](http://go.microsoft.com/fwlink/?LinkId=513188) e usar o recurso de diagnóstico hello mais recente.

1. No menu de atalho Olá para função hello que você deseja tooconfigure, escolha Propriedades e, em seguida, escolha a guia de configuração de saudação.
2. Em Olá **diagnóstico** seção, certifique-se de que Olá **habilitar o diagnóstico** caixa de seleção é marcada.
3. Escolha Olá **configurar** botão.

   ![Acessando a opção de habilitar o diagnóstico Olá](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Consulte [Configurando o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para obter mais informações.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Evitar declarar objetos DbContext como estáticos
### <a name="id"></a>ID
AP6000

### <a name="description"></a>Descrição
memória toosave, evite declarando objetos DBContext como estático.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Objetos de DBContext mantêm Olá resultados da consulta de cada chamada. Objetos de DBContext estáticos não são descartados até que o domínio de aplicativo hello é descarregado. Portanto, um objeto DBContext estático pode consumir grandes quantidades de memória.

### <a name="solution"></a>Solução
Declare DBContext como uma variável local ou um campo de instância não estático, use-o para uma tarefa e deixe-o ser descartado após o uso.

saudação de classe do controlador MVC exemplo a seguir mostra como toouse Olá objeto DBContext.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a otimização e Solucionando problemas de aplicativos do Azure, consulte [solucionar problemas de um aplicativo web no serviço de aplicativo do Azure usando o Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
