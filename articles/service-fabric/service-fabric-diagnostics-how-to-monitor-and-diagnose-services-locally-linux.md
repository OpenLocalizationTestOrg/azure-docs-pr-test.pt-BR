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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Monitorar e diagnosticar serviços em uma configuração de desenvolvimento do computador local


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Monitoramento, detectar, diagnosticar e solucionar problemas permitem toocontinue de serviços com a experiência do usuário toohello mínimo de interrupção. O monitoramento e o diagnóstico são essenciais em um ambiente de produção implantado. Adotar um modelo semelhante durante o desenvolvimento de serviços garante que esse pipeline de diagnóstico Olá funciona quando você move tooa ambiente de produção. Malha do serviço facilita para diagnóstico de tooimplement de desenvolvedores de serviço que pode funcionar perfeitamente em configurações de desenvolvimento local único computador e configurações de cluster de produção do mundo real.


## <a name="debugging-service-fabric-java-applications"></a>Depuração de aplicativos Java do Service Fabric

Para aplicativos Java, [várias estrutura de registros](http://en.wikipedia.org/wiki/Java_logging_framework) estão disponíveis. Como `java.util.logging` é a opção padrão de saudação com hello JRE, ele também é usado para Olá [exemplos de código na github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Olá discussão a seguir explica como Olá tooconfigure `java.util.logging` framework.

Usar Logging, você pode redirecionar seu aplicativo registra toomemory, fluxos de saída, os arquivos do console ou soquetes. Para cada uma dessas opções, há manipuladores padrão já fornecidos no framework de saudação. Você pode criar um `app.properties` manipulador de arquivo do arquivo tooconfigure Olá para sua tooredirect aplicativo todos os logs de arquivo local tooa.

saudação de trecho de código a seguir contém um exemplo de configuração:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

saudação de tooby apontada pasta Olá `app.properties` arquivo deve existir. Depois de saudação `app.properties` arquivo é criado, você precisa tooalso modificar o script de ponto de entrada, `entrypoint.sh` em Olá `<applicationfolder>/<servicePkg>/Code/` propriedade saudação da pasta tooset `java.util.logging.config.file` muito`app.propertes` arquivo. entrada de saudação deve ter aparência Olá trecho de código a seguir:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Esta configuração resulta em logs sendo coletados em um modo de rotação em `/tmp/servicefabric/logs/`. arquivo de log de saudação nesse caso é chamado mysfapp%u.%g.log onde:
* **%u** é um tooresolve número exclusivo conflitos entre processos simultâneos de Java.
* **%g** é Olá geração número toodistinguish entre girando logs.

Por padrão se nenhum manipulador explicitamente estiver configurado, o manipulador de console do hello está registrado. Um pode exibir logs de saudação no syslog em /var/log/syslog.

Para obter mais informações, consulte Olá [exemplos de código na github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Depuração de aplicativos C# do Service Fabric


Várias estruturas estão disponíveis para rastreamento de aplicativos CoreCLR no Linux. Para saber mais, consulte [GitHub: registro em log](http:/github.com/aspnet/logging).  Como EventSource é tooC # familiar aos desenvolvedores,' Este artigo usa EventSource para rastreamento CoreCLR exemplos no Linux.

Olá primeira etapa é tooinclude Tracing para que você pode escrever seus logs toomemory, fluxos de saída ou arquivos de console.  Para fazer logon usando EventSource, adicione Olá projeto tooyour Project a seguir:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Você pode usar um toolisten EventListener personalizado para eventos de serviço hello e, em seguida, adequadamente redirecioná-los tootrace arquivos. Olá trecho de código a seguir mostra uma implementação de exemplo de log usando EventSource e um EventListener personalizado:


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


trecho de código anterior Hello gera Olá logs tooa arquivo `/tmp/MyServiceLog.txt`. Este nome de arquivo precisa toobe atualizado adequadamente. Caso você deseje tooredirect Olá logs tooconsole, use Olá trecho de código em sua classe EventListener personalizado a seguir:

```csharp
public static TextWriter Out = Console.Out;
```

Olá exemplos em [amostras c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) usar EventSource e um arquivo de tooa eventos personalizado EventListener toolog.



## <a name="next-steps"></a>Próximas etapas
Olá mesmo código de rastreamento adicionado tooyour aplicativo também funciona com o diagnóstico de saudação do seu aplicativo em um cluster do Azure. Check-out esses artigos que abordam opções diferentes de saudação para ferramentas hello e descrevem como tooset-los para cima.
* [Como toocollect registra com o diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-lad.md)
