---
title: "Depurar microsserviços do Azure no Linux | Microsoft Docs"
description: "Saiba como monitorar e diagnosticar seus serviços escritos com o Service Fabric do Microsoft Azure em um computador de desenvolvimento local."
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
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="c1e2c-103">Monitorar e diagnosticar serviços em uma configuração de desenvolvimento do computador local</span><span class="sxs-lookup"><span data-stu-id="c1e2c-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1e2c-104">Windows</span><span class="sxs-lookup"><span data-stu-id="c1e2c-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="c1e2c-105">Linux</span><span class="sxs-lookup"><span data-stu-id="c1e2c-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="c1e2c-106">Monitoramento, detecção, diagnóstico e solução de problemas permitem dar continuidade aos serviços com mínima interrupção da experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="c1e2c-107">O monitoramento e o diagnóstico são essenciais em um ambiente de produção implantado.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="c1e2c-108">A adoção de um modelo semelhante durante o desenvolvimento de serviços garante que o pipeline de diagnóstico funcionará quando você se deslocar para um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="c1e2c-109">O Service Fabric facilita para o desenvolvedor de serviço implementar diagnóstico que possa funcionar perfeitamente tanto em configurações de desenvolvimento local de computador único, quanto em configurações reais de cluster de produção.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="c1e2c-110">Depuração de aplicativos Java do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c1e2c-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="c1e2c-111">Para aplicativos Java, [várias estrutura de registros](http://en.wikipedia.org/wiki/Java_logging_framework) estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="c1e2c-112">Uma vez que `java.util.logging` é a opção padrão com o JRE, ele também é usado nos [códigos de exemplos no GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c1e2c-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="c1e2c-113">A discussão a seguir explica como configurar a estrutura `java.util.logging` .</span><span class="sxs-lookup"><span data-stu-id="c1e2c-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="c1e2c-114">Ao usar java.util.logging, você pode redirecionar os logs do aplicativo para a memória, os fluxos de saída, os arquivos de consoles ou os soquetes.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="c1e2c-115">Para cada uma dessas opções, há manipuladores padrão já fornecidos na estrutura.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="c1e2c-116">Você pode criar um arquivo `app.properties` para configurar o manipulador de arquivo para o seu aplicativo redirecionar todos os logs para um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="c1e2c-117">O trecho de código a seguir contém um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="c1e2c-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="c1e2c-118">A pasta apontada pelo arquivo `app.properties` deve existir.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="c1e2c-119">Depois que o arquivo `app.properties` for criado, você também precisará modificar o script de ponto de entrada `entrypoint.sh` na pasta `<applicationfolder>/<servicePkg>/Code/` para definir a propriedade `java.util.logging.config.file` para o arquivo `app.propertes`.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="c1e2c-120">A entrada deverá se parecer com o seguinte trecho:</span><span class="sxs-lookup"><span data-stu-id="c1e2c-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="c1e2c-121">Esta configuração resulta em logs sendo coletados em um modo de rotação em `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="c1e2c-122">O arquivo de log nesse caso é chamado mysfapp%u.%g.log, em que:</span><span class="sxs-lookup"><span data-stu-id="c1e2c-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="c1e2c-123">**%u** é um número exclusivo para resolver conflitos entre processos Java simultâneos.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="c1e2c-124">**%g** é o número de geração para distinguir entre logs rotativos.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="c1e2c-125">Por padrão, se nenhum manipulador for configurado explicitamente, o manipulador de console será registrado.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="c1e2c-126">Estes logs podem ser vistos no syslog, em /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="c1e2c-127">Para obter mais informações, confira os [códigos de exemplos no GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c1e2c-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="c1e2c-128">Depuração de aplicativos C# do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c1e2c-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="c1e2c-129">Várias estruturas estão disponíveis para rastreamento de aplicativos CoreCLR no Linux.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="c1e2c-130">Para saber mais, consulte [GitHub: registro em log](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="c1e2c-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="c1e2c-131">Uma vez que o EventSource é familiar aos desenvolvedores do C#, este artigo usa EventSource para rastreamento em exemplos de CoreCLR no Linux.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="c1e2c-132">A primeira etapa é incluir System.Diagnostics.Tracing para que você possa escrever seus logs na memória, fluxos de saída ou arquivos de console.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="c1e2c-133">Para registrar em log usando o EventSource, adicione o projeto a seguir a seu project.json:</span><span class="sxs-lookup"><span data-stu-id="c1e2c-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="c1e2c-134">Você pode usar um EventListener personalizado para ouvir o evento de serviço e redirecioná-lo apropriadamente para arquivos de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="c1e2c-135">O trecho de código a seguir mostra uma implementação de exemplo de registo em log usando EventSource e um EventListener personalizado:</span><span class="sxs-lookup"><span data-stu-id="c1e2c-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need to add method for sample event.

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


<span data-ttu-id="c1e2c-136">O trecho anterior gera os logs para um arquivo em `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="c1e2c-137">Esse nome de arquivo precisa ser atualizado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="c1e2c-138">Caso você deseje redirecionar os logs para o console, use o trecho a seguir em sua classe EventListener personalizada:</span><span class="sxs-lookup"><span data-stu-id="c1e2c-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="c1e2c-139">Os exemplos neste [Exemplos de C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) usam EventSource e um EventListener personalizado para registrar eventos em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c1e2c-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1e2c-140">Next steps</span></span>
<span data-ttu-id="c1e2c-141">O mesmo código de rastreamento adicionado ao seu aplicativo também funciona com o diagnóstico do seu aplicativo em um cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="c1e2c-142">Consulte estes artigos que discutem as diferentes opções para as ferramentas e descrevem como configurá-las.</span><span class="sxs-lookup"><span data-stu-id="c1e2c-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="c1e2c-143">Como coletar logs com o Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="c1e2c-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
