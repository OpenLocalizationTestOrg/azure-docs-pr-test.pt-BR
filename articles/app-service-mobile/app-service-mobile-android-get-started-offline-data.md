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
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="aab65-103">Habilitar sincronização offline para seu aplicativo móvel Android</span><span class="sxs-lookup"><span data-stu-id="aab65-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="aab65-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="aab65-104">Overview</span></span>
<span data-ttu-id="aab65-105">Este tutorial apresenta o recurso de sincronização offline de saudação de aplicativos móveis do Azure para Android.</span><span class="sxs-lookup"><span data-stu-id="aab65-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="aab65-106">Sincronização offline permite toointeract de usuários finais com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="aab65-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="aab65-107">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="aab65-107">Changes are stored in a local database.</span></span> <span data-ttu-id="aab65-108">Depois que o dispositivo de saudação estiver online novamente, essas alterações são sincronizadas com o back-end de saudação remoto.</span><span class="sxs-lookup"><span data-stu-id="aab65-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="aab65-109">Se esta for sua primeira experiência com aplicativos móveis do Azure, primeiro você deve concluir o tutorial de saudação [criar um aplicativo do Android].</span><span class="sxs-lookup"><span data-stu-id="aab65-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="aab65-110">Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso de dados de hello.</span><span class="sxs-lookup"><span data-stu-id="aab65-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="aab65-111">Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="aab65-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="aab65-112">toolearn mais sobre o recurso de sincronização offline hello, consulte o tópico de saudação [sincronização de dados Offline em aplicativos móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="aab65-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="aab65-113">Atualizar sincronização offline do hello aplicativo toosupport</span><span class="sxs-lookup"><span data-stu-id="aab65-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="aab65-114">Com a sincronização offline, você ler tooand gravação de um *tabela sincronização* (usando Olá *IMobileServiceSyncTable* interface), que é parte de um **SQLite** banco de dados em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aab65-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="aab65-115">alterações de pull e toopush entre o dispositivo hello e serviços móveis do Azure, use um *contexto de sincronização* (*MobileServiceClient.SyncContext*), que você inicializar com o banco de dados local Olá toostore dados localmente.</span><span class="sxs-lookup"><span data-stu-id="aab65-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="aab65-116">Em `TodoActivity.java`, comente a definição existente de saudação do `mToDoTable` e remova os comentários de versão da tabela Olá sincronização:</span><span class="sxs-lookup"><span data-stu-id="aab65-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="aab65-117">Em Olá `onCreate` método, comente inicialização existente de saudação do `mToDoTable` e remova essa definição:</span><span class="sxs-lookup"><span data-stu-id="aab65-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="aab65-118">Em `refreshItemsFromTable` comente a definição de saudação do `results` e remova essa definição:</span><span class="sxs-lookup"><span data-stu-id="aab65-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="aab65-119">Comente a definição de saudação do `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="aab65-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="aab65-120">Remova a definição de saudação do `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="aab65-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="aab65-121">Remova a definição de saudação do `sync`:</span><span class="sxs-lookup"><span data-stu-id="aab65-121">Uncomment hello definition of `sync`:</span></span>
   
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

## <a name="test-hello-app"></a><span data-ttu-id="aab65-122">Aplicativo de teste de saudação</span><span class="sxs-lookup"><span data-stu-id="aab65-122">Test hello app</span></span>
<span data-ttu-id="aab65-123">Nesta seção, você testar o comportamento de saudação com Wi-Fi no e desligue WiFi toocreate um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="aab65-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="aab65-124">Quando você adiciona itens de dados, são mantidos no armazenamento local de SQLite Olá, mas o serviço móvel toohello não sincronizado até que você pressione Olá **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="aab65-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="aab65-125">Outros aplicativos podem ter requisitos diferentes sobre quando os dados tiverem toobe sincronizado, mas para fins de demonstração este tutorial tem usuário Olá a solicitá-la explicitamente.</span><span class="sxs-lookup"><span data-stu-id="aab65-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="aab65-126">Quando você pressiona o botão, inicia uma nova tarefa em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="aab65-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="aab65-127">Primeiro, ele envia todas as alterações feitas toohello armazenamento local usando o contexto de sincronização e, em seguida, alterado recebe todos os dados de tabela local toohello do Azure.</span><span class="sxs-lookup"><span data-stu-id="aab65-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="aab65-128">Teste offline</span><span class="sxs-lookup"><span data-stu-id="aab65-128">Offline testing</span></span>
1. <span data-ttu-id="aab65-129">Dispositivo de saudação do local ou o simulador no *modo avião*.</span><span class="sxs-lookup"><span data-stu-id="aab65-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="aab65-130">Isso cria um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="aab65-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="aab65-131">Adicione alguns itens *ToDo* ou marque alguns itens como concluídos.</span><span class="sxs-lookup"><span data-stu-id="aab65-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="aab65-132">Encerre Olá dispositivo ou simulador (ou aplicativo hello fechamento forçado) e reinicie.</span><span class="sxs-lookup"><span data-stu-id="aab65-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="aab65-133">Verifique se que as alterações foram persistidas no dispositivo Olá porque eles são mantidos no repositório local do SQLite de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab65-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="aab65-134">Exibir o conteúdo de saudação do hello Azure *TodoItem* tabela com uma ferramenta SQL, como *SQL Server Management Studio*, ou um cliente REST, como *Fiddler* ou  *Carteiro*.</span><span class="sxs-lookup"><span data-stu-id="aab65-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="aab65-135">Verifique se novos itens de saudação tem *não* foi sincronizado toohello server</span><span class="sxs-lookup"><span data-stu-id="aab65-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="aab65-136">Para um back-end node. js, vá toohello [portal do Azure](https://portal.azure.com/), e em seu aplicativo móvel back-end em **tabelas fácil** > **TodoItem** tooview conteúdo Olá Olá `TodoItem` tabela.</span><span class="sxs-lookup"><span data-stu-id="aab65-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="aab65-137">Para um back-end .NET, tabela de saudação do modo de exibição de conteúdo com uma ferramenta SQL, como *SQL Server Management Studio*, ou um cliente REST, como *Fiddler* ou *carteiro*.</span><span class="sxs-lookup"><span data-stu-id="aab65-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="aab65-138">Ative o Wi-Fi no simulador ou dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="aab65-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="aab65-139">Em seguida, pressione Olá **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="aab65-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="aab65-140">Exiba dados de TodoItem de saudação novamente no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aab65-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="aab65-141">Olá que todoitems novas e alteradas agora deve aparecer.</span><span class="sxs-lookup"><span data-stu-id="aab65-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aab65-142">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="aab65-142">Additional Resources</span></span>
* <span data-ttu-id="aab65-143">[sincronização de dados Offline em aplicativos móveis do Azure]</span><span class="sxs-lookup"><span data-stu-id="aab65-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="aab65-144">[Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure] \(Observação: Olá vídeo está em serviços móveis, mas a sincronização offline funciona de maneira semelhante em aplicativos móveis do Azure\)</span><span class="sxs-lookup"><span data-stu-id="aab65-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[sincronização de dados Offline em aplicativos móveis do Azure]: app-service-mobile-offline-data-sync.md

[criar um aplicativo do Android]: app-service-mobile-android-get-started.md

[Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

