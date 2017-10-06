---
title: "gatilhos de aplicativo de API do serviço de aaaApp | Microsoft Docs"
description: "Como tooimplement dispara no App API no serviço de aplicativo do Azure"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Gatilhos de aplicativo de API do Serviço de Aplicativo do Azure
> [!NOTE]
> Nesta versão do artigo Olá aplica-se a versão do esquema tooAPI aplicativos 2014-12-01-preview.
>
>

## <a name="overview"></a>Visão geral
Este artigo explica como o aplicativo tooimplement API dispara e consumi-los em um aplicativo lógico.

Todos os trechos de código Olá neste tópico são copiados do hello [exemplo de código do aplicativo de API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Observe que você precisará Olá toodownload pacote nuget para o código de saudação em toobuild este artigo a seguir e execute: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>O que são gatilhos de aplicativo de API?
É um cenário comum para um aplicativo de API toofire um evento para que os clientes do aplicativo de API de saudação podem tomar as devidas providências de saudação no evento de toohello de resposta. Olá mecanismo baseados na API de REST que dá suporte a esse cenário é chamado de um gatilho de aplicativo de API.

Por exemplo, digamos que seu código de cliente está usando Olá [aplicativo de API do conector do Twitter](../connectors/connectors-create-api-twitter.md) e seu código precisa tooperform uma ação com base no novo tweets que contêm palavras específicas. Nesse caso, você pode configurar um toofacilitate de gatilho sondagem ou envio por push essa necessidade.

## <a name="poll-trigger-versus-push-trigger"></a>Gatilho de sondagem versus gatilho de envio
Atualmente, há suporte para dois tipos de gatilhos:

* Gatilho de sondagem - cliente sonda saudação do aplicativo de API para notificação de um evento ter sido disparado
* Gatilho push - o cliente é notificado por aplicativo hello API quando um evento é acionado

### <a name="poll-trigger"></a>Gatilho de sondagem
Um gatilho de sondagem é implementado como uma API REST regular e espera que seu toopoll clientes (como um aplicativo de lógica) na notificação de tooget de ordem. Enquanto o cliente Olá pode manter o estado, o gatilho de sondagem de Olá em si é sem monitoração de estado.

Olá informações sobre pacotes de solicitação e resposta de saudação a seguir ilustra alguns aspectos fundamentais de contrato de gatilho de sondagem hello:

* Solicitação
  * Método HTTP: GET
  * parâmetros
    * triggerState - este parâmetro opcional permite que os clientes toospecify seu estado para que Olá gatilho sondagem corretamente pode decidir se notificação tooreturn ou não com base em hello especificado estado.
    * Parâmetros específicos de API
* Resposta
  * Código de status **200** - solicitação é válida e se houver uma notificação de disparador hello. conteúdo de saudação da notificação de saudação será corpo da resposta hello. Um cabeçalho "Retry-After" em resposta Olá indica que os dados de notificação adicionais devem ser recuperados com uma chamada de solicitação subsequente.
  * Código de status **202** - a solicitação é válida, mas não há nenhuma nova notificação de gatilho de saudação.
  * Código de status **4xx** - a solicitação não é válida. cliente de saudação não deve tentar novamente a solicitação de saudação.
  * Código de status **5xx** - a solicitação resultou em um erro interno do servidor e/ou em um problema temporário. cliente Olá deve tentar novamente a solicitação de saudação.

saudação de trecho de código a seguir é um exemplo de como tooimplement uma sondagem disparar.

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

tootest esta pesquisa disparar, siga estas etapas:

1. Implantar Olá API aplicativo com uma configuração de autenticação de **público anônimo**.
2. Chamar hello **touch** operação tootouch um arquivo. Olá a imagem a seguir mostra um exemplo de solicitação por meio de carteiro.
   ![Operação de toque de chamada via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Chamar o gatilho de sondagem de saudação com hello **triggerState** parâmetro definido tooStep anterior de carimbo de data / hora da tooa #2. Olá imagem a seguir mostra exemplo de solicitação Olá via carteiro.
   ![Gatilho de sondagem de chamada via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Gatilho de push
Um disparador de envio é implementado como uma API REST regular que envia tooclients de notificações que se inscreveram toobe notificado quando eventos específicos.

Olá informações sobre pacotes de solicitação e resposta de saudação a seguir ilustra alguns aspectos fundamentais de contrato de gatilho de push hello.

* Solicitação
  * Método HTTP: PUT
  * parâmetros
    * triggerId: necessária - opaco de cadeia de caracteres (como um GUID) que representa Olá o registro de um disparador de envio.
    * callbackUrl: necessária - URL da saudação tooinvoke de retorno de chamada quando Olá evento é acionado. invocação de saudação é uma chamada POST HTTP simples.
    * Parâmetros específicos de API
* Resposta
  * Código de status **200** -solicitação tooregister cliente com êxito.
  * Código de status **4xx** - a solicitação não é válida. cliente de saudação não deve tentar novamente a solicitação de saudação.
  * Código de status **5xx** - a solicitação resultou em um erro interno do servidor e/ou em um problema temporário. cliente Olá deve tentar novamente a solicitação de saudação.
* Callback
  * Método HTTP: POST
  * Corpo da solicitação: conteúdo da notificação.

saudação de trecho de código a seguir é um exemplo de como disparar o tooimplement um envio por push:

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

tootest esta pesquisa disparar, siga estas etapas:

1. Implantar Olá API aplicativo com uma configuração de autenticação de **público anônimo**.
2. Procurar muito[http://requestb.in/](http://requestb.in/) toocreate um RequestBin que servirá como a URL de retorno de chamada.
3. Chame o disparador de envio de saudação com um GUID como **triggerId** e Olá RequestBin URL como **callbackUrl**.
   ![Gatilho de push de chamada via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Chamar hello **touch** operação tootouch um arquivo. Olá a imagem a seguir mostra um exemplo de solicitação por meio de carteiro.
   ![Operação de toque de chamada via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Seleção Olá RequestBin tooconfirm que Olá disparador de envio de retorno de chamada é invocado com a saída de propriedade.
   ![Gatilho de sondagem de chamada via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Descrever gatilhos na definição de API
Após implementar gatilhos hello e implantar seu tooAzure do aplicativo de API, navegue toohello **de definição de API** folha no portal de visualização do Azure hello e você verá que gatilhos são reconhecidos automaticamente no hello da interface do usuário, que é controlada por Olá definição Swagger 2.0 API do aplicativo hello API.

![Folha Definição de API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Se você clicar em Olá **baixar Swagger** botão e arquivo JSON de saudação aberta, você verá resultados toohello semelhante a seguir:

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

Olá a propriedade de extensão **x-ms-da programação-o gatilho** é como os gatilhos são descritos na definição de API e é adicionada automaticamente pelo gateway de aplicativo hello API quando você solicitar definição Olá API por meio do gateway de saudação se Olá solicitação tooone de Olá critérios a seguir. (Você pode também adicionar essa propriedade manualmente.)

* Gatilho de sondagem
  * Se for Olá método HTTP **obter**.
  * Se hello **operationId** propriedade contém a cadeia de caracteres hello **gatilho**.
  * Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida muito**triggerState**.
* Gatilho de push
  * Se for Olá método HTTP **colocar**.
  * Se hello **operationId** propriedade contém a cadeia de caracteres hello **gatilho**.
  * Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida muito**triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Usar gatilhos de aplicativo de API em aplicativos lógicos
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Listar e configurar os gatilhos de aplicativo de API no designer de aplicativos de lógica de saudação
Se você criar um aplicativo de lógica em Olá Olá de mesmo grupo de recursos do aplicativo de API, você será capaz de tooadd-tela do designer toohello simplesmente clicando nele. Olá imagens a seguir ilustra isso:

![Gatilhos no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurar o Gatilho de Sondagem no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurar o Gatilho de Push no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Otimizar gatilhos de aplicativo de API para aplicativos lógicos
Depois de adicionar gatilhos tooan API do aplicativo, há algumas coisas que você pode fazer a experiência de saudação tooimprove ao usar o aplicativo hello API em um aplicativo de lógica.

Por exemplo, Olá **triggerState** parâmetro gatilhos de sondagem deve ser definido como toohello expressão no aplicativo do hello lógica a seguir. Essa expressão deve avaliar a última chamada de saudação do gatilho de saudação do aplicativo de lógica de saudação e retornará o valor.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Observação: Para obter uma explicação das funções hello usado na expressão de saudação acima, consulte documentação toohello em [lógica de linguagem de definição de fluxo de trabalho de aplicativo](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Os usuários do aplicativo lógica precisará expressão de saudação tooprovide acima para Olá **triggerState** parâmetro ao usar o gatilho de saudação. É possível toohave esse valor predefinido pelo designer de aplicativo hello lógica por meio da propriedade de extensão Olá **x-ms-Agendador-recomendação**.  Olá **x-ms-visibilidade** propriedade de extensão pode ser definida como valor tooa *interno* para que o parâmetro hello em si não é exibido no designer de saudação.  saudação de trecho de código a seguir ilustra que.

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

Gatilhos de envio, Olá **triggerId** parâmetro deve identificar exclusivamente o aplicativo de lógica de saudação. Uma prática recomendada é tooset o nome da propriedade toohello de fluxo de trabalho hello usando Olá a expressão a seguir:

    @workflow().name

Usando Olá **x-ms-Agendador-recomendação** e **x-ms-visibilidade** propriedades de extensão em sua definição de API, Olá aplicativo de API podem transmitir toohello lógica aplicativo designer tooautomatically definir isso expressão de usuário hello.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Adicionar propriedades de extensão na definição de API
Informações de metadados adicionais - como propriedades de extensão Olá **x-ms-Agendador-recomendação** e **x-ms-visibilidade** -podem ser adicionados na definição Olá API em uma das duas maneiras: estática ou dinâmica.

Para obter metadados estático, você pode editar diretamente o hello */metadata/apiDefinition.swagger.json* arquivo em seu projeto e adicionar propriedades de saudação manualmente.

Para aplicativos de API usando metadados dinâmico, você pode editar Olá SwaggerConfig.cs arquivo tooadd um filtro de operação que pode adicionar essas extensões.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


a seguir Olá é um exemplo de como essa classe pode ser o cenário de metadados dinâmico Olá toofacilitate implementado.

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
