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
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Habilitar sincronização offline para seu aplicativo móvel Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Visão geral
Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para xamarin. Forms. Sincronização offline permite que os usuários finais interajam com um aplicativo móvel, exibindo, adicionando ou modificando dados, mesmo quando não há conexão de rede. As alterações são armazenadas em um banco de dados local. Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o serviço remoto hello.

Este tutorial se baseia na Olá xamarin. Forms quickstart solução para aplicativos móveis que você cria ao concluir o tutorial [criar um aplicativo Xamarin iOS]. solução de início rápido de saudação para xamarin. Forms contém Olá código toosupport sincronização offline, que só precisa toobe habilitado. Neste tutorial, você deve atualizar Olá quickstart solução tooturn recursos offline de saudação do aplicativos móveis do Azure. Podemos também realce o código de off-line específicos de Olá no aplicativo hello. Se você não usar a solução de início rápido de saudação baixada, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso de dados de hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][1].

toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Habilitar a funcionalidade de sincronização offline na solução de início rápido de saudação
código de sincronização offline Hello está incluído no projeto de saudação usando diretivas de pré-processador C#. Olá quando **OFFLINE\_sincronização\_habilitado** símbolo é definido, esses caminhos de código são incluídos na compilação de saudação. Para aplicativos do Windows, instale também plataforma do SQLite hello.

1. No Visual Studio, clique com botão direito solução hello > **gerenciar pacotes NuGet para solução...** , em seguida, procurar e instalar o **Microsoft.Azure.Mobile.Client.SQLiteStore** pacote NuGet para todos os projetos na solução de saudação.
2. Em Olá Solution Explorer, abra o arquivo de TodoItemManager.cs de saudação do projeto Olá com **portátil** em nome de saudação, que é o projeto de biblioteca de classes portátil, em seguida, remova os comentários Olá após diretiva de pré-processador:

        #define OFFLINE_SYNC_ENABLED
3. Dispositivos do Windows toosupport (opcional), instale um dos Olá SQLite pacotes de tempo de execução a seguir:

   * **Tempo de Execução do Windows 8.1**: instale o [SQLite para Windows 8.1][3].
   * **Windows Phone 8.1**: instale o [SQLite para Windows Phone 8.1][4].
   * **Plataforma universal do Windows** instalar [SQLite para Olá Universal do Windows Universal][5].

     Embora Olá quickstart não contém um projeto Universal do Windows, plataforma Universal do Windows de saudação é compatível com o Xamarin Forms.
4. (Opcional) Em cada projeto de aplicativo do Windows, clique com botão direito **referências** > **adicionar referência...** , expanda Olá **Windows** pasta > **extensões**.
    Habilitar Olá apropriado **SQLite para Windows** SDK junto com hello **Visual C++ 2013 em tempo de execução para da Windows** SDK.
    Hello nomes SQLite SDK variam ligeiramente em cada plataforma do Windows.

## <a name="review-hello-client-sync-code"></a>Examine o código de sincronização do cliente Olá
Aqui está uma breve visão geral do que já está incluído no tutorial código Olá Olá `#if OFFLINE_SYNC_ENABLED` diretivas. A funcionalidade de sincronização offline está no arquivo de projeto TodoItemManager.cs Olá no projeto de biblioteca de classes portátil hello. Para obter uma visão geral conceitual do recurso hello, consulte [sincronização de dados Offline em aplicativos móveis do Azure][2].

* Antes de quaisquer operações de tabela podem ser executadas, armazenamento local Olá deve ser inicializado. Olá banco de dados do armazenamento local é inicializado no hello **TodoItemManager** construtor da classe usando Olá código a seguir:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Esse código cria um novo local SQLite banco de dados usando Olá **MobileServiceSQLiteStore** classe.

    Olá **DefineTable** método cria uma tabela no repositório local de saudação que corresponda a campos Olá no tipo hello fornecido.  tipo de saudação não tem tooinclude todas as colunas de saudação que estão no banco de dados remoto hello. É possível toostore um subconjunto de colunas.
* Olá **todoTable** campo **TodoItemManager** é um **IMobileServiceSyncTable** digite, em vez de **IMobileServiceTable**. Essa classe usa Olá banco de dados local para todos os criar, ler, atualizar e excluir operações de tabela (CRUD). Você decide quando essas alterações são enviados por push back-end de aplicativo móvel toohello chamando **PushAsync** em Olá **IMobileServiceSyncContext**. Hello contexto de sincronização ajuda a preservar relações de tabela, controle e enviar as alterações em todas as tabelas de um aplicativo cliente tenha modificado quando **PushAsync** é chamado.

    a seguir Olá **SyncAsync** método é chamado toosync com back-end de aplicativo móvel hello:

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

    Este exemplo usa com o manipulador de sincronização saudação padrão de tratamento de erros simples. Um aplicativo real trataria Olá vários erros como condições de rede e o servidor está em conflito usando um personalizado **IMobileServiceSyncHandler** implementação.

## <a name="offline-sync-considerations"></a>Considerações sobre a sincronização offline
No exemplo hello, Olá **SyncAsync** método é chamado somente na inicialização e quando a sincronização é solicitada.  tooinitiate uma sincronização em um aplicativo do Android ou iOS, pull para baixo na lista de itens de saudação; para o Windows, use Olá **sincronização** botão. Em um aplicativo do mundo real, você também poderia fazer o gatilho de sincronização hello quando alterações de estado da rede hello.

Quando a extração é executada em uma tabela que tem pendente atualizações locais rastreadas pelo contexto de hello, puxe a operação automaticamente gatilhos um envio por push do contexto anterior. Quando a atualização, a adição e Concluindo itens neste exemplo, você pode omitir Olá explícita **PushAsync** chamar.

No código Olá fornecido, todos os registros na tabela TodoItem remota de saudação são consultados, mas também é possível toofilter registros, passando uma id de consulta e uma consulta muito**PushAsync**. Para obter mais informações, consulte a seção de saudação *Sincronização Incremental* na [sincronização de dados Offline em aplicativos móveis do Azure][2].

## <a name="run-hello-client-app"></a>Execute o aplicativo de cliente Olá
Com a sincronização offline agora está habilitada, execute o aplicativo de cliente de saudação pelo menos uma vez em cada banco de dados plataforma toopopulate Olá repositório local. Posteriormente, simular um cenário offline e modificar dados de saudação no repositório local Olá enquanto o aplicativo hello está offline.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Atualizar o comportamento de sincronização de saudação do aplicativo de cliente Olá
Nesta seção, modifique Olá cliente projeto toosimulate um cenário offline usando uma URL de aplicativo inválido para o back-end. Como alternativa, você pode desativar conexões de rede, movendo o dispositivo muito "Modo avião".  Quando você adicionar ou alterar itens de dados, essas alterações são mantidas no repositório local hello, mas não sincronizadas do repositório de dados de back-end de toohello até que a conexão de saudação é restabelecida.

1. Em Olá Gerenciador de soluções, abra o arquivo de projeto de Constants.cs de saudação de saudação **portátil** projeto e altere o valor de saudação do `ApplicationURL` toopoint tooan inválido URL:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Arquivo TodoItemManager.cs abrir Olá Olá **portátil** projeto e, em seguida, adicionar um **catch** para Olá base **exceção** toohello classe **try... catch** bloco em **SyncAsync**. Isso **catch** bloco grava o console de toohello de mensagem de exceção hello, da seguinte maneira:

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Compilar e executar o aplicativo de cliente hello.  Adicione alguns novos itens. Observe que uma exceção seja registrada no console de saudação para toosync cada tentativa com hello back-end. Os novos itens só existem no repositório local Olá até que elas podem ser enviadas back-end do toohello móvel. Olá aplicativo de cliente se comporta como se estivesse conectado toohello back-end, dando suporte a que todos os criar, ler, update, as operações de exclusão (CRUD).
4. Feche o aplicativo hello e reiniciá-lo tooverify que você criou novos itens de saudação são repositório local toohello persistente.
5. (Opcional) Use Visual Studio tooview seu toosee de tabela de banco de dados do Azure SQL Olá dados no banco de dados de back-end de saudação não foram alterados.

    No Visual Studio, abra **Gerenciador de Servidores**. Navegue de banco de dados tooyour no **Azure**->**bancos de dados SQL**. Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**. Agora você pode procurar a tabela de banco de dados do SQL tooyour e seu conteúdo.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Atualizar tooreconnect de aplicativo cliente Olá seu back-end móvel
Nesta seção, reconecte Olá aplicativo toohello móvel back-end, que simula um aplicativo hello que voltar para o estado online tooan. Quando você executa o gesto de atualização Olá, dados são back-end de móveis tooyour sincronizados.

1. Reabra Constants.cs. Olá correto `applicationURL` toopoint toohello corrigir URL.
2. Recriar e execute o aplicativo de cliente hello. aplicativo Hello tentativas toosync com back-end de aplicativo móvel Olá depois de iniciar. Verifique se que nenhuma exceção é registradas no console de depuração de saudação.
3. (Opcional) Saudação de exibição atualizada dados usando o Pesquisador de objetos do SQL Server ou uma ferramenta REST, como o Fiddler ou [carteiro][6]. Aviso Olá dados entre o banco de dados de back-end hello e armazenamento local Olá foi sincronizados.

    Observe dados saudação foi sincronizados entre o banco de dados de saudação e armazenamento local hello e contém itens Olá adicionados enquanto seu aplicativo estava desconectado.

## <a name="additional-resources"></a>Recursos adicionais
* [Sincronização de Dados Offline em Aplicativos Móveis do Azure][2]
* [SDK .NET de Aplicativos Móveis do Azure HOWTO][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
