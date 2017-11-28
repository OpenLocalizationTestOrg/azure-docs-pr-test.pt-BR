---
title: "sincronização offline aaaEnable com aplicativos móveis iOS | Microsoft Docs"
description: "Saiba como toouse do serviço de aplicativo do Azure aplicativos móveis toocache e sincronização de dados offline em aplicativos do iOS."
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
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="d8744-103">Habilitar a sincronização offline com aplicativos móveis do iOS</span><span class="sxs-lookup"><span data-stu-id="d8744-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="d8744-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d8744-104">Overview</span></span>
<span data-ttu-id="d8744-105">Este tutorial aborda offline sincronizando com o recurso de aplicativos móveis de saudação do serviço de aplicativo do Azure para iOS.</span><span class="sxs-lookup"><span data-stu-id="d8744-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="d8744-106">Com os usuários finais sincronização offline podem interagir com um aplicativo móvel tooview, adicionar ou modificar dados, mesmo quando eles têm nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="d8744-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="d8744-107">As alterações são armazenadas em um banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="d8744-107">Changes are stored in a local database.</span></span> <span data-ttu-id="d8744-108">Depois que o dispositivo de saudação estiver online novamente, as alterações de saudação são sincronizadas com Olá remoto back-end.</span><span class="sxs-lookup"><span data-stu-id="d8744-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="d8744-109">Se esta for sua primeira experiência com aplicativos móveis, primeiro você deve concluir o tutorial de saudação [criar um aplicativo iOS].</span><span class="sxs-lookup"><span data-stu-id="d8744-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="d8744-110">Se você não usar o projeto de início rápido do servidor de saudação baixado, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso a dados hello.</span><span class="sxs-lookup"><span data-stu-id="d8744-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="d8744-111">Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d8744-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="d8744-112">toolearn mais sobre o recurso de sincronização offline hello, consulte [sincronização de dados Offline em aplicativos móveis].</span><span class="sxs-lookup"><span data-stu-id="d8744-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="d8744-113"><a name="review-sync"></a>Examine o código de sincronização do cliente Olá</span><span class="sxs-lookup"><span data-stu-id="d8744-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="d8744-114">projeto de cliente de saudação que baixou para Olá [criar um aplicativo iOS] tutorial já contém código que oferece suporte à sincronização offline usando um banco de dados local com base em dados de núcleo.</span><span class="sxs-lookup"><span data-stu-id="d8744-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="d8744-115">Esta seção resume o que já está incluído no código tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="d8744-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="d8744-116">Para obter uma visão geral conceitual do recurso hello, consulte [sincronização de dados Offline em aplicativos móveis].</span><span class="sxs-lookup"><span data-stu-id="d8744-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="d8744-117">Usando o recurso de sincronização de dados offline Olá de aplicativos móveis, os usuários finais podem interagir com um banco de dados local mesmo quando a rede hello está inacessível.</span><span class="sxs-lookup"><span data-stu-id="d8744-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="d8744-118">toouse esses recursos em seu aplicativo, que você inicializar o contexto de sincronização de saudação do `MSClient` e fazer referência a um repositório local.</span><span class="sxs-lookup"><span data-stu-id="d8744-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="d8744-119">Em seguida, você referenciar a tabela por meio de saudação **MSSyncTable** interface.</span><span class="sxs-lookup"><span data-stu-id="d8744-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="d8744-120">Em **QSTodoService.m** (Objective-C) ou **ToDoTableViewController.swift** (rápida), observe que Olá tipo de membro Olá **syncTable** é  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="d8744-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="d8744-121">A sincronização offline usa esta interface de tabela de sincronização em vez de **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="d8744-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="d8744-122">Quando uma tabela de sincronização é usada, todas as operações vá repositório local toohello e sejam sincronizadas somente com hello remoto back-end com envio por push explícito e pull operações.</span><span class="sxs-lookup"><span data-stu-id="d8744-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="d8744-123">tooget uma tabela de sincronização de tooa de referência, use Olá **syncTableWithName** método `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="d8744-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="d8744-124">funcionalidade de sincronização offline tooremove, use **tableWithName** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d8744-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="d8744-125">Antes de quaisquer operações de tabela podem ser executadas, armazenamento local Olá deve ser inicializado.</span><span class="sxs-lookup"><span data-stu-id="d8744-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="d8744-126">Aqui está o código relevante hello:</span><span class="sxs-lookup"><span data-stu-id="d8744-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="d8744-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="d8744-127">**Objective-C**.</span></span> <span data-ttu-id="d8744-128">Em Olá **QSTodoService.init** método:</span><span class="sxs-lookup"><span data-stu-id="d8744-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="d8744-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="d8744-129">**Swift**.</span></span> <span data-ttu-id="d8744-130">Em Olá **ToDoTableViewController.viewDidLoad** método:</span><span class="sxs-lookup"><span data-stu-id="d8744-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="d8744-131">Esse método cria um repositório local usando Olá `MSCoreDataStore` fornece interface, que Olá SDK de aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="d8744-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="d8744-132">Como alternativa, você pode fornecer um armazenamento local diferente implementando Olá `MSSyncContextDataSource` protocolo.</span><span class="sxs-lookup"><span data-stu-id="d8744-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="d8744-133">Além disso, Olá primeiro parâmetro de **MSSyncContext** é toospecify usado um manipulador de conflito.</span><span class="sxs-lookup"><span data-stu-id="d8744-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="d8744-134">Como podemos ter passado `nil`, obtemos o manipulador de conflito padrão hello, falha em qualquer conflito.</span><span class="sxs-lookup"><span data-stu-id="d8744-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="d8744-135">Agora, vamos executar a operação de sincronização real hello e obter dados de saudação remoto back-end:</span><span class="sxs-lookup"><span data-stu-id="d8744-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="d8744-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="d8744-136">**Objective-C**.</span></span> <span data-ttu-id="d8744-137">`syncData`envia primeiro novas alterações e, em seguida, chama **pullData** tooget dados de saudação remoto back-end.</span><span class="sxs-lookup"><span data-stu-id="d8744-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="d8744-138">Por sua vez, Olá **pullData** método obtém novos dados que corresponde a uma consulta:</span><span class="sxs-lookup"><span data-stu-id="d8744-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="d8744-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d8744-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="d8744-140">Na versão Olá Objective-C, em `syncData`, podemos chamar primeiro **pushWithCompletion** no contexto de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8744-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="d8744-141">Esse método é um membro do `MSSyncContext` (e não Olá sincronização própria tabela) porque ele envia as alterações em todas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="d8744-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="d8744-142">Somente os registros que foram modificados de alguma forma localmente (por meio de operações de CUD) são enviados toohello server.</span><span class="sxs-lookup"><span data-stu-id="d8744-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="d8744-143">Olá, em seguida, o auxiliar **pullData** é chamado, que chama **MSSyncTable.pullWithQuery** tooretrieve remoto de dados e armazená-lo no banco de dados local hello.</span><span class="sxs-lookup"><span data-stu-id="d8744-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="d8744-144">Na versão de Swift hello, porque não foi estritamente necessária, a operação de envio de Olá não há nenhuma chamada muito**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="d8744-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="d8744-145">Se houver alterações pendentes no contexto de sincronização de saudação para tabela Olá que está executando uma operação de envio por push, pull sempre emite um envio por push primeiro.</span><span class="sxs-lookup"><span data-stu-id="d8744-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="d8744-146">No entanto, se você tiver mais de uma tabela de sincronização, é melhor tooexplicitly chamada push tooensure que tudo o que é consistente em tabelas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="d8744-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="d8744-147">Olá Objective-C e ágil versões, você pode usar Olá **pullWithQuery** método toospecify toofilter uma consulta Olá registros que você deseja tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="d8744-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="d8744-148">Neste exemplo, a consulta Olá recupera todos os registros no hello remoto `TodoItem` tabela.</span><span class="sxs-lookup"><span data-stu-id="d8744-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="d8744-149">Olá segundo parâmetro de **pullWithQuery** é uma ID de consulta que é usada para *sincronização incremental*. A sincronização incremental recupera somente os registros que foram modificados desde a última sincronização hello, usando o registro de saudação `UpdatedAt` carimbo de data / hora (chamado `updatedAt` no hello repositório local.) Olá ID da consulta deve ser uma cadeia de caracteres descritiva é exclusiva para cada consulta lógica em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8744-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="d8744-150">tooopt fora de sincronização incremental, passar `nil` como Olá ID da consulta.</span><span class="sxs-lookup"><span data-stu-id="d8744-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="d8744-151">Observe que isso pode ser potencialmente ineficiente, já que recupera todos os registros de cada operação de recepção.</span><span class="sxs-lookup"><span data-stu-id="d8744-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="d8744-152">Olá Objective-C aplicativo será sincronizado quando você modifica ou adicionar dados, quando um usuário executa Olá gesto de atualização e, na inicialização.</span><span class="sxs-lookup"><span data-stu-id="d8744-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="d8744-153">aplicativo Swift Olá sincronizado quando o usuário Olá executa Olá gesto de atualização e na inicialização.</span><span class="sxs-lookup"><span data-stu-id="d8744-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="d8744-154">Porque hello, sincronizações de aplicativo sempre que dados são modificados (Objective-C) ou sempre que inicia o aplicativo hello (Objective-C e Swift), aplicativo hello pressupõe que o usuário hello está online.</span><span class="sxs-lookup"><span data-stu-id="d8744-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="d8744-155">Em uma seção posterior, você irá atualizar o aplicativo hello para que os usuários possam editar mesmo quando estão offline.</span><span class="sxs-lookup"><span data-stu-id="d8744-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="d8744-156"><a name="review-core-data"></a>Modelo de dados de núcleo de saudação de revisão</span><span class="sxs-lookup"><span data-stu-id="d8744-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="d8744-157">Quando você usa o armazenamento offline de dados principais hello, você deve definir determinadas tabelas e campos em seu modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="d8744-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="d8744-158">aplicativo de exemplo Hello já inclui um modelo de dados com o formato correto de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8744-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="d8744-159">Nesta seção, vemos tooshow essas tabelas como eles são usados.</span><span class="sxs-lookup"><span data-stu-id="d8744-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="d8744-160">Abra **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="d8744-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="d8744-161">Quatro tabelas são três que são usados por definido - Olá SDK e que é usado para tarefas de saudação itens se:</span><span class="sxs-lookup"><span data-stu-id="d8744-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="d8744-162">MS_TableOperations: Rastreia Olá itens que precisam de toobe sincronizado com o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8744-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="d8744-163">MS_TableOperationErrors: para acompanhar todos os erros que ocorrerem durante a sincronização offline.</span><span class="sxs-lookup"><span data-stu-id="d8744-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="d8744-164">MS_TableConfig: Rastreia Olá hora da última atualização para a última operação de sincronização Olá para todas as operações de recepção.</span><span class="sxs-lookup"><span data-stu-id="d8744-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="d8744-165">TodoItem: Armazena itens de tarefas pendentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8744-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="d8744-166">Olá colunas do sistema **criadona**, **updatedAt**, e **versão** são propriedades de sistema opcional.</span><span class="sxs-lookup"><span data-stu-id="d8744-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="d8744-167">Olá SDK de aplicativos móveis reserva nomes de coluna que começam com "**``**".</span><span class="sxs-lookup"><span data-stu-id="d8744-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="d8744-168">Não use esse prefixo em algo diferente das colunas do sistema.</span><span class="sxs-lookup"><span data-stu-id="d8744-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="d8744-169">Caso contrário, os nomes de coluna são modificados quando você usa Olá remoto back-end.</span><span class="sxs-lookup"><span data-stu-id="d8744-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="d8744-170">Quando você usa o recurso de sincronização offline hello, defina três tabelas do sistema hello e uma tabela de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8744-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="d8744-171">Tabelas do sistema</span><span class="sxs-lookup"><span data-stu-id="d8744-171">System tables</span></span>

<span data-ttu-id="d8744-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="d8744-172">**MS_TableOperations**</span></span>  

![Atributos da tabela MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="d8744-174">Atributo</span><span class="sxs-lookup"><span data-stu-id="d8744-174">Attribute</span></span> | <span data-ttu-id="d8744-175">Tipo</span><span class="sxs-lookup"><span data-stu-id="d8744-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="d8744-176">ID</span><span class="sxs-lookup"><span data-stu-id="d8744-176">id</span></span> | <span data-ttu-id="d8744-177">Número Inteiro 64</span><span class="sxs-lookup"><span data-stu-id="d8744-177">Integer 64</span></span> |
| <span data-ttu-id="d8744-178">itemId</span><span class="sxs-lookup"><span data-stu-id="d8744-178">itemId</span></span> | <span data-ttu-id="d8744-179">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-179">String</span></span> |
| <span data-ttu-id="d8744-180">propriedades</span><span class="sxs-lookup"><span data-stu-id="d8744-180">properties</span></span> | <span data-ttu-id="d8744-181">Dados binários</span><span class="sxs-lookup"><span data-stu-id="d8744-181">Binary Data</span></span> |
| <span data-ttu-id="d8744-182">tabela</span><span class="sxs-lookup"><span data-stu-id="d8744-182">table</span></span> | <span data-ttu-id="d8744-183">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-183">String</span></span> |
| <span data-ttu-id="d8744-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="d8744-184">tableKind</span></span> | <span data-ttu-id="d8744-185">Número inteiro 16</span><span class="sxs-lookup"><span data-stu-id="d8744-185">Integer 16</span></span> |


<span data-ttu-id="d8744-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="d8744-186">**MS_TableOperationErrors**</span></span>

 ![Atributos da tabela MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="d8744-188">Atributo</span><span class="sxs-lookup"><span data-stu-id="d8744-188">Attribute</span></span> | <span data-ttu-id="d8744-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="d8744-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="d8744-190">ID</span><span class="sxs-lookup"><span data-stu-id="d8744-190">id</span></span> |<span data-ttu-id="d8744-191">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-191">String</span></span> |
| <span data-ttu-id="d8744-192">operationId</span><span class="sxs-lookup"><span data-stu-id="d8744-192">operationId</span></span> |<span data-ttu-id="d8744-193">Número Inteiro 64</span><span class="sxs-lookup"><span data-stu-id="d8744-193">Integer 64</span></span> |
| <span data-ttu-id="d8744-194">propriedades</span><span class="sxs-lookup"><span data-stu-id="d8744-194">properties</span></span> |<span data-ttu-id="d8744-195">Dados binários</span><span class="sxs-lookup"><span data-stu-id="d8744-195">Binary Data</span></span> |
| <span data-ttu-id="d8744-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="d8744-196">tableKind</span></span> |<span data-ttu-id="d8744-197">Número inteiro 16</span><span class="sxs-lookup"><span data-stu-id="d8744-197">Integer 16</span></span> |

 <span data-ttu-id="d8744-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="d8744-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="d8744-199">Atributo</span><span class="sxs-lookup"><span data-stu-id="d8744-199">Attribute</span></span> | <span data-ttu-id="d8744-200">Tipo</span><span class="sxs-lookup"><span data-stu-id="d8744-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="d8744-201">ID</span><span class="sxs-lookup"><span data-stu-id="d8744-201">id</span></span> |<span data-ttu-id="d8744-202">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-202">String</span></span> |
| <span data-ttu-id="d8744-203">chave</span><span class="sxs-lookup"><span data-stu-id="d8744-203">key</span></span> |<span data-ttu-id="d8744-204">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-204">String</span></span> |
| <span data-ttu-id="d8744-205">keyType</span><span class="sxs-lookup"><span data-stu-id="d8744-205">keyType</span></span> |<span data-ttu-id="d8744-206">Número Inteiro 64</span><span class="sxs-lookup"><span data-stu-id="d8744-206">Integer 64</span></span> |
| <span data-ttu-id="d8744-207">tabela</span><span class="sxs-lookup"><span data-stu-id="d8744-207">table</span></span> |<span data-ttu-id="d8744-208">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-208">String</span></span> |
| <span data-ttu-id="d8744-209">valor</span><span class="sxs-lookup"><span data-stu-id="d8744-209">value</span></span> |<span data-ttu-id="d8744-210">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="d8744-211">Tabela de dados</span><span class="sxs-lookup"><span data-stu-id="d8744-211">Data table</span></span>

<span data-ttu-id="d8744-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="d8744-212">**TodoItem**</span></span>

| <span data-ttu-id="d8744-213">Atributo</span><span class="sxs-lookup"><span data-stu-id="d8744-213">Attribute</span></span> | <span data-ttu-id="d8744-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="d8744-214">Type</span></span> | <span data-ttu-id="d8744-215">Observação</span><span class="sxs-lookup"><span data-stu-id="d8744-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d8744-216">ID</span><span class="sxs-lookup"><span data-stu-id="d8744-216">id</span></span> | <span data-ttu-id="d8744-217">Cadeia de caracteres, marcadas como obrigatórias</span><span class="sxs-lookup"><span data-stu-id="d8744-217">String, marked required</span></span> |<span data-ttu-id="d8744-218">Chave primária no repositório remoto</span><span class="sxs-lookup"><span data-stu-id="d8744-218">Primary key in remote store</span></span> |
| <span data-ttu-id="d8744-219">concluído</span><span class="sxs-lookup"><span data-stu-id="d8744-219">complete</span></span> | <span data-ttu-id="d8744-220">Booliano</span><span class="sxs-lookup"><span data-stu-id="d8744-220">Boolean</span></span> | <span data-ttu-id="d8744-221">Campo To-do item</span><span class="sxs-lookup"><span data-stu-id="d8744-221">To-do item field</span></span> |
| <span data-ttu-id="d8744-222">texto</span><span class="sxs-lookup"><span data-stu-id="d8744-222">text</span></span> |<span data-ttu-id="d8744-223">string</span><span class="sxs-lookup"><span data-stu-id="d8744-223">String</span></span> |<span data-ttu-id="d8744-224">Campo To-do item</span><span class="sxs-lookup"><span data-stu-id="d8744-224">To-do item field</span></span> |
| <span data-ttu-id="d8744-225">createdAt</span><span class="sxs-lookup"><span data-stu-id="d8744-225">createdAt</span></span> | <span data-ttu-id="d8744-226">Data</span><span class="sxs-lookup"><span data-stu-id="d8744-226">Date</span></span> | <span data-ttu-id="d8744-227">(opcional) Mapeia muito**criadona** propriedade do sistema</span><span class="sxs-lookup"><span data-stu-id="d8744-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="d8744-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="d8744-228">updatedAt</span></span> | <span data-ttu-id="d8744-229">Data</span><span class="sxs-lookup"><span data-stu-id="d8744-229">Date</span></span> | <span data-ttu-id="d8744-230">(opcional) Mapeia muito**updatedAt** propriedade do sistema</span><span class="sxs-lookup"><span data-stu-id="d8744-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="d8744-231">version</span><span class="sxs-lookup"><span data-stu-id="d8744-231">version</span></span> | <span data-ttu-id="d8744-232">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d8744-232">String</span></span> | <span data-ttu-id="d8744-233">(opcional) Conflitos de toodetect usadas, tooversion de mapas</span><span class="sxs-lookup"><span data-stu-id="d8744-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="d8744-234"><a name="setup-sync"></a>Alterar o comportamento de sincronização de saudação do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d8744-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="d8744-235">Nesta seção, você deve modificar um aplicativo hello para que ele não sincronizado no início do aplicativo ou quando você insere e atualizar itens.</span><span class="sxs-lookup"><span data-stu-id="d8744-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="d8744-236">Sincronizar apenas quando o botão de gesto Olá atualização é executada.</span><span class="sxs-lookup"><span data-stu-id="d8744-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="d8744-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d8744-237">**Objective-C**:</span></span>

1. <span data-ttu-id="d8744-238">Em **QSTodoListViewController.m**, alterar Olá **viewDidLoad** tooremove método hello chamada muito`[self refresh]` final de saudação do método hello.</span><span class="sxs-lookup"><span data-stu-id="d8744-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="d8744-239">Agora dados saudação não estão sincronizados com o servidor de saudação no início do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8744-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="d8744-240">Em vez disso, ele é sincronizado com o conteúdo de saudação do repositório local hello.</span><span class="sxs-lookup"><span data-stu-id="d8744-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="d8744-241">Em **QSTodoService.m**, modificar a definição de saudação do `addItem` para que ele não sincronizado após Olá item é inserido.</span><span class="sxs-lookup"><span data-stu-id="d8744-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="d8744-242">Remover Olá `self syncData` bloquear e substitua-o pelo seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="d8744-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="d8744-243">Modificar a definição de saudação do `completeItem` conforme mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d8744-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="d8744-244">Remover bloco Olá para `self syncData` e substitua-o pelo seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="d8744-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="d8744-245">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d8744-245">**Swift**:</span></span>

<span data-ttu-id="d8744-246">Em `viewDidLoad`, na **ToDoTableViewController.swift**, comente duas linhas de saudação mostrada aqui, toostop sincronização no início do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8744-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="d8744-247">Em tempo de saudação da redação deste artigo, Olá Swift Todo aplicativo não atualizar o serviço de saudação quando alguém adiciona ou conclusão de um item.</span><span class="sxs-lookup"><span data-stu-id="d8744-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="d8744-248">Ele atualiza o serviço Olá apenas no início do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8744-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="d8744-249"><a name="test-app"></a>Aplicativo de teste de saudação</span><span class="sxs-lookup"><span data-stu-id="d8744-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="d8744-250">Nesta seção, você pode se conectar toosimulate de URL inválido tooan um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="d8744-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="d8744-251">Quando você adiciona itens de dados, são mantidos na saudação do repositório de dados do local principal, mas eles não estão sincronizados com o back-end de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="d8744-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="d8744-252">Alterar URL do aplicativo móvel Olá em **QSTodoService.m** tooan URL inválida e aplicativo hello execução novamente:</span><span class="sxs-lookup"><span data-stu-id="d8744-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="d8744-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="d8744-253">**Objective-C**.</span></span> <span data-ttu-id="d8744-254">Em QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="d8744-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="d8744-255">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="d8744-255">**Swift**.</span></span> <span data-ttu-id="d8744-256">Em ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="d8744-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="d8744-257">Adicione alguns itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="d8744-257">Add some to-do items.</span></span> <span data-ttu-id="d8744-258">Encerrar simulador hello (ou aplicativo hello forçará a fechar) e, em seguida, reiniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="d8744-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="d8744-259">Verifique se suas mudanças foram mantidas.</span><span class="sxs-lookup"><span data-stu-id="d8744-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="d8744-260">Exibir conteúdo Olá Olá remoto **TodoItem** tabela:</span><span class="sxs-lookup"><span data-stu-id="d8744-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="d8744-261">Para um Node. js back-end, vá toohello [portal do Azure](https://portal.azure.com/) e, em seu aplicativo móvel back-end, clique em **tabelas fácil** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="d8744-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="d8744-262">Para um back-end do .NET, use uma ferramenta SQL, como o SQL Server Management Studio, ou um cliente REST, como o Fiddler ou o Postman.</span><span class="sxs-lookup"><span data-stu-id="d8744-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="d8744-263">Verifique se novos itens de saudação tem *não* foram sincronizadas com o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8744-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="d8744-264">Alteração Olá URL back toohello corrigir um em **QSTodoService.m**e o aplicativo hello execute.</span><span class="sxs-lookup"><span data-stu-id="d8744-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="d8744-265">Execute Olá atualização gesto colocando-o para baixo na lista de saudação de itens.</span><span class="sxs-lookup"><span data-stu-id="d8744-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="d8744-266">Um controle giratório de progresso é exibido.</span><span class="sxs-lookup"><span data-stu-id="d8744-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="d8744-267">Saudação de exibição **TodoItem** dados novamente.</span><span class="sxs-lookup"><span data-stu-id="d8744-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="d8744-268">itens de tarefas pendentes de novas e alteradas Olá agora devem ser exibidos.</span><span class="sxs-lookup"><span data-stu-id="d8744-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="d8744-269">Resumo</span><span class="sxs-lookup"><span data-stu-id="d8744-269">Summary</span></span>
<span data-ttu-id="d8744-270">recurso de sincronização offline de saudação toosupport, usamos Olá `MSSyncTable` interface e inicializado `MSClient.syncContext` com um repositório local.</span><span class="sxs-lookup"><span data-stu-id="d8744-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="d8744-271">Nesse caso, o armazenamento local Olá foi um banco de dados com base em dados de núcleo.</span><span class="sxs-lookup"><span data-stu-id="d8744-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="d8744-272">Quando você usa um armazenamento local de dados principal, você deve definir várias tabelas com hello [corrigir as propriedades do sistema](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="d8744-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="d8744-273">saudação normal criar, ler, atualizar e excluir operações CRUD () para o trabalho de aplicativos móveis, como se o aplicativo hello ainda está conectado, mas todas as operações de saudação ocorrerem no repositório local hello.</span><span class="sxs-lookup"><span data-stu-id="d8744-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="d8744-274">Quando é sincronizada repositório local Olá com o servidor de saudação, usamos Olá **MSSyncTable.pullWithQuery** método.</span><span class="sxs-lookup"><span data-stu-id="d8744-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8744-275">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d8744-275">Additional resources</span></span>
* <span data-ttu-id="d8744-276">[sincronização de dados Offline em aplicativos móveis]</span><span class="sxs-lookup"><span data-stu-id="d8744-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="d8744-277">[Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure] \(Olá vídeo é sobre serviços móveis, mas os aplicativos móveis offline a sincronização funciona de maneira semelhante.\)</span><span class="sxs-lookup"><span data-stu-id="d8744-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[criar um aplicativo iOS]: app-service-mobile-ios-get-started.md
[sincronização de dados Offline em aplicativos móveis]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
