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
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Habilitar a sincronização offline com aplicativos móveis do iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Visão geral
Este tutorial aborda offline sincronizando com o recurso de aplicativos móveis de saudação do serviço de aplicativo do Azure para iOS. Com os usuários finais sincronização offline podem interagir com um aplicativo móvel tooview, adicionar ou modificar dados, mesmo quando eles têm nenhuma conexão de rede. As alterações são armazenadas em um banco de dados local. Depois que o dispositivo de saudação estiver online novamente, as alterações de saudação são sincronizadas com Olá remoto back-end.

Se esta for sua primeira experiência com aplicativos móveis, primeiro você deve concluir o tutorial de saudação [criar um aplicativo iOS]. Se você não usar o projeto de início rápido do servidor de saudação baixado, você deve adicionar o projeto de tooyour de pacotes de extensão de acesso a dados hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn mais sobre o recurso de sincronização offline hello, consulte [sincronização de dados Offline em aplicativos móveis].

## <a name="review-sync"></a>Examine o código de sincronização do cliente Olá
projeto de cliente de saudação que baixou para Olá [criar um aplicativo iOS] tutorial já contém código que oferece suporte à sincronização offline usando um banco de dados local com base em dados de núcleo. Esta seção resume o que já está incluído no código tutorial hello. Para obter uma visão geral conceitual do recurso hello, consulte [sincronização de dados Offline em aplicativos móveis].

Usando o recurso de sincronização de dados offline Olá de aplicativos móveis, os usuários finais podem interagir com um banco de dados local mesmo quando a rede hello está inacessível. toouse esses recursos em seu aplicativo, que você inicializar o contexto de sincronização de saudação do `MSClient` e fazer referência a um repositório local. Em seguida, você referenciar a tabela por meio de saudação **MSSyncTable** interface.

Em **QSTodoService.m** (Objective-C) ou **ToDoTableViewController.swift** (rápida), observe que Olá tipo de membro Olá **syncTable** é  **MSSyncTable**. A sincronização offline usa esta interface de tabela de sincronização em vez de **MSTable**. Quando uma tabela de sincronização é usada, todas as operações vá repositório local toohello e sejam sincronizadas somente com hello remoto back-end com envio por push explícito e pull operações.

 tooget uma tabela de sincronização de tooa de referência, use Olá **syncTableWithName** método `MSClient`. funcionalidade de sincronização offline tooremove, use **tableWithName** em vez disso.

Antes de quaisquer operações de tabela podem ser executadas, armazenamento local Olá deve ser inicializado. Aqui está o código relevante hello:

* **Objective-C**. Em Olá **QSTodoService.init** método:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Swift**. Em Olá **ToDoTableViewController.viewDidLoad** método:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Esse método cria um repositório local usando Olá `MSCoreDataStore` fornece interface, que Olá SDK de aplicativos móveis. Como alternativa, você pode fornecer um armazenamento local diferente implementando Olá `MSSyncContextDataSource` protocolo. Além disso, Olá primeiro parâmetro de **MSSyncContext** é toospecify usado um manipulador de conflito. Como podemos ter passado `nil`, obtemos o manipulador de conflito padrão hello, falha em qualquer conflito.

Agora, vamos executar a operação de sincronização real hello e obter dados de saudação remoto back-end:

* **Objective-C**. `syncData`envia primeiro novas alterações e, em seguida, chama **pullData** tooget dados de saudação remoto back-end. Por sua vez, Olá **pullData** método obtém novos dados que corresponde a uma consulta:

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
* **Swift**:
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

Na versão Olá Objective-C, em `syncData`, podemos chamar primeiro **pushWithCompletion** no contexto de sincronização de saudação. Esse método é um membro do `MSSyncContext` (e não Olá sincronização própria tabela) porque ele envia as alterações em todas as tabelas. Somente os registros que foram modificados de alguma forma localmente (por meio de operações de CUD) são enviados toohello server. Olá, em seguida, o auxiliar **pullData** é chamado, que chama **MSSyncTable.pullWithQuery** tooretrieve remoto de dados e armazená-lo no banco de dados local hello.

Na versão de Swift hello, porque não foi estritamente necessária, a operação de envio de Olá não há nenhuma chamada muito**pushWithCompletion**. Se houver alterações pendentes no contexto de sincronização de saudação para tabela Olá que está executando uma operação de envio por push, pull sempre emite um envio por push primeiro. No entanto, se você tiver mais de uma tabela de sincronização, é melhor tooexplicitly chamada push tooensure que tudo o que é consistente em tabelas relacionadas.

Olá Objective-C e ágil versões, você pode usar Olá **pullWithQuery** método toospecify toofilter uma consulta Olá registros que você deseja tooretrieve. Neste exemplo, a consulta Olá recupera todos os registros no hello remoto `TodoItem` tabela.

Olá segundo parâmetro de **pullWithQuery** é uma ID de consulta que é usada para *sincronização incremental*. A sincronização incremental recupera somente os registros que foram modificados desde a última sincronização hello, usando o registro de saudação `UpdatedAt` carimbo de data / hora (chamado `updatedAt` no hello repositório local.) Olá ID da consulta deve ser uma cadeia de caracteres descritiva é exclusiva para cada consulta lógica em seu aplicativo. tooopt fora de sincronização incremental, passar `nil` como Olá ID da consulta. Observe que isso pode ser potencialmente ineficiente, já que recupera todos os registros de cada operação de recepção.

Olá Objective-C aplicativo será sincronizado quando você modifica ou adicionar dados, quando um usuário executa Olá gesto de atualização e, na inicialização.

aplicativo Swift Olá sincronizado quando o usuário Olá executa Olá gesto de atualização e na inicialização.

Porque hello, sincronizações de aplicativo sempre que dados são modificados (Objective-C) ou sempre que inicia o aplicativo hello (Objective-C e Swift), aplicativo hello pressupõe que o usuário hello está online. Em uma seção posterior, você irá atualizar o aplicativo hello para que os usuários possam editar mesmo quando estão offline.

## <a name="review-core-data"></a>Modelo de dados de núcleo de saudação de revisão
Quando você usa o armazenamento offline de dados principais hello, você deve definir determinadas tabelas e campos em seu modelo de dados. aplicativo de exemplo Hello já inclui um modelo de dados com o formato correto de saudação. Nesta seção, vemos tooshow essas tabelas como eles são usados.

Abra **QSDataModel.xcdatamodeld**. Quatro tabelas são três que são usados por definido - Olá SDK e que é usado para tarefas de saudação itens se:
  * MS_TableOperations: Rastreia Olá itens que precisam de toobe sincronizado com o servidor de saudação.
  * MS_TableOperationErrors: para acompanhar todos os erros que ocorrerem durante a sincronização offline.
  * MS_TableConfig: Rastreia Olá hora da última atualização para a última operação de sincronização Olá para todas as operações de recepção.
  * TodoItem: Armazena itens de tarefas pendentes de saudação. Olá colunas do sistema **criadona**, **updatedAt**, e **versão** são propriedades de sistema opcional.

> [!NOTE]
> Olá SDK de aplicativos móveis reserva nomes de coluna que começam com "**``**". Não use esse prefixo em algo diferente das colunas do sistema. Caso contrário, os nomes de coluna são modificados quando você usa Olá remoto back-end.
>
>

Quando você usa o recurso de sincronização offline hello, defina três tabelas do sistema hello e uma tabela de dados de saudação.

### <a name="system-tables"></a>Tabelas do sistema

**MS_TableOperations**  

![Atributos da tabela MS_TableOperations][defining-core-data-tableoperations-entity]

| Atributo | Tipo |
| --- | --- |
| ID | Número Inteiro 64 |
| itemId | Cadeia de caracteres |
| propriedades | Dados binários |
| tabela | Cadeia de caracteres |
| tableKind | Número inteiro 16 |


**MS_TableOperationErrors**

 ![Atributos da tabela MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| Atributo | Tipo |
| --- | --- |
| ID |Cadeia de caracteres |
| operationId |Número Inteiro 64 |
| propriedades |Dados binários |
| tableKind |Número inteiro 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Atributo | Tipo |
| --- | --- |
| ID |Cadeia de caracteres |
| chave |Cadeia de caracteres |
| keyType |Número Inteiro 64 |
| tabela |Cadeia de caracteres |
| valor |Cadeia de caracteres |

### <a name="data-table"></a>Tabela de dados

**TodoItem**

| Atributo | Tipo | Observação |
| --- | --- | --- |
| ID | Cadeia de caracteres, marcadas como obrigatórias |Chave primária no repositório remoto |
| concluído | Booliano | Campo To-do item |
| texto |string |Campo To-do item |
| createdAt | Data | (opcional) Mapeia muito**criadona** propriedade do sistema |
| updatedAt | Data | (opcional) Mapeia muito**updatedAt** propriedade do sistema |
| version | Cadeia de caracteres | (opcional) Conflitos de toodetect usadas, tooversion de mapas |

## <a name="setup-sync"></a>Alterar o comportamento de sincronização de saudação do aplicativo hello
Nesta seção, você deve modificar um aplicativo hello para que ele não sincronizado no início do aplicativo ou quando você insere e atualizar itens. Sincronizar apenas quando o botão de gesto Olá atualização é executada.

**Objective-C**:

1. Em **QSTodoListViewController.m**, alterar Olá **viewDidLoad** tooremove método hello chamada muito`[self refresh]` final de saudação do método hello. Agora dados saudação não estão sincronizados com o servidor de saudação no início do aplicativo. Em vez disso, ele é sincronizado com o conteúdo de saudação do repositório local hello.
2. Em **QSTodoService.m**, modificar a definição de saudação do `addItem` para que ele não sincronizado após Olá item é inserido. Remover Olá `self syncData` bloquear e substitua-o pelo seguinte hello:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Modificar a definição de saudação do `completeItem` conforme mencionado anteriormente. Remover bloco Olá para `self syncData` e substitua-o pelo seguinte hello:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**Swift**:

Em `viewDidLoad`, na **ToDoTableViewController.swift**, comente duas linhas de saudação mostrada aqui, toostop sincronização no início do aplicativo. Em tempo de saudação da redação deste artigo, Olá Swift Todo aplicativo não atualizar o serviço de saudação quando alguém adiciona ou conclusão de um item. Ele atualiza o serviço Olá apenas no início do aplicativo.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Aplicativo de teste de saudação
Nesta seção, você pode se conectar toosimulate de URL inválido tooan um cenário offline. Quando você adiciona itens de dados, são mantidos na saudação do repositório de dados do local principal, mas eles não estão sincronizados com o back-end de aplicativo móvel hello.

1. Alterar URL do aplicativo móvel Olá em **QSTodoService.m** tooan URL inválida e aplicativo hello execução novamente:

   **Objective-C**. Em QSTodoService.m:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Swift**. Em ToDoTableViewController.swift:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Adicione alguns itens pendentes. Encerrar simulador hello (ou aplicativo hello forçará a fechar) e, em seguida, reiniciá-lo. Verifique se suas mudanças foram mantidas.

3. Exibir conteúdo Olá Olá remoto **TodoItem** tabela:
   * Para um Node. js back-end, vá toohello [portal do Azure](https://portal.azure.com/) e, em seu aplicativo móvel back-end, clique em **tabelas fácil** > **TodoItem**.  
   * Para um back-end do .NET, use uma ferramenta SQL, como o SQL Server Management Studio, ou um cliente REST, como o Fiddler ou o Postman.  

4. Verifique se novos itens de saudação tem *não* foram sincronizadas com o servidor de saudação.

5. Alteração Olá URL back toohello corrigir um em **QSTodoService.m**e o aplicativo hello execute.

6. Execute Olá atualização gesto colocando-o para baixo na lista de saudação de itens.  
Um controle giratório de progresso é exibido.

7. Saudação de exibição **TodoItem** dados novamente. itens de tarefas pendentes de novas e alteradas Olá agora devem ser exibidos.

## <a name="summary"></a>Resumo
recurso de sincronização offline de saudação toosupport, usamos Olá `MSSyncTable` interface e inicializado `MSClient.syncContext` com um repositório local. Nesse caso, o armazenamento local Olá foi um banco de dados com base em dados de núcleo.

Quando você usa um armazenamento local de dados principal, você deve definir várias tabelas com hello [corrigir as propriedades do sistema](#review-core-data).

saudação normal criar, ler, atualizar e excluir operações CRUD () para o trabalho de aplicativos móveis, como se o aplicativo hello ainda está conectado, mas todas as operações de saudação ocorrerem no repositório local hello.

Quando é sincronizada repositório local Olá com o servidor de saudação, usamos Olá **MSSyncTable.pullWithQuery** método.

## <a name="additional-resources"></a>Recursos adicionais
* [sincronização de dados Offline em aplicativos móveis]
* [Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure] \(Olá vídeo é sobre serviços móveis, mas os aplicativos móveis offline a sincronização funciona de maneira semelhante.\)

<!-- URLs. -->


[criar um aplicativo iOS]: app-service-mobile-ios-get-started.md
[sincronização de dados Offline em aplicativos móveis]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Cobertura de nuvem: A sincronização Offline em serviços móveis do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
