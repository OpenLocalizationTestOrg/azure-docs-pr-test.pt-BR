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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="ac260-103">Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="ac260-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="ac260-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ac260-104">Overview</span></span>

<span data-ttu-id="ac260-105">Armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="ac260-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="ac260-106">serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac260-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="ac260-107">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="ac260-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="ac260-108">Este tutorial mostra como toowrite ASP.NET código em alguns cenários comuns usando entidades de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac260-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="ac260-109">Os cenários abordados incluem a criação de tabela e a adição, consulta e exclusão de entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="ac260-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac260-110">Prerequisites</span></span>

* [<span data-ttu-id="ac260-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac260-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="ac260-112">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ac260-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="ac260-113">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="ac260-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="ac260-114">Em Olá **Gerenciador de soluções**, clique com botão direito **controladores**e, no menu de contexto hello, selecione **Adicionar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="ac260-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador tooan aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="ac260-116">Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC 5 - vazio**e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="ac260-118">Em Olá **Adicionar controlador** caixa de diálogo, o nome de controlador de saudação *TablesController*e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Controlador MVC Olá nome](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="ac260-120">Adicione o seguinte Olá *usando* diretivas toohello `TablesController.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="ac260-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="ac260-121">Criar uma classe de modelo</span><span class="sxs-lookup"><span data-stu-id="ac260-121">Create a model class</span></span>

<span data-ttu-id="ac260-122">Muitos dos exemplos de saudação neste artigo use um **TableEntity**-chamado de classe derivada **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="ac260-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="ac260-123">Olá, as etapas a seguir orientam você pelo declarar esta classe como uma classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="ac260-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="ac260-124">Em Olá **Solution Explorer**, clique com botão direito **modelos**e, no menu de contexto hello, selecione **Adicionar -> classe**.</span><span class="sxs-lookup"><span data-stu-id="ac260-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="ac260-125">Em Olá **Adicionar Novo Item** caixa de diálogo, a classe de saudação do nome, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="ac260-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="ac260-126">Olá abrir `CustomerEntity.cs` de arquivo e adicione o seguinte Olá **usando** diretiva:</span><span class="sxs-lookup"><span data-stu-id="ac260-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="ac260-127">Modificar classe Olá para que, quando terminar, a classe de saudação é declarada como Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ac260-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="ac260-128">classe Olá declara uma classe de entidade chamada **CustomerEntity** que usa Olá nome do cliente como chave de linha de saudação e último nome como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="ac260-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="ac260-129">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="ac260-129">Create a table</span></span>

<span data-ttu-id="ac260-130">Olá etapas a seguir ilustram como toocreate uma tabela:</span><span class="sxs-lookup"><span data-stu-id="ac260-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ac260-131">Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ac260-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ac260-132">Olá abrir `TablesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac260-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="ac260-133">Adicione um método chamado **CreateTable** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ac260-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="ac260-134">Dentro de saudação **CreateTable** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac260-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ac260-135">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="ac260-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="ac260-136">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="ac260-137">Obter um **CloudTable** objeto que representa um nome de tabela desejada de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="ac260-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="ac260-138">Olá **CloudTableClient.GetTableReference** método não faz uma solicitação em relação ao armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="ac260-139">referência de saudação é retornada se tabela Olá existe ou não.</span><span class="sxs-lookup"><span data-stu-id="ac260-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="ac260-140">Chamar hello **CloudTable.CreateIfNotExists** tabela de saudação do método toocreate se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="ac260-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="ac260-141">Olá **CloudTable.CreateIfNotExists** método **true** se Olá tabela não existe e foi criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="ac260-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="ac260-142">Caso contrário, **false** será retornado.</span><span class="sxs-lookup"><span data-stu-id="ac260-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="ac260-143">Saudação de atualização **ViewBag** com o nome de saudação da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac260-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="ac260-144">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="ac260-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ac260-145">Em Olá **adicionar exibição** caixa de diálogo, digite **CreateTable** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ac260-146">Abra `CreateTable.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="ac260-147">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ac260-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ac260-148">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ac260-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="ac260-149">Execute o aplicativo hello e selecione **criar tabela** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Criar Tabela](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="ac260-151">Conforme mencionado anteriormente, Olá **CloudTable.CreateIfNotExists** método **true** somente quando a tabela de saudação não existe e é criada.</span><span class="sxs-lookup"><span data-stu-id="ac260-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="ac260-152">Portanto, se você executar o aplicativo hello quando Olá tabela existe, método hello retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="ac260-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="ac260-153">toorun Olá aplicativo várias vezes, você deve excluir tabela Olá antes de executar o aplicativo hello novamente.</span><span class="sxs-lookup"><span data-stu-id="ac260-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="ac260-154">Excluir tabela Olá pode ser feita por meio de saudação **CloudTable.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="ac260-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="ac260-155">Você também pode excluir tabela hello usando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="ac260-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="ac260-156">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="ac260-156">Add an entity tooa table</span></span>

<span data-ttu-id="ac260-157">*Entidades* mapear tooC\# objetos por meio de uma classe personalizada derivam de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="ac260-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="ac260-158">tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de saudação da entidade.</span><span class="sxs-lookup"><span data-stu-id="ac260-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="ac260-159">Nesta seção, você verá como toodefine uma classe de entidade que usa Olá nome do cliente como chave de linha de saudação e último nome como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="ac260-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="ac260-160">Juntas, chave de linha e de partição da entidade identificam exclusivamente Olá entidade na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac260-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="ac260-161">As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes, mas usar chaves de partição diferentes permite uma escalabilidade maior de operações paralelas.</span><span class="sxs-lookup"><span data-stu-id="ac260-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="ac260-162">Para qualquer propriedade que deve ser armazenada no serviço de tabela hello, propriedade Olá deve ser uma propriedade pública de um tipo com suporte que expõe definindo e recuperando valores.</span><span class="sxs-lookup"><span data-stu-id="ac260-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="ac260-163">Olá classe da entidade *deve* declara um construtor sem parâmetros público.</span><span class="sxs-lookup"><span data-stu-id="ac260-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ac260-164">Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ac260-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="ac260-165">Olá abrir `TablesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac260-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="ac260-166">Adicionar Olá após diretiva de forma que Olá código Olá `TablesController.cs` arquivo pode acessar Olá **CustomerEntity** classe:</span><span class="sxs-lookup"><span data-stu-id="ac260-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="ac260-167">Adicione um método chamado **AddEntity** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ac260-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="ac260-168">Dentro de saudação **AddEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac260-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ac260-169">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="ac260-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="ac260-170">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="ac260-171">Obter um **CloudTable** objeto que representa uma referência toohello tabela toowhich que você vai nova entidade do tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="ac260-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="ac260-172">Criar uma instância e inicializar Olá **CustomerEntity** classe.</span><span class="sxs-lookup"><span data-stu-id="ac260-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="ac260-173">Criar um **TableOperation** objeto que insere a entidade de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="ac260-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="ac260-174">Executar operação de inserção Olá por chamada hello **CloudTable.Execute** método.</span><span class="sxs-lookup"><span data-stu-id="ac260-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="ac260-175">Você pode verificar o resultado de saudação da operação de saudação inspecionando Olá **TableResult.HttpStatusCode** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ac260-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="ac260-176">Um código de status de 2xx indica a ação Olá solicitada pelo cliente Olá foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="ac260-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="ac260-177">Por exemplo, inserções bem-sucedida de novas entidades resulta em um código de status HTTP 204, que significa que a operação Olá foi processada com êxito e servidor de saudação não retornou nenhum conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ac260-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="ac260-178">Saudação de atualização **ViewBag** com nome de tabela Olá e os resultados de saudação da operação de inserção de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac260-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="ac260-179">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="ac260-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ac260-180">Em Olá **adicionar exibição** caixa de diálogo, digite **AddEntity** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ac260-181">Abra `AddEntity.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="ac260-182">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ac260-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ac260-183">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ac260-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="ac260-184">Execute o aplicativo hello e selecione **Adicionar entidade** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Adicionar entidade](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="ac260-186">Você pode verificar se entidade Olá foi adicionada, seguindo as etapas de saudação na seção hello, [obter uma única entidade](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="ac260-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="ac260-187">Você também pode usar o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Olá entidades para as tabelas.</span><span class="sxs-lookup"><span data-stu-id="ac260-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="ac260-188">Adicionar um lote de tabela de tooa de entidades</span><span class="sxs-lookup"><span data-stu-id="ac260-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="ac260-189">Em adição toobeing capaz muito[adicionar uma tabela de tooa de entidade um por vez](#add-an-entity-to-a-table), você também pode adicionar entidades em lote.</span><span class="sxs-lookup"><span data-stu-id="ac260-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="ac260-190">Adicionando entidades em lote reduz o número de saudação de ida e volta entre o código e Olá serviço tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac260-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="ac260-191">Olá, as etapas a seguir ilustra como tooadd tooa de várias entidades de tabela com uma operação de inserção de única:</span><span class="sxs-lookup"><span data-stu-id="ac260-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ac260-192">Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ac260-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="ac260-193">Olá abrir `TablesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac260-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="ac260-194">Adicione um método chamado **AddEntities** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ac260-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="ac260-195">Dentro de saudação **AddEntities** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac260-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ac260-196">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="ac260-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="ac260-197">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="ac260-198">Obter um **CloudTable** objeto que representa uma referência toohello tabela toowhich que você está indo tooadd novas entidades hello.</span><span class="sxs-lookup"><span data-stu-id="ac260-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="ac260-199">Criar alguns objetos de cliente com base em Olá **CustomerEntity** classe apresentado na seção hello, modelo [adicionar uma tabela de entidade tooa](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="ac260-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="ac260-200">Obtenha um objeto **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="ac260-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="ac260-201">Adicione objeto de operação de inserção de lote de toohello entidades.</span><span class="sxs-lookup"><span data-stu-id="ac260-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="ac260-202">Executar operação de inserção em lotes Olá por chamada hello **CloudTable.ExecuteBatch** método.</span><span class="sxs-lookup"><span data-stu-id="ac260-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="ac260-203">Olá **CloudTable.ExecuteBatch** método retorna uma lista de **TableResult** objetos onde cada **TableResult** objeto pode ser examinadas toodetermine Olá êxito ou falha de cada operação individual.</span><span class="sxs-lookup"><span data-stu-id="ac260-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="ac260-204">Neste exemplo, passar o modo de exibição do hello lista tooa e permitem que exibição Olá exibir resultados de saudação de cada operação.</span><span class="sxs-lookup"><span data-stu-id="ac260-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="ac260-205">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="ac260-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ac260-206">Em Olá **adicionar exibição** caixa de diálogo, digite **AddEntities** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ac260-207">Abra `AddEntities.cshtml`e modifique-o para que ele se parece com o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="ac260-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

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

1. <span data-ttu-id="ac260-208">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ac260-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ac260-209">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ac260-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="ac260-210">Execute o aplicativo hello e selecione **adicionar entidades** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Adicionar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="ac260-212">Você pode verificar se entidade Olá foi adicionada, seguindo as etapas de saudação na seção hello, [obter uma única entidade](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="ac260-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="ac260-213">Você também pode usar o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Olá entidades para as tabelas.</span><span class="sxs-lookup"><span data-stu-id="ac260-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="ac260-214">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="ac260-214">Get a single entity</span></span>

<span data-ttu-id="ac260-215">Esta seção ilustra como tooget uma única entidade de uma tabela usando Olá chave de linha e a chave de partição da entidade.</span><span class="sxs-lookup"><span data-stu-id="ac260-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="ac260-216">Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment)e usa dados de [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="ac260-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="ac260-217">Olá abrir `TablesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac260-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="ac260-218">Adicione um método chamado **GetSingle** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ac260-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="ac260-219">Dentro de saudação **GetSingle** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac260-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ac260-220">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="ac260-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="ac260-221">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="ac260-222">Obter um **CloudTable** objeto que representa uma tabela de toohello de referência do qual você está recuperando entidade hello.</span><span class="sxs-lookup"><span data-stu-id="ac260-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="ac260-223">Crie um objeto de operação de recuperação que usa um objeto de entidade derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="ac260-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="ac260-224">Olá primeiro parâmetro é Olá *partitionKey*, e Olá segundo parâmetro é Olá *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="ac260-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="ac260-225">Usando Olá **CustomerEntity** classe e os dados apresentados na seção Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), Olá a tabela a seguir código trecho consultas Olá para um **CustomerEntity** entidade com uma *partitionKey* valor de "Smith" e um *rowKey* valor de "Ben":</span><span class="sxs-lookup"><span data-stu-id="ac260-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="ac260-226">Execute operação de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac260-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="ac260-227">Passe toohello exibição de resultado da saudação para exibição.</span><span class="sxs-lookup"><span data-stu-id="ac260-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="ac260-228">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="ac260-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ac260-229">Em Olá **adicionar exibição** caixa de diálogo, digite **GetSingle** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ac260-230">Abra `GetSingle.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="ac260-231">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ac260-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ac260-232">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ac260-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="ac260-233">Execute o aplicativo hello e selecione **obter único** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter um único](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="ac260-235">Obter todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="ac260-235">Get all entities in a partition</span></span>

<span data-ttu-id="ac260-236">Conforme mencionado na seção hello, [adicionar uma tabela de entidade tooa](#add-an-entity-to-a-table), combinação de saudação de uma partição e uma chave de linha identificam exclusivamente uma entidade em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="ac260-237">As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes.</span><span class="sxs-lookup"><span data-stu-id="ac260-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="ac260-238">Esta seção ilustra como tooquery uma tabela para todas as entidades de saudação de uma partição especificada.</span><span class="sxs-lookup"><span data-stu-id="ac260-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="ac260-239">Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment)e usa dados de [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="ac260-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="ac260-240">Olá abrir `TablesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac260-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="ac260-241">Adicione um método chamado **GetPartition** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ac260-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="ac260-242">Dentro de saudação **GetPartition** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac260-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ac260-243">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="ac260-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="ac260-244">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="ac260-245">Obter um **CloudTable** objeto que representa uma tabela de toohello de referência do qual você está recuperando entidades hello.</span><span class="sxs-lookup"><span data-stu-id="ac260-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="ac260-246">Criar uma instância de um **TableQuery** objeto especificando consulta Olá no hello **onde** cláusula.</span><span class="sxs-lookup"><span data-stu-id="ac260-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="ac260-247">Usando Olá **CustomerEntity** classe e os dados apresentados na seção Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table), tabela de Olá consultas trecho de código para uma todas as entidades de código a seguir Olá onde hello  **PartitionKey** (Sobrenome do cliente) tem um valor de "Smith":</span><span class="sxs-lookup"><span data-stu-id="ac260-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="ac260-248">Em um loop, chame Olá **CloudTable.ExecuteQuerySegmented** passando o objeto de consulta de saudação criada por você na etapa anterior de saudação do método.</span><span class="sxs-lookup"><span data-stu-id="ac260-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="ac260-249">Olá **CloudTable.ExecuteQuerySegmented** método retorna um **TableContinuationToken** do objeto que - quando **nulo** -indica que não há mais nenhum entidades tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="ac260-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="ac260-250">Dentro do loop de saudação usam outro tooiterate de loop Olá retornado de entidades.</span><span class="sxs-lookup"><span data-stu-id="ac260-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="ac260-251">Olá exemplo de código a seguir, cada entidade retornada é adicionada tooa lista.</span><span class="sxs-lookup"><span data-stu-id="ac260-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="ac260-252">Uma vez Olá termina, lista de saudação é passada tooa exibição para exibição:</span><span class="sxs-lookup"><span data-stu-id="ac260-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

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

1. <span data-ttu-id="ac260-253">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="ac260-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ac260-254">Em Olá **adicionar exibição** caixa de diálogo, digite **GetPartition** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ac260-255">Abra `GetPartition.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="ac260-256">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ac260-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ac260-257">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ac260-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="ac260-258">Execute o aplicativo hello e selecione **obter partição** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter Partição](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="ac260-260">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="ac260-260">Delete an entity</span></span>

<span data-ttu-id="ac260-261">Esta seção ilustra como toodelete uma entidade de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ac260-262">Esta seção pressupõe que você concluiu as etapas de saudação em [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment)e usa dados de [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="ac260-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="ac260-263">Olá abrir `TablesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ac260-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="ac260-264">Adicione um método chamado **DeleteEntity** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ac260-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="ac260-265">Dentro de saudação **DeleteEntity** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac260-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ac260-266">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="ac260-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="ac260-267">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="ac260-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="ac260-268">Obter um **CloudTable** objeto que representa uma tabela de toohello de referência do qual você está excluindo a entidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac260-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="ac260-269">Crie um objeto de operação de exclusão que usa um objeto de entidade derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="ac260-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="ac260-270">Nesse caso, usamos Olá **CustomerEntity** classe e os dados apresentados na seção Olá [adicionar um lote de tabela de tooa entidades](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="ac260-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="ac260-271">Olá da entidade **ETag** deve ser definido um valor válido de tooa.</span><span class="sxs-lookup"><span data-stu-id="ac260-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="ac260-272">Execute a operação de exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac260-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="ac260-273">Passe toohello exibição de resultado da saudação para exibição.</span><span class="sxs-lookup"><span data-stu-id="ac260-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="ac260-274">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **tabelas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="ac260-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ac260-275">Em Olá **adicionar exibição** caixa de diálogo, digite **DeleteEntity** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ac260-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="ac260-276">Abra `DeleteEntity.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="ac260-277">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ac260-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ac260-278">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ac260-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="ac260-279">Execute o aplicativo hello e selecione **excluir entidade** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac260-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter um único](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="ac260-281">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac260-281">Next steps</span></span>
<span data-ttu-id="ac260-282">Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="ac260-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="ac260-283">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="ac260-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="ac260-284">Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="ac260-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
