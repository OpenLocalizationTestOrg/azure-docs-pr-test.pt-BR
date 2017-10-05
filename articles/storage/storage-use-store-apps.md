---
title: Usar o Armazenamento do Azure em aplicativos da Windows Store | Microsoft Docs
description: Saiba como criar um aplicativo da Windows Store que usa o Armazenamento de Arquivos, Tabela, Fila ou Blobs do Azure.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="777ec-103">Como usar o Armazenamento do Azure em aplicativos da Windows Store</span><span class="sxs-lookup"><span data-stu-id="777ec-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="777ec-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="777ec-104">Overview</span></span>
<span data-ttu-id="777ec-105">Este guia mostra como iniciar o desenvolvimento de um aplicativo da Windows Store que utiliza o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="777ec-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="777ec-106">Baixar as ferramentas necessárias</span><span class="sxs-lookup"><span data-stu-id="777ec-106">Download required tools</span></span>
* <span data-ttu-id="777ec-107">O [Visual Studio](https://www.visualstudio.com/downloads/) facilita a criação, a depuração, a localização, o empacotamento e a implantação de aplicativos da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="777ec-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="777ec-108">É necessário o Visual Studio 2012 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="777ec-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="777ec-109">A [Biblioteca de cliente de armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage) fornece uma biblioteca de classes do Windows Runtime para trabalhar com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="777ec-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="777ec-110">[Ferramentas do WCF Data Services para aplicativos da Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) ampliam a experiência Adicionar Referência de Serviço com o suporte a OData no lado do cliente para aplicativos da Windows Store no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="777ec-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="777ec-111">Desenvolver aplicativos</span><span class="sxs-lookup"><span data-stu-id="777ec-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="777ec-112">Preparando-se</span><span class="sxs-lookup"><span data-stu-id="777ec-112">Getting ready</span></span>
<span data-ttu-id="777ec-113">Crie um novo projeto de aplicativo da Windows Store no Visual Studio 2012 ou posterior:</span><span class="sxs-lookup"><span data-stu-id="777ec-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="777ec-115">Em seguida, adicione uma referência à Biblioteca de Cliente de Armazenamento do Azure clicando com o botão direito do mouse em **Referências**, clicando em **Adicionar Referência** e navegando até a Biblioteca de Cliente de Armazenamento para Tempo de Execução do Windows que você baixou:</span><span class="sxs-lookup"><span data-stu-id="777ec-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="777ec-117">Usando a biblioteca com os serviços Blob e Fila</span><span class="sxs-lookup"><span data-stu-id="777ec-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="777ec-118">Neste ponto, seu aplicativo está pronto para chamar os serviços Blob e Fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="777ec-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="777ec-119">Adicione as instruções **using** a seguir, de forma que os tipos de armazenamento do Azure possam ser referenciados diretamente:</span><span class="sxs-lookup"><span data-stu-id="777ec-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="777ec-120">Em seguida, adicione um botão à sua página.</span><span class="sxs-lookup"><span data-stu-id="777ec-120">Next, add a button to your page.</span></span> <span data-ttu-id="777ec-121">Adicione o código a seguir ao evento **Click** e modifique seu método de manipulador de eventos usando a [palavra-chave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="777ec-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="777ec-122">Esse código pressupõe que você tenha duas variáveis de cadeia de caracteres, *accountName* e *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="777ec-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="777ec-123">Elas representam o nome da sua conta de armazenamento e a chave de conta associada a essa conta.</span><span class="sxs-lookup"><span data-stu-id="777ec-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="777ec-124">Compile e execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="777ec-124">Build and run the application.</span></span> <span data-ttu-id="777ec-125">Clicar no botão verificará se existe um contêiner chamado *container1* em sua conta e, se não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="777ec-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="777ec-126">Usando a biblioteca com o serviço Tabela</span><span class="sxs-lookup"><span data-stu-id="777ec-126">Using the library with the Table service</span></span>
<span data-ttu-id="777ec-127">Os tipos que são usados para se comunicar com o serviço Tabela do Azure dependem do WFC Data Services para a biblioteca de aplicativos da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="777ec-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="777ec-128">Em seguida, adicione uma referência às bibliotecas necessárias do WCF usando o Console do Gerenciador de Pacotes:</span><span class="sxs-lookup"><span data-stu-id="777ec-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="777ec-130">Use o comando a seguir para apontar o Gerenciador de Pacotes para a localização de sua máquina:</span><span class="sxs-lookup"><span data-stu-id="777ec-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="777ec-131">Esse comando adicionará todas as referências necessárias ao seu projeto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="777ec-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="777ec-132">Se não quiser usar o Console do Gerenciador de Pacotes, você poderá adicionar a pasta NuGet do WCF Data Services em seu computador local à lista de origens do pacote e, em seguida, adicionar a referência por meio da interface do usuário, conforme descrito em [Gerenciando pacotes NuGet usando a caixa de diálogo](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="777ec-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="777ec-133">Quando fizer referência ao pacote NuGet do WCF Data Services, altere o código no evento **Click** de seu botão:</span><span class="sxs-lookup"><span data-stu-id="777ec-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="777ec-134">Esse código verifica se uma tabela nomeada *table1* existe em sua conta, criando-a se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="777ec-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="777ec-135">Você também pode adicionar uma referência à Microsoft.WindowsAzure.Storage.Table.dll, que está disponível no mesmo pacote que você baixou.</span><span class="sxs-lookup"><span data-stu-id="777ec-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="777ec-136">Essa biblioteca contém funcionalidades adicionais, como consultas genéricas e serialização com base em reflexão.</span><span class="sxs-lookup"><span data-stu-id="777ec-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="777ec-137">Observe que essa biblioteca não dá suporte a JavaScript.</span><span class="sxs-lookup"><span data-stu-id="777ec-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
