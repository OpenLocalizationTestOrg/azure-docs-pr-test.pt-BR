---
title: aaaUse armazenamento do Azure em aplicativos da Windows Store | Microsoft Docs
description: Saiba como toocreate um Windows armazenam aplicativo que usa o armazenamento de BLOBs do Azure, fila, tabela ou arquivo.
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
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="74ae0-103">Como toouse o armazenamento do Azure em aplicativos da Windows Store</span><span class="sxs-lookup"><span data-stu-id="74ae0-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="74ae0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="74ae0-104">Overview</span></span>
<span data-ttu-id="74ae0-105">Este guia mostra como tooget iniciada com o desenvolvimento de um aplicativo da Windows Store que usa o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74ae0-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="74ae0-106">Baixar as ferramentas necessárias</span><span class="sxs-lookup"><span data-stu-id="74ae0-106">Download required tools</span></span>
* <span data-ttu-id="74ae0-107">[O Visual Studio](https://www.visualstudio.com/downloads/) torna fácil toobuild, depurar, localizar, empacotar e implantar aplicativos da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="74ae0-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="74ae0-108">É necessário o Visual Studio 2012 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="74ae0-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="74ae0-109">Olá [biblioteca de cliente de armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage) fornece uma biblioteca de classes de tempo de execução do Windows para trabalhar com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74ae0-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="74ae0-110">[WCF Data Services ferramentas para aplicativos da Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) estende a experiência do hello adicionar referência de serviço com suporte de OData do lado do cliente para aplicativos da Windows Store no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74ae0-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="74ae0-111">Desenvolver aplicativos</span><span class="sxs-lookup"><span data-stu-id="74ae0-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="74ae0-112">Preparando-se</span><span class="sxs-lookup"><span data-stu-id="74ae0-112">Getting ready</span></span>
<span data-ttu-id="74ae0-113">Crie um novo projeto de aplicativo da Windows Store no Visual Studio 2012 ou posterior:</span><span class="sxs-lookup"><span data-stu-id="74ae0-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="74ae0-115">Em seguida, adicione uma referência toohello biblioteca de cliente de armazenamento do Azure clicando **referências**, clicando em **adicionar referência**e, em seguida, navegação toohello biblioteca de cliente de armazenamento para o Runtime do Windows que você download:</span><span class="sxs-lookup"><span data-stu-id="74ae0-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="74ae0-117">Usando a biblioteca Olá Olá Blob e serviços de fila</span><span class="sxs-lookup"><span data-stu-id="74ae0-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="74ae0-118">Neste ponto, seu aplicativo estiver pronto toocall hello Azure Blob e fila dos serviços.</span><span class="sxs-lookup"><span data-stu-id="74ae0-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="74ae0-119">Adicione o seguinte Olá **usando** instruções para que os tipos de armazenamento do Azure podem ser referenciados diretamente:</span><span class="sxs-lookup"><span data-stu-id="74ae0-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="74ae0-120">Em seguida, adicione uma página de tooyour do botão.</span><span class="sxs-lookup"><span data-stu-id="74ae0-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="74ae0-121">Adicionar Olá tooits de código a seguir **clique** eventos e modificar seu método de manipulador de eventos usando Olá [palavra-chave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="74ae0-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="74ae0-122">Esse código pressupõe que você tenha duas variáveis de cadeia de caracteres, *accountName* e *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="74ae0-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="74ae0-123">Eles representam o nome de saudação da sua conta e hello chave conta de armazenamento que está associado essa conta.</span><span class="sxs-lookup"><span data-stu-id="74ae0-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="74ae0-124">Compilar e executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="74ae0-124">Build and run hello application.</span></span> <span data-ttu-id="74ae0-125">Botão de saudação clicando em verificará se um contêiner nomeado *container1* existe em sua conta e, em seguida, crie-o se não.</span><span class="sxs-lookup"><span data-stu-id="74ae0-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="74ae0-126">Usando a biblioteca de saudação com hello serviço tabela</span><span class="sxs-lookup"><span data-stu-id="74ae0-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="74ae0-127">Tipos de toocommunicate usado com o serviço de tabela do Azure Olá dependem do WCF Data Services para a biblioteca de aplicativo da Windows Store hello.</span><span class="sxs-lookup"><span data-stu-id="74ae0-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="74ae0-128">Em seguida, adicione que uma referência toohello necessário bibliotecas WCF usando Olá Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="74ae0-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="74ae0-130">Use Olá após o comando toopoint toohello Gerenciador de pacote local no seu computador:</span><span class="sxs-lookup"><span data-stu-id="74ae0-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="74ae0-131">Esse comando adicionará automaticamente o projeto de tooyour todas as referências necessárias.</span><span class="sxs-lookup"><span data-stu-id="74ae0-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="74ae0-132">Se você não quiser toouse Olá Package Manager Console, você pode adicionar pasta do WCF Data Services NuGet Olá na sua lista de toohello do computador local de origens do pacote e, em seguida, adicionar referência de saudação por meio de saudação da interface do usuário, conforme descrito em [gerenciar usando de pacotes do NuGet Olá diálogo](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="74ae0-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="74ae0-133">Quando você referenciou um pacote do NuGet do WCF Data Services hello, alterar o código de saudação do botão **clique** evento:</span><span class="sxs-lookup"><span data-stu-id="74ae0-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="74ae0-134">Esse código verifica se uma tabela nomeada *table1* existe em sua conta, criando-a se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="74ae0-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="74ae0-135">Você também pode adicionar uma referência tooMicrosoft.WindowsAzure.Storage.Table.dll, que está disponível no hello mesmo pacote que você baixou.</span><span class="sxs-lookup"><span data-stu-id="74ae0-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="74ae0-136">Essa biblioteca contém funcionalidades adicionais, como consultas genéricas e serialização com base em reflexão.</span><span class="sxs-lookup"><span data-stu-id="74ae0-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="74ae0-137">Observe que essa biblioteca não dá suporte a JavaScript.</span><span class="sxs-lookup"><span data-stu-id="74ae0-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
