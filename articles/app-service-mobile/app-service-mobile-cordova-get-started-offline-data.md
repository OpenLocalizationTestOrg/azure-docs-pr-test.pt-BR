---
title: "sincronização offline de aaaEnable para seu aplicativo móvel do Azure (Cordova) | Microsoft Docs"
description: "Saiba como toouse aplicativo do serviço de aplicativo móvel toocache e sincronização de dados offline em seu aplicativo Cordova"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="8bbfc-103">Habilitar a sincronização offline para seu aplicativo móvel Cordova</span><span class="sxs-lookup"><span data-stu-id="8bbfc-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="8bbfc-104">Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para Cordova.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="8bbfc-105">Sincronização offline permite toointeract de usuários finais com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="8bbfc-106">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="8bbfc-107">Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o serviço remoto hello.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="8bbfc-108">Este tutorial baseia-se em Olá solução de início rápido do Cordova para aplicativos móveis que você cria ao concluir Olá tutorial [início rápido do Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="8bbfc-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="8bbfc-109">Neste tutorial, você deve atualizar Olá quickstart tooadd offline recursos de solução de aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="8bbfc-110">Podemos também realce o código de off-line específicos de Olá no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="8bbfc-111">toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="8bbfc-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="8bbfc-112">Para obter detalhes de uso da API, consulte Olá [documentação da API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="8bbfc-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="8bbfc-113">Adicionar solução de início rápido de toohello sincronização offline</span><span class="sxs-lookup"><span data-stu-id="8bbfc-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="8bbfc-114">código de sincronização offline Olá deve ser adicionado toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="8bbfc-115">Sincronização offline requer Olá armazenamento cordova-sqlite plug-in, que é adicionado automaticamente tooyour aplicativo quando o plug-in do hello os aplicativos móveis do Azure está incluído no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="8bbfc-116">projeto de início rápido de saudação inclui ambos esses plug-ins.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="8bbfc-117">No Gerenciador de soluções do Visual Studio, abra js e substitua Olá código a seguir</span><span class="sxs-lookup"><span data-stu-id="8bbfc-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="8bbfc-118">por este código:</span><span class="sxs-lookup"><span data-stu-id="8bbfc-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="8bbfc-119">Em seguida, substitua Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bbfc-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="8bbfc-120">por este código:</span><span class="sxs-lookup"><span data-stu-id="8bbfc-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    <span data-ttu-id="8bbfc-121">Olá adições de código anterior inicializar o repositório local hello e definir uma tabela local que faz a correspondência de valores de coluna Olá usados no seu Azure back-end.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="8bbfc-122">(Não é necessário tooinclude todos os valores de coluna nesse código.)  Olá `version` campo é mantido pelo back-end de saudação móvel e é usado para resolução de conflitos.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="8bbfc-123">Obter um contexto de sincronização referência toohello chamando **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="8bbfc-124">Hello contexto de sincronização ajuda a preservar relações de tabela, controle e enviar as alterações em todas as tabelas de um aplicativo cliente tenha modificado quando `.push()` é chamado.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="8bbfc-125">Atualize a URL do aplicativo hello aplicativo URL tooyour aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="8bbfc-126">Em seguida, substitua este código:</span><span class="sxs-lookup"><span data-stu-id="8bbfc-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="8bbfc-127">por este código:</span><span class="sxs-lookup"><span data-stu-id="8bbfc-127">with this code:</span></span>

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="8bbfc-128">Hello código anterior inicializa o contexto de sincronização de saudação e, em seguida, chama tooget getSyncTable (em vez de pode ser obtida) uma tabela local do toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="8bbfc-129">Esse código usa Olá banco de dados local para todos os criar, ler, atualizar e excluir operações de tabela (CRUD).</span><span class="sxs-lookup"><span data-stu-id="8bbfc-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="8bbfc-130">Este exemplo executa o tratamento de erros simples nos conflitos de sincronização.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="8bbfc-131">Um aplicativo real trataria Olá vários erros como condições de rede, conflitos de servidor e outros.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="8bbfc-132">Para obter exemplos de código, consulte Olá [sincronização offline].</span><span class="sxs-lookup"><span data-stu-id="8bbfc-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="8bbfc-133">Em seguida, adicione essa sincronização do função tooperform Olá real.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="8bbfc-134">Você decide quando toopush altera o back-end de aplicativo móvel toohello chamando **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="8bbfc-135">Por exemplo, você poderia chamar **syncBackend** em um botão de sincronização associado tooa do evento manipulador.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="8bbfc-136">Considerações sobre a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="8bbfc-136">Offline sync considerations</span></span>

<span data-ttu-id="8bbfc-137">No exemplo hello, Olá **push** método **syncContext** só é chamado na inicialização do aplicativo na função de retorno de chamada de saudação para logon.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="8bbfc-138">Em um aplicativo do mundo real, você também pode fazer essa funcionalidade de sincronização disparada manualmente ou quando altera o estado da rede hello.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="8bbfc-139">Quando a extração é executada em uma tabela que tem pendente atualizações locais rastreadas pelo contexto de hello, puxe a operação automaticamente gatilhos um envio por push.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="8bbfc-140">Quando a atualização, a adição e Concluindo itens neste exemplo, você pode omitir Olá explícita **push** chamar, já que ele pode ser redundante.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="8bbfc-141">No código Olá fornecido, todos os registros na tabela de remota todoItem Olá são consultados, mas também é possível toofilter registros, passando uma id de consulta e uma consulta muito**push**.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="8bbfc-142">Para obter mais informações, consulte a seção de saudação *Sincronização Incremental* na [sincronização de dados Offline em aplicativos móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="8bbfc-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="8bbfc-143">(Opcional) Desabilitar a autenticação</span><span class="sxs-lookup"><span data-stu-id="8bbfc-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="8bbfc-144">Se você não deseja tooset a autenticação antes de testar a sincronização offline, comente a função de retorno de chamada de saudação para logon, mas deixar Olá código dentro de função de retorno de chamada hello removidos.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="8bbfc-145">Depois de comentar as linhas de logon Olá, código Olá segue:</span><span class="sxs-lookup"><span data-stu-id="8bbfc-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="8bbfc-146">Agora, Olá aplicativo sincronizações com hello back-end do Azure quando você executa o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="8bbfc-147">Execute o aplicativo de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="8bbfc-147">Run hello client app</span></span>
<span data-ttu-id="8bbfc-148">Com a sincronização offline agora está habilitada, você pode executar aplicativos de cliente de saudação pelo menos uma vez em cada plataforma para preencher o banco de dados de armazenamento local de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="8bbfc-149">Posteriormente, simular um cenário offline e modificar dados de saudação no repositório local Olá enquanto o aplicativo hello está offline.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="8bbfc-150">(Opcional) Comportamento de sincronização de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="8bbfc-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="8bbfc-151">Nesta seção, você pode modificar Olá cliente projeto toosimulate um cenário offline usando uma URL de aplicativo inválido para o back-end.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="8bbfc-152">Quando você adicionar ou alterar itens de dados, essas alterações são mantidas no armazenamento local, mas não estão sincronizados toohello repositório de dados de back-end até que a conexão de saudação é restabelecida.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="8bbfc-153">No hello Gerenciador de soluções, abrir o arquivo de projeto do hello js e altere Olá toopoint de URL de aplicativo para uma URL inválida, como saudação de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8bbfc-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="8bbfc-154">Index, atualizar Olá CSP `<meta>` Olá elemento com a mesma URL inválida.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="8bbfc-155">Criar e executar o aplicativo de cliente hello e observe que uma exceção seja registrada no console de saudação quando o aplicativo hello tenta sincronizar com o back-end de saudação após o logon.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="8bbfc-156">Quaisquer novos itens que você adicionar só existem no repositório local Olá até que eles são enviados por push o back-end do toohello móvel.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="8bbfc-157">Olá aplicativo de cliente se comporta como se estivesse conectado toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="8bbfc-158">Feche o aplicativo hello e reiniciá-lo tooverify que você criou novos itens de saudação são repositório local toohello persistente.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="8bbfc-159">(Opcional) Use Visual Studio tooview seu toosee de tabela de banco de dados do Azure SQL Olá dados no banco de dados de back-end de saudação não foram alterados.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="8bbfc-160">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="8bbfc-161">Navegue de banco de dados tooyour no **Azure**->**bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="8bbfc-162">Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="8bbfc-163">Agora você pode procurar a tabela de banco de dados do SQL tooyour e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="8bbfc-164">(Opcional) Teste Olá reconexão tooyour móvel back-end</span><span class="sxs-lookup"><span data-stu-id="8bbfc-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="8bbfc-165">Nesta seção, você pode se reconectar Olá aplicativo toohello móvel back-end, que simula um aplicativo hello volte ao estado online.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="8bbfc-166">Quando você entrar, dados são back-end de móveis tooyour sincronizados.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="8bbfc-167">Reabra js e restaurar a URL do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="8bbfc-168">Reabra Index e corrija a URL do aplicativo hello em Olá CSP `<meta>` elemento.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="8bbfc-169">Recriar e execute o aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="8bbfc-170">aplicativo Hello tentativas toosync com back-end de aplicativo móvel Olá após o logon.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="8bbfc-171">Verifique se que nenhuma exceção é registradas no console de depuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="8bbfc-172">(Opcional) Saudação de exibição atualizada dados usando o Pesquisador de objetos do SQL Server ou uma ferramenta REST, como o Fiddler.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="8bbfc-173">Aviso Olá dados entre o banco de dados de back-end hello e armazenamento local Olá foi sincronizados.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="8bbfc-174">Observe dados saudação foi sincronizados entre o banco de dados de saudação e armazenamento local hello e contém itens Olá adicionados enquanto seu aplicativo estava desconectado.</span><span class="sxs-lookup"><span data-stu-id="8bbfc-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8bbfc-175">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8bbfc-175">Additional resources</span></span>
* <span data-ttu-id="8bbfc-176">[sincronização de dados Offline em aplicativos móveis do Azure]</span><span class="sxs-lookup"><span data-stu-id="8bbfc-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="8bbfc-177">[Ferramentas do Visual Studio para Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="8bbfc-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bbfc-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8bbfc-178">Next steps</span></span>
* <span data-ttu-id="8bbfc-179">Revisão mais avançados recursos de sincronização offline, como resolução de conflito em Olá [sincronização offline]</span><span class="sxs-lookup"><span data-stu-id="8bbfc-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="8bbfc-180">Examine a sincronização offline de Olá referência de API no hello [documentação da API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="8bbfc-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[início rápido do Apache Cordova]: app-service-mobile-cordova-get-started.md
[sincronização offline]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[sincronização de dados Offline em aplicativos móveis do Azure]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Ferramentas do Visual Studio para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
