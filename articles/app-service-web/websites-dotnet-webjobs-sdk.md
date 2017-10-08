---
title: "aaaWhat é hello SDK do Azure WebJobs"
description: "Uma introdução toohello SDK do Azure WebJobs. Explica quais Olá SDK é, geralmente é útil para, e exemplos de código."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>O que é Olá SDK do Azure WebJobs
## <a id="overview"></a>Visão geral
Este artigo explica o que Olá SDK do WebJobs é, examina alguns cenários comuns é útil para e fornece uma visão geral de como usá-lo em seu código.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[WebJobs](websites-webjobs-resources.md) é um recurso do serviço de aplicativo do Azure que permite que você toorun um programa ou script hello mesmo contexto de um aplicativo web, o aplicativo de API ou o aplicativo móvel. Olá finalidade Olá [SDK do WebJobs](websites-webjobs-resources.md) toosimplify Olá código gravar para tarefas comuns que pode executar um trabalho Web, como processamento de imagem, processamento de fila, agregação de RSS, manutenção de arquivo e enviar emails. Olá SDK do WebJobs possui recursos internos para trabalhar com o armazenamento do Azure e o barramento de serviço, para o agendamento de tarefas e tratamento de erros e muitos outros cenários comuns. Além disso, ele é projetado toobe extensível. Olá [WebJobs SDK é o código-fonte aberto](https://github.com/Azure/azure-webjobs-sdk/)e há um [repositório do código-fonte aberto para extensões](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Olá WebJobs SDK inclui Olá componentes a seguir:

* **Pacotes NuGet**. Pacotes do NuGet que você adicione o projeto de aplicativo de Console do Visual Studio tooa fornecem uma estrutura que seu código usa decorando seus métodos com atributos de SDK do WebJobs.
* **Painel**. Parte do SDK do WebJobs do hello está incluído no serviço de aplicativo do Azure e fornece monitoramento avançado e diagnósticos para programas que usam pacotes do NuGet hello. Você não tem toowrite código toouse esses recursos de monitoramento e diagnóstico.

## <a id="scenarios"></a>Cenários
Aqui estão alguns cenários típicos que você pode manipular mais facilmente com hello SDK do Azure WebJobs:

* Processamento de imagens ou outro trabalho com uso intensivo da CPU. Um recurso comum de sites é Olá capacidade tooupload imagens ou vídeos. Geralmente você deseja que toomanipulate Olá conteúdo depois que ele é carregado, mas não deseja toomake Olá usuário espera enquanto você fazer isso.
* Processamento de filas. Uma maneira comum para um toocommunicate de front-end da web com um serviço de back-end é toouse filas. Quando o site Olá precisa tooget trabalho, ele envia uma mensagem para uma fila. Um serviço de back-end recebe mensagens da fila de saudação e Olá trabalho. Você pode usar filas para processamento de imagem: por exemplo, após o usuário Olá carrega um número de arquivos, coloque os nomes de arquivo hello em uma toobe de mensagem da fila captado pelo back-end Olá para processamento. Ou você pode usar a capacidade de resposta do filas tooimprove site. Por exemplo, em vez de gravar diretamente o banco de dados SQL tooa, tooa fila de gravação, informar o usuário de saudação terminar e permitem Olá back-end serviço identificador alta latência banco de dados relacional de trabalho. Para obter um exemplo de fila de processamento com o processo de imagem, consulte Olá [WebJobs SDK começar o tutorial](websites-dotnet-webjobs-sdk-get-started.md).
* Agregação de RSS. Se você tiver um site que mantém uma lista de feeds RSS, você pode efetuar pull de todos os artigos Olá Olá feeds em um processo em segundo plano.
* Manutenção de arquivos, como agregar ou limpar arquivos de log.  Você pode ter arquivos de log que está sendo criados por vários sites ou para separar os intervalos de tempo que você deseja toocombine em ordem toorun trabalhos de análise neles. Ou talvez você queira tooschedule um toorun de tarefa semanal tooclean backup de arquivos de log antigos.
* Ingresso em Tabelas do Azure. Você pode ter arquivos armazenados e blobs e deseja tooparse-los e armazenar dados de saudação em tabelas. função de entrada Hello poderia escrever várias linhas (em milhões em alguns casos) e Olá SDK do WebJobs torna possível tooimplement essa funcionalidade facilmente. Olá SDK também fornece monitoramento em tempo real de indicadores de progresso, como número de saudação de linhas gravadas na tabela de saudação.
* Outras tarefas de longa execução que você deseja toorun em um thread em segundo plano, como [enviar emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* As tarefas que você deseja toorun em um agendamento, como executar uma operação de backup todas as noites.

Em muitos cenários, convém tooscale um toorun de aplicativo web em várias VMs, o que poderia executar vários trabalhos de Web simultaneamente. Em alguns cenários, isso pode resultar em Olá mesmo processados de dados várias vezes, mas isso não é um problema quando você usa a fila interna hello, blob e gatilhos de barramento de serviço do SDK do WebJobs de saudação. Olá SDK garante que as funções serão processadas apenas uma vez para cada mensagem ou blob.

Olá SDK do WebJobs também torna fácil toohandle cenários comuns de tratamento de erros. Você pode configurar alertas toosend notificações quando uma função falhar, e você pode definir tempos limite para que uma função é cancelada automaticamente se ela não for concluída dentro de um limite de tempo especificado.

## <a id="code"></a> Exemplos de código
saudação de código para lidar com tarefas típicas que funcionam com o armazenamento do Azure é simple. Em seu aplicativo de Console `Main` método é criar um `JobHost` objeto que coordena Olá chama toomethods você escrever. Olá framework SDK do WebJobs sabe quando toocall seus métodos e valores de qual parâmetro toouse com base em Olá SDK do WebJobs atributos usar neles. Olá SDK fornece *gatilhos* que especificam que condições causam Olá toobe de função chamada, e *associadores* que especificam como tooget informações dentro e fora de parâmetros de método.

Por exemplo, Olá [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) atributo faz com que um toobe função chamado quando uma mensagem é recebida em uma fila, e se o formato de mensagem de saudação for JSON para um tipo personalizado ou uma matriz de bytes, a mensagem de saudação é desserializada automaticamente. Olá [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) atributo dispara um processo sempre que um novo blob é criado em uma conta de armazenamento do Azure.

Este é um programa simples que consulta uma fila e cria um blob para cada mensagem de fila recebida:

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

Olá `JobHost` objeto é um contêiner para um conjunto de funções de plano de fundo. Olá `JobHost` objeto monitores Olá funções, procura por eventos que disparam-los e executa funções hello quando ocorrem eventos de gatilho. Você chama um `JobHost` método tooindicate se deseja toorun de processo do contêiner de saudação em Olá thread atual ou em um thread em segundo plano. No exemplo hello, Olá `RunAndBlock` método executa o processo de saudação continuamente no thread atual hello.

Porque Olá `ProcessQueueMessage` método neste exemplo tem um `QueueTrigger` atributo gatilho Olá para essa função é a recepção de saudação de uma nova mensagem da fila. Olá `JobHost` objeto inspeciona novas mensagens de fila na fila especificada da saudação ("webjobsqueue" neste exemplo) e quando um é encontrado, ele chama `ProcessQueueMessage`. 

Olá `QueueTrigger` atributo vincula Olá `inputText` valor do parâmetro toohello de mensagem da fila de saudação. E hello `Blob` atributo associa um `TextWriter` objeto tooa blob denominado "blobname" em um contêiner chamado "containername".  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

função Hello, em seguida, usa essas valor parâmetros toowrite Olá blob de toohello de mensagens de fila hello:

        writer.WriteLine(inputText);

recursos de gatilho e associador de saudação do hello SDK do WebJobs simplificam código Olá ter toowrite. Olá código de baixo nível necessário tooprocess filas, blobs, ou arquivos ou tarefas tooinitiate agendada, é feito para você por saudação do framework do SDK do WebJobs. Por exemplo, framework Olá cria filas que ainda não existirem, abre Olá fila, leituras Enfileirar mensagens, exclui mensagens da fila quando o processamento for concluído, cria os contêineres de blob que não existem ainda, grava tooblobs e assim por diante.

Olá exemplo de código a seguir mostra uma variedade de gatilhos em um WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, e `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## Agendamento <a id="schedule"></a>
Olá `TimerTrigger` atributo fornece Olá capacidade tootrigger funções toorun em uma agenda. Você pode agendar um trabalho Web como um total por meio do Azure ou agenda individuais funções de um trabalho Web usando Olá SDK do WebJobs `TimerTrigger`. Aqui está um exemplo de código.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Para mais de exemplo de código, consulte [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) no repositório de extensões do azure-webjobs-sdk Olá em GitHub.com.

## <a name="extensibility"></a>Extensibilidade
Você não está limitado toobuilt na funcionalidade – Olá SDK do WebJobs permite que você gatilhos personalizados toowrite e associadores.  Por exemplo, você pode escrever gatilhos para eventos de cache e agendamentos periódicos. Um [repositório do código-fonte aberto](https://github.com/Azure/azure-webjobs-sdk-extensions) contém um [guia detalhado sobre extensibilidade do SDK do WebJobs](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) e toohelp do código de exemplo proporcionar a você escrever seus próprios gatilhos e associadores.

## <a id="workerrole"></a>Usando Olá SDK do WebJobs fora do WebJobs
Um programa que usa Olá Olá SDK do WebJobs é um aplicativo de Console padrão e pode ser executado em qualquer lugar – não tem toorun como um trabalho Web. Você pode testar o programa hello localmente no computador de desenvolvimento e que você pode executá-lo em uma função de trabalho do serviço de nuvem ou um serviço do Windows, se você preferir um dos ambientes de produção. 

No entanto, o painel Olá só está disponível como uma extensão para um aplicativo da web do serviço de aplicativo do Azure. Se você quiser toorun fora de um trabalho Web e ainda usa Olá painel, você pode configurar uma web toouse aplicativo hello a mesma conta de armazenamento que sua cadeia de caracteres de conexão do painel de SDK do WebJobs refere-se a, e painel desse aplicativo web do WebJobs mostrará dados sobre a função execução de seu programa que está sendo executado em outro lugar. Você pode obter toohello painel usando Olá URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Para obter mais informações, consulte [obtendo um painel para desenvolvimento local com hello SDK do WebJobs](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), mas observe que a postagem do blog Olá mostra um nome de cadeia de caracteres de conexão antigo. 

## <a id="nostorage"></a>Recursos do painel de controle
Olá SDK do WebJobs oferece várias vantagens, mesmo se você não usar o SDK do WebJobs gatilhos ou associadores:

* Você pode chamar funções da saudação painel.
* Você pode reproduzir funções da saudação painel.
* Você pode exibir logs em Olá Dashboard, vinculado toohello WebJob específico (logs de aplicativo, gravadas usando Console.Out, Console.Error, rastreamento, etc.) ou vinculados toohello invocação de função específica que gerou (logs escritos usando um `TextWriter` objeto que Olá que SDK passa toohello função como um parâmetro). 

Para obter mais informações, consulte [como toomanually invocar uma função](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) e [como toowrite registra](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Próximas etapas
Para obter mais informações sobre o SDK do WebJobs do hello, consulte [recursos recomendada do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

Para obter informações sobre toohello de aprimoramentos mais recente Olá WebJobs SDK, consulte Olá [notas de versão](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

