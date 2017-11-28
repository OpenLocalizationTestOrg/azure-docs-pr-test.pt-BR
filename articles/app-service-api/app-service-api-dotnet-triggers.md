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
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="43a00-103">Gatilhos de aplicativo de API do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="43a00-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="43a00-104">Nesta versão do artigo Olá aplica-se a versão do esquema tooAPI aplicativos 2014-12-01-preview.</span><span class="sxs-lookup"><span data-stu-id="43a00-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="43a00-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="43a00-105">Overview</span></span>
<span data-ttu-id="43a00-106">Este artigo explica como o aplicativo tooimplement API dispara e consumi-los em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="43a00-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="43a00-107">Todos os trechos de código Olá neste tópico são copiados do hello [exemplo de código do aplicativo de API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="43a00-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="43a00-108">Observe que você precisará Olá toodownload pacote nuget para o código de saudação em toobuild este artigo a seguir e execute: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="43a00-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="43a00-109">O que são gatilhos de aplicativo de API?</span><span class="sxs-lookup"><span data-stu-id="43a00-109">What are API app triggers?</span></span>
<span data-ttu-id="43a00-110">É um cenário comum para um aplicativo de API toofire um evento para que os clientes do aplicativo de API de saudação podem tomar as devidas providências de saudação no evento de toohello de resposta.</span><span class="sxs-lookup"><span data-stu-id="43a00-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="43a00-111">Olá mecanismo baseados na API de REST que dá suporte a esse cenário é chamado de um gatilho de aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a00-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="43a00-112">Por exemplo, digamos que seu código de cliente está usando Olá [aplicativo de API do conector do Twitter](../connectors/connectors-create-api-twitter.md) e seu código precisa tooperform uma ação com base no novo tweets que contêm palavras específicas.</span><span class="sxs-lookup"><span data-stu-id="43a00-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="43a00-113">Nesse caso, você pode configurar um toofacilitate de gatilho sondagem ou envio por push essa necessidade.</span><span class="sxs-lookup"><span data-stu-id="43a00-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="43a00-114">Gatilho de sondagem versus gatilho de envio</span><span class="sxs-lookup"><span data-stu-id="43a00-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="43a00-115">Atualmente, há suporte para dois tipos de gatilhos:</span><span class="sxs-lookup"><span data-stu-id="43a00-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="43a00-116">Gatilho de sondagem - cliente sonda saudação do aplicativo de API para notificação de um evento ter sido disparado</span><span class="sxs-lookup"><span data-stu-id="43a00-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="43a00-117">Gatilho push - o cliente é notificado por aplicativo hello API quando um evento é acionado</span><span class="sxs-lookup"><span data-stu-id="43a00-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="43a00-118">Gatilho de sondagem</span><span class="sxs-lookup"><span data-stu-id="43a00-118">Poll trigger</span></span>
<span data-ttu-id="43a00-119">Um gatilho de sondagem é implementado como uma API REST regular e espera que seu toopoll clientes (como um aplicativo de lógica) na notificação de tooget de ordem.</span><span class="sxs-lookup"><span data-stu-id="43a00-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="43a00-120">Enquanto o cliente Olá pode manter o estado, o gatilho de sondagem de Olá em si é sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="43a00-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="43a00-121">Olá informações sobre pacotes de solicitação e resposta de saudação a seguir ilustra alguns aspectos fundamentais de contrato de gatilho de sondagem hello:</span><span class="sxs-lookup"><span data-stu-id="43a00-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="43a00-122">Solicitação</span><span class="sxs-lookup"><span data-stu-id="43a00-122">Request</span></span>
  * <span data-ttu-id="43a00-123">Método HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="43a00-123">HTTP method: GET</span></span>
  * <span data-ttu-id="43a00-124">parâmetros</span><span class="sxs-lookup"><span data-stu-id="43a00-124">Parameters</span></span>
    * <span data-ttu-id="43a00-125">triggerState - este parâmetro opcional permite que os clientes toospecify seu estado para que Olá gatilho sondagem corretamente pode decidir se notificação tooreturn ou não com base em hello especificado estado.</span><span class="sxs-lookup"><span data-stu-id="43a00-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="43a00-126">Parâmetros específicos de API</span><span class="sxs-lookup"><span data-stu-id="43a00-126">API-specific parameters</span></span>
* <span data-ttu-id="43a00-127">Resposta</span><span class="sxs-lookup"><span data-stu-id="43a00-127">Response</span></span>
  * <span data-ttu-id="43a00-128">Código de status **200** - solicitação é válida e se houver uma notificação de disparador hello.</span><span class="sxs-lookup"><span data-stu-id="43a00-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="43a00-129">conteúdo de saudação da notificação de saudação será corpo da resposta hello.</span><span class="sxs-lookup"><span data-stu-id="43a00-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="43a00-130">Um cabeçalho "Retry-After" em resposta Olá indica que os dados de notificação adicionais devem ser recuperados com uma chamada de solicitação subsequente.</span><span class="sxs-lookup"><span data-stu-id="43a00-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="43a00-131">Código de status **202** - a solicitação é válida, mas não há nenhuma nova notificação de gatilho de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="43a00-132">Código de status **4xx** - a solicitação não é válida.</span><span class="sxs-lookup"><span data-stu-id="43a00-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="43a00-133">cliente de saudação não deve tentar novamente a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="43a00-134">Código de status **5xx** - a solicitação resultou em um erro interno do servidor e/ou em um problema temporário.</span><span class="sxs-lookup"><span data-stu-id="43a00-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="43a00-135">cliente Olá deve tentar novamente a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-135">hello client should retry hello request.</span></span>

<span data-ttu-id="43a00-136">saudação de trecho de código a seguir é um exemplo de como tooimplement uma sondagem disparar.</span><span class="sxs-lookup"><span data-stu-id="43a00-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

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

<span data-ttu-id="43a00-137">tootest esta pesquisa disparar, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="43a00-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="43a00-138">Implantar Olá API aplicativo com uma configuração de autenticação de **público anônimo**.</span><span class="sxs-lookup"><span data-stu-id="43a00-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="43a00-139">Chamar hello **touch** operação tootouch um arquivo.</span><span class="sxs-lookup"><span data-stu-id="43a00-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="43a00-140">Olá a imagem a seguir mostra um exemplo de solicitação por meio de carteiro.</span><span class="sxs-lookup"><span data-stu-id="43a00-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="43a00-141">![Operação de toque de chamada via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="43a00-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="43a00-142">Chamar o gatilho de sondagem de saudação com hello **triggerState** parâmetro definido tooStep anterior de carimbo de data / hora da tooa #2.</span><span class="sxs-lookup"><span data-stu-id="43a00-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="43a00-143">Olá imagem a seguir mostra exemplo de solicitação Olá via carteiro.</span><span class="sxs-lookup"><span data-stu-id="43a00-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="43a00-144">![Gatilho de sondagem de chamada via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="43a00-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="43a00-145">Gatilho de push</span><span class="sxs-lookup"><span data-stu-id="43a00-145">Push trigger</span></span>
<span data-ttu-id="43a00-146">Um disparador de envio é implementado como uma API REST regular que envia tooclients de notificações que se inscreveram toobe notificado quando eventos específicos.</span><span class="sxs-lookup"><span data-stu-id="43a00-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="43a00-147">Olá informações sobre pacotes de solicitação e resposta de saudação a seguir ilustra alguns aspectos fundamentais de contrato de gatilho de push hello.</span><span class="sxs-lookup"><span data-stu-id="43a00-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="43a00-148">Solicitação</span><span class="sxs-lookup"><span data-stu-id="43a00-148">Request</span></span>
  * <span data-ttu-id="43a00-149">Método HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="43a00-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="43a00-150">parâmetros</span><span class="sxs-lookup"><span data-stu-id="43a00-150">Parameters</span></span>
    * <span data-ttu-id="43a00-151">triggerId: necessária - opaco de cadeia de caracteres (como um GUID) que representa Olá o registro de um disparador de envio.</span><span class="sxs-lookup"><span data-stu-id="43a00-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="43a00-152">callbackUrl: necessária - URL da saudação tooinvoke de retorno de chamada quando Olá evento é acionado.</span><span class="sxs-lookup"><span data-stu-id="43a00-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="43a00-153">invocação de saudação é uma chamada POST HTTP simples.</span><span class="sxs-lookup"><span data-stu-id="43a00-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="43a00-154">Parâmetros específicos de API</span><span class="sxs-lookup"><span data-stu-id="43a00-154">API-specific parameters</span></span>
* <span data-ttu-id="43a00-155">Resposta</span><span class="sxs-lookup"><span data-stu-id="43a00-155">Response</span></span>
  * <span data-ttu-id="43a00-156">Código de status **200** -solicitação tooregister cliente com êxito.</span><span class="sxs-lookup"><span data-stu-id="43a00-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="43a00-157">Código de status **4xx** - a solicitação não é válida.</span><span class="sxs-lookup"><span data-stu-id="43a00-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="43a00-158">cliente de saudação não deve tentar novamente a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="43a00-159">Código de status **5xx** - a solicitação resultou em um erro interno do servidor e/ou em um problema temporário.</span><span class="sxs-lookup"><span data-stu-id="43a00-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="43a00-160">cliente Olá deve tentar novamente a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="43a00-161">Callback</span><span class="sxs-lookup"><span data-stu-id="43a00-161">Callback</span></span>
  * <span data-ttu-id="43a00-162">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="43a00-162">HTTP method: POST</span></span>
  * <span data-ttu-id="43a00-163">Corpo da solicitação: conteúdo da notificação.</span><span class="sxs-lookup"><span data-stu-id="43a00-163">Request body: Notification content.</span></span>

<span data-ttu-id="43a00-164">saudação de trecho de código a seguir é um exemplo de como disparar o tooimplement um envio por push:</span><span class="sxs-lookup"><span data-stu-id="43a00-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

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

<span data-ttu-id="43a00-165">tootest esta pesquisa disparar, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="43a00-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="43a00-166">Implantar Olá API aplicativo com uma configuração de autenticação de **público anônimo**.</span><span class="sxs-lookup"><span data-stu-id="43a00-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="43a00-167">Procurar muito[http://requestb.in/](http://requestb.in/) toocreate um RequestBin que servirá como a URL de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="43a00-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="43a00-168">Chame o disparador de envio de saudação com um GUID como **triggerId** e Olá RequestBin URL como **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="43a00-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="43a00-169">![Gatilho de push de chamada via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="43a00-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="43a00-170">Chamar hello **touch** operação tootouch um arquivo.</span><span class="sxs-lookup"><span data-stu-id="43a00-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="43a00-171">Olá a imagem a seguir mostra um exemplo de solicitação por meio de carteiro.</span><span class="sxs-lookup"><span data-stu-id="43a00-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="43a00-172">![Operação de toque de chamada via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="43a00-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="43a00-173">Seleção Olá RequestBin tooconfirm que Olá disparador de envio de retorno de chamada é invocado com a saída de propriedade.</span><span class="sxs-lookup"><span data-stu-id="43a00-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="43a00-174">![Gatilho de sondagem de chamada via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="43a00-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="43a00-175">Descrever gatilhos na definição de API</span><span class="sxs-lookup"><span data-stu-id="43a00-175">Describe triggers in API definition</span></span>
<span data-ttu-id="43a00-176">Após implementar gatilhos hello e implantar seu tooAzure do aplicativo de API, navegue toohello **de definição de API** folha no portal de visualização do Azure hello e você verá que gatilhos são reconhecidos automaticamente no hello da interface do usuário, que é controlada por Olá definição Swagger 2.0 API do aplicativo hello API.</span><span class="sxs-lookup"><span data-stu-id="43a00-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![Folha Definição de API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="43a00-178">Se você clicar em Olá **baixar Swagger** botão e arquivo JSON de saudação aberta, você verá resultados toohello semelhante a seguir:</span><span class="sxs-lookup"><span data-stu-id="43a00-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

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

<span data-ttu-id="43a00-179">Olá a propriedade de extensão **x-ms-da programação-o gatilho** é como os gatilhos são descritos na definição de API e é adicionada automaticamente pelo gateway de aplicativo hello API quando você solicitar definição Olá API por meio do gateway de saudação se Olá solicitação tooone de Olá critérios a seguir.</span><span class="sxs-lookup"><span data-stu-id="43a00-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="43a00-180">(Você pode também adicionar essa propriedade manualmente.)</span><span class="sxs-lookup"><span data-stu-id="43a00-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="43a00-181">Gatilho de sondagem</span><span class="sxs-lookup"><span data-stu-id="43a00-181">Poll trigger</span></span>
  * <span data-ttu-id="43a00-182">Se for Olá método HTTP **obter**.</span><span class="sxs-lookup"><span data-stu-id="43a00-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="43a00-183">Se hello **operationId** propriedade contém a cadeia de caracteres hello **gatilho**.</span><span class="sxs-lookup"><span data-stu-id="43a00-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="43a00-184">Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida muito**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="43a00-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="43a00-185">Gatilho de push</span><span class="sxs-lookup"><span data-stu-id="43a00-185">Push trigger</span></span>
  * <span data-ttu-id="43a00-186">Se for Olá método HTTP **colocar**.</span><span class="sxs-lookup"><span data-stu-id="43a00-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="43a00-187">Se hello **operationId** propriedade contém a cadeia de caracteres hello **gatilho**.</span><span class="sxs-lookup"><span data-stu-id="43a00-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="43a00-188">Se hello **parâmetros** propriedade inclui um parâmetro com um **nome** propriedade definida muito**triggerId**.</span><span class="sxs-lookup"><span data-stu-id="43a00-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="43a00-189">Usar gatilhos de aplicativo de API em aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="43a00-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="43a00-190">Listar e configurar os gatilhos de aplicativo de API no designer de aplicativos de lógica de saudação</span><span class="sxs-lookup"><span data-stu-id="43a00-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="43a00-191">Se você criar um aplicativo de lógica em Olá Olá de mesmo grupo de recursos do aplicativo de API, você será capaz de tooadd-tela do designer toohello simplesmente clicando nele.</span><span class="sxs-lookup"><span data-stu-id="43a00-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="43a00-192">Olá imagens a seguir ilustra isso:</span><span class="sxs-lookup"><span data-stu-id="43a00-192">hello following images illustrate this:</span></span>

![Gatilhos no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurar o Gatilho de Sondagem no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurar o Gatilho de Push no Designer de Aplicativos Lógicos](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="43a00-196">Otimizar gatilhos de aplicativo de API para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="43a00-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="43a00-197">Depois de adicionar gatilhos tooan API do aplicativo, há algumas coisas que você pode fazer a experiência de saudação tooimprove ao usar o aplicativo hello API em um aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="43a00-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="43a00-198">Por exemplo, Olá **triggerState** parâmetro gatilhos de sondagem deve ser definido como toohello expressão no aplicativo do hello lógica a seguir.</span><span class="sxs-lookup"><span data-stu-id="43a00-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="43a00-199">Essa expressão deve avaliar a última chamada de saudação do gatilho de saudação do aplicativo de lógica de saudação e retornará o valor.</span><span class="sxs-lookup"><span data-stu-id="43a00-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="43a00-200">Observação: Para obter uma explicação das funções hello usado na expressão de saudação acima, consulte documentação toohello em [lógica de linguagem de definição de fluxo de trabalho de aplicativo](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="43a00-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="43a00-201">Os usuários do aplicativo lógica precisará expressão de saudação tooprovide acima para Olá **triggerState** parâmetro ao usar o gatilho de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="43a00-202">É possível toohave esse valor predefinido pelo designer de aplicativo hello lógica por meio da propriedade de extensão Olá **x-ms-Agendador-recomendação**.</span><span class="sxs-lookup"><span data-stu-id="43a00-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="43a00-203">Olá **x-ms-visibilidade** propriedade de extensão pode ser definida como valor tooa *interno* para que o parâmetro hello em si não é exibido no designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="43a00-204">saudação de trecho de código a seguir ilustra que.</span><span class="sxs-lookup"><span data-stu-id="43a00-204">hello following snippet illustrates that.</span></span>

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

<span data-ttu-id="43a00-205">Gatilhos de envio, Olá **triggerId** parâmetro deve identificar exclusivamente o aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="43a00-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="43a00-206">Uma prática recomendada é tooset o nome da propriedade toohello de fluxo de trabalho hello usando Olá a expressão a seguir:</span><span class="sxs-lookup"><span data-stu-id="43a00-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="43a00-207">Usando Olá **x-ms-Agendador-recomendação** e **x-ms-visibilidade** propriedades de extensão em sua definição de API, Olá aplicativo de API podem transmitir toohello lógica aplicativo designer tooautomatically definir isso expressão de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="43a00-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="43a00-208">Adicionar propriedades de extensão na definição de API</span><span class="sxs-lookup"><span data-stu-id="43a00-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="43a00-209">Informações de metadados adicionais - como propriedades de extensão Olá **x-ms-Agendador-recomendação** e **x-ms-visibilidade** -podem ser adicionados na definição Olá API em uma das duas maneiras: estática ou dinâmica.</span><span class="sxs-lookup"><span data-stu-id="43a00-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="43a00-210">Para obter metadados estático, você pode editar diretamente o hello */metadata/apiDefinition.swagger.json* arquivo em seu projeto e adicionar propriedades de saudação manualmente.</span><span class="sxs-lookup"><span data-stu-id="43a00-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="43a00-211">Para aplicativos de API usando metadados dinâmico, você pode editar Olá SwaggerConfig.cs arquivo tooadd um filtro de operação que pode adicionar essas extensões.</span><span class="sxs-lookup"><span data-stu-id="43a00-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="43a00-212">a seguir Olá é um exemplo de como essa classe pode ser o cenário de metadados dinâmico Olá toofacilitate implementado.</span><span class="sxs-lookup"><span data-stu-id="43a00-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

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
