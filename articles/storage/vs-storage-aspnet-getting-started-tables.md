---
title: "aaaGet de Introdução ao armazenamento de tabela do Azure e o Visual Studio conectado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado usando o armazenamento de tabela do Azure em um projeto do ASP.NET no Visual Studio depois de se conectar a conta de armazenamento tooa usando o Visual Studio conectado Services
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: e7ed17098c8742954972dc9e1b50eca77221e327
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Visão geral

Armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados. serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.

Este tutorial mostra como toowrite ASP.NET código em alguns cenários comuns usando entidades de armazenamento de tabela do Azure. Os cenários abordados incluem a criação de tabela e a adição, consulta e exclusão de entidades de tabela. 

##<a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Conta de armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Criar um controlador MVC 

1. Em Olá **Gerenciador de soluções**, clique com botão direito **controladores**e, no menu de contexto hello, selecione **Adicionar -> controlador**.

    ![Adicionar um controlador tooan aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC 5 - vazio**e selecione **adicionar**.

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. Em Olá **Adicionar controlador** caixa de diálogo, o nome de controlador de saudação *TablesController*e selecione **adicionar**.

    ![Controlador MVC Olá nome](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Adicione o seguinte Olá *usando* diretivas toohello `TablesController.cs` arquivo:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Criar uma classe de modelo

Muitos dos exemplos de saudação neste artigo use um **TableEntity**-chamado de classe derivada **CustomerEntity**. Olá, as etapas a seguir orientam você pelo declarar esta classe como uma classe de modelo.

1. Em Olá **Solution Explorer**, clique com botão direito **modelos**e, no menu de contexto hello, selecione **Adicionar -> classe**.

1. Em Olá **Adicionar Novo Item** caixa de diálogo, a classe de saudação do nome, **CustomerEntity**.

1. Olá abrir `CustomerEntity.cs` de arquivo e adicione o seguinte Olá **usando** diretiva:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Modificar classe Olá para que, quando terminar, a classe de saudação é declarada como Olá código a seguir. classe Olá declara uma classe de entidade chamada **CustomerEntity** que usa Olá nome do cliente como chave de linha de saudação e último nome como chave de partição hello.

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a>Criar uma tabela

Olá etapas a seguir ilustram como toocreate uma tabela:

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `TablesController.cs` arquivo.

1. Adicione um método chamado **CreateTable** que retorna um **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de saudação **CreateTable** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa um nome de tabela desejada de toohello de referência. Olá **CloudTableClient.GetTableReference** método não faz uma solicitação em relação ao armazenamento de tabela. referência de saudação é retornada se tabela Olá existe ou não. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Chamar hello **CloudTable.CreateIfNotExists** tabela de saudação do método toocreate se ele ainda não existir. Olá **CloudTable.CreateIfNotExists** método **true** se Olá tabela não existe e foi criada com êxito. Caso contrário, **false** será retornado.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Saudação de atualização **ViewBag** com o nome de saudação da tabela de saudação.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **CreateTable** para o nome de exibição hello e selecione **adicionar**.

1. Abra `CreateTable.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Execute o aplicativo hello e selecione **criar tabela** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Criar Tabela](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Conforme mencionado anteriormente, Olá **CloudTable.CreateIfNotExists** método **true** somente quando a tabela de saudação não existe e é criada. Portanto, se você executar o aplicativo hello quando Olá tabela existe, método hello retorna **false**. toorun Olá aplicativo várias vezes, você deve excluir tabela Olá antes de executar o aplicativo hello novamente. Excluir tabela Olá pode ser feita por meio de saudação **CloudTable.Delete** método. Você também pode excluir tabela hello usando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa

*Entidades* mapear tooC\# objetos por meio de uma classe personalizada derivam de **TableEntity**. tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de saudação da entidade. Nesta seção, você verá como toodefine uma classe de entidade que usa Olá nome do cliente como chave de linha de saudação e último nome como chave de partição hello. Juntas, chave de linha e de partição da entidade identificam exclusivamente Olá entidade na tabela de saudação. As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes, mas usar chaves de partição diferentes permite uma escalabilidade maior de operações paralelas. Para qualquer propriedade que deve ser armazenada no serviço de tabela hello, propriedade Olá deve ser uma propriedade pública de um tipo com suporte que expõe definindo e recuperando valores.
Olá classe da entidade *deve* declara um construtor sem parâmetros público.

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).

1. Olá abrir `TablesController.cs` arquivo.

1. Adicionar Olá após diretiva de forma que Olá código Olá `TablesController.cs` arquivo pode acessar Olá **CustomerEntity** classe:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Adicione um método chamado **AddEntity** que retorna um **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de saudação **AddEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma referência toohello tabela toowhich que você vai nova entidade do tooadd hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Criar uma instância e inicializar Olá **CustomerEntity** classe.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Criar um **TableOperation** objeto que insere a entidade de saudação do cliente.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Executar operação de inserção Olá por chamada hello **CloudTable.Execute** método. Você pode verificar o resultado de saudação da operação de saudação inspecionando Olá **TableResult.HttpStatusCode** propriedade. Um código de status de 2xx indica a ação Olá solicitada pelo cliente Olá foi processada com êxito. Por exemplo, inserções bem-sucedida de novas entidades resulta em um código de status HTTP 204, que significa que a operação Olá foi processada com êxito e servidor de saudação não retornou nenhum conteúdo.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Saudação de atualização **ViewBag** com nome de tabela Olá e os resultados de saudação da operação de inserção de saudação.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **AddEntity** para o nome de exibição hello e selecione **adicionar**.

1. Abra `AddEntity.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Execute o aplicativo hello e selecione **Adicionar entidade** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Adicionar entidade](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Você pode verificar se entidade Olá foi adicionada, seguindo as etapas de saudação na seção hello, [obter uma única entidade](#get-a-single-entity). Você também pode usar o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Olá entidades para as tabelas.

## <a name="add-a-batch-of-entities-tooa-table"></a>Adicionar um lote de tabela de tooa de entidades

Em adição toobeing capaz muito[adicionar uma tabela de tooa de entidade um por vez](#add-an-entity-to-a-table), você também pode adicionar entidades em lote. Adicionando entidades em lote reduz o número de saudação de ida e volta entre o código e Olá serviço tabela do Azure. Olá, as etapas a seguir ilustra como tooadd tooa de várias entidades de tabela com uma operação de inserção de única:

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).

1. Olá abrir `TablesController.cs` arquivo.

1. Adicione um método chamado **AddEntities** que retorna um **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de saudação **AddEntities** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma referência toohello tabela toowhich que você está indo tooadd novas entidades hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Criar alguns objetos de cliente com base em Olá **CustomerEntity** classe apresentado na seção hello, modelo [adicionar uma tabela de entidade tooa](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Obtenha um objeto **TableBatchOperation**.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Adicione objeto de operação de inserção de lote de toohello entidades.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Executar operação de inserção em lotes Olá por chamada hello **CloudTable.ExecuteBatch** método.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Olá **CloudTable.ExecuteBatch** método retorna uma lista de **TableResult** objetos onde cada **TableResult** objeto pode ser examinadas toodetermine Olá êxito ou falha de cada operação individual. Neste exemplo, passar o modo de exibição do hello lista tooa e permitem que exibição Olá exibir resultados de saudação de cada operação. 
 
    ```csharp
    return View(results);
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **AddEntities** para o nome de exibição hello e selecione **adicionar**.

1. Abra `AddEntities.cshtml`e modifique-o para que ele se parece com o seguinte hello.

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Execute o aplicativo hello e selecione **adicionar entidades** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Adicionar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Você pode verificar se entidade Olá foi adicionada, seguindo as etapas de saudação na seção hello, [obter uma única entidade](#get-a-single-entity). Você também pode usar o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Olá entidades para as tabelas.

## <a name="get-a-single-entity"></a>Obter uma única entidade

Esta seção ilustra como tooget uma única entidade de uma tabela usando Olá chave de linha e a chave de partição da entidade. 

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment)e usa dados de [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). 

1. Olá abrir `TablesController.cs` arquivo.

1. Adicione um método chamado **GetSingle** que retorna um **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de saudação **GetSingle** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello de referência do qual você está recuperando entidade hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Crie um objeto de operação de recuperação que usa um objeto de entidade derivado de **TableEntity**. Olá primeiro parâmetro é Olá *partitionKey*, e Olá segundo parâmetro é Olá *rowKey*. Usando Olá **CustomerEntity** classe e os dados apresentados na seção Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), Olá a tabela a seguir código trecho consultas Olá para um **CustomerEntity** entidade com uma *partitionKey* valor de "Smith" e um *rowKey* valor de "Ben":

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Execute operação de recuperação de saudação.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Passe toohello exibição de resultado da saudação para exibição.

    ```csharp
    return View(result);
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **GetSingle** para o nome de exibição hello e selecione **adicionar**.

1. Abra `GetSingle.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Execute o aplicativo hello e selecione **obter único** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Obter um único](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Obter todas as entidades em uma partição

Conforme mencionado na seção hello, [adicionar uma tabela de entidade tooa](#add-an-entity-to-a-table), combinação de saudação de uma partição e uma chave de linha identificam exclusivamente uma entidade em uma tabela. As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes. Esta seção ilustra como tooquery uma tabela para todas as entidades de saudação de uma partição especificada.  

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment)e usa dados de [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). 

1. Olá abrir `TablesController.cs` arquivo.

1. Adicione um método chamado **GetPartition** que retorna um **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de saudação **GetPartition** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello de referência do qual você está recuperando entidades hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Criar uma instância de um **TableQuery** objeto especificando consulta Olá no hello **onde** cláusula. Usando Olá **CustomerEntity** classe e os dados apresentados na seção Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), tabela de Olá consultas trecho de código para uma todas as entidades de código a seguir Olá onde hello  **PartitionKey** (Sobrenome do cliente) tem um valor de "Smith":

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. Em um loop, chame Olá **CloudTable.ExecuteQuerySegmented** passando o objeto de consulta de saudação criada por você na etapa anterior de saudação do método.  Olá **CloudTable.ExecuteQuerySegmented** método retorna um **TableContinuationToken** do objeto que - quando **nulo** -indica que não há mais nenhum entidades tooretrieve. Dentro do loop de saudação usam outro tooiterate de loop Olá retornado de entidades. Olá exemplo de código a seguir, cada entidade retornada é adicionada tooa lista. Uma vez Olá termina, lista de saudação é passada tooa exibição para exibição: 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **GetPartition** para o nome de exibição hello e selecione **adicionar**.

1. Abra `GetPartition.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Execute o aplicativo hello e selecione **obter partição** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Obter Partição](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Excluir uma entidade

Esta seção ilustra como toodelete uma entidade de uma tabela.

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment)e usa dados de [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). 

1. Olá abrir `TablesController.cs` arquivo.

1. Adicione um método chamado **DeleteEntity** que retorna um **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de saudação **DeleteEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obter um **CloudTable** objeto que representa uma tabela de toohello de referência do qual você está excluindo a entidade de saudação. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Crie um objeto de operação de exclusão que usa um objeto de entidade derivado de **TableEntity**. Nesse caso, usamos Olá **CustomerEntity** classe e os dados apresentados na seção Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table). Olá da entidade **ETag** deve ser definido um valor válido de tooa.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Execute a operação de exclusão de saudação.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Passe toohello exibição de resultado da saudação para exibição.

    ```csharp
    return View(result);
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **DeleteEntity** para o nome de exibição hello e selecione **adicionar**.

1. Abra `DeleteEntity.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Execute o aplicativo hello e selecione **excluir entidade** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Obter um único](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Próximas etapas
Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.

  * [Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)
