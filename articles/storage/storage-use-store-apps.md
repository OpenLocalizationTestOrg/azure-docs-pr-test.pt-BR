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
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Como toouse o armazenamento do Azure em aplicativos da Windows Store
## <a name="overview"></a>Visão geral
Este guia mostra como tooget iniciada com o desenvolvimento de um aplicativo da Windows Store que usa o armazenamento do Azure.

## <a name="download-required-tools"></a>Baixar as ferramentas necessárias
* [O Visual Studio](https://www.visualstudio.com/downloads/) torna fácil toobuild, depurar, localizar, empacotar e implantar aplicativos da Windows Store. É necessário o Visual Studio 2012 ou posterior.
* Olá [biblioteca de cliente de armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage) fornece uma biblioteca de classes de tempo de execução do Windows para trabalhar com o armazenamento do Azure.
* [WCF Data Services ferramentas para aplicativos da Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) estende a experiência do hello adicionar referência de serviço com suporte de OData do lado do cliente para aplicativos da Windows Store no Visual Studio.

## <a name="develop-apps"></a>Desenvolver aplicativos
### <a name="getting-ready"></a>Preparando-se
Crie um novo projeto de aplicativo da Windows Store no Visual Studio 2012 ou posterior:

![store-apps-storage-vs-project][store-apps-storage-vs-project]

Em seguida, adicione uma referência toohello biblioteca de cliente de armazenamento do Azure clicando **referências**, clicando em **adicionar referência**e, em seguida, navegação toohello biblioteca de cliente de armazenamento para o Runtime do Windows que você download:

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>Usando a biblioteca Olá Olá Blob e serviços de fila
Neste ponto, seu aplicativo estiver pronto toocall hello Azure Blob e fila dos serviços. Adicione o seguinte Olá **usando** instruções para que os tipos de armazenamento do Azure podem ser referenciados diretamente:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Em seguida, adicione uma página de tooyour do botão. Adicionar Olá tooits de código a seguir **clique** eventos e modificar seu método de manipulador de eventos usando Olá [palavra-chave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Esse código pressupõe que você tenha duas variáveis de cadeia de caracteres, *accountName* e *accountKey*. Eles representam o nome de saudação da sua conta e hello chave conta de armazenamento que está associado essa conta.

Compilar e executar o aplicativo hello. Botão de saudação clicando em verificará se um contêiner nomeado *container1* existe em sua conta e, em seguida, crie-o se não.

### <a name="using-hello-library-with-hello-table-service"></a>Usando a biblioteca de saudação com hello serviço tabela
Tipos de toocommunicate usado com o serviço de tabela do Azure Olá dependem do WCF Data Services para a biblioteca de aplicativo da Windows Store hello. Em seguida, adicione que uma referência toohello necessário bibliotecas WCF usando Olá Package Manager Console:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

Use Olá após o comando toopoint toohello Gerenciador de pacote local no seu computador:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Esse comando adicionará automaticamente o projeto de tooyour todas as referências necessárias. Se você não quiser toouse Olá Package Manager Console, você pode adicionar pasta do WCF Data Services NuGet Olá na sua lista de toohello do computador local de origens do pacote e, em seguida, adicionar referência de saudação por meio de saudação da interface do usuário, conforme descrito em [gerenciar usando de pacotes do NuGet Olá diálogo](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Quando você referenciou um pacote do NuGet do WCF Data Services hello, alterar o código de saudação do botão **clique** evento:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Esse código verifica se uma tabela nomeada *table1* existe em sua conta, criando-a se ela não existir.

Você também pode adicionar uma referência tooMicrosoft.WindowsAzure.Storage.Table.dll, que está disponível no hello mesmo pacote que você baixou. Essa biblioteca contém funcionalidades adicionais, como consultas genéricas e serialização com base em reflexão. Observe que essa biblioteca não dá suporte a JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
