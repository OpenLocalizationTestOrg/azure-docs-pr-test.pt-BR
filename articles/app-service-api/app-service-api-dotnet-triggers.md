---
title: "Gatilhos de aplicativo de API do Serviço de Aplicativo | Microsoft Docs"
description: "Como implementar gatilhos em um aplicativo de API no Serviço de Aplicativo do Azure"
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
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="d9622-103">Gatilhos de aplicativo de API do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="d9622-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="d9622-104">Esta versão do artigo se aplica à versão do esquema 2014-12-01-preview de aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="d9622-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="d9622-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d9622-105">Overview</span></span>
<span data-ttu-id="d9622-106">Este artigo explica como implementar gatilhos de aplicativo de API e consumi-los por meio de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d9622-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="d9622-107">Todos os trechos de código mostrados neste tópico foram copiados do [exemplo de código do aplicativo de API do FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="d9622-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="d9622-108">Observe que você precisará baixar o seguinte pacote do nuget para que o código neste artigo seja compilado e executado: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="d9622-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="d9622-109">O que são gatilhos de aplicativo de API?</span><span class="sxs-lookup"><span data-stu-id="d9622-109">What are API app triggers?</span></span>
<span data-ttu-id="d9622-110">É um cenário comum para um aplicativo de API disparar um evento para que os clientes do aplicativo de API possam realizar a ação apropriada em resposta ao evento.</span><span class="sxs-lookup"><span data-stu-id="d9622-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="d9622-111">O mecanismo baseado em API REST que oferece suporte a esse cenário é chamado de gatilho de aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="d9622-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="d9622-112">Por exemplo, digamos que seu código de cliente está usando o [Aplicativo de API para conexão ao Twitter](../connectors/connectors-create-api-twitter.md) e seu código precisa executar uma ação com base em novos tweets que contêm palavras específicas.</span><span class="sxs-lookup"><span data-stu-id="d9622-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="d9622-113">Nesse caso, você pode definir um gatilho de sondagem ou de envio por push para facilitar essa necessidade.</span><span class="sxs-lookup"><span data-stu-id="d9622-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="d9622-114">Gatilho de sondagem versus gatilho de envio</span><span class="sxs-lookup"><span data-stu-id="d9622-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="d9622-115">Atualmente, há suporte para dois tipos de gatilhos:</span><span class="sxs-lookup"><span data-stu-id="d9622-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="d9622-116">Gatilho de sondagem - o cliente faz a sondagem no aplicativo de API buscando notificação de um determinado evento ter sido acionado</span><span class="sxs-lookup"><span data-stu-id="d9622-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="d9622-117">Disparador de envio - o cliente é notificado pelo aplicativo API quando um evento é acionado</span><span class="sxs-lookup"><span data-stu-id="d9622-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="d9622-118">Gatilho de sondagem</span><span class="sxs-lookup"><span data-stu-id="d9622-118">Poll trigger</span></span>
<span data-ttu-id="d9622-119">Um gatilho de sondagem é implementado como uma API REST regular e espera que seus clientes (por exemplo, um aplicativo lógico) consultem-no para obter notificações.</span><span class="sxs-lookup"><span data-stu-id="d9622-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="d9622-120">Enquanto o cliente pode manter o estado, o gatilho de sondagem em si é sem estado.</span><span class="sxs-lookup"><span data-stu-id="d9622-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="d9622-121">As informações sobre os pacotes de solicitação e resposta a seguir ilustram alguns aspectos fundamentais do contrato de gatilho de sondagem.</span><span class="sxs-lookup"><span data-stu-id="d9622-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="d9622-122">Solicitação</span><span class="sxs-lookup"><span data-stu-id="d9622-122">Request</span></span>
  * <span data-ttu-id="d9622-123">Método HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="d9622-123">HTTP method: GET</span></span>
  * <span data-ttu-id="d9622-124">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d9622-124">Parameters</span></span>
    * <span data-ttu-id="d9622-125">triggerState - esse parâmetro opcional permite que os clientes especifiquem seu estado para que o gatilho de sondagem possa decidir corretamente se deseja retornar ou não a notificação com base no estado especificado.</span><span class="sxs-lookup"><span data-stu-id="d9622-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="d9622-126">Parâmetros específicos de API</span><span class="sxs-lookup"><span data-stu-id="d9622-126">API-specific parameters</span></span>
* <span data-ttu-id="d9622-127">Resposta</span><span class="sxs-lookup"><span data-stu-id="d9622-127">Response</span></span>
  * <span data-ttu-id="d9622-128">Código de status **200** - a solicitação é válida e há uma notificação do gatilho.</span><span class="sxs-lookup"><span data-stu-id="d9622-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="d9622-129">O conteúdo da notificação será o corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="d9622-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="d9622-130">Um cabeçalho de "Tente novamente após" na resposta indica que os dados de notificação adicionais devem ser recuperados com uma chamada de solicitação subsequente.</span><span class="sxs-lookup"><span data-stu-id="d9622-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="d9622-131">Código de status **202** - a solicitação é válida, mas não há uma nova notificação do gatilho.</span><span class="sxs-lookup"><span data-stu-id="d9622-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="d9622-132">Código de status **4xx** - a solicitação não é válida.</span><span class="sxs-lookup"><span data-stu-id="d9622-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="d9622-133">O cliente não deve tentar solicitar novamente.</span><span class="sxs-lookup"><span data-stu-id="d9622-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="d9622-134">Código de status **5xx** - a solicitação resultou em um erro interno do servidor e/ou em um problema temporário.</span><span class="sxs-lookup"><span data-stu-id="d9622-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="d9622-135">O cliente deve tentar solicitar novamente.</span><span class="sxs-lookup"><span data-stu-id="d9622-135">The client should retry the request.</span></span>

<span data-ttu-id="d9622-136">O trecho de código a seguir é um exemplo de como implementar um gatilho de sondagem.</span><span class="sxs-lookup"><span data-stu-id="d9622-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="d9622-137">Para testar esse gatilho de sondagem, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d9622-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="d9622-138">Implante o Aplicativo de API com uma configuração de autenticação **Público (anônimo)**.</span><span class="sxs-lookup"><span data-stu-id="d9622-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="d9622-139">Chame a operação **touch** para tocar em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="d9622-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="d9622-140">A imagem a seguir mostra um exemplo de solicitação via Postman.</span><span class="sxs-lookup"><span data-stu-id="d9622-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="d9622-141">![Operação de toque de chamada via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="d9622-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="d9622-142">Chame o gatilho de sondagem com o parâmetro **triggerState** definido como um carimbo de data/hora antes da etapa 2.</span><span class="sxs-lookup"><span data-stu-id="d9622-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="d9622-143">A imagem a seguir mostra o exemplo de solicitação via Postman.</span><span class="sxs-lookup"><span data-stu-id="d9622-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="d9622-144">![Gatilho de sondagem de chamada via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="d9622-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="d9622-145">Gatilho de push</span><span class="sxs-lookup"><span data-stu-id="d9622-145">Push trigger</span></span>
<span data-ttu-id="d9622-146">Um gatilho de push é implementado como uma API REST regular que envia notificações para clientes que se inscreveram para serem notificados quando eventos específicos forem disparados.</span><span class="sxs-lookup"><span data-stu-id="d9622-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="d9622-147">As informações a seguir sobre os pacotes de solicitação e resposta ilustram alguns aspectos fundamentais do contrato de gatilho de push:</span><span class="sxs-lookup"><span data-stu-id="d9622-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="d9622-148">Solicitação</span><span class="sxs-lookup"><span data-stu-id="d9622-148">Request</span></span>
  * <span data-ttu-id="d9622-149">Método HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="d9622-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="d9622-150">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d9622-150">Parameters</span></span>
    * <span data-ttu-id="d9622-151">triggerId: requerida - cadeia de caracteres opaca (como uma GUID) que representa o registro de um gatilho de push.</span><span class="sxs-lookup"><span data-stu-id="d9622-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="d9622-152">callbackUrl: requerida - URL do retorno de chamada a ser invocado quando o evento for acionado.</span><span class="sxs-lookup"><span data-stu-id="d9622-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="d9622-153">A chamada é uma chamada simples do HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d9622-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="d9622-154">Parâmetros específicos de API</span><span class="sxs-lookup"><span data-stu-id="d9622-154">API-specific parameters</span></span>
* <span data-ttu-id="d9622-155">Resposta</span><span class="sxs-lookup"><span data-stu-id="d9622-155">Response</span></span>
  * <span data-ttu-id="d9622-156">Código de status **200** - solicitação para registrar o cliente bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d9622-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="d9622-157">Código de status **4xx** - a solicitação não é válida.</span><span class="sxs-lookup"><span data-stu-id="d9622-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="d9622-158">O cliente não deve tentar solicitar novamente.</span><span class="sxs-lookup"><span data-stu-id="d9622-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="d9622-159">Código de status **5xx** - a solicitação resultou em um erro interno do servidor e/ou em um problema temporário.</span><span class="sxs-lookup"><span data-stu-id="d9622-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="d9622-160">O cliente deve tentar solicitar novamente.</span><span class="sxs-lookup"><span data-stu-id="d9622-160">The client should retry the request.</span></span>
* <span data-ttu-id="d9622-161">Callback</span><span class="sxs-lookup"><span data-stu-id="d9622-161">Callback</span></span>
  * <span data-ttu-id="d9622-162">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="d9622-162">HTTP method: POST</span></span>
  * <span data-ttu-id="d9622-163">Corpo da solicitação: conteúdo da notificação.</span><span class="sxs-lookup"><span data-stu-id="d9622-163">Request body: Notification content.</span></span>

<span data-ttu-id="d9622-164">O trecho de código a seguir é um exemplo de como implementar um gatilho de push:</span><span class="sxs-lookup"><span data-stu-id="d9622-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
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
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="d9622-165">Para testar esse gatilho de sondagem, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d9622-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="d9622-166">Implante o Aplicativo de API com uma configuração de autenticação **Público (anônimo)**.</span><span class="sxs-lookup"><span data-stu-id="d9622-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="d9622-167">Navegue até [http://requestb.in/](http://requestb.in/) para criar um RequestBin que servirá como sua URL de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="d9622-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="d9622-168">Chame o gatilho de envio com uma GUID como **triggerId** e a URL RequestBin como **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="d9622-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="d9622-169">![Gatilho de push de chamada via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="d9622-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="d9622-170">Chame a operação **touch** para tocar em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="d9622-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="d9622-171">A imagem a seguir mostra um exemplo de solicitação via Postman.</span><span class="sxs-lookup"><span data-stu-id="d9622-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="d9622-172">![Operação de toque de chamada via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="d9622-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="d9622-173">Verifique o RequestBin para confirmar que o retorno de chamada do gatilho de push é invocado com a saída da propriedade.</span><span class="sxs-lookup"><span data-stu-id="d9622-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="d9622-174">![Gatilho de sondagem de chamada via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="d9622-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="d9622-175">Descrever gatilhos na definição de API</span><span class="sxs-lookup"><span data-stu-id="d9622-175">Describe triggers in API definition</span></span>
<span data-ttu-id="d9622-176">Depois de implementar os gatilhos e implantar seu aplicativo de API no Azure, navegue até a folha **definição API** no portal de visualização do Azure e você verá que os gatilhos são reconhecidos automaticamente na interface do usuário, que é orientada pela definição de API Swagger 2.0 do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="d9622-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![Folha Definição de API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="d9622-178">Se você clicar no botão **Baixar Swagger** e abrir o arquivo JSON, você verá resultados semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="d9622-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

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

<span data-ttu-id="d9622-179">A propriedade de extensão **x-ms-schedular-trigger** é como os gatilhos são descritos na definição de API, e é adicionada automaticamente pelo gateway de aplicativo de API quando você solicita a definição de API por meio do gateway se a solicitação corresponde a um dos critérios a seguir.</span><span class="sxs-lookup"><span data-stu-id="d9622-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="d9622-180">(Você pode também adicionar essa propriedade manualmente.)</span><span class="sxs-lookup"><span data-stu-id="d9622-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="d9622-181">Gatilho de sondagem</span><span class="sxs-lookup"><span data-stu-id="d9622-181">Poll trigger</span></span>
  * <span data-ttu-id="d9622-182">Se o método HTTP é **GET**.</span><span class="sxs-lookup"><span data-stu-id="d9622-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="d9622-183">Se a propriedade **operationId** contém a cadeia de caracteres **trigger**.</span><span class="sxs-lookup"><span data-stu-id="d9622-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="d9622-184">Se a propriedade **parameters** inclui um parâmetro com uma propriedade **name** definida como **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="d9622-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="d9622-185">Gatilho de push</span><span class="sxs-lookup"><span data-stu-id="d9622-185">Push trigger</span></span>
  * <span data-ttu-id="d9622-186">Se o método HTTP é **PUT**.</span><span class="sxs-lookup"><span data-stu-id="d9622-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="d9622-187">Se a propriedade **operationId** contém a cadeia de caracteres **trigger**.</span><span class="sxs-lookup"><span data-stu-id="d9622-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="d9622-188">Se a propriedade **parameters** inclui um parâmetro com uma propriedade **name** definida como **triggerId**.</span><span class="sxs-lookup"><span data-stu-id="d9622-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="d9622-189">Usar gatilhos de aplicativo de API em aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="d9622-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="d9622-190">Listar e configurar gatilhos de aplicativo de API no designer de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="d9622-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="d9622-191">Se você criar um aplicativo lógico no mesmo grupo de recursos que o aplicativo de API, você poderá adicioná-la à tela do designer simplesmente clicando nele.</span><span class="sxs-lookup"><span data-stu-id="d9622-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="d9622-192">As imagens a seguir ilustram isso:</span><span class="sxs-lookup"><span data-stu-id="d9622-192">The following images illustrate this:</span></span>

![Gatilhos no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurar o Gatilho de Sondagem no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurar o Gatilho de Push no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="d9622-196">Otimizar gatilhos de aplicativo de API para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="d9622-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="d9622-197">Depois de adicionar gatilhos a um aplicativo de API, há algumas coisas que você pode fazer para melhorar a experiência ao usar o aplicativo de API em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d9622-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="d9622-198">Por exemplo, o parâmetro **triggerState** para gatilhos sondagem deve ser definido como a expressão a seguir no aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d9622-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="d9622-199">Essa expressão deve avaliar a última chamada do gatilho pelo aplicativo lógico e retornar esse valor.</span><span class="sxs-lookup"><span data-stu-id="d9622-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="d9622-200">OBSERVAÇÃO: Para obter uma explicação das funções usadas na expressão acima, consulte a documentação sobre [Linguagem de definição de fluxo de trabalho de aplicativos lógicos](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9622-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="d9622-201">Os usuários de aplicativos lógicos precisariam fornecer a expressão acima para o parâmetro **triggerState** ao usar o gatilho.</span><span class="sxs-lookup"><span data-stu-id="d9622-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="d9622-202">É possível fazer com que esse valor seja predefinido pelo designer do aplicativo lógico por meio da propriedade de extensão **x-ms-scheduler-recommendation**.</span><span class="sxs-lookup"><span data-stu-id="d9622-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="d9622-203">A propriedade de extensão **x-ms-visibility** pode ser definida com o um valor *internal* para que o parâmetro em si não seja exibido no designer.</span><span class="sxs-lookup"><span data-stu-id="d9622-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="d9622-204">O trecho de código a seguir ilustra isso.</span><span class="sxs-lookup"><span data-stu-id="d9622-204">The following snippet illustrates that.</span></span>

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

<span data-ttu-id="d9622-205">Para gatilhos de envio, o parâmetro **triggerId** deve identificar o aplicativo lógico de modo único.</span><span class="sxs-lookup"><span data-stu-id="d9622-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="d9622-206">Uma prática recomendada é definir essa propriedade como o nome do fluxo de trabalho, usando a seguinte expressão:</span><span class="sxs-lookup"><span data-stu-id="d9622-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="d9622-207">Usando as propriedades de extensão **x-ms-scheduler-recommendation** e **x-ms-visibility** em sua definição de API, o aplicativo de API pode transmitir ao designer de aplicativos lógicos uma instrução para definir automaticamente essa expressão para o usuário.</span><span class="sxs-lookup"><span data-stu-id="d9622-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="d9622-208">Adicionar propriedades de extensão na definição de API</span><span class="sxs-lookup"><span data-stu-id="d9622-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="d9622-209">Informações adicionais de metadados – como as propriedades de extensão **x-ms-scheduler-recommendation** e **x-ms-visibility** -podem ser adicionadas à definição de API de dois modos: estáticos ou dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="d9622-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="d9622-210">Para metadados estáticos, você pode editar diretamente o arquivo */metadata/apiDefinition.swagger.json* em seu projeto e adicionar as propriedades manualmente.</span><span class="sxs-lookup"><span data-stu-id="d9622-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="d9622-211">Para aplicativos de API usando metadados dinâmicos, você pode editar o arquivo SwaggerConfig.cs para adicionar um filtro de operação que possa adicionar essas extensões.</span><span class="sxs-lookup"><span data-stu-id="d9622-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="d9622-212">Este é um exemplo de como essa classe pode ser implementada para facilitar o cenário de metadados dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="d9622-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
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
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
