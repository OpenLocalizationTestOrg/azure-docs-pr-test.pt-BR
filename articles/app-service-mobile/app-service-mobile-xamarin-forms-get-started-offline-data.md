---
title: "sincronização offline de aaaEnable para seu aplicativo móvel do Azure (xamarin. Forms) | Microsoft Docs"
description: "Saiba como toouse aplicativo do serviço de aplicativo móvel toocache e sincronização de dados offline em seu aplicativo xamarin. Forms"
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
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="50330-103">Habilitar sincronização offline para seu aplicativo móvel Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="50330-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="50330-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="50330-104">Overview</span></span>
<span data-ttu-id="50330-105">Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para xamarin. Forms.</span><span class="sxs-lookup"><span data-stu-id="50330-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="50330-106">Sincronização offline permite que os usuários finais interajam com um aplicativo móvel, exibindo, adicionando ou modificando dados, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="50330-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="50330-107">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="50330-107">Changes are stored in a local database.</span></span> <span data-ttu-id="50330-108">Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o serviço remoto hello.</span><span class="sxs-lookup"><span data-stu-id="50330-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="50330-109">Este tutorial se baseia na Olá xamarin. Forms quickstart solução para aplicativos móveis que você cria ao concluir o tutorial [criar um aplicativo Xamarin iOS].</span><span class="sxs-lookup"><span data-stu-id="50330-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="50330-110">solução de início rápido de saudação para xamarin. Forms contém Olá código toosupport sincronização offline, que só precisa toobe habilitado.</span><span class="sxs-lookup"><span data-stu-id="50330-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="50330-111">Neste tutorial, você deve atualizar Olá quickstart solução tooturn recursos offline de saudação do aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="50330-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="50330-112">Podemos também realce o código de off-line específicos de Olá no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="50330-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="50330-113">Se você não usar a solução de início rápido de saudação baixada, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso de dados de hello.</span><span class="sxs-lookup"><span data-stu-id="50330-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="50330-114">Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="50330-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="50330-115">toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="50330-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="50330-116">Habilitar a funcionalidade de sincronização offline na solução de início rápido de saudação</span><span class="sxs-lookup"><span data-stu-id="50330-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="50330-117">código de sincronização offline Hello está incluído no projeto de saudação usando diretivas de pré-processador C#.</span><span class="sxs-lookup"><span data-stu-id="50330-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="50330-118">Olá quando **OFFLINE\_sincronização\_habilitado** símbolo é definido, esses caminhos de código são incluídos na compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="50330-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="50330-119">Para aplicativos do Windows, instale também plataforma do SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="50330-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="50330-120">No Visual Studio, clique com botão direito solução hello > **gerenciar pacotes NuGet para solução...** , em seguida, procurar e instalar o **Microsoft.Azure.Mobile.Client.SQLiteStore** pacote NuGet para todos os projetos na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="50330-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="50330-121">Em Olá Solution Explorer, abra o arquivo de TodoItemManager.cs de saudação do projeto Olá com **portátil** em nome de saudação, que é o projeto de biblioteca de classes portátil, em seguida, remova os comentários Olá após diretiva de pré-processador:</span><span class="sxs-lookup"><span data-stu-id="50330-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="50330-122">Dispositivos do Windows toosupport (opcional), instale um dos Olá SQLite pacotes de tempo de execução a seguir:</span><span class="sxs-lookup"><span data-stu-id="50330-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="50330-123">**Tempo de Execução do Windows 8.1**: instale o [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="50330-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="50330-124">**Windows Phone 8.1**: instale o [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="50330-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="50330-125">**Plataforma universal do Windows** instalar [SQLite para Olá Universal do Windows Universal][5].</span><span class="sxs-lookup"><span data-stu-id="50330-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="50330-126">Embora Olá quickstart não contém um projeto Universal do Windows, plataforma Universal do Windows de saudação é compatível com o Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="50330-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="50330-127">(Opcional) Em cada projeto de aplicativo do Windows, clique com botão direito **referências** > **adicionar referência...** , expanda Olá **Windows** pasta > **extensões**.</span><span class="sxs-lookup"><span data-stu-id="50330-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="50330-128">Habilitar Olá apropriado **SQLite para Windows** SDK junto com hello **Visual C++ 2013 em tempo de execução para da Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="50330-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="50330-129">Hello nomes SQLite SDK variam ligeiramente em cada plataforma do Windows.</span><span class="sxs-lookup"><span data-stu-id="50330-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="50330-130">Examine o código de sincronização do cliente Olá</span><span class="sxs-lookup"><span data-stu-id="50330-130">Review hello client sync code</span></span>
<span data-ttu-id="50330-131">Aqui está uma breve visão geral do que já está incluído no tutorial código Olá Olá `#if OFFLINE_SYNC_ENABLED` diretivas.</span><span class="sxs-lookup"><span data-stu-id="50330-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="50330-132">A funcionalidade de sincronização offline está no arquivo de projeto TodoItemManager.cs Olá no projeto de biblioteca de classes portátil hello.</span><span class="sxs-lookup"><span data-stu-id="50330-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="50330-133">Para obter uma visão geral conceitual do recurso hello, consulte [sincronização de dados Offline em aplicativos móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="50330-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="50330-134">Antes de quaisquer operações de tabela podem ser executadas, armazenamento local Olá deve ser inicializado.</span><span class="sxs-lookup"><span data-stu-id="50330-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="50330-135">Olá banco de dados do armazenamento local é inicializado no hello **TodoItemManager** construtor da classe usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="50330-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="50330-136">Esse código cria um novo local SQLite banco de dados usando Olá **MobileServiceSQLiteStore** classe.</span><span class="sxs-lookup"><span data-stu-id="50330-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="50330-137">Olá **DefineTable** método cria uma tabela no repositório local de saudação que corresponda a campos Olá no tipo hello fornecido.</span><span class="sxs-lookup"><span data-stu-id="50330-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="50330-138">tipo de saudação não tem tooinclude todas as colunas de saudação que estão no banco de dados remoto hello.</span><span class="sxs-lookup"><span data-stu-id="50330-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="50330-139">É possível toostore um subconjunto de colunas.</span><span class="sxs-lookup"><span data-stu-id="50330-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="50330-140">Olá **todoTable** campo **TodoItemManager** é um **IMobileServiceSyncTable** digite, em vez de **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="50330-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="50330-141">Essa classe usa Olá banco de dados local para todos os criar, ler, atualizar e excluir operações de tabela (CRUD).</span><span class="sxs-lookup"><span data-stu-id="50330-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="50330-142">Você decide quando essas alterações são enviados por push back-end de aplicativo móvel toohello chamando **PushAsync** em Olá **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="50330-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="50330-143">Hello contexto de sincronização ajuda a preservar relações de tabela, controle e enviar as alterações em todas as tabelas de um aplicativo cliente tenha modificado quando **PushAsync** é chamado.</span><span class="sxs-lookup"><span data-stu-id="50330-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="50330-144">a seguir Olá **SyncAsync** método é chamado toosync com back-end de aplicativo móvel hello:</span><span class="sxs-lookup"><span data-stu-id="50330-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

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
                        //Update failed, reverting tooserver's copy.
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

    <span data-ttu-id="50330-145">Este exemplo usa com o manipulador de sincronização saudação padrão de tratamento de erros simples.</span><span class="sxs-lookup"><span data-stu-id="50330-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="50330-146">Um aplicativo real trataria Olá vários erros como condições de rede e o servidor está em conflito usando um personalizado **IMobileServiceSyncHandler** implementação.</span><span class="sxs-lookup"><span data-stu-id="50330-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="50330-147">Considerações sobre a sincronização offline</span><span class="sxs-lookup"><span data-stu-id="50330-147">Offline sync considerations</span></span>
<span data-ttu-id="50330-148">No exemplo hello, Olá **SyncAsync** método é chamado somente na inicialização e quando a sincronização é solicitada.</span><span class="sxs-lookup"><span data-stu-id="50330-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="50330-149">tooinitiate uma sincronização em um aplicativo do Android ou iOS, pull para baixo na lista de itens de saudação; para o Windows, use Olá **sincronização** botão.</span><span class="sxs-lookup"><span data-stu-id="50330-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="50330-150">Em um aplicativo do mundo real, você também poderia fazer o gatilho de sincronização hello quando alterações de estado da rede hello.</span><span class="sxs-lookup"><span data-stu-id="50330-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="50330-151">Quando a extração é executada em uma tabela que tem pendente atualizações locais rastreadas pelo contexto de hello, puxe a operação automaticamente gatilhos um envio por push do contexto anterior.</span><span class="sxs-lookup"><span data-stu-id="50330-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="50330-152">Quando a atualização, a adição e Concluindo itens neste exemplo, você pode omitir Olá explícita **PushAsync** chamar.</span><span class="sxs-lookup"><span data-stu-id="50330-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="50330-153">No código Olá fornecido, todos os registros na tabela TodoItem remota de saudação são consultados, mas também é possível toofilter registros, passando uma id de consulta e uma consulta muito**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="50330-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="50330-154">Para obter mais informações, consulte a seção de saudação *Sincronização Incremental* na [sincronização de dados Offline em aplicativos móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="50330-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="50330-155">Execute o aplicativo de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="50330-155">Run hello client app</span></span>
<span data-ttu-id="50330-156">Com a sincronização offline agora está habilitada, execute o aplicativo de cliente de saudação pelo menos uma vez em cada banco de dados plataforma toopopulate Olá repositório local.</span><span class="sxs-lookup"><span data-stu-id="50330-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="50330-157">Posteriormente, simular um cenário offline e modificar dados de saudação no repositório local Olá enquanto o aplicativo hello está offline.</span><span class="sxs-lookup"><span data-stu-id="50330-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="50330-158">Atualizar o comportamento de sincronização de saudação do aplicativo de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="50330-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="50330-159">Nesta seção, modifique Olá cliente projeto toosimulate um cenário offline usando uma URL de aplicativo inválido para o back-end.</span><span class="sxs-lookup"><span data-stu-id="50330-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="50330-160">Como alternativa, você pode desativar conexões de rede, movendo o dispositivo muito "Modo avião".</span><span class="sxs-lookup"><span data-stu-id="50330-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="50330-161">Quando você adicionar ou alterar itens de dados, essas alterações são mantidas no repositório local hello, mas não sincronizadas do repositório de dados de back-end de toohello até que a conexão de saudação é restabelecida.</span><span class="sxs-lookup"><span data-stu-id="50330-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="50330-162">Em Olá Gerenciador de soluções, abra o arquivo de projeto de Constants.cs de saudação de saudação **portátil** projeto e altere o valor de saudação do `ApplicationURL` toopoint tooan inválido URL:</span><span class="sxs-lookup"><span data-stu-id="50330-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="50330-163">Arquivo TodoItemManager.cs abrir Olá Olá **portátil** projeto e, em seguida, adicionar um **catch** para Olá base **exceção** toohello classe **try... catch** bloco em **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="50330-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="50330-164">Isso **catch** bloco grava o console de toohello de mensagem de exceção hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="50330-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="50330-165">Compilar e executar o aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="50330-165">Build and run hello client app.</span></span>  <span data-ttu-id="50330-166">Adicione alguns novos itens.</span><span class="sxs-lookup"><span data-stu-id="50330-166">Add some new items.</span></span> <span data-ttu-id="50330-167">Observe que uma exceção seja registrada no console de saudação para toosync cada tentativa com hello back-end.</span><span class="sxs-lookup"><span data-stu-id="50330-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="50330-168">Os novos itens só existem no repositório local Olá até que elas podem ser enviadas back-end do toohello móvel.</span><span class="sxs-lookup"><span data-stu-id="50330-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="50330-169">Olá aplicativo de cliente se comporta como se estivesse conectado toohello back-end, dando suporte a que todos os criar, ler, update, as operações de exclusão (CRUD).</span><span class="sxs-lookup"><span data-stu-id="50330-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="50330-170">Feche o aplicativo hello e reiniciá-lo tooverify que você criou novos itens de saudação são repositório local toohello persistente.</span><span class="sxs-lookup"><span data-stu-id="50330-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="50330-171">(Opcional) Use Visual Studio tooview seu toosee de tabela de banco de dados do Azure SQL Olá dados no banco de dados de back-end de saudação não foram alterados.</span><span class="sxs-lookup"><span data-stu-id="50330-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="50330-172">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="50330-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="50330-173">Navegue de banco de dados tooyour no **Azure**->**bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="50330-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="50330-174">Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="50330-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="50330-175">Agora você pode procurar a tabela de banco de dados do SQL tooyour e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="50330-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="50330-176">Atualizar tooreconnect de aplicativo cliente Olá seu back-end móvel</span><span class="sxs-lookup"><span data-stu-id="50330-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="50330-177">Nesta seção, reconecte Olá aplicativo toohello móvel back-end, que simula um aplicativo hello que voltar para o estado online tooan.</span><span class="sxs-lookup"><span data-stu-id="50330-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="50330-178">Quando você executa o gesto de atualização Olá, dados são back-end de móveis tooyour sincronizados.</span><span class="sxs-lookup"><span data-stu-id="50330-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="50330-179">Reabra Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="50330-179">Reopen Constants.cs.</span></span> <span data-ttu-id="50330-180">Olá correto `applicationURL` toopoint toohello corrigir URL.</span><span class="sxs-lookup"><span data-stu-id="50330-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="50330-181">Recriar e execute o aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="50330-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="50330-182">aplicativo Hello tentativas toosync com back-end de aplicativo móvel Olá depois de iniciar.</span><span class="sxs-lookup"><span data-stu-id="50330-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="50330-183">Verifique se que nenhuma exceção é registradas no console de depuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="50330-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="50330-184">(Opcional) Saudação de exibição atualizada dados usando o Pesquisador de objetos do SQL Server ou uma ferramenta REST, como o Fiddler ou [carteiro][6].</span><span class="sxs-lookup"><span data-stu-id="50330-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="50330-185">Aviso Olá dados entre o banco de dados de back-end hello e armazenamento local Olá foi sincronizados.</span><span class="sxs-lookup"><span data-stu-id="50330-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="50330-186">Observe dados saudação foi sincronizados entre o banco de dados de saudação e armazenamento local hello e contém itens Olá adicionados enquanto seu aplicativo estava desconectado.</span><span class="sxs-lookup"><span data-stu-id="50330-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50330-187">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="50330-187">Additional Resources</span></span>
* <span data-ttu-id="50330-188">[Sincronização de Dados Offline em Aplicativos Móveis do Azure][2]</span><span class="sxs-lookup"><span data-stu-id="50330-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="50330-189">[SDK .NET de Aplicativos Móveis do Azure HOWTO][8]</span><span class="sxs-lookup"><span data-stu-id="50330-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
