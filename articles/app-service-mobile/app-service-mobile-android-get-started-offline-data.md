---
title: "Habilitar sincronização offline para o seu Aplicativo móvel do Azure (Android)"
description: "Aprenda a usar os aplicativos móveis do Serviço de Aplicativo para cache e sincronização de dados offline no aplicativo Android."
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
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="1fab0-103">Habilitar sincronização offline para seu aplicativo móvel Android</span><span class="sxs-lookup"><span data-stu-id="1fab0-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="1fab0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1fab0-104">Overview</span></span>
<span data-ttu-id="1fab0-105">Este tutorial aborda o recurso de sincronização offline de Aplicativos móveis do Azure para Android.</span><span class="sxs-lookup"><span data-stu-id="1fab0-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="1fab0-106">A sincronização offline permite que os usuários finais interajam com um aplicativo móvel, &mdash;exibindo, adicionando ou modificando dados&mdash;, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="1fab0-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="1fab0-107">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="1fab0-107">Changes are stored in a local database.</span></span> <span data-ttu-id="1fab0-108">Quando o dispositivo estiver online novamente, essas alterações serão sincronizadas com o back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="1fab0-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="1fab0-109">Se essa for sua primeira experiência com os Aplicativos Móveis do Azure, você deve primeiro concluir o tutorial [Criar um aplicativo do iOS].</span><span class="sxs-lookup"><span data-stu-id="1fab0-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="1fab0-110">Se você não usar o projeto baixado do início rápido do servidor, deve adicionar os pacotes de extensão de acesso de dados autenticação ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="1fab0-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="1fab0-111">Para obter mais informações sobre pacotes de extensão do servidor, confira [Trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1fab0-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="1fab0-112">Para saber mais sobre o recurso de sincronização offline, confira o tópico [Sincronização de dados offline em Aplicativos Móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="1fab0-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="1fab0-113">Atualizar o aplicativo para dar suporte à sincronização offline</span><span class="sxs-lookup"><span data-stu-id="1fab0-113">Update the app to support offline sync</span></span>
<span data-ttu-id="1fab0-114">Com sincronização offline você lê e grava de uma *tabela de sincronização* (usando a interface *IMobileServiceSyncTable*), que é parte de um banco de dados **SQLite** no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1fab0-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="1fab0-115">Para enviar e receber alterações entre o dispositivo e os serviços móveis do Azure, você deve usar um o *contexto de sincronização* (*MobileServiceClient.SyncContext*), que você inicializar com o banco de dados local para armazenar dados localmente.</span><span class="sxs-lookup"><span data-stu-id="1fab0-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="1fab0-116">Em `TodoActivity.java`, comente a definição existente de `mToDoTable` e remova a versão da tabela de sincronização:</span><span class="sxs-lookup"><span data-stu-id="1fab0-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="1fab0-117">No método `onCreate`, comente a inicialização existente de `mToDoTable` e remova essa definição:</span><span class="sxs-lookup"><span data-stu-id="1fab0-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="1fab0-118">Em `refreshItemsFromTable`, comente a definição de `results` e remova essa definição:</span><span class="sxs-lookup"><span data-stu-id="1fab0-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="1fab0-119">Comente a definição de `refreshItemsFromMobileServiceTable`:</span><span class="sxs-lookup"><span data-stu-id="1fab0-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="1fab0-120">Remova a definição de `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="1fab0-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="1fab0-121">Remova a definição de `sync`:</span><span class="sxs-lookup"><span data-stu-id="1fab0-121">Uncomment the definition of `sync`:</span></span>
   
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

## <a name="test-the-app"></a><span data-ttu-id="1fab0-122">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="1fab0-122">Test the app</span></span>
<span data-ttu-id="1fab0-123">Nesta seção, você testará o comportamento com o WiFi ativado e depois o desativará para criar um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="1fab0-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="1fab0-124">Quando você adiciona itens de dados, eles são mantidos no armazenamento local do SQL Lite , mas não sincronizados para o serviço móvel, até que você pressione o botão **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="1fab0-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="1fab0-125">Outros aplicativos podem ter necessidades diferentes em relação a quando os dados precisam ser sincronizados, mas para fins de demonstração neste tutorial o usuário tem que solicitá-lo explicitamente.</span><span class="sxs-lookup"><span data-stu-id="1fab0-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="1fab0-126">Quando você pressiona o botão, inicia uma nova tarefa em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="1fab0-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="1fab0-127">Primeiro, ela envia por push todas as alterações feitas no repositório local usando o contexto de sincronização, e depois recebe todos os dados alterados do Azure para a tabela local.</span><span class="sxs-lookup"><span data-stu-id="1fab0-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="1fab0-128">Teste offline</span><span class="sxs-lookup"><span data-stu-id="1fab0-128">Offline testing</span></span>
1. <span data-ttu-id="1fab0-129">Coloque o dispositivo ou o simulador em *Modo de Avião*.</span><span class="sxs-lookup"><span data-stu-id="1fab0-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="1fab0-130">Isso cria um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="1fab0-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="1fab0-131">Adicione alguns itens *ToDo* ou marque alguns itens como concluídos.</span><span class="sxs-lookup"><span data-stu-id="1fab0-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="1fab0-132">Feche o dispositivo ou simulador (ou feche forçadamente o aplicativo) e reinicie.</span><span class="sxs-lookup"><span data-stu-id="1fab0-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="1fab0-133">Por ainda estarem vigentes no armazenamento do SQL Lite local, as alterações ficam mantidas no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1fab0-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="1fab0-134">Exiba os conteúdos da tabela *TodoItem* do Azure com uma ferramenta SQL, como o *SQL Server Management Studio*, ou então com um cliente REST, como o *Fiddler* ou o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="1fab0-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="1fab0-135">Confirme que os novos itens *não* foram sincronizados com o servidor</span><span class="sxs-lookup"><span data-stu-id="1fab0-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="1fab0-136">Para um back-end Node.js, vá para o [Portal do Azure](https://portal.azure.com/) e no back-end do aplicativo móvel clique em **Tabelas Fáceis** > **TodoItem** para exibir o conteúdo da tabela `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="1fab0-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="1fab0-137">Para um back-end do .NET, exiba o conteúdo da tabela com uma ferramenta SQL como o *SQL Server Management Studio*, ou então com um cliente REST, como o *Fiddler* ou o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="1fab0-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="1fab0-138">Ative o WiFi no simulador ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1fab0-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="1fab0-139">Em seguida, pressione o botão **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="1fab0-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="1fab0-140">Exiba os dados de TodoItem novamente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fab0-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="1fab0-141">Os TodoItems novos e modificados agora devem aparecer.</span><span class="sxs-lookup"><span data-stu-id="1fab0-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fab0-142">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1fab0-142">Additional Resources</span></span>
* <span data-ttu-id="1fab0-143">[Sincronização de dados offline em Aplicativos Móveis do Azure]</span><span class="sxs-lookup"><span data-stu-id="1fab0-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="1fab0-144">[Cobertura em nuvem: sincronização offline nos serviços móveis do Azure] \(observação: o vídeo está nos Serviços Móveis, mas a sincronização offline funciona de maneira semelhante nos Aplicativos Móveis do Azure\)</span><span class="sxs-lookup"><span data-stu-id="1fab0-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="1fab0-145">[Sincronização de dados offline em Aplicativos Móveis do Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="1fab0-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="1fab0-146">[Criar um aplicativo do iOS]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="1fab0-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="1fab0-147">[Cobertura em nuvem: sincronização offline nos serviços móveis do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="1fab0-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

