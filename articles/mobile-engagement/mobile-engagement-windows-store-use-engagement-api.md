---
title: "saudação de tooUse aaaHow contrato de API no Windows Universal"
description: "Como tooUse Olá contrato de API no Windows Universal"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a>Como tooUse Olá contrato de API no Windows Universal
Este é um documento de toohello complemento [como tooIntegrate contrato no Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): fornece encontrar detalhes sobre como toouse Olá contrato API tooreport suas estatísticas do aplicativo.

Tenha em mente que se você desejar contrato tooreport somente sessões, atividades, falhas e obter informações técnicas do seu aplicativo, em seguida, hello forma mais simples é toomake todos os seus `Page` subclasses herdam Olá `EngagementPage` classe.

Se você quiser toodo mais, por exemplo, se você precisar de trabalhos, erros e eventos específicos do aplicativo tooreport, ou se você tiver tooreport atividades do seu aplicativo de maneira diferente de Olá um implementado em Olá `EngagementPage` classes, e em seguida, você precisa toouse Olá Contrato de API.

Olá contrato de API é fornecida pelo Olá `EngagementAgent` classe. Você pode acessar os métodos de toothose por meio de `EngagementAgent.Instance`.

Mesmo que o módulo de saudação do agente não foi inicializado, cada API toohello de chamada é adiada e será executado novamente quando o agente hello está disponível.

## <a name="engagement-concepts"></a>Conceitos de Engagement
seguintes partes Hello refinar Olá comuns [Mobile Engagement conceitos](mobile-engagement-concepts.md) para plataforma Universal do Windows hello.

### <a name="session-and-activity"></a>`Session` e `Activity`
Um *atividade* geralmente está associado com uma página de aplicativo hello, que é toosay hello *atividade* inicia quando a página Olá é exibida e é interrompido quando Olá página é fechada: esse é o caso de Olá quando hello SDK do contrato é integrado usando Olá `EngagementPage` classe.

Mas *atividades* também podem ser controladas manualmente usando Olá contrato de API. Isso permite que você toosplit uma determinada página em várias sub partes tooget mais detalhes sobre o uso de saudação desta página (por exemplo tooknow frequência e quanto tempo as caixas de diálogo são usadas dentro desta página).

## <a name="reporting-activities"></a>Relatório de atividades
### <a name="user-starts-a-new-activity"></a>O usuário inicia uma nova atividade
#### <a name="reference"></a>Referência
            void StartActivity(string name, Dictionary<object, object> extras = null)

Você precisa toocall `StartActivity()` alterações de cada atividade de usuário de saudação do tempo. Olá primeira chamada toothis função inicia uma nova sessão de usuário.

> [!IMPORTANT]
> Olá SDK automaticamente chama o método de EndActivity de saudação quando o aplicativo hello está fechado. Portanto, é altamente recomendável método de StartActivity toocall hello sempre hello atividade de usuário Olá alterações e término da chamada tooNEVER Olá método EndActivity, desde chamar esse método força Olá toobe de sessão atual.
> 
> 

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>O usuário encerra sua atividade atual
#### <a name="reference"></a>Referência
            void EndActivity()

Isso encerra a atividade de saudação e a sessão de saudação. Você não deve chamar esse método, a menos que você realmente sabe o que está fazendo.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Relatório de trabalhos
### <a name="start-a-job"></a>Iniciar um trabalho
#### <a name="reference"></a>Referência
            void StartJob(string name, Dictionary<object, object> extras = null)

Você pode usar o hello tootrack alguns tarefas em um período de tempo.

#### <a name="example"></a>Exemplo
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Encerrar um trabalho
#### <a name="reference"></a>Referência
            void EndJob(string name)

Assim que uma tarefa controlada por um trabalho foi encerrada, você deve chamar o método de EndJob de saudação para esse trabalho, fornecendo o nome do trabalho hello.

#### <a name="example"></a>Exemplo
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Eventos de relatório
Há três tipos de eventos :

* Eventos autônomos
* Eventos de sessão
* Eventos de trabalho

### <a name="standalone-events"></a>Eventos autônomos
#### <a name="reference"></a>Referência
            void SendEvent(string name, Dictionary<object, object> extras = null)

Autônomo eventos podem ocorrer fora do contexto de saudação de uma sessão.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Eventos de sessão
#### <a name="reference"></a>Referência
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Eventos de sessão são ações que Olá tooreport usados normalmente executadas por um usuário durante a sessão.

#### <a name="example"></a>Exemplo
**Sem dados :**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Com dados :**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Eventos de trabalho
#### <a name="reference"></a>Referência
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Eventos de trabalho são ações que Olá tooreport usados normalmente executadas por um usuário durante um trabalho.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Erros de relatório
Há três tipos de erros:

* Erros autônomos
* Erros de sessão
* Erros de trabalho

### <a name="standalone-errors"></a>Erros autônomos
#### <a name="reference"></a>Referência
            void SendError(string name, Dictionary<object, object> extras = null)

Erros de toosession contrary, podem ocorrer erros autônomo fora do contexto de saudação de uma sessão.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Erros de sessão
#### <a name="reference"></a>Referência
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Erros de sessão são erros de saudação do tooreport geralmente usados afetar o usuário Olá durante a sessão.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Erros de trabalho
#### <a name="reference"></a>Referência
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Os erros podem ser relacionada tooa executando o trabalho em vez de ser relacionados toohello sessão do usuário atual.

#### <a name="example"></a>Exemplo
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Relatórios de falhas
Agente de saudação fornece dois toodeal de métodos com falhas.

### <a name="send-an-exception"></a>Enviar uma exceção
#### <a name="reference"></a>Referência
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Exemplo
Você pode enviar uma exceção a qualquer momento chamando :

            EngagementAgent.Instance.SendCrash(aCatchedException);

Você também pode usar uma sessão de contrato de saudação do parâmetro opcional tooterminate em Olá mesmo tempo que o envio de falhas de saudação. Portanto, chame toodo:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Se você fizer isso, trabalhos e sessão Olá serão fechados imediatamente após enviar falha de saudação.

### <a name="send-an-unhandled-exception"></a>Enviar uma exceção sem tratamento
#### <a name="reference"></a>Referência
            void SendCrash(Exception e)

Contrato também fornece um exceções toosend sem tratamento de método se você tiver **desabilitado** contrato automático **falha** reporting. Isso é especialmente útil quando usado dentro do manipulador de eventos do hello aplicativo UnhandledException.

Esse método será **sempre** encerrar a sessão de contrato hello e trabalhos após a chamada.

#### <a name="example"></a>Exemplo
Você pode usá-lo tooimplement seu próprio manipulador de UnhandledExceptionEventArgs. Por exemplo, adicionar Olá `Current_UnhandledException` método hello `App.xaml.cs` arquivo:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

Em App.xaml.cs em "Public App(){}" adicione:

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a>Id do dispositivo
            String EngagementAgent.Instance.GetDeviceId()

Você pode obter o id do dispositivo Olá engagement por chamar esse método.

## <a name="extras-parameters"></a>Parâmetros adicionais
Dados arbitrários podem ser anexados tooan evento, um erro, uma atividade ou um trabalho. Esses dados podem ser estruturados usando um dicionário. Chaves e valores podem ser de qualquer tipo.

Dados extras são serializados para que tooinsert seu próprio tipo de extras você ter se tooadd um contrato de dados para este tipo.

### <a name="example"></a>Exemplo
Criamos uma nova classe "Person".

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Em seguida, adicionaremos um `Person` tooan de instância extra.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Se você colocar outros tipos de objetos, verifique se que o método ToString () é implementado tooreturn uma cadeia de caracteres legível humana.
> 
> 

### <a name="limits"></a>limites
#### <a name="keys"></a>simétricas
Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="size"></a>Tamanho
Extras são muito limitadas**1024** caracteres por chamada.

## <a name="reporting-application-information"></a>Relatório de informações de aplicativo
### <a name="reference"></a>Referência
            void SendAppInfo(Dictionary<object, object> appInfos)

Manualmente, você pode relatar informações (ou quaisquer outras informações específicas do aplicativo) usando a função de SendAppInfo() hello de controle.

Observe que esses dados podem ser enviados de forma incremental: somente Olá valor mais recente para uma determinada chave será mantido para um determinado dispositivo. Como o evento extras, usar um dicionário\<objeto, objeto\> tooattach dados.

### <a name="example"></a>Exemplo
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Limites
#### <a name="keys"></a>simétricas
Cada chave no objeto de saudação deve corresponder Olá expressão regular a seguir:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Isso significa que as chaves devem começar com pelo menos uma letra, seguida por letras, dígitos ou sublinhados (\_).

#### <a name="size"></a>Tamanho
Informações do aplicativo são muito limitadas**1024** caracteres por chamada.

Em Olá o exemplo anterior, Olá JSON enviado toohello server é 44 caracteres:

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a>Registro em log
### <a name="enable-logging"></a>Habilitar registro em log
Olá SDK pode ser configurado tooproduce logs de teste no console do IDE hello.
Esses logs não são ativados por padrão. toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

