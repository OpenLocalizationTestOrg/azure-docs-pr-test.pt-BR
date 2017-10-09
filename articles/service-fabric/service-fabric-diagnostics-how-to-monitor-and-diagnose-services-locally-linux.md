---
title: aaaDebug microservices do Azure no Linux | Microsoft Docs
description: "Saiba como toomonitor e diagnosticar seus serviços escritos usando o Microsoft Azure Service Fabric em uma máquina de desenvolvimento local."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="62b4f-103">Monitorar e diagnosticar serviços em uma configuração de desenvolvimento do computador local</span><span class="sxs-lookup"><span data-stu-id="62b4f-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="62b4f-104">Windows</span><span class="sxs-lookup"><span data-stu-id="62b4f-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="62b4f-105">Linux</span><span class="sxs-lookup"><span data-stu-id="62b4f-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="62b4f-106">Monitoramento, detectar, diagnosticar e solucionar problemas permitem toocontinue de serviços com a experiência do usuário toohello mínimo de interrupção.</span><span class="sxs-lookup"><span data-stu-id="62b4f-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="62b4f-107">O monitoramento e o diagnóstico são essenciais em um ambiente de produção implantado.</span><span class="sxs-lookup"><span data-stu-id="62b4f-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="62b4f-108">Adotar um modelo semelhante durante o desenvolvimento de serviços garante que esse pipeline de diagnóstico Olá funciona quando você move tooa ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="62b4f-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="62b4f-109">Malha do serviço facilita para diagnóstico de tooimplement de desenvolvedores de serviço que pode funcionar perfeitamente em configurações de desenvolvimento local único computador e configurações de cluster de produção do mundo real.</span><span class="sxs-lookup"><span data-stu-id="62b4f-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="62b4f-110">Depuração de aplicativos Java do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="62b4f-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="62b4f-111">Para aplicativos Java, [várias estrutura de registros](http://en.wikipedia.org/wiki/Java_logging_framework) estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="62b4f-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="62b4f-112">Como `java.util.logging` é a opção padrão de saudação com hello JRE, ele também é usado para Olá [exemplos de código na github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="62b4f-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="62b4f-113">Olá discussão a seguir explica como Olá tooconfigure `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="62b4f-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="62b4f-114">Usar Logging, você pode redirecionar seu aplicativo registra toomemory, fluxos de saída, os arquivos do console ou soquetes.</span><span class="sxs-lookup"><span data-stu-id="62b4f-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="62b4f-115">Para cada uma dessas opções, há manipuladores padrão já fornecidos no framework de saudação.</span><span class="sxs-lookup"><span data-stu-id="62b4f-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="62b4f-116">Você pode criar um `app.properties` manipulador de arquivo do arquivo tooconfigure Olá para sua tooredirect aplicativo todos os logs de arquivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="62b4f-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="62b4f-117">saudação de trecho de código a seguir contém um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="62b4f-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="62b4f-118">saudação de tooby apontada pasta Olá `app.properties` arquivo deve existir.</span><span class="sxs-lookup"><span data-stu-id="62b4f-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="62b4f-119">Depois de saudação `app.properties` arquivo é criado, você precisa tooalso modificar o script de ponto de entrada, `entrypoint.sh` em Olá `<applicationfolder>/<servicePkg>/Code/` propriedade saudação da pasta tooset `java.util.logging.config.file` muito`app.propertes` arquivo.</span><span class="sxs-lookup"><span data-stu-id="62b4f-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="62b4f-120">entrada de saudação deve ter aparência Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="62b4f-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="62b4f-121">Esta configuração resulta em logs sendo coletados em um modo de rotação em `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="62b4f-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="62b4f-122">arquivo de log de saudação nesse caso é chamado mysfapp%u.%g.log onde:</span><span class="sxs-lookup"><span data-stu-id="62b4f-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="62b4f-123">**%u** é um tooresolve número exclusivo conflitos entre processos simultâneos de Java.</span><span class="sxs-lookup"><span data-stu-id="62b4f-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="62b4f-124">**%g** é Olá geração número toodistinguish entre girando logs.</span><span class="sxs-lookup"><span data-stu-id="62b4f-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="62b4f-125">Por padrão se nenhum manipulador explicitamente estiver configurado, o manipulador de console do hello está registrado.</span><span class="sxs-lookup"><span data-stu-id="62b4f-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="62b4f-126">Um pode exibir logs de saudação no syslog em /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="62b4f-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="62b4f-127">Para obter mais informações, consulte Olá [exemplos de código na github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="62b4f-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="62b4f-128">Depuração de aplicativos C# do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="62b4f-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="62b4f-129">Várias estruturas estão disponíveis para rastreamento de aplicativos CoreCLR no Linux.</span><span class="sxs-lookup"><span data-stu-id="62b4f-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="62b4f-130">Para saber mais, consulte [GitHub: registro em log](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="62b4f-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="62b4f-131">Como EventSource é tooC # familiar aos desenvolvedores,' Este artigo usa EventSource para rastreamento CoreCLR exemplos no Linux.</span><span class="sxs-lookup"><span data-stu-id="62b4f-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="62b4f-132">Olá primeira etapa é tooinclude Tracing para que você pode escrever seus logs toomemory, fluxos de saída ou arquivos de console.</span><span class="sxs-lookup"><span data-stu-id="62b4f-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="62b4f-133">Para fazer logon usando EventSource, adicione Olá projeto tooyour Project a seguir:</span><span class="sxs-lookup"><span data-stu-id="62b4f-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="62b4f-134">Você pode usar um toolisten EventListener personalizado para eventos de serviço hello e, em seguida, adequadamente redirecioná-los tootrace arquivos.</span><span class="sxs-lookup"><span data-stu-id="62b4f-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="62b4f-135">Olá trecho de código a seguir mostra uma implementação de exemplo de log usando EventSource e um EventListener personalizado:</span><span class="sxs-lookup"><span data-stu-id="62b4f-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="62b4f-136">trecho de código anterior Hello gera Olá logs tooa arquivo `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="62b4f-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="62b4f-137">Este nome de arquivo precisa toobe atualizado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="62b4f-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="62b4f-138">Caso você deseje tooredirect Olá logs tooconsole, use Olá trecho de código em sua classe EventListener personalizado a seguir:</span><span class="sxs-lookup"><span data-stu-id="62b4f-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="62b4f-139">Olá exemplos em [amostras c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) usar EventSource e um arquivo de tooa eventos personalizado EventListener toolog.</span><span class="sxs-lookup"><span data-stu-id="62b4f-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="62b4f-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="62b4f-140">Next steps</span></span>
<span data-ttu-id="62b4f-141">Olá mesmo código de rastreamento adicionado tooyour aplicativo também funciona com o diagnóstico de saudação do seu aplicativo em um cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="62b4f-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="62b4f-142">Check-out esses artigos que abordam opções diferentes de saudação para ferramentas hello e descrevem como tooset-los para cima.</span><span class="sxs-lookup"><span data-stu-id="62b4f-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="62b4f-143">Como toocollect registra com o diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="62b4f-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
