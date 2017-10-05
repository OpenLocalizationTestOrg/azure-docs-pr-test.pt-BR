---
title: "Habilitar a sincronização offline com aplicativos móveis do iOS | Microsoft Docs"
description: "Aprenda a usar os aplicativos móveis do Serviço de Aplicativo do Azure para colocar em cache e sincronizar dados offline em aplicativos iOS."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 44c0d26b2d7d28322d436d4bda319d728c31a635
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="939a1-103">Habilitar a sincronização offline com aplicativos móveis do iOS</span><span class="sxs-lookup"><span data-stu-id="939a1-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="939a1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="939a1-104">Overview</span></span>
<span data-ttu-id="939a1-105">Este tutorial aborda a sincronização offline com o recurso Aplicativos Móveis do Serviço de Aplicativo do Azure para iOS.</span><span class="sxs-lookup"><span data-stu-id="939a1-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="939a1-106">Com a sincronização offline, os usuários podem interagir com um aplicativo móvel para exibir, adicionar ou alterar dados, mesmo quando não têm conexão com a rede.</span><span class="sxs-lookup"><span data-stu-id="939a1-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="939a1-107">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="939a1-107">Changes are stored in a local database.</span></span> <span data-ttu-id="939a1-108">Quando o dispositivo estiver online novamente, as alterações são sincronizadas com o back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="939a1-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="939a1-109">Se essa for sua primeira experiência com Aplicativos Móveis, você deve primeiro concluir o tutorial [Criar um aplicativo iOS].</span><span class="sxs-lookup"><span data-stu-id="939a1-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="939a1-110">Se você não usar o projeto baixado do início rápido do servidor, deve adicionar os pacotes de extensão de acesso de dados ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="939a1-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="939a1-111">Para obter mais informações sobre pacotes de extensão do servidor, confira [Trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="939a1-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="939a1-112">Para saber mais sobre o recurso de sincronização offline, confira [Sincronização de dados offline em Aplicativos Móveis].</span><span class="sxs-lookup"><span data-stu-id="939a1-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="939a1-113"><a name="review-sync"></a>Examine o código de sincronização do cliente</span><span class="sxs-lookup"><span data-stu-id="939a1-113"><a name="review-sync"></a>Review the client sync code</span></span>
<span data-ttu-id="939a1-114">O projeto cliente que você baixou para o tutorial [Criar um aplicativo iOS] já contém o código que oferece suporte à sincronização offline usando um banco de dados local baseado em Dados Básicos.</span><span class="sxs-lookup"><span data-stu-id="939a1-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="939a1-115">Esta seção resume o que já está incluso no código do tutorial.</span><span class="sxs-lookup"><span data-stu-id="939a1-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="939a1-116">Para obter uma visão geral conceitual do recurso, confira [Sincronização de dados offline em Aplicativos Móveis].</span><span class="sxs-lookup"><span data-stu-id="939a1-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="939a1-117">Usando o recurso de sincronização de dados offline dos Aplicativos Móveis, os usuários podem interagir com um banco de dados local mesmo quando a rede estiver inacessível.</span><span class="sxs-lookup"><span data-stu-id="939a1-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="939a1-118">Para usar esses recursos em seu aplicativo, inicialize o contexto de sincronização de `MSClient` e faça referência a um repositório local.</span><span class="sxs-lookup"><span data-stu-id="939a1-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="939a1-119">Em seguida, faça referência à sua tabela por meio da interface **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="939a1-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="939a1-120">Em **QSTodoService.m** (Objective-C) ou em **ToDoTableViewController.swift** (Swift), observe que o tipo do membro **syncTable** é **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="939a1-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="939a1-121">A sincronização offline usa esta interface de tabela de sincronização em vez de **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="939a1-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="939a1-122">Ao usar uma tabela de sincronização, todas as operações vão para o armazenamento local e são sincronizadas somente com o back-end remoto com operações de push e pull explícitas.</span><span class="sxs-lookup"><span data-stu-id="939a1-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="939a1-123">Para obter uma referência a uma tabela de sincronização, use o método **syncTableWithName** no `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="939a1-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="939a1-124">Para remover a funcionalidade de sincronização offline, use **tableWithName**.</span><span class="sxs-lookup"><span data-stu-id="939a1-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="939a1-125">Antes de qualquer operação de tabela poder ser executada, o armazenamento local deve ser inicializado.</span><span class="sxs-lookup"><span data-stu-id="939a1-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="939a1-126">Este é o código relevante:</span><span class="sxs-lookup"><span data-stu-id="939a1-126">Here is the relevant code:</span></span>

* <span data-ttu-id="939a1-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="939a1-127">**Objective-C**.</span></span> <span data-ttu-id="939a1-128">No método **QSTodoService.init**:</span><span class="sxs-lookup"><span data-stu-id="939a1-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="939a1-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="939a1-129">**Swift**.</span></span> <span data-ttu-id="939a1-130">No método **ToDoTableViewController.viewDidLoad**:</span><span class="sxs-lookup"><span data-stu-id="939a1-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="939a1-131">Isso cria um repositório local usando a interface `MSCoreDataStore`, que é fornecida no SDK de Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="939a1-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="939a1-132">Como alternativa, é possível fornecer um repositório local diferente implementando o protocolo `MSSyncContextDataSource`.</span><span class="sxs-lookup"><span data-stu-id="939a1-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="939a1-133">Além disso, usa-se o primeiro parâmetro de **MSSyncContext** para especificar um manipulador de conflito.</span><span class="sxs-lookup"><span data-stu-id="939a1-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="939a1-134">Já que passamos `nil`, obteremos o manipulador de conflito padrão, que falha em qualquer conflito.</span><span class="sxs-lookup"><span data-stu-id="939a1-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="939a1-135">Agora vamos executar a operação de sincronização em si e obter dados do back-end remoto:</span><span class="sxs-lookup"><span data-stu-id="939a1-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="939a1-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="939a1-136">**Objective-C**.</span></span> <span data-ttu-id="939a1-137">Primeiro, `syncData` envia novas alterações por push e chama **pullData** para obter dados do back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="939a1-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="939a1-138">Por sua vez, o método **pullData** obtém novos dados que correspondem a uma consulta:</span><span class="sxs-lookup"><span data-stu-id="939a1-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="939a1-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="939a1-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="939a1-140">Na versão do Objective-C, em `syncData`, primeiro chamamos **pushWithCompletion** no contexto da sincronização.</span><span class="sxs-lookup"><span data-stu-id="939a1-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="939a1-141">Esse método é um membro de `MSSyncContext` (e não da tabela de sincronização em si) porque envia por push as alterações para todas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="939a1-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="939a1-142">Somente os registros que foram modificados localmente de alguma forma (por meio de operações CUD) são enviados ao servidor.</span><span class="sxs-lookup"><span data-stu-id="939a1-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="939a1-143">Em seguida, o auxiliar **pullData** é chamado, o que chama **MSSyncTable.pullWithQuery** para recuperar os dados remotos e armazená-los no banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="939a1-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="939a1-144">Na versão do Swift, porque a operação de envio não era estritamente necessária, não há nenhuma chamada para **pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="939a1-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="939a1-145">Se houver alterações pendentes no contexto de sincronização para a tabela que está executando uma operação de push/pull, push é sempre emitido primeiro.</span><span class="sxs-lookup"><span data-stu-id="939a1-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="939a1-146">No entanto, se você tiver mais de uma tabela de sincronização, é melhor chamar explicitamente por push para garantir que tudo esteja consistente em todas as tabelas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="939a1-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="939a1-147">Em ambas as versões Objective-C e Swift, o método **pullWithQuery** permite que você especifique uma consulta para filtrar os registros que deseja recuperar.</span><span class="sxs-lookup"><span data-stu-id="939a1-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="939a1-148">Neste exemplo, a consulta recupera todos os registros na tabela remota `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="939a1-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="939a1-149">O segundo parâmetro de **pullWithQuery** é uma ID de consulta usada para *sincronização incremental*.</span><span class="sxs-lookup"><span data-stu-id="939a1-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*.</span></span> <span data-ttu-id="939a1-150">A sincronização incremental recupera somente os registros modificados desde a última sincronização, usando o carimbo de data/hora `UpdatedAt` do registro (chamado de `updatedAt` no repositório local). A ID da consulta deve ser uma cadeia de caracteres descritiva que é exclusiva para cada consulta lógica em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939a1-150">Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="939a1-151">Se desejar sair da sincronização incremental, passe `nil` como a ID da consulta.</span><span class="sxs-lookup"><span data-stu-id="939a1-151">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="939a1-152">Observe que isso pode ser potencialmente ineficiente, já que recupera todos os registros de cada operação de recepção.</span><span class="sxs-lookup"><span data-stu-id="939a1-152">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="939a1-153">O aplicativo Objective-C é sincronizado ao modificar ou adicionar dados, quando um usuário executa a atualização e na inicialização.</span><span class="sxs-lookup"><span data-stu-id="939a1-153">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="939a1-154">O aplicativo Swift é sincronizado quando um usuário executa a atualização e na inicialização.</span><span class="sxs-lookup"><span data-stu-id="939a1-154">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="939a1-155">Como o aplicativo é sincronizado sempre que dados são modificados (Objective-C) ou sempre que o aplicativo é iniciado (Objective-C e Swift), o aplicativo pressupõe que o usuário está online.</span><span class="sxs-lookup"><span data-stu-id="939a1-155">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="939a1-156">Em uma seção posterior, atualizaremos o aplicativo para que os usuários possam editar mesmo quando estiverem offline.</span><span class="sxs-lookup"><span data-stu-id="939a1-156">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="939a1-157"><a name="review-core-data"></a>Examinar o modelo de dados principais</span><span class="sxs-lookup"><span data-stu-id="939a1-157"><a name="review-core-data"></a>Review the Core Data model</span></span>
<span data-ttu-id="939a1-158">Ao usar o armazenamento offline de Dados Básicos, você precisa definir determinadas tabelas e campos em seu modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="939a1-158">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="939a1-159">O aplicativo de exemplo já inclui um modelo de dados com o formato correto.</span><span class="sxs-lookup"><span data-stu-id="939a1-159">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="939a1-160">Nesta seção percorreremos essas tabelas e veremos como são usadas.</span><span class="sxs-lookup"><span data-stu-id="939a1-160">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="939a1-161">Abra **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="939a1-161">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="939a1-162">Há quatro tabelas definidas - três que são usadas pelo SDK e uma usada para os itens pendentes:</span><span class="sxs-lookup"><span data-stu-id="939a1-162">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="939a1-163">MS_TableOperations: para acompanhar os itens que devem ser sincronizados com o servidor.</span><span class="sxs-lookup"><span data-stu-id="939a1-163">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="939a1-164">MS_TableOperationErrors: para acompanhar todos os erros que ocorrerem durante a sincronização offline.</span><span class="sxs-lookup"><span data-stu-id="939a1-164">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="939a1-165">MS_TableConfig: para controlar a hora da última atualização para a última operação de sincronização para todas as operações de recepção.</span><span class="sxs-lookup"><span data-stu-id="939a1-165">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="939a1-166">TodoItem: armazena os itens de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="939a1-166">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="939a1-167">As colunas do sistema **createdAt**, **updatedAt** e **version** são propriedades opcionais do sistema.</span><span class="sxs-lookup"><span data-stu-id="939a1-167">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="939a1-168">O SDK dos Aplicativos Móveis reserva nomes de coluna que começam com "**``**".</span><span class="sxs-lookup"><span data-stu-id="939a1-168">The Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="939a1-169">Não use esse prefixo em algo diferente das colunas do sistema.</span><span class="sxs-lookup"><span data-stu-id="939a1-169">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="939a1-170">Caso contrário, os nomes de coluna serão modificados ao usar o back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="939a1-170">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="939a1-171">Ao usar o recurso de sincronização offline, você define as três tabelas do sistema e a tabela de dados.</span><span class="sxs-lookup"><span data-stu-id="939a1-171">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="939a1-172">Tabelas do sistema</span><span class="sxs-lookup"><span data-stu-id="939a1-172">System tables</span></span>

<span data-ttu-id="939a1-173">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="939a1-173">**MS_TableOperations**</span></span>  

![Atributos da tabela MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="939a1-175">Atributo</span><span class="sxs-lookup"><span data-stu-id="939a1-175">Attribute</span></span> | <span data-ttu-id="939a1-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="939a1-176">Type</span></span> |
| --- | --- |
| <span data-ttu-id="939a1-177">ID</span><span class="sxs-lookup"><span data-stu-id="939a1-177">id</span></span> | <span data-ttu-id="939a1-178">Número Inteiro 64</span><span class="sxs-lookup"><span data-stu-id="939a1-178">Integer 64</span></span> |
| <span data-ttu-id="939a1-179">itemId</span><span class="sxs-lookup"><span data-stu-id="939a1-179">itemId</span></span> | <span data-ttu-id="939a1-180">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="939a1-180">String</span></span> |
| <span data-ttu-id="939a1-181">propriedades</span><span class="sxs-lookup"><span data-stu-id="939a1-181">properties</span></span> | <span data-ttu-id="939a1-182">Dados binários</span><span class="sxs-lookup"><span data-stu-id="939a1-182">Binary Data</span></span> |
| <span data-ttu-id="939a1-183">tabela</span><span class="sxs-lookup"><span data-stu-id="939a1-183">table</span></span> | <span data-ttu-id="939a1-184">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="939a1-184">String</span></span> |
| <span data-ttu-id="939a1-185">tableKind</span><span class="sxs-lookup"><span data-stu-id="939a1-185">tableKind</span></span> | <span data-ttu-id="939a1-186">Número inteiro 16</span><span class="sxs-lookup"><span data-stu-id="939a1-186">Integer 16</span></span> |


<span data-ttu-id="939a1-187">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="939a1-187">**MS_TableOperationErrors**</span></span>

 ![Atributos da tabela MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="939a1-189">Atributo</span><span class="sxs-lookup"><span data-stu-id="939a1-189">Attribute</span></span> | <span data-ttu-id="939a1-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="939a1-190">Type</span></span> |
| --- | --- |
| <span data-ttu-id="939a1-191">ID</span><span class="sxs-lookup"><span data-stu-id="939a1-191">id</span></span> |<span data-ttu-id="939a1-192">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="939a1-192">String</span></span> |
| <span data-ttu-id="939a1-193">operationId</span><span class="sxs-lookup"><span data-stu-id="939a1-193">operationId</span></span> |<span data-ttu-id="939a1-194">Número Inteiro 64</span><span class="sxs-lookup"><span data-stu-id="939a1-194">Integer 64</span></span> |
| <span data-ttu-id="939a1-195">propriedades</span><span class="sxs-lookup"><span data-stu-id="939a1-195">properties</span></span> |<span data-ttu-id="939a1-196">Dados binários</span><span class="sxs-lookup"><span data-stu-id="939a1-196">Binary Data</span></span> |
| <span data-ttu-id="939a1-197">tableKind</span><span class="sxs-lookup"><span data-stu-id="939a1-197">tableKind</span></span> |<span data-ttu-id="939a1-198">Número inteiro 16</span><span class="sxs-lookup"><span data-stu-id="939a1-198">Integer 16</span></span> |

 <span data-ttu-id="939a1-199">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="939a1-199">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="939a1-200">Atributo</span><span class="sxs-lookup"><span data-stu-id="939a1-200">Attribute</span></span> | <span data-ttu-id="939a1-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="939a1-201">Type</span></span> |
| --- | --- |
| <span data-ttu-id="939a1-202">ID</span><span class="sxs-lookup"><span data-stu-id="939a1-202">id</span></span> |<span data-ttu-id="939a1-203">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="939a1-203">String</span></span> |
| <span data-ttu-id="939a1-204">chave</span><span class="sxs-lookup"><span data-stu-id="939a1-204">key</span></span> |<span data-ttu-id="939a1-205">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="939a1-205">String</span></span> |
| <span data-ttu-id="939a1-206">keyType</span><span class="sxs-lookup"><span data-stu-id="939a1-206">keyType</span></span> |<span data-ttu-id="939a1-207">Número Inteiro 64</span><span class="sxs-lookup"><span data-stu-id="939a1-207">Integer 64</span></span> |
| <span data-ttu-id="939a1-208">tabela</span><span class="sxs-lookup"><span data-stu-id="939a1-208">table</span></span> |<span data-ttu-id="939a1-209">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="939a1-209">String</span></span> |
| <span data-ttu-id="939a1-210">valor</span><span class="sxs-lookup"><span data-stu-id="939a1-210">value</span></span> |<span data-ttu-id="939a1-211">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="939a1-211">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="939a1-212">Tabela de dados</span><span class="sxs-lookup"><span data-stu-id="939a1-212">Data table</span></span>

<span data-ttu-id="939a1-213">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="939a1-213">**TodoItem**</span></span>

| <span data-ttu-id="939a1-214">Atributo</span><span class="sxs-lookup"><span data-stu-id="939a1-214">Attribute</span></span> | <span data-ttu-id="939a1-215">Tipo</span><span class="sxs-lookup"><span data-stu-id="939a1-215">Type</span></span> | <span data-ttu-id="939a1-216">Observação</span><span class="sxs-lookup"><span data-stu-id="939a1-216">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="939a1-217">ID</span><span class="sxs-lookup"><span data-stu-id="939a1-217">id</span></span> | <span data-ttu-id="939a1-218">Cadeia de caracteres, marcadas como obrigatórias</span><span class="sxs-lookup"><span data-stu-id="939a1-218">String, marked required</span></span> |<span data-ttu-id="939a1-219">Chave primária no repositório remoto</span><span class="sxs-lookup"><span data-stu-id="939a1-219">Primary key in remote store</span></span> |
| <span data-ttu-id="939a1-220">concluído</span><span class="sxs-lookup"><span data-stu-id="939a1-220">complete</span></span> | <span data-ttu-id="939a1-221">Booliano</span><span class="sxs-lookup"><span data-stu-id="939a1-221">Boolean</span></span> | <span data-ttu-id="939a1-222">Campo To-do item</span><span class="sxs-lookup"><span data-stu-id="939a1-222">To-do item field</span></span> |
| <span data-ttu-id="939a1-223">texto</span><span class="sxs-lookup"><span data-stu-id="939a1-223">text</span></span> |<span data-ttu-id="939a1-224">string</span><span class="sxs-lookup"><span data-stu-id="939a1-224">String</span></span> |<span data-ttu-id="939a1-225">Campo To-do item</span><span class="sxs-lookup"><span data-stu-id="939a1-225">To-do item field</span></span> |
| <span data-ttu-id="939a1-226">createdAt</span><span class="sxs-lookup"><span data-stu-id="939a1-226">createdAt</span></span> | <span data-ttu-id="939a1-227">Data</span><span class="sxs-lookup"><span data-stu-id="939a1-227">Date</span></span> | <span data-ttu-id="939a1-228">(opcional) É mapeado para a propriedade do sistema **createdAt**</span><span class="sxs-lookup"><span data-stu-id="939a1-228">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="939a1-229">updatedAt</span><span class="sxs-lookup"><span data-stu-id="939a1-229">updatedAt</span></span> | <span data-ttu-id="939a1-230">Data</span><span class="sxs-lookup"><span data-stu-id="939a1-230">Date</span></span> | <span data-ttu-id="939a1-231">(opcional) É mapeado para a propriedade do sistema **updatedAt**</span><span class="sxs-lookup"><span data-stu-id="939a1-231">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="939a1-232">version</span><span class="sxs-lookup"><span data-stu-id="939a1-232">version</span></span> | <span data-ttu-id="939a1-233">string</span><span class="sxs-lookup"><span data-stu-id="939a1-233">String</span></span> | <span data-ttu-id="939a1-234">(opcional) Usado para detectar conflitos, é mapeado para a versão</span><span class="sxs-lookup"><span data-stu-id="939a1-234">(optional) Used to detect conflicts, maps to version</span></span> |

## <span data-ttu-id="939a1-235"><a name="setup-sync"></a>Alterar o comportamento de sincronização do aplicativo</span><span class="sxs-lookup"><span data-stu-id="939a1-235"><a name="setup-sync"></a>Change the sync behavior of the app</span></span>
<span data-ttu-id="939a1-236">Nesta seção, você altera o aplicativo para que ele não sincronize na inicialização ou ao inserir e atualizar itens.</span><span class="sxs-lookup"><span data-stu-id="939a1-236">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="939a1-237">Ele sincroniza somente quando o botão de atualização é executado.</span><span class="sxs-lookup"><span data-stu-id="939a1-237">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="939a1-238">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="939a1-238">**Objective-C**:</span></span>

1. <span data-ttu-id="939a1-239">Em **QSTodoListViewController.m**, altere o método **viewDidLoad** para remover a chamada para `[self refresh]` no final do método.</span><span class="sxs-lookup"><span data-stu-id="939a1-239">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="939a1-240">Agora os dados não são sincronizados com o servidor na inicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939a1-240">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="939a1-241">Em vez disso, são sincronizados com o conteúdo do repositório local.</span><span class="sxs-lookup"><span data-stu-id="939a1-241">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="939a1-242">Em **QSTodoService.m**, modifique a definição de `addItem` para que não ocorra sincronização após o item ser inserido.</span><span class="sxs-lookup"><span data-stu-id="939a1-242">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="939a1-243">Remova o bloco `self syncData` e substitua-o pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="939a1-243">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="939a1-244">Modifique a definição de `completeItem` como mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="939a1-244">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="939a1-245">Remova o bloco `self syncData` e substitua-o pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="939a1-245">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="939a1-246">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="939a1-246">**Swift**:</span></span>

<span data-ttu-id="939a1-247">Em `viewDidLoad` de **ToDoTableViewController.swift**, comente essas duas linhas para parar a sincronização na inicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939a1-247">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="939a1-248">No momento da redação deste artigo, o aplicativo Todo do Swift não atualiza o serviço quando alguém adiciona ou conclui um item,</span><span class="sxs-lookup"><span data-stu-id="939a1-248">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="939a1-249">somente na inicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939a1-249">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="939a1-250"><a name="test-app"></a>Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="939a1-250"><a name="test-app"></a>Test the app</span></span>
<span data-ttu-id="939a1-251">Nesta seção, você se conecta a uma URL inválida para simular um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="939a1-251">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="939a1-252">Ao adicionar itens de dados, eles serão mantidos no repositório local de Dados Básicos, mas não serão sincronizados com o back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="939a1-252">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="939a1-253">Altere a URL do aplicativo móvel em **QSTodoService.m** para uma URL inválida e execute novamente o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="939a1-253">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="939a1-254">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="939a1-254">**Objective-C**.</span></span> <span data-ttu-id="939a1-255">Em QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="939a1-255">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="939a1-256">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="939a1-256">**Swift**.</span></span> <span data-ttu-id="939a1-257">Em ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="939a1-257">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="939a1-258">Adicione alguns itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="939a1-258">Add some to-do items.</span></span> <span data-ttu-id="939a1-259">Feche o simulador (ou force o fechamento do aplicativo) e reinicie.</span><span class="sxs-lookup"><span data-stu-id="939a1-259">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="939a1-260">Verifique se suas mudanças foram mantidas.</span><span class="sxs-lookup"><span data-stu-id="939a1-260">Verify that your changes persist.</span></span>

3. <span data-ttu-id="939a1-261">Exiba o conteúdo da tabela **TodoItem** remota:</span><span class="sxs-lookup"><span data-stu-id="939a1-261">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="939a1-262">Para um back-end do Node.js, vá para o [Portal do Azure](https://portal.azure.com/) e, no back-end de seu aplicativo móvel, clique em **Tabelas simples** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="939a1-262">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="939a1-263">Para um back-end do .NET, use uma ferramenta SQL, como o SQL Server Management Studio, ou um cliente REST, como o Fiddler ou o Postman.</span><span class="sxs-lookup"><span data-stu-id="939a1-263">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="939a1-264">Confirme que os novos itens *não* tenham sido sincronizados com o servidor.</span><span class="sxs-lookup"><span data-stu-id="939a1-264">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="939a1-265">Altere a URL novamente para a correta em **QSTodoService.m** e execute o aplicativo outra vez.</span><span class="sxs-lookup"><span data-stu-id="939a1-265">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="939a1-266">Faça o gesto de atualização puxando a lista de itens para baixo.</span><span class="sxs-lookup"><span data-stu-id="939a1-266">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="939a1-267">Um controle giratório de progresso é exibido.</span><span class="sxs-lookup"><span data-stu-id="939a1-267">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="939a1-268">Exiba os dados de **TodoItem** novamente.</span><span class="sxs-lookup"><span data-stu-id="939a1-268">View the **TodoItem** data again.</span></span> <span data-ttu-id="939a1-269">Os itens de tarefas novos e modificados agora devem ser exibidos.</span><span class="sxs-lookup"><span data-stu-id="939a1-269">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="939a1-270">Resumo</span><span class="sxs-lookup"><span data-stu-id="939a1-270">Summary</span></span>
<span data-ttu-id="939a1-271">Para dar suporte a esse recurso de sincronização offline, usamos a interface `MSSyncTable` e inicializamos `MSClient.syncContext` com um repositório local.</span><span class="sxs-lookup"><span data-stu-id="939a1-271">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="939a1-272">Nesse caso, o repositório local era um banco de dados baseado em Dados Básicos.</span><span class="sxs-lookup"><span data-stu-id="939a1-272">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="939a1-273">Ao usar um repositório local de Dados Básicos, você deve definir várias tabelas com as [propriedades corretas do sistema](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="939a1-273">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="939a1-274">As operações CRUD (criar, ler, atualizar e excluir) normais nos aplicativos móveis funcionam como se o aplicativo ainda estivesse conectado, mas todas as operações ocorrem no repositório local.</span><span class="sxs-lookup"><span data-stu-id="939a1-274">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="939a1-275">Ao sincronizar o repositório local com o servidor, usamos o método **MSSyncTable.pullWithQuery**.</span><span class="sxs-lookup"><span data-stu-id="939a1-275">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="939a1-276">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="939a1-276">Additional resources</span></span>
* <span data-ttu-id="939a1-277">[Sincronização de dados offline em Aplicativos Móveis]</span><span class="sxs-lookup"><span data-stu-id="939a1-277">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="939a1-278">[Cloud Cover: sincronização offline nos serviços móveis do Azure] \(O vídeo é sobre Serviços Móveis, mas a sincronização offline de Aplicativos Móveis funciona de maneira semelhante.\)</span><span class="sxs-lookup"><span data-stu-id="939a1-278">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


<span data-ttu-id="939a1-279">[Criar um aplicativo iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="939a1-279">[Create an iOS App]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="939a1-280">[Sincronização de dados offline em Aplicativos Móveis]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="939a1-280">[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

<span data-ttu-id="939a1-281">[Cloud Cover: sincronização offline nos serviços móveis do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="939a1-281">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
