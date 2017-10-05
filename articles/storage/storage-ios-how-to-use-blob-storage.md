---
title: Como usar o Armazenamento de Blobs do Azure no iOS | Microsoft Docs
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: cb2810636c8c23dbd476dc2adf58b17d1887d575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="2b89e-103">Como usar o armazenamento de Blob no iOS</span><span class="sxs-lookup"><span data-stu-id="2b89e-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2b89e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2b89e-104">Overview</span></span>
<span data-ttu-id="2b89e-105">Este artigo mostra como executar cenários comuns usando o armazenamento de Blob do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b89e-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="2b89e-106">Os exemplos são escritos em Objective-C e usam a [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios)(Biblioteca do Cliente de Armazenamento do Azure para iOS).</span><span class="sxs-lookup"><span data-stu-id="2b89e-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="2b89e-107">Os cenários abrangidos incluem **carregamento**, **listagem**, **download** e **exclusão** de blobs.</span><span class="sxs-lookup"><span data-stu-id="2b89e-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="2b89e-108">Para obter mais informações sobre blobs, consulte a seção [Próximas etapas](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="2b89e-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="2b89e-109">Você também pode baixar o [aplicativo de exemplo](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) para ver rapidamente o uso do Armazenamento do Azure em um aplicativo do iOS.</span><span class="sxs-lookup"><span data-stu-id="2b89e-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="2b89e-110">Importar a biblioteca do iOS de Armazenamento do Azure para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b89e-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="2b89e-111">Você pode importar a biblioteca do iOS de Armazenamento do Azure para seu aplicativo usando o [CocoaPod para Armazenamento do Azure](https://cocoapods.org/pods/AZSClient) ou importando o arquivo **Framework** .</span><span class="sxs-lookup"><span data-stu-id="2b89e-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span> <span data-ttu-id="2b89e-112">O CocoaPod é a maneira recomendada, pois ele facilita a integração à biblioteca, enquanto a importação do arquivo de estrutura é menos intrusiva para seu projeto existente.</span><span class="sxs-lookup"><span data-stu-id="2b89e-112">CocoaPod is the recommended way as it makes integrating the library easier, however importing from the framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="2b89e-113">Para usar essa biblioteca, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="2b89e-113">To use this library, you need the following:</span></span>
- <span data-ttu-id="2b89e-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="2b89e-114">iOS 8+</span></span>
- <span data-ttu-id="2b89e-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="2b89e-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="2b89e-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="2b89e-116">CocoaPod</span></span>
1. <span data-ttu-id="2b89e-117">Se você ainda não fez isso, [instale os CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) em seu computador abrindo uma janela de terminal e executando o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="2b89e-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="2b89e-118">Em seguida, no diretório do projeto (o diretório que contém o arquivo .xcodeproj), crie um novo arquivo chamado _Podfile_ (sem extensão de arquivo).</span><span class="sxs-lookup"><span data-stu-id="2b89e-118">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="2b89e-119">Adicione o seguinte a _Podfile_ e salve.</span><span class="sxs-lookup"><span data-stu-id="2b89e-119">Add the following to _Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="2b89e-120">Na janela do terminal, navegue até o diretório do projeto e execute o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="2b89e-120">In the terminal window, navigate to the project directory and run the following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="2b89e-121">Se o seu .xcodeproj estiver aberto no Xcode, feche-o.</span><span class="sxs-lookup"><span data-stu-id="2b89e-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="2b89e-122">No diretório do projeto, abra o arquivo de projeto recém-criado que terá a extensão .xcworkspace.</span><span class="sxs-lookup"><span data-stu-id="2b89e-122">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="2b89e-123">Esse é o arquivo no qual você trabalhará a partir de agora.</span><span class="sxs-lookup"><span data-stu-id="2b89e-123">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="2b89e-124">Framework</span><span class="sxs-lookup"><span data-stu-id="2b89e-124">Framework</span></span>
<span data-ttu-id="2b89e-125">A outra maneira de usar a biblioteca é criar a estrutura manualmente:</span><span class="sxs-lookup"><span data-stu-id="2b89e-125">The other way to use the library is to build the framework manually:</span></span>

1. <span data-ttu-id="2b89e-126">Primeiro, baixe ou clone o [repositório azure-storage-ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="2b89e-126">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="2b89e-127">Vá para *azure-storage-ios* -> *Lib* -> *Biblioteca de cliente de Armazenamento do Azure* e abra `AZSClient.xcodeproj` no Xcode.</span><span class="sxs-lookup"><span data-stu-id="2b89e-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="2b89e-128">No canto superior esquerdo do Xcode, altere o esquema ativo de "Biblioteca de Cliente de Armazenamento do Azure" para "Estrutura".</span><span class="sxs-lookup"><span data-stu-id="2b89e-128">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="2b89e-129">Compile o projeto (⌘+B).</span><span class="sxs-lookup"><span data-stu-id="2b89e-129">Build the project (⌘+B).</span></span> <span data-ttu-id="2b89e-130">Isso criará um arquivo `AZSClient.framework` na Área de Trabalho.</span><span class="sxs-lookup"><span data-stu-id="2b89e-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="2b89e-131">Você pode importar o arquivo de estrutura em seu aplicativo fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2b89e-131">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="2b89e-132">Crie um novo projeto ou abra um projeto existente no Xcode.</span><span class="sxs-lookup"><span data-stu-id="2b89e-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="2b89e-133">Arraste e solte o `AZSClient.framework` em seu navegador de projeto Xcode.</span><span class="sxs-lookup"><span data-stu-id="2b89e-133">Drag and drop the `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="2b89e-134">Selecione *Copiar itens se necessário* e clique em *Concluir*.</span><span class="sxs-lookup"><span data-stu-id="2b89e-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="2b89e-135">Clique no projeto no painel de navegação esquerdo e clique na guia *Geral* na parte superior do editor de projeto.</span><span class="sxs-lookup"><span data-stu-id="2b89e-135">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
5. <span data-ttu-id="2b89e-136">Na seção *Estruturas e Bibliotecas Vinculadas* , clique no botão Adicionar (+).</span><span class="sxs-lookup"><span data-stu-id="2b89e-136">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
6. <span data-ttu-id="2b89e-137">Na lista de bibliotecas já fornecida, pesquise `libxml2.2.tbd` e adicione-a ao projeto.</span><span class="sxs-lookup"><span data-stu-id="2b89e-137">In the list of libraries already provided, search for `libxml2.2.tbd` and add it to your project.</span></span>

## <a name="import-the-library"></a><span data-ttu-id="2b89e-138">Importar a Biblioteca</span><span class="sxs-lookup"><span data-stu-id="2b89e-138">Import the Library</span></span> 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="2b89e-139">Se você estiver usando Swift, você precisará criar um cabeçalho ponte e importar <AZSClient/AZSClient.h> para lá:</span><span class="sxs-lookup"><span data-stu-id="2b89e-139">If you are using Swift, you will need to create a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="2b89e-140">Crie um arquivo de cabeçalho `Bridging-Header.h` e adicione a instrução de importação acima.</span><span class="sxs-lookup"><span data-stu-id="2b89e-140">Create a header file `Bridging-Header.h`, and add the above import statement.</span></span>
2. <span data-ttu-id="2b89e-141">Vá para a guia *Configurações de Build* e pesquise por *Cabeçalho Ponte do Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="2b89e-141">Go to the *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="2b89e-142">Clique duas vezes no campo de *Cabeçalho Ponte do Objective-C* e adicione o caminho para o arquivo de cabeçalho:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="2b89e-142">Double-click on the field of *Objective-C Bridging Header* and add the path to your header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="2b89e-143">Compile o projeto (⌘+B) para verificar se o cabeçalho de ponte foi recebido pelo Xcode.</span><span class="sxs-lookup"><span data-stu-id="2b89e-143">Build the project (⌘+B) to verify that the bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="2b89e-144">Comece a usar a biblioteca diretamente em qualquer arquivo Swift, instruções de importação não são necessárias.</span><span class="sxs-lookup"><span data-stu-id="2b89e-144">Start using the library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="2b89e-145">Operações assíncronas</span><span class="sxs-lookup"><span data-stu-id="2b89e-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="2b89e-146">Todos os métodos que realizam uma solicitação ao serviço são operações assíncronas.</span><span class="sxs-lookup"><span data-stu-id="2b89e-146">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="2b89e-147">Nos exemplos de código, você verá que esses métodos têm um manipulador de conclusão.</span><span class="sxs-lookup"><span data-stu-id="2b89e-147">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="2b89e-148">O código no manipulador de conclusão será executado **após** a solicitação ser concluída.</span><span class="sxs-lookup"><span data-stu-id="2b89e-148">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="2b89e-149">O código depois do manipulador de conclusão será executado **enquanto** a solicitação está sendo feita.</span><span class="sxs-lookup"><span data-stu-id="2b89e-149">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="2b89e-150">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="2b89e-150">Create a container</span></span>
<span data-ttu-id="2b89e-151">Todos os blobs no Armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="2b89e-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="2b89e-152">O exemplo a seguir mostra como criar um contêiner, chamado *newcontainer*, em sua Conta de armazenamento, se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="2b89e-152">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="2b89e-153">Ao escolher um nome para o contêiner, leve em conta as regras de nomenclatura mencionadas acima.</span><span class="sxs-lookup"><span data-stu-id="2b89e-153">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="2b89e-154">Você pode confirmar que isso funciona observando o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com) e verificando se *newcontainer* está na lista de contêineres para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2b89e-154">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="2b89e-155">Definir permissões de contêiner</span><span class="sxs-lookup"><span data-stu-id="2b89e-155">Set Container Permissions</span></span>
<span data-ttu-id="2b89e-156">As permissões do contêiner são configuradas para acesso **privado** por padrão.</span><span class="sxs-lookup"><span data-stu-id="2b89e-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="2b89e-157">No entanto, os contêineres fornecem algumas opções diferentes para acesso ao contêiner:</span><span class="sxs-lookup"><span data-stu-id="2b89e-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="2b89e-158">**Privado**: os dados de contêiner e blob podem ser lidos apenas pelo proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="2b89e-158">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="2b89e-159">**Blob**: os dados do blob nesse contêiner podem ser lidos por meio de solicitação anônima, mas os dados do contêiner não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2b89e-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="2b89e-160">Os clientes não podem enumerar os blobs no contêiner por meio de uma solicitação anônima.</span><span class="sxs-lookup"><span data-stu-id="2b89e-160">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="2b89e-161">**Contêiner**: os dados do contêiner e do blob podem ser lidos por solicitação anônima.</span><span class="sxs-lookup"><span data-stu-id="2b89e-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="2b89e-162">Os clientes podem enumerar os blobs no contêiner por meio de uma solicitação anônima, mas não podem enumerar os contêineres em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2b89e-162">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="2b89e-163">O exemplo a seguir mostra como criar um contêiner com permissões de acesso de **Contêiner** que permitirão o acesso público e somente leitura para todos os usuários na Internet:</span><span class="sxs-lookup"><span data-stu-id="2b89e-163">The following example shows you how to create a container with **Container** access permissions, which will allow public, read-only access for all users on the Internet:</span></span>

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2b89e-164">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="2b89e-164">Upload a blob into a container</span></span>
<span data-ttu-id="2b89e-165">Conforme mencionado na seção [Conceitos do serviço de Blob](#blob-service-concepts) , o Armazenamento de Blob oferece três tipos diferentes de blobs: blobs de bloco, blobs de acréscimo e blobs de página.</span><span class="sxs-lookup"><span data-stu-id="2b89e-165">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="2b89e-166">A biblioteca do iOS de armazenamento do Azure dá suporte a todos os três tipos de blobs.</span><span class="sxs-lookup"><span data-stu-id="2b89e-166">The Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="2b89e-167">Na maioria dos casos, o blob de blocos é o tipo recomendado.</span><span class="sxs-lookup"><span data-stu-id="2b89e-167">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="2b89e-168">O exemplo a seguir mostra como carregar um blob de bloco de um NSString.</span><span class="sxs-lookup"><span data-stu-id="2b89e-168">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="2b89e-169">Se um blob com o mesmo nome já existir no contêiner, o conteúdo desse blob será substituído.</span><span class="sxs-lookup"><span data-stu-id="2b89e-169">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="2b89e-170">Você pode confirmar que isso funciona observando o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com) e verificando se o contêiner *containerpublic*, contém o blob *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="2b89e-170">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="2b89e-171">Neste exemplo, usamos um contêiner público, de modo que você também pode verificar se esse aplicativo funcionou indo para o URI de blobs:</span><span class="sxs-lookup"><span data-stu-id="2b89e-171">In this sample, we used a public container so you can also verify that this application worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="2b89e-172">Além de carregar um blob de blocos de um NSString, existem métodos semelhantes para NSData, NSInputStream ou um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="2b89e-172">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="2b89e-173">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="2b89e-173">List the blobs in a container</span></span>
<span data-ttu-id="2b89e-174">O exemplo a seguir mostra como listar todos os blobs em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="2b89e-174">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="2b89e-175">Ao executar essa operação, leve em conta os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2b89e-175">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="2b89e-176">**continuationToken** - O token de continuação representa onde a operação de listagem deve começar.</span><span class="sxs-lookup"><span data-stu-id="2b89e-176">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="2b89e-177">Se nenhum token for fornecido, ele listará os blobs desde o início.</span><span class="sxs-lookup"><span data-stu-id="2b89e-177">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="2b89e-178">Qualquer número de blobs pode ser listado, desde zero até um máximo definido.</span><span class="sxs-lookup"><span data-stu-id="2b89e-178">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="2b89e-179">Mesmo que esse método retorne zero resultado, se `results.continuationToken` não for nulo, poderá haver mais blobs no serviço que não foram listados.</span><span class="sxs-lookup"><span data-stu-id="2b89e-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="2b89e-180">**prefixo** -Você pode especificar o prefixo a ser usado para a listagem de blobs.</span><span class="sxs-lookup"><span data-stu-id="2b89e-180">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="2b89e-181">Somente os blobs que começarem com esse prefixo serão listados.</span><span class="sxs-lookup"><span data-stu-id="2b89e-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="2b89e-182">**useFlatBlobListing** – conforme mencionado na seção [Nomeando e referenciando contêineres e blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata), embora o serviço Blob seja um esquema de armazenamento simples, você pode criar uma hierarquia virtual nomeando blobs com informações de caminho.</span><span class="sxs-lookup"><span data-stu-id="2b89e-182">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="2b89e-183">No entanto, atualmente não há suporte para listagem não plana.</span><span class="sxs-lookup"><span data-stu-id="2b89e-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="2b89e-184">Este recurso estará disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="2b89e-184">This feature is coming soon.</span></span> <span data-ttu-id="2b89e-185">Por enquanto, esse valor deve ser **YES**.</span><span class="sxs-lookup"><span data-stu-id="2b89e-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="2b89e-186">**blobListingDetails** - Você pode especificar os itens a serem incluídos ao listar blobs</span><span class="sxs-lookup"><span data-stu-id="2b89e-186">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="2b89e-187">_AZSBlobListingDetailsNone_: lista apenas os blobs confirmados e não retorna os metadados dos blobs.</span><span class="sxs-lookup"><span data-stu-id="2b89e-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="2b89e-188">_AZSBlobListingDetailsSnapshots_: lista os blobs confirmados e os instantâneos dos blobs.</span><span class="sxs-lookup"><span data-stu-id="2b89e-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="2b89e-189">_AZSBlobListingDetailsMetadata_: recupera os metadados dos blobs de cada blob retornado na listagem.</span><span class="sxs-lookup"><span data-stu-id="2b89e-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="2b89e-190">_AZSBlobListingDetailsUncommittedBlobs_: lista os blobs confirmados e não confirmados.</span><span class="sxs-lookup"><span data-stu-id="2b89e-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="2b89e-191">_AZSBlobListingDetailsCopy_: inclui propriedades de cópia na listagem.</span><span class="sxs-lookup"><span data-stu-id="2b89e-191">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="2b89e-192">_AZSBlobListingDetailsAll_: lista todos os blobs confirmados disponíveis, os blobs não confirmados e os instantâneos e retorna todos os metadados e status de cópia dos blobs.</span><span class="sxs-lookup"><span data-stu-id="2b89e-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="2b89e-193">**maxResults** - O número máximo de resultados a serem retornados para a operação.</span><span class="sxs-lookup"><span data-stu-id="2b89e-193">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="2b89e-194">Use -1 para não definir um limite.</span><span class="sxs-lookup"><span data-stu-id="2b89e-194">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="2b89e-195">**completionHandler** - O bloco de código a ser executado com os resultados da operação de listagem.</span><span class="sxs-lookup"><span data-stu-id="2b89e-195">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="2b89e-196">Neste exemplo, um método auxiliar é usado para chamar recursivamente o método de listagem de blobs sempre que um token de continuação é retornado.</span><span class="sxs-lookup"><span data-stu-id="2b89e-196">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a><span data-ttu-id="2b89e-197">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="2b89e-197">Download a blob</span></span>
<span data-ttu-id="2b89e-198">O exemplo a seguir mostra como baixar um blob para um objeto NSString.</span><span class="sxs-lookup"><span data-stu-id="2b89e-198">The following example shows how to download a blob to a NSString object.</span></span>

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="2b89e-199">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="2b89e-199">Delete a blob</span></span>
<span data-ttu-id="2b89e-200">O exemplo a seguir mostra como excluir um blob.</span><span class="sxs-lookup"><span data-stu-id="2b89e-200">The following example shows how to delete a blob.</span></span>

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="2b89e-201">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="2b89e-201">Delete a blob container</span></span>
<span data-ttu-id="2b89e-202">O exemplo a seguir mostra como excluir um contêiner.</span><span class="sxs-lookup"><span data-stu-id="2b89e-202">The following example shows how to delete a container.</span></span>

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a><span data-ttu-id="2b89e-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b89e-203">Next steps</span></span>
<span data-ttu-id="2b89e-204">Agora que você aprendeu como usar o Armazenamento de Blobs do iOS, siga esses links para saber mais sobre a biblioteca do iOS e o serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2b89e-204">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="2b89e-205">Biblioteca de Cliente do Armazenamento do Azure para iOS</span><span class="sxs-lookup"><span data-stu-id="2b89e-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="2b89e-206">Documentação de referência do iOS do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2b89e-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="2b89e-207">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2b89e-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="2b89e-208">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2b89e-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="2b89e-209">Se você tiver dúvidas sobre a biblioteca, fique à vontade para postar em nosso [Fórum do Azure do MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) ou no [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="2b89e-209">If you have questions regarding this library, feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="2b89e-210">Se você tiver sugestões de recursos para o Armazenamento do Azure, poste nos [Comentários do Armazenamento do Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="2b89e-210">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

