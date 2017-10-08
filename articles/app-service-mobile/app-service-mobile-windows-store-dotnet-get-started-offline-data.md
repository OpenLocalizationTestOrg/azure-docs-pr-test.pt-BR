---
title: "sincronização offline de aaaEnable para seu aplicativo do Windows UWP (plataforma Universal) com aplicativos móveis | Microsoft Docs"
description: "Saiba como toouse um aplicativo do Azure Mobile toocache e sincronização de dados offline em seu aplicativo do Windows UWP (plataforma Universal)."
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Habilitar sincronização offline para o seu aplicativo do Windows
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como off-line tooadd dão suporte ao aplicativo do Windows UWP (plataforma Universal) tooa usando um back-end do aplicativo do Azure Mobile. Sincronização offline permite toointeract de usuários finais com um aplicativo móvel – exibindo, adicionando ou modificando dados - mesmo quando não há nenhuma conexão de rede. As alterações são armazenadas em um banco de dados local. Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o back-end de saudação remoto.

Neste tutorial, você atualizar o projeto de aplicativo UWP de saudação do tutorial de saudação [criar um aplicativo do Windows] toosupport Olá recursos offline de aplicativos móveis do Azure. Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso de dados de hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="requirements"></a>Requisitos
Este tutorial requer Olá os pré-requisitos a seguir:

* Visual Studio 2013 em execução no Windows 8.1 ou mais recente.
* Conclusão de [Criar um aplicativo do Windows][Criar um aplicativo do Windows].
* [Armazenamento do SQLite dos Serviços Móveis Azure][sqlite store nuget]
* [SQLite para desenvolvimento na Plataforma Universal do Windows](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Atualizar recursos offline de toosupport Olá de aplicativo cliente
Recursos offline de aplicativo móvel do Azure permitem que você toointeract com um banco de dados local quando estiver em um cenário offline. toouse esses recursos em seu aplicativo, você inicializar um [SyncContext] [ synccontext] repositório local tooa. Faça referência a sua tabela por meio de saudação [IMobileServiceSyncTable][IMobileServiceSyncTable] interface. SQLite é usado como o repositório local de saudação no dispositivo de saudação.

1. Instalar Olá [tempo de execução do SQLite para Olá plataforma Universal do Windows](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. No Visual Studio, abra o Gerenciador de pacotes do NuGet Olá para o projeto de aplicativo UWP Olá que você concluiu nas Olá [criar um aplicativo do Windows] tutorial.
    Procurar e instalar Olá **Microsoft.Azure.Mobile.Client.SQLiteStore** pacote NuGet.
3. No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** > **Adicionar Referência...** >**Universal do Windows**>**Extensões**; em seguida, habilite o **SQLite para Plataforma Universal do Windows** e o **Tempo de execução do Visual C++ 2015 para aplicativos da Plataforma Universal do Windows**.

    ![Adicionar referência SQLite UWP][1]
4. Abrir o arquivo de MainPage.xaml.cs hello e remova os Olá `#define OFFLINE_SYNC_ENABLED` definição.
5. No Visual Studio, pressione Olá **F5** toorebuild e aplicativo de cliente de execução Olá da chave. aplicativo Hello funciona hello, mesmo que ele foi antes de você habilitou a sincronização offline. No entanto, o banco de dados local Olá agora é preenchido com dados que podem ser usados em um cenário offline.

## <a name="update-sync"></a>Atualizar Olá aplicativo toodisconnect de saudação back-end
Nesta seção, você deve interromper Olá conexão tooyour aplicativo móvel back-end toosimulate uma situação offline. Quando você adiciona itens de dados, o manipulador de exceção informa que o aplicativo hello está no modo offline. Nesse estado, novos itens adicionados no local de saudação armazenam em serão sincronizados para Olá back-end do aplicativo móvel quando push lado é executado em um estado conectado.

1. Edite App.xaml.cs no projeto compartilhado hello. Comente a inicialização de saudação do hello **MobileServiceClient** e adicione Olá linha, que usa uma URL de aplicativo móvel inválido a seguir:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    Você também pode demonstrar o comportamento offline desabilitando Wi-Fi e redes de celulares no dispositivo hello ou usar o modo avião.
2. Pressione **F5** toobuild e executar o aplicativo hello. Observe a sincronização falha na atualização hello quando o aplicativo iniciado.
3. Digite os novos itens e observe que o envio falha com um status [CancelledByNetworkError] toda vez que você clicar em **Salvar**. No entanto, novos itens de tarefas Olá existem no repositório local Olá até que elas podem ser enviadas back-end de aplicativo móvel toohello.  Em um de produção o aplicativo, se você suprimir essas exceções Olá cliente aplicativo se comporta como se ainda estiver conectado back-end de aplicativo móvel toohello.
4. Feche o aplicativo hello e reiniciá-lo tooverify que você criou novos itens de saudação são repositório local toohello persistente.
5. (Opcional) No Visual Studio, abra o **Gerenciador de Servidores**. Navegue de banco de dados tooyour no **Azure**->**bancos de dados SQL**. Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**. Agora você pode procurar a tabela de banco de dados do SQL tooyour e seu conteúdo. Verifique se que dados Olá no banco de dados de back-end de saudação não foi alterado.
6. (Opcional) Use uma ferramenta REST, como o Fiddler ou carteiro tooquery seu back-end móvel, usando uma consulta GET na forma `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Atualizar Olá aplicativo tooreconnect seu back-end do aplicativo móvel
Nesta seção, você pode se reconectar Olá aplicativo toohello aplicativo móvel back-end. Essas alterações simular a reconexão de rede no aplicativo hello.

Quando você executa o aplicativo hello primeiro, Olá `OnNavigatedTo` chamadas de manipulador de eventos `InitLocalStoreAsync`. Este método chama `SyncAsync` toosync repositório local com o banco de dados de back-end de saudação. aplicativo Hello tentativas toosync na inicialização.

1. Abra App.xaml.cs no projeto compartilhado hello e remova sua inicialização anterior do `MobileServiceClient` URL de aplicativo móvel toouse Olá Olá correto.
2. Olá pressione **F5** toorebuild e aplicativo hello execução da chave. Olá aplicativo sincroniza as alterações locais com hello Azure Mobile App back-end usando operações de push e pull quando hello `OnNavigatedTo` executa do manipulador de eventos.
3. (Opcional) Saudação de exibição atualizada dados usando o Pesquisador de objetos do SQL Server ou uma ferramenta REST, como o Fiddler. Aviso Olá dados entre o banco de dados de back-end de aplicativo do Azure Mobile hello e armazenamento local Olá foi sincronizados.
4. No aplicativo hello, clique em seleção de saudação caixa ao lado de alguns toocomplete de itens-los no repositório local hello.

   `UpdateCheckedTodoItem`chamadas `SyncAsync` item toosync cada concluída com o back-end de aplicativo móvel hello. `SyncAsync` chama push e pull. No entanto, **sempre que você executar um pull em uma tabela cliente Olá fez as alterações, um envio por push sempre é executado automaticamente**. Esse comportamento garante que todas as tabelas no armazenamento local de saudação junto com relações permanecem consistentes. Esse comportamento pode resultar em um push inesperado.  Para obter mais informações sobre esse comportamento, confira [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="api-summary"></a>Resumo da API
recursos offline de saudação de toosupport dos serviços móveis, usamos Olá [IMobileServiceSyncTable] interface e inicializado [MobileServiceClient.SyncContext] [ synccontext] com um banco de dados local do SQLite. Quando off-line, as operações CRUD normais Olá para aplicativos móveis trabalhem como se Olá aplicativo ainda está conectado enquanto Olá operações no repositório local hello. Olá métodos a seguir é repositório local do hello toosynchronize usado com o servidor de saudação:

* **[PushAsync]**  como esse método é um membro de [IMobileServicesSyncContext], alterações em todas as tabelas são enviados por push toohello back-end. Somente os registros com as alterações locais são enviados toohello server.
* **[PullAsync]** Um pull é iniciado de um [IMobileServiceSyncTable]. Quando houver alterações controladas na tabela hello, um envio implícita é executado toomake-se de que todas as tabelas no armazenamento local de saudação junto com relações permaneçam consistentes. Olá *pushOtherTables* parâmetro controla se outras tabelas no contexto de saudação são enviados por push em um envio implícita. Olá *consulta* parâmetro aceita um [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] ou saudação de toofilter de cadeia de caracteres de consulta OData retornou dados. Olá *queryId* parâmetro é usado toodefine a sincronização incremental. Para saber mais, veja [Sincronização de Dados Offline em Aplicativos Móveis do Azure](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  seu aplicativo deve chamar periodicamente dados método toopurge obsoleto do armazenamento local hello. Saudação de uso *forçar* parâmetro quando precisar toopurge as alterações que ainda não foram sincronizadas.

Para saber mais sobre esses conceitos, veja [Sincronização de Dados Offline em Aplicativos Móveis do Azure](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>Mais informações
Olá tópicos a seguir fornecem informações detalhadas adicionais no recurso de sincronização offline de saudação de aplicativos móveis:

* [sincronização de dados Offline em aplicativos móveis do Azure]
* [SDK .NET de Aplicativos Móveis do Azure HOWTO][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[sincronização de dados Offline em aplicativos móveis do Azure]: app-service-mobile-offline-data-sync.md
[Criar um aplicativo do Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
