---
title: "Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET) | Microsoft Docs"
description: "Como começar a usar o Armazenamento de Tabelas do Azure em um projeto do ASP.NET no Visual Studio após a conexão a uma conta de armazenamento usando os Serviços Conectados do Visual Studio"
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
ms.openlocfilehash: d9cb32483d3f582bbeb0ccc6a204a8b6d9ea5c96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="6de15-103">Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6de15-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="6de15-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6de15-104">Overview</span></span>

<span data-ttu-id="6de15-105">O serviço de armazenamento de Tabela do Azure permite que você armazene grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="6de15-105">Azure Table storage enables you to store large amounts of structured data.</span></span> <span data-ttu-id="6de15-106">O serviço é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e de fora da nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de15-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="6de15-107">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="6de15-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="6de15-108">Este tutorial mostra como gravar código ASP.NET para alguns cenários comuns usando entidades do Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de15-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="6de15-109">Os cenários abordados incluem a criação de tabela e a adição, consulta e exclusão de entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="6de15-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6de15-110">Prerequisites</span></span>

* [<span data-ttu-id="6de15-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6de15-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="6de15-112">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6de15-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="6de15-113">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="6de15-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="6de15-114">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Controladores** e, no menu de contexto, selecione **Adicionar-> Controlador**.</span><span class="sxs-lookup"><span data-stu-id="6de15-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador a um aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="6de15-116">Na caixa de diálogo **Adicionar Scaffold**, clique em **Controlador MVC 5 – Vazio** e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="6de15-118">Na caixa de diálogo **Adicionar Controlador**, nomeie o controlador *TablesController* e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span></span>

    ![Dê um nome ao controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="6de15-120">Adicione as seguintes diretivas *using* ao arquivo `TablesController.cs`:</span><span class="sxs-lookup"><span data-stu-id="6de15-120">Add the following *using* directives to the `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="6de15-121">Criar uma classe de modelo</span><span class="sxs-lookup"><span data-stu-id="6de15-121">Create a model class</span></span>

<span data-ttu-id="6de15-122">Muitos dos exemplos neste artigo usam uma classe derivada de **TableEntity** chamada **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="6de15-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="6de15-123">As etapas a seguir o orientarão pela declaração desta classe como uma classe de modelo:</span><span class="sxs-lookup"><span data-stu-id="6de15-123">The following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="6de15-124">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Modelos** e, no menu de contexto, selecione **Adicionar->Classe**.</span><span class="sxs-lookup"><span data-stu-id="6de15-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="6de15-125">Na caixa de diálogo **Adicionar Novo Item**, nomeie a classe como **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="6de15-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="6de15-126">Abra o arquivo `CustomerEntity.cs` e adicione a seguinte diretiva **using**:</span><span class="sxs-lookup"><span data-stu-id="6de15-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="6de15-127">Modifique a classe de modo que, quando terminar, ela será declarada como no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="6de15-127">Modify the class so that, when finished, the class is declared as in the following code.</span></span> <span data-ttu-id="6de15-128">A classe é declarada em uma classe de entidade chamada **CustomerEntity** que usa o nome do cliente como a chave de linha e o sobrenome como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="6de15-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="6de15-129">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="6de15-129">Create a table</span></span>

<span data-ttu-id="6de15-130">As etapas a seguir ilustram como criar uma tabela:</span><span class="sxs-lookup"><span data-stu-id="6de15-130">The following steps illustrate how to create a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6de15-131">Esta seção pressupõe que você concluiu as etapas em [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6de15-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="6de15-132">Abra o arquivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="6de15-132">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6de15-133">Adicione um método chamado **CreateTable** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6de15-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6de15-134">Dentro do método **CreateTable**, obtenha um objeto **CloudStorageAccount** que representa as informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de15-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6de15-135">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="6de15-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6de15-136">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6de15-137">Obtenha um objeto **CloudTable** que representa uma referência ao nome da tabela desejada.</span><span class="sxs-lookup"><span data-stu-id="6de15-137">Get a **CloudTable** object that represents a reference to the desired table name.</span></span> <span data-ttu-id="6de15-138">O método **CloudTableClient.GetTableReference** não faz uma solicitação para o Armazenamento de Tabelas.</span><span class="sxs-lookup"><span data-stu-id="6de15-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="6de15-139">A referência é retornada mesmo se a tabela não existir.</span><span class="sxs-lookup"><span data-stu-id="6de15-139">The reference is returned whether or not the table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6de15-140">Chame o método **CloudTable.CreateIfNotExists** para criar a tabela se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="6de15-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span></span> <span data-ttu-id="6de15-141">O método **CloudTable.CreateIfNotExists** retorna **true** se a tabela não existir e for criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="6de15-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span></span> <span data-ttu-id="6de15-142">Caso contrário, **false** será retornado.</span><span class="sxs-lookup"><span data-stu-id="6de15-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="6de15-143">Atualize o **ViewBag** com o nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-143">Update the **ViewBag** with the name of the table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="6de15-144">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Tabelas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6de15-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6de15-145">Na caixa de diálogo **Adicionar Exibição**, insira **CreateTable** para o nome de exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="6de15-146">Abra `CreateTable.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="6de15-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="6de15-147">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6de15-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6de15-148">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6de15-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="6de15-149">Execute o aplicativo e selecione **Criar tabela** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="6de15-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span></span>
  
    ![Criar Tabela](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="6de15-151">Conforme mencionado anteriormente, o método **CloudTable.CreateIfNotExists** retornará **true** apenas quando a tabela não existir e for criada.</span><span class="sxs-lookup"><span data-stu-id="6de15-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span></span> <span data-ttu-id="6de15-152">Portanto, se você executar o aplicativo quando a tabela existir, o método retornará **false**.</span><span class="sxs-lookup"><span data-stu-id="6de15-152">Therefore, if you run the app when the table exists, the method returns **false**.</span></span> <span data-ttu-id="6de15-153">Para executar o aplicativo várias vezes, você deverá excluir a tabela antes de executar o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="6de15-153">To run the app multiple times, you must delete the table before running the app again.</span></span> <span data-ttu-id="6de15-154">É possível excluir a tabela por meio do método **CloudTable.Delete**.</span><span class="sxs-lookup"><span data-stu-id="6de15-154">Deleting the table can be done via the **CloudTable.Delete** method.</span></span> <span data-ttu-id="6de15-155">Também é possível excluir a tabela usando o [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou o [Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6de15-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="6de15-156">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="6de15-156">Add an entity to a table</span></span>

<span data-ttu-id="6de15-157">As *entidades* são mapeadas para objetos C\# usando uma classe personalizada derivada de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="6de15-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="6de15-158">Para adicionar uma entidade a uma tabela, crie uma classe que defina as propriedades da sua entidade.</span><span class="sxs-lookup"><span data-stu-id="6de15-158">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="6de15-159">Nesta seção, você verá como definir uma classe de entidade que usa o nome do cliente como a chave de linha e o sobrenome como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="6de15-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="6de15-160">Juntas, uma chave de partição e uma chave de linha identificam exclusivamente a entidade na tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="6de15-161">As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes, mas usar chaves de partição diferentes permite uma escalabilidade maior de operações paralelas.</span><span class="sxs-lookup"><span data-stu-id="6de15-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="6de15-162">Para qualquer propriedade que deva ser armazenada no serviço Tabela, a propriedade deve ser uma propriedade pública de um tipo com suporte que exponha os valores de configuração e recuperação.</span><span class="sxs-lookup"><span data-stu-id="6de15-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="6de15-163">A classe da entidade *deve* declarar um construtor público sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="6de15-163">The entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6de15-164">Esta seção pressupõe que você concluiu as etapas em [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6de15-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="6de15-165">Abra o arquivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="6de15-165">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6de15-166">Adicione a seguinte diretiva para que o código no arquivo `TablesController.cs` possa acessar a classe **CustomerEntity**:</span><span class="sxs-lookup"><span data-stu-id="6de15-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="6de15-167">Adicione um método chamado **AddEntity** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6de15-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6de15-168">Dentro do método **AddEntity**, obtenha um objeto **CloudStorageAccount** que representa as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de15-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6de15-169">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="6de15-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6de15-170">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6de15-171">Obtenha um objeto **CloudTable** que representa uma referência à tabela na qual a nova entidade será adicionada.</span><span class="sxs-lookup"><span data-stu-id="6de15-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6de15-172">Instancie e inicialize a classe **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="6de15-172">Instantiate and initialize the **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="6de15-173">Crie um objeto **TableOperation** que insere a entidade do cliente.</span><span class="sxs-lookup"><span data-stu-id="6de15-173">Create a **TableOperation** object that inserts the customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="6de15-174">Execute a operação de inserção chamando o método **Cloudtable.Execute**.</span><span class="sxs-lookup"><span data-stu-id="6de15-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span></span> <span data-ttu-id="6de15-175">Você pode verificar o resultado da operação inspecionando a propriedade **TableResult.HttpStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="6de15-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="6de15-176">Um código de status de 2xx indica que a ação solicitada pelo cliente foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="6de15-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span></span> <span data-ttu-id="6de15-177">Por exemplo, inserções bem-sucedidas de novas entidades resultam em um código de status HTTP 204, indicando que a operação foi processada com êxito, e o servidor não retornou qualquer conteúdo.</span><span class="sxs-lookup"><span data-stu-id="6de15-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="6de15-178">Atualize o **ViewBag** com o nome da tabela e os resultados da operação de inserção.</span><span class="sxs-lookup"><span data-stu-id="6de15-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="6de15-179">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Tabelas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6de15-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6de15-180">Na caixa de diálogo **Adicionar Exibição**, digite **AddEntity** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="6de15-181">Abra `AddEntity.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="6de15-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="6de15-182">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6de15-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6de15-183">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6de15-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="6de15-184">Execute o aplicativo e selecione **Adicionar entidade** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="6de15-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span></span>
  
    ![Adicionar entidade](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="6de15-186">Você pode verificar se a entidade foi adicionada seguindo as etapas na seção [Obter uma única entidade](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="6de15-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="6de15-187">Você também pode usar o [Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) para exibir todas as entidades para suas tabelas.</span><span class="sxs-lookup"><span data-stu-id="6de15-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-to-a-table"></a><span data-ttu-id="6de15-188">Adicionar um lote de entidades a uma tabela</span><span class="sxs-lookup"><span data-stu-id="6de15-188">Add a batch of entities to a table</span></span>

<span data-ttu-id="6de15-189">Além de poder [adicionar uma entidade por vez a uma tabela](#add-an-entity-to-a-table), também é possível adicionar entidades em lote.</span><span class="sxs-lookup"><span data-stu-id="6de15-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="6de15-190">Adicionar entidades em lote reduz o número de viagens de ida e volta entre o código e o serviço Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="6de15-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span></span> <span data-ttu-id="6de15-191">As etapas a seguir ilustram como adicionar várias entidades a uma tabela com uma única operação de inserção:</span><span class="sxs-lookup"><span data-stu-id="6de15-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6de15-192">Esta seção pressupõe que você concluiu as etapas em [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="6de15-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="6de15-193">Abra o arquivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="6de15-193">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6de15-194">Adicione um método chamado **AddEntities** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6de15-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6de15-195">Dentro do método **AddEntities**, obtenha um objeto **CloudStorageAccount** que representa as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de15-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6de15-196">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="6de15-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6de15-197">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6de15-198">Obtenha um objeto **CloudTable** que representa uma referência à tabela na qual as novas entidades serão adicionadas.</span><span class="sxs-lookup"><span data-stu-id="6de15-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6de15-199">Instancie alguns objetos de cliente com base na classe modelo **CustomerEntity** apresentada na seção [Adicionar uma entidade a uma tabela](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6de15-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="6de15-200">Obtenha um objeto **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="6de15-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="6de15-201">Adicione entidades ao objeto da operação de inserção em lote.</span><span class="sxs-lookup"><span data-stu-id="6de15-201">Add entities to the batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="6de15-202">Execute a operação de inserção em lote chamando o método **CloudTable.ExecuteBatch**.</span><span class="sxs-lookup"><span data-stu-id="6de15-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="6de15-203">O método **CloudTable.ExecuteBatch** retorna uma lista de objetos **TableResult** em que cada objeto **TableResult** pode ser examinado para determinar o sucesso ou falha de cada operação individual.</span><span class="sxs-lookup"><span data-stu-id="6de15-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span></span> <span data-ttu-id="6de15-204">Para este exemplo, passe a lista para uma exibição e permita que os resultado de cada operação sejam mostrados pela exibição.</span><span class="sxs-lookup"><span data-stu-id="6de15-204">For this example, pass the list to a view and let the view display the results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="6de15-205">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Tabelas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6de15-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6de15-206">Na caixa de diálogo **Adicionar Exibição**, digite **AddEntities** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="6de15-207">Abra `AddEntities.cshtml` e modifique-o para que se pareça com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="6de15-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span></span>

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

1. <span data-ttu-id="6de15-208">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6de15-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6de15-209">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6de15-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="6de15-210">Execute o aplicativo e selecione **Adicionar entidades** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="6de15-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span></span>
  
    ![Adicionar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="6de15-212">Você pode verificar se a entidade foi adicionada seguindo as etapas na seção [Obter uma única entidade](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="6de15-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="6de15-213">Você também pode usar o [Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) para exibir todas as entidades para suas tabelas.</span><span class="sxs-lookup"><span data-stu-id="6de15-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="6de15-214">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="6de15-214">Get a single entity</span></span>

<span data-ttu-id="6de15-215">Esta seção mostra como obter uma única entidade de uma tabela usando a chave de linha e de partição da entidade.</span><span class="sxs-lookup"><span data-stu-id="6de15-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="6de15-216">Esta seção pressupõe que você concluiu as etapas em [configurar o ambiente de desenvolvimento](#set-up-the-development-environment) e usa dados de [Adicionar um lote de entidades a uma tabela](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6de15-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="6de15-217">Abra o arquivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="6de15-217">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6de15-218">Adicione um método chamado **GetSingle** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6de15-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6de15-219">Dentro do método **GetSingle**, obtenha um objeto **CloudStorageAccount** que representa as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de15-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6de15-220">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="6de15-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6de15-221">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6de15-222">Obtenha um objeto **CloudTable** que representa uma referência à tabela da qual a entidade será recuperada.</span><span class="sxs-lookup"><span data-stu-id="6de15-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6de15-223">Crie um objeto de operação de recuperação que usa um objeto de entidade derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="6de15-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="6de15-224">O primeiro parâmetro é *partitionKey*, e o segundo parâmetro é *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="6de15-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span></span> <span data-ttu-id="6de15-225">Usando a classe **CustomerEntity** e os dados apresentados na seção [Adicionar um lote de entidades a uma tabela](#add-a-batch-of-entities-to-a-table), o trecho de código a seguir consulta a tabela em busca de uma entidade **CustomerEntity** com um valor de *partitionKey* de “Mateus” e um valor de *rowKey* de “Rodrigues”:</span><span class="sxs-lookup"><span data-stu-id="6de15-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="6de15-226">Execute a operação de recuperação.</span><span class="sxs-lookup"><span data-stu-id="6de15-226">Execute the retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="6de15-227">Passe o resultado para ser mostrado na exibição.</span><span class="sxs-lookup"><span data-stu-id="6de15-227">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="6de15-228">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Tabelas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6de15-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6de15-229">Na caixa de diálogo **Adicionar Exibição**, insira **GetSingle** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="6de15-230">Abra `GetSingle.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="6de15-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="6de15-231">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6de15-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6de15-232">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6de15-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="6de15-233">Execute o aplicativo e selecione **Obter Único** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="6de15-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span></span>
  
    ![Obter um único](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="6de15-235">Obter todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="6de15-235">Get all entities in a partition</span></span>

<span data-ttu-id="6de15-236">Conforme mencionado na seção [Adicionar uma entidade a uma tabela](#add-an-entity-to-a-table), a combinação de uma partição e uma chave de linha identifica com exclusividade uma entidade em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="6de15-237">As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes.</span><span class="sxs-lookup"><span data-stu-id="6de15-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="6de15-238">Esta seção mostra como consultar uma tabela de todas as entidades de uma partição específica.</span><span class="sxs-lookup"><span data-stu-id="6de15-238">This section illustrates how to query a table for all the entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="6de15-239">Esta seção pressupõe que você concluiu as etapas em [configurar o ambiente de desenvolvimento](#set-up-the-development-environment) e usa dados de [Adicionar um lote de entidades a uma tabela](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6de15-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="6de15-240">Abra o arquivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="6de15-240">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6de15-241">Adicione um método chamado **GetPartition** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6de15-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6de15-242">Dentro do método **GetPartition**, obtenha um objeto **CloudStorageAccount** que representa as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de15-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6de15-243">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="6de15-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6de15-244">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6de15-245">Obtenha um objeto **CloudTable** que representa uma referência à tabela da qual as entidades serão recuperadas.</span><span class="sxs-lookup"><span data-stu-id="6de15-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6de15-246">Crie uma instância de um objeto **TableQuery** que especifica a consulta na cláusula **Where**.</span><span class="sxs-lookup"><span data-stu-id="6de15-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span></span> <span data-ttu-id="6de15-247">Usando a classe **CustomerEntity** e os dados apresentados na seção [Adicionar um lote de entidades a uma tabela](#add-a-batch-of-entities-to-a-table), o trecho de código a seguir consulta a tabela em busca de uma entidade na qual **PartitionKey** (sobrenome do cliente) tem um valor de “Rodrigues”:</span><span class="sxs-lookup"><span data-stu-id="6de15-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="6de15-248">Dentro de um loop, chame o método **CloudTable.ExecuteQuerySegmented** passando o objeto de consulta para o qual você criou uma instância na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="6de15-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span></span>  <span data-ttu-id="6de15-249">O método **CloudTable.ExecuteQuerySegmented** retorna um objeto **TableContinuationToken** que - quando é **nulo** -indica que não há mais entidades para recuperação.</span><span class="sxs-lookup"><span data-stu-id="6de15-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span></span> <span data-ttu-id="6de15-250">Dentro do loop, use outro loop para iterar sobre as entidades retornadas.</span><span class="sxs-lookup"><span data-stu-id="6de15-250">Within the loop, use another loop to iterate over the returned entities.</span></span> <span data-ttu-id="6de15-251">No código de exemplo a seguir, cada entidade retornada é adicionada a uma lista.</span><span class="sxs-lookup"><span data-stu-id="6de15-251">In the following code example, each returned entity is added to a list.</span></span> <span data-ttu-id="6de15-252">Depois que o loop é encerrado, a lista é passada para ser mostrada em uma exibição:</span><span class="sxs-lookup"><span data-stu-id="6de15-252">Once the loop ends, the list is passed to a view for display:</span></span> 

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

1. <span data-ttu-id="6de15-253">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Tabelas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6de15-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6de15-254">Na caixa de diálogo **Adicionar Exibição**, insira **GetPartition** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="6de15-255">Abra `GetPartition.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="6de15-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="6de15-256">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6de15-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6de15-257">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6de15-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="6de15-258">Execute o aplicativo e selecione **Obter Partição** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="6de15-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span></span>
  
    ![Obter Partição](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="6de15-260">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="6de15-260">Delete an entity</span></span>

<span data-ttu-id="6de15-261">Esta seção ilustra como excluir uma entidade de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-261">This section illustrates how to delete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6de15-262">Esta seção pressupõe que você concluiu as etapas em [configurar o ambiente de desenvolvimento](#set-up-the-development-environment) e usa dados de [Adicionar um lote de entidades a uma tabela](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6de15-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="6de15-263">Abra o arquivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="6de15-263">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="6de15-264">Adicione um método chamado **DeleteEntity** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="6de15-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="6de15-265">Dentro do método **DeleteEntity**, obtenha um objeto **CloudStorageAccount** que representa as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6de15-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6de15-266">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="6de15-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="6de15-267">Obtenha um objeto **CloudTableClient** que representa um cliente do serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="6de15-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="6de15-268">Obtenha um objeto **CloudTable** que representa uma referência à tabela da qual a entidade será excluída.</span><span class="sxs-lookup"><span data-stu-id="6de15-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="6de15-269">Crie um objeto de operação de exclusão que usa um objeto de entidade derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="6de15-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="6de15-270">Neste caso, usamos a classe **CustomerEntity** e os dados apresentados na seção, [Adicionar um lote de entidades a uma tabela](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="6de15-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="6de15-271">A **Etag** da entidade deve ser definida como um valor válido.</span><span class="sxs-lookup"><span data-stu-id="6de15-271">The entity's **ETag** must be set to a valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="6de15-272">Execute a operação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="6de15-272">Execute the delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="6de15-273">Passe o resultado para ser mostrado na exibição.</span><span class="sxs-lookup"><span data-stu-id="6de15-273">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="6de15-274">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Tabelas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6de15-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="6de15-275">Na caixa de diálogo **Adicionar Exibição**, digite **DeleteEntity** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6de15-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="6de15-276">Abra `DeleteEntity.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="6de15-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="6de15-277">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6de15-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="6de15-278">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="6de15-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="6de15-279">Execute o aplicativo e selecione **Excluir entidade** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="6de15-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span></span>
  
    ![Obter um único](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="6de15-281">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6de15-281">Next steps</span></span>
<span data-ttu-id="6de15-282">Consulte outros guias de recursos para obter informações sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="6de15-282">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="6de15-283">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6de15-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="6de15-284">Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="6de15-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
