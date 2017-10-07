---
title: aaaHow toouse armazenamento de BLOBs do Azure do iOS | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="078e0-103">Como toouse armazenamento de Blob do iOS</span><span class="sxs-lookup"><span data-stu-id="078e0-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="078e0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="078e0-104">Overview</span></span>
<span data-ttu-id="078e0-105">Este artigo mostra como tooperform cenários comuns de usar o armazenamento de BLOBs do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="078e0-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="078e0-106">exemplos de Hello são escritos em Objective-C e usar Olá [biblioteca de cliente de armazenamento do Azure para iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="078e0-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="078e0-107">Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs.</span><span class="sxs-lookup"><span data-stu-id="078e0-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="078e0-108">Para obter mais informações sobre blobs, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="078e0-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="078e0-109">Você também pode baixar Olá [aplicativo de exemplo](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly consulte Olá o uso do armazenamento do Azure em um aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="078e0-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="078e0-110">Importar biblioteca de iOS Olá armazenamento do Azure para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="078e0-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="078e0-111">Você pode importar biblioteca de iOS Olá armazenamento do Azure para seu aplicativo usando Olá [CocoaPod de armazenamento do Azure](https://cocoapods.org/pods/AZSClient) ou importando Olá **Framework** arquivo.</span><span class="sxs-lookup"><span data-stu-id="078e0-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="078e0-112">CocoaPod é hello maneira é recomendada, pois ele facilita biblioteca de integração hello, porém importar do arquivo de estrutura de saudação é menos intrusiva para seu projeto existente.</span><span class="sxs-lookup"><span data-stu-id="078e0-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="078e0-113">toouse nessa biblioteca, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="078e0-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="078e0-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="078e0-114">iOS 8+</span></span>
- <span data-ttu-id="078e0-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="078e0-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="078e0-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="078e0-116">CocoaPod</span></span>
1. <span data-ttu-id="078e0-117">Se você ainda não fez isso, [CocoaPods instalar](https://guides.cocoapods.org/using/getting-started.html#toc_3) em seu computador abrindo uma janela do terminal e executando o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="078e0-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="078e0-118">Em seguida, no diretório do projeto hello (diretório de saudação que contém o arquivo .xcodeproj), crie um novo arquivo chamado _Podfile_(extensão de arquivo).</span><span class="sxs-lookup"><span data-stu-id="078e0-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="078e0-119">Adicionar Olá too_Podfile_ a seguir e salve.</span><span class="sxs-lookup"><span data-stu-id="078e0-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="078e0-120">Na janela do terminal hello, navegar toohello diretório de projeto e execução hello comando a seguir</span><span class="sxs-lookup"><span data-stu-id="078e0-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="078e0-121">Se o seu .xcodeproj estiver aberto no Xcode, feche-o.</span><span class="sxs-lookup"><span data-stu-id="078e0-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="078e0-122">O arquivo de projeto do projeto diretório aberto Olá recém-criado que terão extensão de .xcworkspace Olá.</span><span class="sxs-lookup"><span data-stu-id="078e0-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="078e0-123">Este é o arquivo de saudação em que você trabalhará partir de agora.</span><span class="sxs-lookup"><span data-stu-id="078e0-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="078e0-124">Framework</span><span class="sxs-lookup"><span data-stu-id="078e0-124">Framework</span></span>
<span data-ttu-id="078e0-125">Olá outra maneira de biblioteca de saudação toouse é a estrutura de saudação de toobuild manualmente:</span><span class="sxs-lookup"><span data-stu-id="078e0-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="078e0-126">Primeiro, o download ou o clone hello [ios de armazenamento do azure repositório](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="078e0-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="078e0-127">Vá para *azure-storage-ios* -> *Lib* -> *Biblioteca de cliente de Armazenamento do Azure* e abra `AZSClient.xcodeproj` no Xcode.</span><span class="sxs-lookup"><span data-stu-id="078e0-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="078e0-128">Em Olá superior esquerdo do Xcode, alteração Olá active esquema de "Biblioteca de cliente de armazenamento do Azure" muito "Estrutura".</span><span class="sxs-lookup"><span data-stu-id="078e0-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="078e0-129">Compile o projeto de saudação (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="078e0-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="078e0-130">Isso criará um arquivo `AZSClient.framework` na Área de Trabalho.</span><span class="sxs-lookup"><span data-stu-id="078e0-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="078e0-131">Você pode importar de arquivo hello framework em seu aplicativo hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="078e0-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="078e0-132">Crie um novo projeto ou abra um projeto existente no Xcode.</span><span class="sxs-lookup"><span data-stu-id="078e0-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="078e0-133">Saudação de arrastar e soltar `AZSClient.framework` em seu navegador de projeto Xcode.</span><span class="sxs-lookup"><span data-stu-id="078e0-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="078e0-134">Selecione *Copiar itens se necessário* e clique em *Concluir*.</span><span class="sxs-lookup"><span data-stu-id="078e0-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="078e0-135">Clique no seu projeto na navegação esquerda hello e clique em Olá *geral* guia na parte superior de saudação do editor de saudação do projeto.</span><span class="sxs-lookup"><span data-stu-id="078e0-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="078e0-136">Em Olá *estruturas e bibliotecas vinculadas* seção, clique no botão Adicionar de saudação (+).</span><span class="sxs-lookup"><span data-stu-id="078e0-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="078e0-137">Na lista de saudação de bibliotecas já fornecido, procure `libxml2.2.tbd` e adicioná-lo tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="078e0-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="078e0-138">Olá Importar biblioteca</span><span class="sxs-lookup"><span data-stu-id="078e0-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="078e0-139">Se você estiver usando Swift, será necessário toocreate um cabeçalho de ponte e importar < AZSClient/AZSClient.h > existe:</span><span class="sxs-lookup"><span data-stu-id="078e0-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="078e0-140">Criar um arquivo de cabeçalho `Bridging-Header.h`e adicione Olá acima da declaração de importação.</span><span class="sxs-lookup"><span data-stu-id="078e0-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="078e0-141">Vá toohello *configurações da compilação* guia e procure *cabeçalho de ponte Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="078e0-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="078e0-142">Clique duas vezes no campo de saudação do *cabeçalho de ponte Objective-C* e adicione o arquivo de cabeçalho de tooyour Olá caminho:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="078e0-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="078e0-143">Compilação Olá projeto (⌘ + B) tooverify que Olá cabeçalho ponte foi recebida pelo Xcode.</span><span class="sxs-lookup"><span data-stu-id="078e0-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="078e0-144">Começar a usar a biblioteca Olá diretamente em qualquer arquivo Swift, não é necessário para instruções de importação.</span><span class="sxs-lookup"><span data-stu-id="078e0-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="078e0-145">Operações assíncronas</span><span class="sxs-lookup"><span data-stu-id="078e0-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="078e0-146">Todos os métodos que realizam uma solicitação no serviço de saudação são operações assíncronas.</span><span class="sxs-lookup"><span data-stu-id="078e0-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="078e0-147">Exemplos de código hello, você encontrará esses métodos têm um processador de conclusão.</span><span class="sxs-lookup"><span data-stu-id="078e0-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="078e0-148">Código de manipulador de conclusão Olá executará **depois** Olá solicitação é concluída.</span><span class="sxs-lookup"><span data-stu-id="078e0-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="078e0-149">Depois que o processador de conclusão Olá será executado de código **enquanto** Olá solicitação está sendo feita.</span><span class="sxs-lookup"><span data-stu-id="078e0-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="078e0-150">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="078e0-150">Create a container</span></span>
<span data-ttu-id="078e0-151">Todos os blobs no Armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="078e0-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="078e0-152">Olá exemplo a seguir mostra como toocreate um contêiner chamado *newcontainer*, em sua conta de armazenamento, se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="078e0-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="078e0-153">Ao escolher um nome para o contêiner, estar atento a saudação mencionadas acima de regras de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="078e0-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

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

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="078e0-154">Você pode confirmar que isso funciona, observando Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verificar se *newcontainer* está na lista de saudação de contêineres para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="078e0-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="078e0-155">Definir permissões de contêiner</span><span class="sxs-lookup"><span data-stu-id="078e0-155">Set Container Permissions</span></span>
<span data-ttu-id="078e0-156">As permissões do contêiner são configuradas para acesso **privado** por padrão.</span><span class="sxs-lookup"><span data-stu-id="078e0-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="078e0-157">No entanto, os contêineres fornecem algumas opções diferentes para acesso ao contêiner:</span><span class="sxs-lookup"><span data-stu-id="078e0-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="078e0-158">**Privada**: dados de contêiner e blob podem ser lidos pelo proprietário da conta Olá somente.</span><span class="sxs-lookup"><span data-stu-id="078e0-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="078e0-159">**Blob**: os dados do blob nesse contêiner podem ser lidos por meio de solicitação anônima, mas os dados do contêiner não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="078e0-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="078e0-160">Os clientes não podem enumerar blobs no contêiner Olá por solicitação anônima.</span><span class="sxs-lookup"><span data-stu-id="078e0-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="078e0-161">**Contêiner**: os dados do contêiner e do blob podem ser lidos por solicitação anônima.</span><span class="sxs-lookup"><span data-stu-id="078e0-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="078e0-162">Os clientes podem enumerar blobs dentro do contêiner de saudação por solicitação anônima, mas não é possível enumerar os contêineres na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="078e0-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="078e0-163">Olá exemplo a seguir mostra como toocreate um contêiner com **contêiner** acessar permissões, que permitem o acesso público, somente leitura para todos os usuários Olá Internet:</span><span class="sxs-lookup"><span data-stu-id="078e0-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

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

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="078e0-164">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="078e0-164">Upload a blob into a container</span></span>
<span data-ttu-id="078e0-165">Conforme mencionado em Olá [conceitos do serviço de Blob](#blob-service-concepts) seção, o armazenamento de Blob oferece três tipos diferentes de blobs: blobs de blocos, blobs de acréscimo e blobs de página.</span><span class="sxs-lookup"><span data-stu-id="078e0-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="078e0-166">biblioteca de iOS do armazenamento do Azure Olá dá suporte a todos os três tipos de blobs.</span><span class="sxs-lookup"><span data-stu-id="078e0-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="078e0-167">Na maioria dos casos, o blob de blocos é hello recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="078e0-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="078e0-168">saudação de exemplo a seguir mostra como tooupload um bloco de blob de um NSString.</span><span class="sxs-lookup"><span data-stu-id="078e0-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="078e0-169">Se um blob com o mesmo nome já existe neste recipiente de hello, conteúdo de saudação desse blob será substituído.</span><span class="sxs-lookup"><span data-stu-id="078e0-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

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

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="078e0-170">Você pode confirmar que isso funciona, observando Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verificar o contêiner hello, *containerpublic*, contém o blob hello, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="078e0-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="078e0-171">Neste exemplo, usamos um contêiner público, então você também pode verificar se este aplicativo trabalhou vai toohello blobs URI:</span><span class="sxs-lookup"><span data-stu-id="078e0-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="078e0-172">Além disso toouploading um blob de bloco de um NSString, existem métodos semelhantes para NSData, NSInputStream ou um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="078e0-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="078e0-173">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="078e0-173">List hello blobs in a container</span></span>
<span data-ttu-id="078e0-174">Olá exemplo a seguir mostra como toolist todos os blobs em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="078e0-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="078e0-175">Ao executar esta operação, estar atento a saudação parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="078e0-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="078e0-176">**continuationToken** -Olá representa token de continuação onde começar Olá operação de listagem.</span><span class="sxs-lookup"><span data-stu-id="078e0-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="078e0-177">Se nenhum token for fornecido, ele irá listar blobs desde o início de saudação.</span><span class="sxs-lookup"><span data-stu-id="078e0-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="078e0-178">Qualquer número de blobs pode ser listado, de tooa definir máximo de zero.</span><span class="sxs-lookup"><span data-stu-id="078e0-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="078e0-179">Mesmo se esse método retornar zero resultados, se `results.continuationToken` não for nulo, pode haver mais blobs no serviço de saudação que não foram listados.</span><span class="sxs-lookup"><span data-stu-id="078e0-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="078e0-180">**prefixo** -você pode especificar Olá prefixo toouse listagem do blob.</span><span class="sxs-lookup"><span data-stu-id="078e0-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="078e0-181">Somente os blobs que começarem com esse prefixo serão listados.</span><span class="sxs-lookup"><span data-stu-id="078e0-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="078e0-182">**useFlatBlobListing** - conforme mencionado em Olá [nomeando e referenciando contêineres e blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) seção, embora Olá serviço Blob é um esquema de armazenamento simples, você pode criar uma hierarquia virtual nomeando blobs com caminho informações.</span><span class="sxs-lookup"><span data-stu-id="078e0-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="078e0-183">No entanto, atualmente não há suporte para listagem não plana.</span><span class="sxs-lookup"><span data-stu-id="078e0-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="078e0-184">Este recurso estará disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="078e0-184">This feature is coming soon.</span></span> <span data-ttu-id="078e0-185">Por enquanto, esse valor deve ser **YES**.</span><span class="sxs-lookup"><span data-stu-id="078e0-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="078e0-186">**blobListingDetails** -você pode especificar quais itens tooinclude ao listar blobs</span><span class="sxs-lookup"><span data-stu-id="078e0-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="078e0-187">_AZSBlobListingDetailsNone_: lista apenas os blobs confirmados e não retorna os metadados dos blobs.</span><span class="sxs-lookup"><span data-stu-id="078e0-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="078e0-188">_AZSBlobListingDetailsSnapshots_: lista os blobs confirmados e os instantâneos dos blobs.</span><span class="sxs-lookup"><span data-stu-id="078e0-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="078e0-189">_AZSBlobListingDetailsMetadata_: recupera metadados de blob para cada blob retornado na listagem hello.</span><span class="sxs-lookup"><span data-stu-id="078e0-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="078e0-190">_AZSBlobListingDetailsUncommittedBlobs_: lista os blobs confirmados e não confirmados.</span><span class="sxs-lookup"><span data-stu-id="078e0-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="078e0-191">_AZSBlobListingDetailsCopy_: incluem copiar propriedades na listagem hello.</span><span class="sxs-lookup"><span data-stu-id="078e0-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="078e0-192">_AZSBlobListingDetailsAll_: lista todos os blobs confirmados disponíveis, os blobs não confirmados e os instantâneos e retorna todos os metadados e status de cópia dos blobs.</span><span class="sxs-lookup"><span data-stu-id="078e0-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="078e0-193">**maxResults** -Olá número máximo de resultados tooreturn para esta operação.</span><span class="sxs-lookup"><span data-stu-id="078e0-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="078e0-194">Use -1 toonot define um limite.</span><span class="sxs-lookup"><span data-stu-id="078e0-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="078e0-195">**completionHandler** -bloco de saudação do código tooexecute com resultados Olá Olá operação de listagem.</span><span class="sxs-lookup"><span data-stu-id="078e0-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="078e0-196">Neste exemplo, um método auxiliar é usado toorecursively chamada hello lista blobs método toda vez que um token de continuação será retornado.</span><span class="sxs-lookup"><span data-stu-id="078e0-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="078e0-197">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="078e0-197">Download a blob</span></span>
<span data-ttu-id="078e0-198">Olá mostrado no exemplo a seguir como toodownload um objeto de NSString tooa blob.</span><span class="sxs-lookup"><span data-stu-id="078e0-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="078e0-199">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="078e0-199">Delete a blob</span></span>
<span data-ttu-id="078e0-200">Olá mostrado no exemplo a seguir como toodelete um blob.</span><span class="sxs-lookup"><span data-stu-id="078e0-200">hello following example shows how toodelete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="078e0-201">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="078e0-201">Delete a blob container</span></span>
<span data-ttu-id="078e0-202">Olá mostrado no exemplo a seguir como toodelete um contêiner.</span><span class="sxs-lookup"><span data-stu-id="078e0-202">hello following example shows how toodelete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="078e0-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="078e0-203">Next steps</span></span>
<span data-ttu-id="078e0-204">Agora que você aprendeu como toouse armazenamento de Blob do iOS, siga essas toolearn links mais informações sobre a biblioteca de iOS hello e Olá o serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="078e0-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="078e0-205">Biblioteca de Cliente do Armazenamento do Azure para iOS</span><span class="sxs-lookup"><span data-stu-id="078e0-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="078e0-206">Documentação de referência do iOS do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="078e0-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="078e0-207">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="078e0-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="078e0-208">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="078e0-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="078e0-209">Se você tiver dúvidas sobre essa biblioteca, sinta-se livre toopost tooour [Fórum do MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) ou [estouro de pilha](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="078e0-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="078e0-210">Se você tiver sugestões de recursos de armazenamento do Azure, poste muito[comentários de armazenamento do Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="078e0-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

