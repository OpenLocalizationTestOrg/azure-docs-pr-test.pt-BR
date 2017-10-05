---
title: "Habilitar sincronização offline para seu aplicativo móvel do Azure (Xamarin.Forms) | Microsoft Docs"
description: "Aprenda a usar o aplicativo móvel do Serviço de Aplicativo para armazenar em cache e sincronizar dados offline no aplicativo Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: f2bed0a7124517319cc82405c4ab6b4d79aacfe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="503b7-103">Habilitar sincronização offline para seu aplicativo móvel Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="503b7-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="503b7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="503b7-104">Overview</span></span>
<span data-ttu-id="503b7-105">Este tutorial apresenta o recurso de sincronização offline de Aplicativos móveis do Azure para Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="503b7-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="503b7-106">Sincronização offline permite que os usuários finais interajam com um aplicativo móvel, exibindo, adicionando ou modificando dados, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="503b7-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="503b7-107">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="503b7-107">Changes are stored in a local database.</span></span> <span data-ttu-id="503b7-108">Quando o dispositivo estiver online novamente, essas alterações serão sincronizadas com o serviço remoto.</span><span class="sxs-lookup"><span data-stu-id="503b7-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="503b7-109">Este tutorial se baseia na solução de início rápido do Xamarin.Forms para aplicativos móveis criados quando você conclui o tutorial [Criar um aplicativo iOS Xamarin].</span><span class="sxs-lookup"><span data-stu-id="503b7-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="503b7-110">A solução de início rápido para Xamarin.Forms contém o código para dar suporte à sincronização offline, que só precisa ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="503b7-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span></span> <span data-ttu-id="503b7-111">Neste tutorial, você atualiza a solução de início rápido para ativar os recursos offline dos Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="503b7-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="503b7-112">Também destacamos o código especificamente offline no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="503b7-112">We also highlight the offline-specific code in the app.</span></span> <span data-ttu-id="503b7-113">Se você não usar a solução de início rápido baixada, deverá adicionar os pacotes de extensão de acesso de dados autenticação ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="503b7-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="503b7-114">Para saber mais sobre pacotes de extensão do servidor, confira [Trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="503b7-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="503b7-115">Para saber mais sobre o recurso de sincronização offline, confira o tópico [Sincronização de dados offline nos Aplicativos Móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="503b7-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-the-quickstart-solution"></a><span data-ttu-id="503b7-116">Habilitar a funcionalidade de sincronização offline na solução de início rápido</span><span class="sxs-lookup"><span data-stu-id="503b7-116">Enable offline sync functionality in the quickstart solution</span></span>
<span data-ttu-id="503b7-117">O código de sincronização offline é incluído no projeto usando diretivas de pré-processador C#.</span><span class="sxs-lookup"><span data-stu-id="503b7-117">The offline sync code is included in the project by using C# preprocessor directives.</span></span> <span data-ttu-id="503b7-118">Quando o símbolo **OFFLINE\_SYNC\_ENABLED** é definido, esses caminhos de código são incluídos na compilação.</span><span class="sxs-lookup"><span data-stu-id="503b7-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span></span> <span data-ttu-id="503b7-119">Para aplicativos do Windows, você deve instalar também a plataforma SQLite.</span><span class="sxs-lookup"><span data-stu-id="503b7-119">For Windows apps, you must also install the SQLite platform.</span></span>

1. <span data-ttu-id="503b7-120">No Visual Studio, clique com o botão direito do mouse na solução > **Gerenciar Pacotes NuGet para a Solução...**, procure e instale o pacote NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** para todos os projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="503b7-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="503b7-121">No Gerenciador de Soluções, abra o arquivo TodoItemManager.cs do projeto com **Portable** no nome, que é o projeto da Biblioteca de Classes Portátil e remova o comentário da seguinte diretiva de pré-processador:</span><span class="sxs-lookup"><span data-stu-id="503b7-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="503b7-122">(Opcional) Para dar suporte a dispositivos Windows, instale um dos seguintes pacotes de tempo de execução do SQLite:</span><span class="sxs-lookup"><span data-stu-id="503b7-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="503b7-123">**Tempo de Execução do Windows 8.1**: instale o [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="503b7-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="503b7-124">**Windows Phone 8.1**: instale o [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="503b7-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="503b7-125">**Plataforma Universal do Windows** Instale o [SQLite para a Plataforma Universal do Windows][5].</span><span class="sxs-lookup"><span data-stu-id="503b7-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span></span>

     <span data-ttu-id="503b7-126">Embora o início rápido não contenha um projeto Universal do Windows, a plataforma Universal do Windows tem suporte com formulários do Xamarin.</span><span class="sxs-lookup"><span data-stu-id="503b7-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="503b7-127">(Opcional) Em cada projeto de aplicativo do Windows, clique com o botão direito do mouse em **Referências** > **Adicionar referência…** e expanda a pasta **Windows** > **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="503b7-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="503b7-128">Habilite o SDK do **SQLite para Windows** apropriado, junto com o SDK do **Tempo de execução do Visual C++ 2013 para Windows**.</span><span class="sxs-lookup"><span data-stu-id="503b7-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="503b7-129">Os nomes do SDK do SQLite variam ligeiramente de acordo com cada plataforma Windows.</span><span class="sxs-lookup"><span data-stu-id="503b7-129">The SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="503b7-130">Examine o código de sincronização do cliente</span><span class="sxs-lookup"><span data-stu-id="503b7-130">Review the client sync code</span></span>
<span data-ttu-id="503b7-131">Aqui há uma breve visão geral do que já está incluído no código do tutorial nas diretivas do `#if OFFLINE_SYNC_ENABLED` .</span><span class="sxs-lookup"><span data-stu-id="503b7-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="503b7-132">A funcionalidade de sincronização offline está no arquivo de projeto TodoItemManager.cs no projeto da Biblioteca de Classes Portátil.</span><span class="sxs-lookup"><span data-stu-id="503b7-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span></span> <span data-ttu-id="503b7-133">Para obter uma visão geral conceitual do recurso, confira [Sincronização de dados Offline em aplicativos móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="503b7-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="503b7-134">Antes de qualquer operação de tabela poder ser executada, o armazenamento local deve ser inicializado.</span><span class="sxs-lookup"><span data-stu-id="503b7-134">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="503b7-135">O banco de dados de armazenamento local é inicializado no construtor da classe **TodoItemManager** usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="503b7-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes the SyncContext using the default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="503b7-136">Este código cria um novo banco de dados SQLite local usando a classe **MobileServiceSQLiteStore**.</span><span class="sxs-lookup"><span data-stu-id="503b7-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="503b7-137">O método **DefineTable** cria uma tabela no repositório local que corresponde aos campos no tipo fornecido.</span><span class="sxs-lookup"><span data-stu-id="503b7-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span></span>  <span data-ttu-id="503b7-138">O tipo não precisa incluir todas as colunas que estão no banco de dados remoto.</span><span class="sxs-lookup"><span data-stu-id="503b7-138">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="503b7-139">É possível armazenar um subconjunto de colunas.</span><span class="sxs-lookup"><span data-stu-id="503b7-139">It is possible to store a subset of columns.</span></span>
* <span data-ttu-id="503b7-140">O campo **todoTable** no **TodoItemManager** é um tipo **IMobileServiceSyncTable** em vez de **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="503b7-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="503b7-141">Essa classe usa o banco de dados local para todas as operações de criação, leitura, atualização e exclusão (CRUD) de tabela.</span><span class="sxs-lookup"><span data-stu-id="503b7-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="503b7-142">Você decide quando essas alterações são enviadas por push ao back-end do Aplicativo Móvel ao chamar **PushAsync** no **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="503b7-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="503b7-143">O contexto de sincronização ajuda a preservar relações da tabela controlando e enviando por push as alterações em todas as tabelas que um aplicativo cliente tenha modificado quando o **PushAsync** é chamado.</span><span class="sxs-lookup"><span data-stu-id="503b7-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="503b7-144">O método **SyncAsync** a seguir é chamado para sincronização com o back-end do Aplicativo Móvel:</span><span class="sxs-lookup"><span data-stu-id="503b7-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span></span>

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting to server's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    <span data-ttu-id="503b7-145">Este exemplo usa o tratamento de erros simples com o manipulador de sincronização padrão.</span><span class="sxs-lookup"><span data-stu-id="503b7-145">This sample uses simple error handling with the default sync handler.</span></span> <span data-ttu-id="503b7-146">Um aplicativo real trataria os diversos erros como condições de rede e conflitos de servidor usando uma personalização da implementação de **IMobileServiceSyncHandler**.</span><span class="sxs-lookup"><span data-stu-id="503b7-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="503b7-147">Considerações sobre a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="503b7-147">Offline sync considerations</span></span>
<span data-ttu-id="503b7-148">No exemplo, o método **SyncAsync** é chamado somente na inicialização e quando a sincronização é solicitada.</span><span class="sxs-lookup"><span data-stu-id="503b7-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="503b7-149">Para iniciar uma sincronização em um aplicativo Android ou iOS, puxe para baixo a lista de itens; para o Windows, use o botão **Sincronizar**.</span><span class="sxs-lookup"><span data-stu-id="503b7-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span></span> <span data-ttu-id="503b7-150">Em um aplicativo do mundo real, você também poderia fazer a sincronização disparar quando o estado da rede mudasse.</span><span class="sxs-lookup"><span data-stu-id="503b7-150">In a real-world application, you could also make the sync trigger when the network state changes.</span></span>

<span data-ttu-id="503b7-151">Quando um pull é executado em uma tabela que tenha atualizações locais pendentes controladas pelo contexto, e essa operação de pull automaticamente dispara um envio por push de contexto anterior.</span><span class="sxs-lookup"><span data-stu-id="503b7-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="503b7-152">Durante a atualização, a adição e a conclusão de itens neste exemplo, você pode omitir a chamada explícita a **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="503b7-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span></span>

<span data-ttu-id="503b7-153">No código fornecido, todos os registros na tabela remota TodoItem são solicitados, mas também é possível filtrar os registros passando uma ID de consulta e uma consulta ao **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="503b7-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span></span> <span data-ttu-id="503b7-154">Para obter mais informações, consulte a seção *Sincronização Incremental* em [Sincronização de Dados Offline em Aplicativos Móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="503b7-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="503b7-155">Execute o aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="503b7-155">Run the client app</span></span>
<span data-ttu-id="503b7-156">Com a sincronização offline agora habilitada, execute o aplicativo cliente pelo menos uma vez em cada plataforma para preencher o banco de dados do armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="503b7-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="503b7-157">Posteriormente, simule um cenário offline e modificará os dados no armazenamento local enquanto o aplicativo estiver offline.</span><span class="sxs-lookup"><span data-stu-id="503b7-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="update-the-sync-behavior-of-the-client-app"></a><span data-ttu-id="503b7-158">Atualize o comportamento de sincronização do aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="503b7-158">Update the sync behavior of the client app</span></span>
<span data-ttu-id="503b7-159">Nesta seção, modifique o projeto do cliente para simular um cenário offline usando uma URL de aplicativo inválida para o back-end.</span><span class="sxs-lookup"><span data-stu-id="503b7-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="503b7-160">Como alternativa, você pode desativar conexões de rede mudando o dispositivo para o "Modo de avião".</span><span class="sxs-lookup"><span data-stu-id="503b7-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span></span>  <span data-ttu-id="503b7-161">Quando você adiciona ou alterar itens de dados, essas alterações são mantidas no armazenamento local, mas não sincronizadas com o armazenamento de dados back-end até que a conexão seja restabelecida.</span><span class="sxs-lookup"><span data-stu-id="503b7-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="503b7-162">No Gerenciador de Soluções, abra o arquivo de projeto Constants.cs do projeto **Portable** e altere o valor de `ApplicationURL` para apontar para uma URL inválida:</span><span class="sxs-lookup"><span data-stu-id="503b7-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="503b7-163">Abra o arquivo TodoItemManager.cs do projeto **Portable** e adicione um **catch** à classe base **Exception** para o bloco **try...catch** em **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="503b7-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="503b7-164">Esse bloco **catch** grava a mensagem de exceção no console, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="503b7-164">This **catch** block writes the exception message to the console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="503b7-165">Compile e execute o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="503b7-165">Build and run the client app.</span></span>  <span data-ttu-id="503b7-166">Adicione alguns novos itens.</span><span class="sxs-lookup"><span data-stu-id="503b7-166">Add some new items.</span></span> <span data-ttu-id="503b7-167">Observe que uma exceção será registrada no console para cada tentativa de sincronização com o back-end.</span><span class="sxs-lookup"><span data-stu-id="503b7-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span></span> <span data-ttu-id="503b7-168">Esses novos itens existem apenas no repositório local até que possam ser enviados por push para o serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="503b7-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span></span> <span data-ttu-id="503b7-169">O aplicativo cliente se comporta como se estivesse conectado ao back-end, dando suporte a todas as operações CRUD (criar, ler, atualizar e excluir).</span><span class="sxs-lookup"><span data-stu-id="503b7-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="503b7-170">Feche o aplicativo e reinicie-o para verificar se os novos itens que você criou persistem no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="503b7-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="503b7-171">(Opcional) Use o Visual Studio para exibir a tabela de Banco de Dados SQL do Azure para ver se os dados no banco de dados do back-end não foram alterados.</span><span class="sxs-lookup"><span data-stu-id="503b7-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="503b7-172">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="503b7-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="503b7-173">Navegue até o banco de dados em **Azure**->**Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="503b7-173">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="503b7-174">Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="503b7-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="503b7-175">Agora você pode navegar até sua tabela de banco de dados SQL e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="503b7-175">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="update-the-client-app-to-reconnect-your-mobile-backend"></a><span data-ttu-id="503b7-176">Atualize o aplicativo cliente para reconectar seu back-end móvel</span><span class="sxs-lookup"><span data-stu-id="503b7-176">Update the client app to reconnect your mobile backend</span></span>
<span data-ttu-id="503b7-177">Nesta seção, reconecte o aplicativo ao back-end móvel, que simula o aplicativo voltando ao estado online.</span><span class="sxs-lookup"><span data-stu-id="503b7-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="503b7-178">Quando você executa o gesto de atualização, os dados são sincronizados com o serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="503b7-178">When you perform the refresh gesture, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="503b7-179">Reabra Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="503b7-179">Reopen Constants.cs.</span></span> <span data-ttu-id="503b7-180">Corrija o `applicationURL` de modo que ele aponte para a URL correta.</span><span class="sxs-lookup"><span data-stu-id="503b7-180">Correct the `applicationURL` to point to the correct URL.</span></span>
2. <span data-ttu-id="503b7-181">Recompile e execute o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="503b7-181">Rebuild and run the client app.</span></span> <span data-ttu-id="503b7-182">O aplicativo tenta sincronizar com o back-end do aplicativo móvel após iniciar.</span><span class="sxs-lookup"><span data-stu-id="503b7-182">The app attempts to sync with the mobile app backend after launching.</span></span> <span data-ttu-id="503b7-183">Verifique se nenhuma exceção está registrada no console de depuração.</span><span class="sxs-lookup"><span data-stu-id="503b7-183">Verify that no exceptions are logged in the debug console.</span></span>
3. <span data-ttu-id="503b7-184">(Opcional) Exiba os dados atualizados usando o Pesquisador de Objetos do SQL Server ou uma ferramenta REST, como o Fiddler ou [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="503b7-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="503b7-185">Observe que os dados foram sincronizados entre o banco de dados de back-end e o repositório local.</span><span class="sxs-lookup"><span data-stu-id="503b7-185">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="503b7-186">Observe que os dados foram sincronizados entre o banco de dados e o armazenamento local e contém os itens que você adicionou enquanto seu aplicativo estava desconectado.</span><span class="sxs-lookup"><span data-stu-id="503b7-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="503b7-187">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="503b7-187">Additional Resources</span></span>
* <span data-ttu-id="503b7-188">[Sincronização de Dados Offline em Aplicativos Móveis do Azure][2]</span><span class="sxs-lookup"><span data-stu-id="503b7-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="503b7-189">[SDK .NET de Aplicativos Móveis do Azure HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="503b7-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
