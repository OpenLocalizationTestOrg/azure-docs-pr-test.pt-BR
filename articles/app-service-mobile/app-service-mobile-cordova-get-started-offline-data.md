---
title: "Habilitar a sincronização offline para seu Aplicativo Móvel do Azure (Cordova) | Microsoft Docs"
description: "Aprenda a usar o Aplicativo Móvel do Serviço de Aplicativo para o cache e a sincronização de dados offline no aplicativo Cordova"
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
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="5a9c7-103">Habilitar a sincronização offline para seu aplicativo móvel Cordova</span><span class="sxs-lookup"><span data-stu-id="5a9c7-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="5a9c7-104">Este tutorial apresenta o recurso de sincronização offline dos Aplicativos Móveis do Azure para o Cordova.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="5a9c7-105">A sincronização offline permite que os usuários finais interajam com um aplicativo móvel, &mdash;exibindo, adicionando ou modificando dados&mdash;, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="5a9c7-106">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="5a9c7-107">Quando o dispositivo estiver online novamente, essas alterações serão sincronizadas com o serviço remoto.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="5a9c7-108">Este tutorial se baseia na solução de início rápido do Cordova para os Aplicativos Móveis criados quando você conclui o tutorial [Início rápido do Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="5a9c7-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="5a9c7-109">Neste tutorial, você atualizará a solução de início rápido para adicionar recursos offline dos Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="5a9c7-110">Também destacamos o código especificamente offline no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="5a9c7-111">Para saber mais sobre o recurso de sincronização offline, confira o tópico [Sincronização de dados offline nos Aplicativos Móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="5a9c7-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="5a9c7-112">Para obter detalhes sobre o uso da API, consulte a [documentação da API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="5a9c7-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="5a9c7-113">Adicionar a sincronização offline à solução de início rápido</span><span class="sxs-lookup"><span data-stu-id="5a9c7-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="5a9c7-114">O código da sincronização offline deve ser adicionado ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="5a9c7-115">A sincronização offline requer o plug-in cordova-sqlite-storage, que é adicionado automaticamente ao seu aplicativo quando o plug-in dos Aplicativos Móveis do Azure está incluído no projeto.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="5a9c7-116">O projeto de Início Rápido inclui os dois plug-ins.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="5a9c7-117">No Gerenciador de Soluções do Visual Studio, abra o index.js e substitua o código a seguir</span><span class="sxs-lookup"><span data-stu-id="5a9c7-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="5a9c7-118">por este código:</span><span class="sxs-lookup"><span data-stu-id="5a9c7-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="5a9c7-119">Em seguida, substitua o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a9c7-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="5a9c7-120">por este código:</span><span class="sxs-lookup"><span data-stu-id="5a9c7-120">with this code:</span></span>

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

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="5a9c7-121">As adições de código anteriores inicializam o armazenamento local e definem uma tabela local que corresponde aos valores da coluna usados no back-end do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="5a9c7-122">(Você não precisa incluir todos os valores da coluna nesse código.)  O campo `version` é mantido pelo back-end móvel e é usado para resolução de conflitos.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="5a9c7-123">Você obtém uma referência para o contexto de sincronização chamando **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="5a9c7-124">O contexto de sincronização ajuda a preservar relações da tabela controlando e enviando por push as alterações em todas as tabelas que um aplicativo cliente tenha modificado quando o `.push()` é chamado.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="5a9c7-125">Atualize a URL do aplicativo para a URL do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="5a9c7-126">Em seguida, substitua este código:</span><span class="sxs-lookup"><span data-stu-id="5a9c7-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="5a9c7-127">por este código:</span><span class="sxs-lookup"><span data-stu-id="5a9c7-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="5a9c7-128">O código anterior inicializa o contexto de sincronização e, em seguida, chama getSyncTable (em vez de getTable) para obter uma referência para a tabela local.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="5a9c7-129">Esse código usa o banco de dados local para todas as operações da tabela para criar, ler, atualizar e excluir (CRUD).</span><span class="sxs-lookup"><span data-stu-id="5a9c7-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="5a9c7-130">Este exemplo executa o tratamento de erros simples nos conflitos de sincronização.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="5a9c7-131">Um aplicativo real trataria os diversos erros, como condições de rede, conflitos do servidor e outros.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="5a9c7-132">Para obter exemplos de código, confira o [exemplo de sincronização offline].</span><span class="sxs-lookup"><span data-stu-id="5a9c7-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="5a9c7-133">Em seguida, adicione esta função para executar a sincronização real.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="5a9c7-134">Você decide quando enviar as alterações por push para o back-end do Aplicativo Móvel chamando **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="5a9c7-135">Por exemplo, você poderia chamar **syncBackend** em um manipulador de eventos ligado a um botão de sincronização.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="5a9c7-136">Considerações sobre a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="5a9c7-136">Offline sync considerations</span></span>

<span data-ttu-id="5a9c7-137">No exemplo, o método **push** de **syncContext** apenas é chamado na inicialização do aplicativo na função de callback do logon.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="5a9c7-138">Em um aplicativo real, você também poderia disparar manualmente essa funcionalidade de sincronização ou quando o estado da rede muda.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="5a9c7-139">Quando um pull é executado em uma tabela que tenha atualizações locais pendentes controladas pelo contexto, essa operação de pull automaticamente dispara um envio por push.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="5a9c7-140">Durante a atualização, a adição e a conclusão de itens neste exemplo, você pode omitir a chamada **push** explícita, pois ela pode ser redundante.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="5a9c7-141">No código fornecido, todos os registros na tabela remota todoItem são consultados, mas também é possível filtrar os registros passando uma id de consulta e uma consulta para **push**.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="5a9c7-142">Para obter mais informações, consulte a seção *Sincronização Incremental* em [Sincronização de dados offline nos Aplicativos Móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="5a9c7-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="5a9c7-143">(Opcional) Desabilitar a autenticação</span><span class="sxs-lookup"><span data-stu-id="5a9c7-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="5a9c7-144">Se você não desejar configurar a autenticação antes da sincronização offline de teste, remova a marca de comentário da função de callback para logon, mas deixe o código dentro dessa função sem comentário.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="5a9c7-145">Após remover as marcas de comentário das linhas de logon, o código será:</span><span class="sxs-lookup"><span data-stu-id="5a9c7-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="5a9c7-146">Agora, o aplicativo será sincronizado com o back-end do Azure quando você executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="5a9c7-147">Execute o aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="5a9c7-147">Run the client app</span></span>
<span data-ttu-id="5a9c7-148">Com a sincronização offline agora habilitada, você poderá executar o aplicativo cliente pelo menos uma vez em cada plataforma para preencher o banco de dados do repositório local.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="5a9c7-149">Posteriormente, simule um cenário offline e modificará os dados no armazenamento local enquanto o aplicativo estiver offline.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="5a9c7-150">(Opcional) Testar o comportamento da sincronização</span><span class="sxs-lookup"><span data-stu-id="5a9c7-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="5a9c7-151">Nesta seção, você modificará o projeto do cliente para simular um cenário offline usando uma URL de aplicativo inválida para o back-end.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="5a9c7-152">Quando você adicionar ou alterar itens de dados, essas alterações são mantidas no repositório local, mas não são sincronizadas com o armazenamento de dados de back-end até que a conexão seja restabelecida.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="5a9c7-153">No Gerenciador de Soluções, abra o arquivo de projeto index.js e altere a URL do aplicativo para apontar para uma URL inválida, como no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a9c7-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="5a9c7-154">Em index.html, atualize o elemento CSP `<meta>` com a mesma URL inválida.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="5a9c7-155">Compile e execute o aplicativo cliente, e observe que uma exceção é registrada no console quando o aplicativo tenta sincronizar com o back-end após o logon.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="5a9c7-156">Todos os novos itens adicionados existem apenas no repositório local até que possam ser enviados por push para o back-end móvel.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="5a9c7-157">O aplicativo cliente se comporta como se ele estivesse conectado ao back-end.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="5a9c7-158">Feche o aplicativo e reinicie-o para verificar se os novos itens que você criou persistem no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="5a9c7-159">(Opcional) Use o Visual Studio para exibir a tabela de Banco de Dados SQL do Azure para ver se os dados no banco de dados do back-end não foram alterados.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="5a9c7-160">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="5a9c7-161">Navegue até o banco de dados em **Azure**->**Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="5a9c7-162">Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="5a9c7-163">Agora você pode navegar até sua tabela de banco de dados SQL e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="5a9c7-164">(Opcional) Testar a reconexão com seu back-end móvel</span><span class="sxs-lookup"><span data-stu-id="5a9c7-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="5a9c7-165">Nesta seção, reconecte o aplicativo ao back-end móvel, que simula o aplicativo voltando ao estado online.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="5a9c7-166">Quando você fizer logon, os dados serão sincronizados com o back-end móvel.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="5a9c7-167">Abra index.js novamente e restaure a URL do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="5a9c7-168">Reabra o index.html e corrija a URL do aplicativo no elemento CSP `<meta>` .</span><span class="sxs-lookup"><span data-stu-id="5a9c7-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="5a9c7-169">Recompile e execute o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-169">Rebuild and run the client app.</span></span> <span data-ttu-id="5a9c7-170">O aplicativo tenta sincronizar com o back-end do aplicativo móvel após fazer logon.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="5a9c7-171">Verifique se nenhuma exceção está registrada no console de depuração.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="5a9c7-172">(Opcional) Exiba os dados atualizados usando o Pesquisador de Objetos do SQL Server ou uma ferramenta REST, como o Fiddler.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="5a9c7-173">Observe que os dados foram sincronizados entre o banco de dados de back-end e o repositório local.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="5a9c7-174">Observe que os dados foram sincronizados entre o banco de dados e o armazenamento local e contém os itens que você adicionou enquanto seu aplicativo estava desconectado.</span><span class="sxs-lookup"><span data-stu-id="5a9c7-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a9c7-175">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5a9c7-175">Additional resources</span></span>
* <span data-ttu-id="5a9c7-176">[Sincronização de dados offline nos Aplicativos Móveis do Azure]</span><span class="sxs-lookup"><span data-stu-id="5a9c7-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="5a9c7-177">[Ferramentas do Visual Studio para Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="5a9c7-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a9c7-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a9c7-178">Next steps</span></span>
* <span data-ttu-id="5a9c7-179">Analise os recursos mais avançados de sincronização offline, como a resolução de conflitos no [exemplo de sincronização offline]</span><span class="sxs-lookup"><span data-stu-id="5a9c7-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="5a9c7-180">Analise a referência da API de sincronização offline na [Documentação de API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="5a9c7-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="5a9c7-181">[Início rápido do Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="5a9c7-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="5a9c7-182">[exemplo de sincronização offline]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="5a9c7-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="5a9c7-183">[Sincronização de dados offline nos Aplicativos Móveis do Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="5a9c7-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="5a9c7-184">[Ferramentas do Visual Studio para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="5a9c7-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
