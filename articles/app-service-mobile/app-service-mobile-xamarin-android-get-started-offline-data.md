---
title: "sincronização offline de aaaEnable para seu aplicativo móvel do Azure (Xamarin Android)"
description: "Saiba como toouse aplicativo do serviço de aplicativo móvel toocache e sincronização de dados offline em seu aplicativo Xamarin Android"
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a>Habilitar sincronização offline para seu aplicativo móvel Xamarin.Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Visão geral
Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para xamarin. Sincronização offline permite toointeract de usuários finais com um aplicativo móvel – exibindo, adicionando ou modificando dados – mesmo quando não há nenhuma conexão de rede. As alterações são armazenadas em um banco de dados local.
Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o serviço remoto hello.

Neste tutorial, você atualizar o projeto de cliente de saudação do tutorial Olá [criar um aplicativo Xamarin Android] toosupport Olá recursos offline de aplicativos móveis do Azure. Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso de dados de hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Atualizar recursos offline de toosupport Olá de aplicativo cliente
Recursos offline de aplicativo móvel do Azure permitem que você toointeract com um banco de dados local quando estiver em um cenário offline. toouse esses recursos em seu aplicativo, você inicializar um [SyncContext] repositório local tooa. Em seguida, fazer referência a sua tabela por meio de saudação [IMobileServiceSyncTable] [IMobileServiceSyncTable] interface. SQLite é usado como o repositório local de saudação no dispositivo de saudação.

1. No Visual Studio, abra o Gerenciador de pacotes do NuGet Olá no projeto de saudação que você concluiu nas Olá [criar um aplicativo Xamarin Android] tutorial.  Procurar e instalar Olá **Microsoft.Azure.Mobile.Client.SQLiteStore** pacote NuGet.
2. Abrir o arquivo de ToDoActivity.cs hello e remova os Olá `#define OFFLINE_SYNC_ENABLED` definição.
3. No Visual Studio, pressione Olá **F5** toorebuild e aplicativo de cliente de execução Olá da chave. aplicativo Hello funciona hello, mesmo que ele foi antes de você habilitou a sincronização offline. No entanto, o banco de dados local Olá agora é preenchido com dados que podem ser usados em um cenário offline.

## <a name="update-sync"></a>Atualizar Olá aplicativo toodisconnect de saudação back-end
Nesta seção, você deve interromper Olá conexão tooyour aplicativo móvel back-end toosimulate uma situação offline. Quando você adiciona itens de dados, o manipulador de exceção informa que o aplicativo hello está no modo offline. Nesse estado, novos itens adicionados no local de saudação armazenam em são sincronizados para o back-end de aplicativo móvel hello quando um envio por push é executado em um estado conectado.

1. Edite ToDoActivity.cs no projeto compartilhado hello. Saudação de alteração **applicationURL** toopoint tooan inválido URL:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Você também pode demonstrar o comportamento offline desabilitando Wi-Fi e redes de celulares no dispositivo hello ou usando o modo avião.
2. Pressione **F5** toobuild e executar o aplicativo hello. Observe a sincronização falha na atualização hello quando o aplicativo iniciado.
3. Insira os novos itens e observe que o envio falha com um status [CancelledByNetworkError] toda vez que você clicar em **Salvar**. No entanto, novos itens de tarefas Olá existem no repositório local Olá até que elas podem ser enviadas back-end de aplicativo móvel toohello.  Em um de produção o aplicativo, se você suprimir essas exceções Olá cliente aplicativo se comporta como se ainda estiver conectado back-end de aplicativo móvel toohello.
4. Feche o aplicativo hello e reiniciá-lo tooverify que você criou novos itens de saudação são repositório local toohello persistente.
5. (Opcional) No Visual Studio, abra o **Gerenciador de Servidores**. Navegue de banco de dados tooyour no **Azure**->**bancos de dados SQL**. Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**. Agora você pode procurar a tabela de banco de dados do SQL tooyour e seu conteúdo. Verifique se que dados Olá no banco de dados de back-end de saudação não foi alterado.
6. (Opcional) Use uma ferramenta REST, como o Fiddler ou carteiro tooquery seu back-end móvel, usando uma consulta GET na forma `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Atualizar Olá aplicativo tooreconnect seu back-end do aplicativo móvel
Nesta seção, reconecte Olá aplicativo toohello aplicativo móvel back-end. Quando você executa o aplicativo hello primeiro, Olá `OnCreate` chamadas de manipulador de eventos `OnRefreshItemsSelected`. Este método chama `SyncAsync` toosync repositório local com o banco de dados de back-end de saudação.

1. Abra ToDoActivity.cs no projeto compartilhado hello e reverter a alteração de saudação **applicationURL** propriedade.
2. Olá pressione **F5** toorebuild e aplicativo hello execução da chave. Olá aplicativo sincroniza as alterações locais com hello Azure Mobile App back-end usando operações de push e pull quando hello `OnRefreshItemsSelected` método é executado.
3. (Opcional) Saudação de exibição atualizada dados usando o Pesquisador de objetos do SQL Server ou uma ferramenta REST, como o Fiddler. Aviso Olá dados entre o banco de dados de back-end de aplicativo do Azure Mobile hello e armazenamento local Olá foi sincronizados.
4. No aplicativo hello, clique em seleção de saudação caixa ao lado de alguns toocomplete de itens-los no repositório local hello.

   `CheckItem`chamadas `SyncAsync` item toosync cada concluída com o back-end de aplicativo móvel hello. `SyncAsync` chama push e pull. **Sempre que você executar um pull em uma tabela cliente Olá fez as alterações, um envio por push sempre é executado automaticamente**. Isso garante que todas as tabelas no repositório local juntamente com os relacionamentos permaneçam consistentes. Esse comportamento pode resultar em um push inesperado. Para obter mais informações sobre esse comportamento, confira [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="review-hello-client-sync-code"></a>Examine o código de sincronização do cliente Olá
projeto de cliente do Xamarin Olá baixado quando você concluiu o tutorial Olá [criar um aplicativo Xamarin Android] já contém o código de suporte a sincronização offline usando um banco de dados local do SQLite. Aqui está uma breve visão geral do que já está incluído no código tutorial hello. Para obter uma visão geral conceitual do recurso hello, consulte [sincronização de dados Offline em aplicativos móveis do Azure].

* Antes de quaisquer operações de tabela podem ser executadas, armazenamento local Olá deve ser inicializado. Olá banco de dados do armazenamento local é inicializado quando `ToDoActivity.OnCreate()` executa `ToDoActivity.InitLocalStoreAsync()`. Esse método cria um banco de dados local do SQLite usando Olá `MobileServiceSQLiteStore` classe fornecida pelo SDK do cliente Olá os aplicativos móveis do Azure.

    Olá `DefineTable` método cria uma tabela no armazenamento local de saudação que corresponda a campos de saudação tipo hello fornecido, `ToDoItem` nesse caso. tipo de saudação não tem tooinclude todas as colunas de saudação que estão no banco de dados remoto hello. É possível toostore apenas um subconjunto de colunas.

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* Olá `toDoTable` membro `ToDoActivity` é de saudação `IMobileServiceSyncTable` digite, em vez de `IMobileServiceTable`. Olá IMobileServiceSyncTable direciona todas criar, ler, atualizar e excluir (CRUD) tabela operações toohello loja local do banco de dados.

    Você decide quando alterações são enviadas back-end de aplicativo do Azure Mobile toohello chamando `IMobileServiceSyncContext.PushAsync()`. Hello contexto de sincronização ajuda a preservar relações de tabela, controle e enviar as alterações em todas as tabelas de um aplicativo cliente tenha modificado quando `PushAsync` é chamado.

    chamadas de código Olá fornecido `ToDoActivity.SyncAsync()` toosync sempre Olá todoitem lista é atualizada ou um todoitem é adicionado ou foi concluído. sincronizações de código Olá após cada alteração local.

    No código Olá fornecido, todos os registros em Olá remoto `TodoItem` tabela são consultadas, mas também é possível toofilter registros, passando uma id de consulta e uma consulta muito`PushAsync`. Para obter mais informações, consulte a seção de saudação *Sincronização Incremental* na [sincronização de dados Offline em aplicativos móveis do Azure].

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a>Recursos adicionais
* [sincronização de dados Offline em aplicativos móveis do Azure]
* [SDK .NET de Aplicativos Móveis do Azure HOWTO][8]

<!-- URLs. -->
[criar um aplicativo Xamarin Android]: ../app-service-mobile-xamarin-android-get-started.md
[sincronização de dados Offline em aplicativos móveis do Azure]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Criar um aplicativo Android do Xamarin]: app-service-mobile-xamarin-android-get-started.md
[Sincronização de dados offline em Aplicativos Móveis do Azure]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
