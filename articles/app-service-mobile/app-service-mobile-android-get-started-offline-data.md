---
title: "sincronização offline de aaaEnable para seu aplicativo móvel do Azure (Android)"
description: "Saiba como toouse serviço de aplicativo móvel de aplicativos toocache e sincronização de dados offline no seu aplicativo do Android"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Habilitar sincronização offline para seu aplicativo móvel Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Visão geral
Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para Android. Sincronização offline permite toointeract de usuários finais com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede. As alterações são armazenadas em um banco de dados local. Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o back-end de saudação remoto.

Se esta for sua primeira experiência com aplicativos móveis do Azure, primeiro você deve concluir o tutorial de saudação [criar um aplicativo do Android]. Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso de dados de hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure].

## <a name="update-hello-app-toosupport-offline-sync"></a>Atualizar sincronização offline do hello aplicativo toosupport
Com a sincronização offline, você ler tooand gravação de um *tabela sincronização* (usando Olá *IMobileServiceSyncTable* interface), que é parte de um **SQLite** banco de dados em seu dispositivo.

alterações de pull e toopush entre o dispositivo hello e serviços móveis do Azure, use um *contexto de sincronização* (*MobileServiceClient.SyncContext*), que você inicializar com o banco de dados local Olá toostore dados localmente.

1. Em `TodoActivity.java`, comente a definição existente de saudação do `mToDoTable` e remova os comentários de versão da tabela Olá sincronização:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. Em Olá `onCreate` método, comente inicialização existente de saudação do `mToDoTable` e remova essa definição:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. Em `refreshItemsFromTable` comente a definição de saudação do `results` e remova essa definição:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Comente a definição de saudação do `refreshItemsFromMobileServiceTable`.
5. Remova a definição de saudação do `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Remova a definição de saudação do `sync`:
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a>Aplicativo de teste de saudação
Nesta seção, você testar o comportamento de saudação com Wi-Fi no e desligue WiFi toocreate um cenário offline.

Quando você adiciona itens de dados, são mantidos no armazenamento local de SQLite Olá, mas o serviço móvel toohello não sincronizado até que você pressione Olá **atualização** botão. Outros aplicativos podem ter requisitos diferentes sobre quando os dados tiverem toobe sincronizado, mas para fins de demonstração este tutorial tem usuário Olá a solicitá-la explicitamente.

Quando você pressiona o botão, inicia uma nova tarefa em segundo plano. Primeiro, ele envia todas as alterações feitas toohello armazenamento local usando o contexto de sincronização e, em seguida, alterado recebe todos os dados de tabela local toohello do Azure.

### <a name="offline-testing"></a>Teste offline
1. Dispositivo de saudação do local ou o simulador no *modo avião*. Isso cria um cenário offline.
2. Adicione alguns itens *ToDo* ou marque alguns itens como concluídos. Encerre Olá dispositivo ou simulador (ou aplicativo hello fechamento forçado) e reinicie. Verifique se que as alterações foram persistidas no dispositivo Olá porque eles são mantidos no repositório local do SQLite de saudação.
3. Exibir o conteúdo de saudação do hello Azure *TodoItem* tabela com uma ferramenta SQL, como *SQL Server Management Studio*, ou um cliente REST, como *Fiddler* ou  *Carteiro*. Verifique se novos itens de saudação tem *não* foi sincronizado toohello server
   
       + Para um back-end node. js, vá toohello [portal do Azure](https://portal.azure.com/), e em seu aplicativo móvel back-end em **tabelas fácil** > **TodoItem** tooview conteúdo Olá Olá `TodoItem` tabela.
       + Para um back-end .NET, tabela de saudação do modo de exibição de conteúdo com uma ferramenta SQL, como *SQL Server Management Studio*, ou um cliente REST, como *Fiddler* ou *carteiro*.
4. Ative o Wi-Fi no simulador ou dispositivo hello. Em seguida, pressione Olá **atualização** botão.
5. Exiba dados de TodoItem de saudação novamente no hello portal do Azure. Olá que todoitems novas e alteradas agora deve aparecer.

## <a name="additional-resources"></a>Recursos adicionais
* [sincronização de dados Offline em aplicativos móveis do Azure]
* [Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure] \(Observação: Olá vídeo está em serviços móveis, mas a sincronização offline funciona de maneira semelhante em aplicativos móveis do Azure\)

<!-- URLs. -->

[sincronização de dados Offline em aplicativos móveis do Azure]: app-service-mobile-offline-data-sync.md

[criar um aplicativo do Android]: app-service-mobile-android-get-started.md

[Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

