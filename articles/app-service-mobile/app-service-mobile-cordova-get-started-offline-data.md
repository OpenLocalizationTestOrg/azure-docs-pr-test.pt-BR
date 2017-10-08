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
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Habilitar a sincronização offline para seu aplicativo móvel Cordova
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para Cordova. Sincronização offline permite toointeract de usuários finais com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede. As alterações são armazenadas em um banco de dados local.  Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o serviço remoto hello.

Este tutorial baseia-se em Olá solução de início rápido do Cordova para aplicativos móveis que você cria ao concluir Olá tutorial [início rápido do Apache Cordova]. Neste tutorial, você deve atualizar Olá quickstart tooadd offline recursos de solução de aplicativos móveis do Azure.  Podemos também realce o código de off-line específicos de Olá no aplicativo hello.

toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure]. Para obter detalhes de uso da API, consulte Olá [documentação da API](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Adicionar solução de início rápido de toohello sincronização offline
código de sincronização offline Olá deve ser adicionado toohello aplicativo. Sincronização offline requer Olá armazenamento cordova-sqlite plug-in, que é adicionado automaticamente tooyour aplicativo quando o plug-in do hello os aplicativos móveis do Azure está incluído no projeto de saudação. projeto de início rápido de saudação inclui ambos esses plug-ins.

1. No Gerenciador de soluções do Visual Studio, abra js e substitua Olá código a seguir

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    por este código:

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. Em seguida, substitua Olá código a seguir:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    por este código:

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

    Olá adições de código anterior inicializar o repositório local hello e definir uma tabela local que faz a correspondência de valores de coluna Olá usados no seu Azure back-end. (Não é necessário tooinclude todos os valores de coluna nesse código.)  Olá `version` campo é mantido pelo back-end de saudação móvel e é usado para resolução de conflitos.

    Obter um contexto de sincronização referência toohello chamando **getSyncContext**. Hello contexto de sincronização ajuda a preservar relações de tabela, controle e enviar as alterações em todas as tabelas de um aplicativo cliente tenha modificado quando `.push()` é chamado.

3. Atualize a URL do aplicativo hello aplicativo URL tooyour aplicativo móvel.

4. Em seguida, substitua este código:

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    por este código:

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

    Hello código anterior inicializa o contexto de sincronização de saudação e, em seguida, chama tooget getSyncTable (em vez de pode ser obtida) uma tabela local do toohello de referência.

    Esse código usa Olá banco de dados local para todos os criar, ler, atualizar e excluir operações de tabela (CRUD).

    Este exemplo executa o tratamento de erros simples nos conflitos de sincronização. Um aplicativo real trataria Olá vários erros como condições de rede, conflitos de servidor e outros. Para obter exemplos de código, consulte Olá [sincronização offline].

5. Em seguida, adicione essa sincronização do função tooperform Olá real.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Você decide quando toopush altera o back-end de aplicativo móvel toohello chamando **syncContext.push()**. Por exemplo, você poderia chamar **syncBackend** em um botão de sincronização associado tooa do evento manipulador.

## <a name="offline-sync-considerations"></a>Considerações sobre a sincronização offline

No exemplo hello, Olá **push** método **syncContext** só é chamado na inicialização do aplicativo na função de retorno de chamada de saudação para logon.  Em um aplicativo do mundo real, você também pode fazer essa funcionalidade de sincronização disparada manualmente ou quando altera o estado da rede hello.

Quando a extração é executada em uma tabela que tem pendente atualizações locais rastreadas pelo contexto de hello, puxe a operação automaticamente gatilhos um envio por push. Quando a atualização, a adição e Concluindo itens neste exemplo, você pode omitir Olá explícita **push** chamar, já que ele pode ser redundante.

No código Olá fornecido, todos os registros na tabela de remota todoItem Olá são consultados, mas também é possível toofilter registros, passando uma id de consulta e uma consulta muito**push**. Para obter mais informações, consulte a seção de saudação *Sincronização Incremental* na [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="optional-disable-authentication"></a>(Opcional) Desabilitar a autenticação

Se você não deseja tooset a autenticação antes de testar a sincronização offline, comente a função de retorno de chamada de saudação para logon, mas deixar Olá código dentro de função de retorno de chamada hello removidos.  Depois de comentar as linhas de logon Olá, código Olá segue:

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

Agora, Olá aplicativo sincronizações com hello back-end do Azure quando você executa o aplicativo hello.

## <a name="run-hello-client-app"></a>Execute o aplicativo de cliente Olá
Com a sincronização offline agora está habilitada, você pode executar aplicativos de cliente de saudação pelo menos uma vez em cada plataforma para preencher o banco de dados de armazenamento local de saudação. Posteriormente, simular um cenário offline e modificar dados de saudação no repositório local Olá enquanto o aplicativo hello está offline.

## <a name="optional-test-hello-sync-behavior"></a>(Opcional) Comportamento de sincronização de saudação do teste
Nesta seção, você pode modificar Olá cliente projeto toosimulate um cenário offline usando uma URL de aplicativo inválido para o back-end. Quando você adicionar ou alterar itens de dados, essas alterações são mantidas no armazenamento local, mas não estão sincronizados toohello repositório de dados de back-end até que a conexão de saudação é restabelecida.

1. No hello Gerenciador de soluções, abrir o arquivo de projeto do hello js e altere Olá toopoint de URL de aplicativo para uma URL inválida, como saudação de código a seguir:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. Index, atualizar Olá CSP `<meta>` Olá elemento com a mesma URL inválida.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Criar e executar o aplicativo de cliente hello e observe que uma exceção seja registrada no console de saudação quando o aplicativo hello tenta sincronizar com o back-end de saudação após o logon. Quaisquer novos itens que você adicionar só existem no repositório local Olá até que eles são enviados por push o back-end do toohello móvel. Olá aplicativo de cliente se comporta como se estivesse conectado toohello back-end.

4. Feche o aplicativo hello e reiniciá-lo tooverify que você criou novos itens de saudação são repositório local toohello persistente.

5. (Opcional) Use Visual Studio tooview seu toosee de tabela de banco de dados do Azure SQL Olá dados no banco de dados de back-end de saudação não foram alterados.

    No Visual Studio, abra **Gerenciador de Servidores**. Navegue de banco de dados tooyour no **Azure**->**bancos de dados SQL**. Clique com o botão direito do mouse em seu banco de dados e selecione **Abrir no Pesquisador de Objetos do SQL Server**. Agora você pode procurar a tabela de banco de dados do SQL tooyour e seu conteúdo.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(Opcional) Teste Olá reconexão tooyour móvel back-end

Nesta seção, você pode se reconectar Olá aplicativo toohello móvel back-end, que simula um aplicativo hello volte ao estado online. Quando você entrar, dados são back-end de móveis tooyour sincronizados.

1. Reabra js e restaurar a URL do aplicativo hello.
2. Reabra Index e corrija a URL do aplicativo hello em Olá CSP `<meta>` elemento.
3. Recriar e execute o aplicativo de cliente hello. aplicativo Hello tentativas toosync com back-end de aplicativo móvel Olá após o logon. Verifique se que nenhuma exceção é registradas no console de depuração de saudação.
4. (Opcional) Saudação de exibição atualizada dados usando o Pesquisador de objetos do SQL Server ou uma ferramenta REST, como o Fiddler. Aviso Olá dados entre o banco de dados de back-end hello e armazenamento local Olá foi sincronizados.

    Observe dados saudação foi sincronizados entre o banco de dados de saudação e armazenamento local hello e contém itens Olá adicionados enquanto seu aplicativo estava desconectado.

## <a name="additional-resources"></a>Recursos adicionais
* [sincronização de dados Offline em aplicativos móveis do Azure]
* [Ferramentas do Visual Studio para Apache Cordova]

## <a name="next-steps"></a>Próximas etapas
* Revisão mais avançados recursos de sincronização offline, como resolução de conflito em Olá [sincronização offline]
* Examine a sincronização offline de Olá referência de API no hello [documentação da API](https://azure.github.io/azure-mobile-apps-js-client).

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
