---
title: "sincronização offline de aaaEnable para seu aplicativo móvel do Azure (Xamarin iOS)"
description: "Saiba como toouse aplicativo do serviço de aplicativo móvel toocache e sincronização de dados offline no aplicativo Xamarin iOS"
documentationcenter: xamarin
author: ggailey777
manager: cfowler
editor: 
services: app-service\mobile
ms.assetid: 828a287c-5d58-4540-9527-1309ebb0f32b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5243f2d292377d8de103a40f45d649394f11b97c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a>Habilitar sincronização offline para seu aplicativo móvel Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Visão geral
Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para xamarin. Sincronização offline permite toointeract de usuários finais com um aplicativo móvel – exibindo, adicionando ou modificando dados – mesmo quando não há nenhuma conexão de rede. As alterações são armazenadas em um banco de dados local. Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o serviço remoto hello.

Neste tutorial, atualizar o projeto de aplicativo xamarin saudação do [criar um aplicativo Xamarin iOS] toosupport Olá recursos offline de aplicativos móveis do Azure. Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar Olá pacotes de extensão de acesso de dados ao seu projeto. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Atualizar recursos offline de toosupport Olá de aplicativo cliente
Recursos offline de aplicativo móvel do Azure permitem que você toointeract com um banco de dados local quando estiver em um cenário offline. toouse esses recursos em seu aplicativo, inicializar um [SyncContext] repositório local tooa. Referência de tabela por meio da interface de saudação [IMobileServiceSyncTable]. SQLite é usado como o repositório local de saudação no dispositivo de saudação.

1. Gerenciador de pacotes do NuGet Olá Abrir projeto Olá que você concluiu nas Olá [criar um aplicativo Xamarin iOS] tutorial, em seguida, procurar e instalar Olá **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet pacote.
2. Abrir o arquivo de QSTodoService.cs hello e remova os Olá `#define OFFLINE_SYNC_ENABLED` definição.
3. Recriar e execute o aplicativo de cliente hello. aplicativo Hello funciona hello, mesmo que ele foi antes de você habilitou a sincronização offline. No entanto, o banco de dados local Olá agora é preenchido com dados que podem ser usados em um cenário offline.

## <a name="update-sync"></a>Atualizar Olá aplicativo toodisconnect de saudação back-end
Nesta seção, você deve interromper Olá conexão tooyour aplicativo móvel back-end toosimulate uma situação offline. Quando você adiciona itens de dados, o manipulador de exceção informa que o aplicativo hello está no modo offline. Nesse estado, novos itens adicionados no local de saudação armazenam em serão sincronizados para Olá back-end do aplicativo móvel quando push lado é executado em um estado conectado.

1. Edite QSToDoService.cs no projeto compartilhado hello. Saudação de alteração **applicationURL** toopoint tooan inválido URL:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Você também pode demonstrar o comportamento offline desabilitando Wi-Fi e redes de celulares no dispositivo hello ou usando o modo avião.
2. Compilar e executar o aplicativo hello. Observe a sincronização falha na atualização hello quando o aplicativo iniciado.
3. Insira os novos itens e observe que o envio falha com um status [CancelledByNetworkError] toda vez que você clicar em **Salvar**. No entanto, novos itens de tarefas Olá existem no repositório local Olá até que elas podem ser enviadas back-end de aplicativo móvel toohello.  Em um de produção o aplicativo, se você suprimir essas exceções Olá cliente aplicativo se comporta como se ainda estiver conectado back-end de aplicativo móvel toohello.
4. Feche o aplicativo hello e reiniciá-lo tooverify que você criou novos itens de saudação são repositório local toohello persistente.
5. (Opcional) Se você tiver o Visual Studio instalado em um computador, abra o **Gerenciador de Servidores**. Navegue de banco de dados tooyour no **Azure**-> **bancos de dados SQL**. Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**. Agora você pode procurar a tabela de banco de dados do SQL tooyour e seu conteúdo. Verifique se que dados Olá no banco de dados de back-end de saudação não foi alterado.
6. (Opcional) Use uma ferramenta REST, como o Fiddler ou carteiro tooquery seu back-end móvel, usando uma consulta GET na forma `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Atualizar Olá aplicativo tooreconnect seu back-end do aplicativo móvel
Nesta seção, reconecte Olá aplicativo toohello aplicativo móvel back-end. Isso simula o aplicativo hello mudança de estado offline tooan estado online com o back-end de aplicativo móvel hello.   Se você simulados quebra de rede Olá desativando a conectividade de rede, nenhuma alteração de código é necessários.
Ative rede Olá novamente.  Quando você executa o aplicativo hello primeiro, Olá `RefreshDataAsync` método é chamado. Por sua vez chama `SyncAsync` toosync repositório local com o banco de dados de back-end de saudação.

1. Abra QSToDoService.cs no projeto compartilhado hello e reverter a alteração de saudação **applicationURL** propriedade.
2. Recriar e execute o aplicativo hello. Olá aplicativo sincroniza as alterações locais com hello Azure Mobile App back-end usando operações de push e pull quando hello `OnRefreshItemsSelected` método é executado.
3. (Opcional) Saudação de exibição atualizada dados usando o Pesquisador de objetos do SQL Server ou uma ferramenta REST, como o Fiddler. Aviso Olá dados entre o banco de dados de back-end de aplicativo do Azure Mobile hello e armazenamento local Olá foi sincronizados.
4. No aplicativo hello, clique em seleção de saudação caixa ao lado de alguns toocomplete de itens-los no repositório local hello.

   `CompleteItemAsync`chamadas `SyncAsync` item toosync cada concluída com o back-end de aplicativo móvel hello. `SyncAsync` chama push e pull.
   **Sempre que você executar um pull em uma tabela cliente Olá fez as alterações, um envio por push no contexto de sincronização do cliente Olá sempre é executado pela primeira vez automaticamente**. push implícita Olá garante que todas as tabelas no armazenamento local de saudação junto com relações permanecem consistentes. Para obter mais informações sobre esse comportamento, confira [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="review-hello-client-sync-code"></a>Examine o código de sincronização do cliente Olá
projeto de cliente do Xamarin Olá baixado quando você concluiu o tutorial Olá [criar um aplicativo Xamarin iOS] já contém o código de suporte a sincronização offline usando um banco de dados local do SQLite. Aqui está uma breve visão geral do que já está incluído no código tutorial hello. Para obter uma visão geral conceitual do recurso hello, consulte [sincronização de dados Offline em aplicativos móveis do Azure].

* Antes de quaisquer operações de tabela podem ser executadas, armazenamento local Olá deve ser inicializado. Olá banco de dados do armazenamento local é inicializado quando `QSTodoListViewController.ViewDidLoad()` executa `QSTodoService.InitializeStoreAsync()`. Esse método cria um novo local SQLite banco de dados usando Olá `MobileServiceSQLiteStore` classe fornecida pelo cliente de aplicativo do Azure Mobile Olá SDK.

    Olá `DefineTable` método cria uma tabela no armazenamento local de saudação que corresponda a campos de saudação tipo hello fornecido, `ToDoItem` nesse caso. tipo de saudação não tem tooinclude todas as colunas de saudação que estão no banco de dados remoto hello. É possível toostore apenas um subconjunto de colunas.

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* Olá `todoTable` membro `QSTodoService` é de saudação `IMobileServiceSyncTable` digite, em vez de `IMobileServiceTable`. Olá IMobileServiceSyncTable direciona todas criar, ler, atualizar e excluir (CRUD) tabela operações toohello loja local do banco de dados.

    Você decide quando essas alterações são enviados por push back-end de aplicativo do Azure Mobile toohello chamando `IMobileServiceSyncContext.PushAsync()`. Hello contexto de sincronização ajuda a preservar relações de tabela, controle e enviar as alterações em todas as tabelas de um aplicativo cliente tenha modificado quando `PushAsync` é chamado.

    chamadas de código Olá fornecido `QSTodoService.SyncAsync()` toosync sempre Olá todoitem lista é atualizada ou um todoitem é adicionado ou foi concluído. O aplicativo é sincronizado a cada alteração local. Se uma recepção é executada em uma tabela que tem as atualizações locais pendentes controladas pelo contexto hello, essa operação de recepção automaticamente irá disparar um envio por push do contexto primeiro.

    No código Olá fornecido, todos os registros em Olá remoto `TodoItem` tabela são consultadas, mas também é possível toofilter registros, passando uma id de consulta e uma consulta muito`PushAsync`. Para obter mais informações, consulte a seção de saudação *Sincronização Incremental* na [sincronização de dados Offline em aplicativos móveis do Azure].

        // QSTodoService.cs
        public async Task SyncAsync()
        {
            try
            {
                await client.SyncContext.PushAsync();
                await todoTable.PullAsync("allTodoItems", todoTable.CreateQuery()); // query ID is used for incremental sync
            }

            catch (MobileServiceInvalidOperationException e)
            {
                Console.Error.WriteLine(@"Sync Failed: {0}", e.Message);
            }
        }

## <a name="additional-resources"></a>Recursos adicionais
* [sincronização de dados Offline em aplicativos móveis do Azure]
* [SDK .NET de Aplicativos Móveis do Azure HOWTO][8]

<!-- Images -->

<!-- URLs. -->
[criar um aplicativo Xamarin iOS]: app-service-mobile-xamarin-ios-get-started.md
[sincronização de dados Offline em aplicativos móveis do Azure]: app-service-mobile-offline-data-sync.md
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
