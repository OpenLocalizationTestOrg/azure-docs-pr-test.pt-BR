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
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>Como toouse armazenamento de Blob do iOS
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Este artigo mostra como tooperform cenários comuns de usar o armazenamento de BLOBs do Microsoft Azure. exemplos de Hello são escritos em Objective-C e usar Olá [biblioteca de cliente de armazenamento do Azure para iOS](https://github.com/Azure/azure-storage-ios). Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs. Para obter mais informações sobre blobs, consulte Olá [próximas etapas](#next-steps) seção. Você também pode baixar Olá [aplicativo de exemplo](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly consulte Olá o uso do armazenamento do Azure em um aplicativo iOS.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Importar biblioteca de iOS Olá armazenamento do Azure para seu aplicativo
Você pode importar biblioteca de iOS Olá armazenamento do Azure para seu aplicativo usando Olá [CocoaPod de armazenamento do Azure](https://cocoapods.org/pods/AZSClient) ou importando Olá **Framework** arquivo. CocoaPod é hello maneira é recomendada, pois ele facilita biblioteca de integração hello, porém importar do arquivo de estrutura de saudação é menos intrusiva para seu projeto existente.

toouse nessa biblioteca, você precisa Olá a seguir:
- iOS 8+
- Xcode 7+

## <a name="cocoapod"></a>CocoaPod
1. Se você ainda não fez isso, [CocoaPods instalar](https://guides.cocoapods.org/using/getting-started.html#toc_3) em seu computador abrindo uma janela do terminal e executando o comando a seguir de saudação
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Em seguida, no diretório do projeto hello (diretório de saudação que contém o arquivo .xcodeproj), crie um novo arquivo chamado _Podfile_(extensão de arquivo). Adicionar Olá too_Podfile_ a seguir e salve.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Na janela do terminal hello, navegar toohello diretório de projeto e execução hello comando a seguir

    ```shell    
    pod install
    ```

4. Se o seu .xcodeproj estiver aberto no Xcode, feche-o. O arquivo de projeto do projeto diretório aberto Olá recém-criado que terão extensão de .xcworkspace Olá. Este é o arquivo de saudação em que você trabalhará partir de agora.

## <a name="framework"></a>Framework
Olá outra maneira de biblioteca de saudação toouse é a estrutura de saudação de toobuild manualmente:

1. Primeiro, o download ou o clone hello [ios de armazenamento do azure repositório](https://github.com/azure/azure-storage-ios).
2. Vá para *azure-storage-ios* -> *Lib* -> *Biblioteca de cliente de Armazenamento do Azure* e abra `AZSClient.xcodeproj` no Xcode.
3. Em Olá superior esquerdo do Xcode, alteração Olá active esquema de "Biblioteca de cliente de armazenamento do Azure" muito "Estrutura".
4. Compile o projeto de saudação (⌘ + B). Isso criará um arquivo `AZSClient.framework` na Área de Trabalho.

Você pode importar de arquivo hello framework em seu aplicativo hello seguinte:

1. Crie um novo projeto ou abra um projeto existente no Xcode.
2. Saudação de arrastar e soltar `AZSClient.framework` em seu navegador de projeto Xcode.
3. Selecione *Copiar itens se necessário* e clique em *Concluir*.
4. Clique no seu projeto na navegação esquerda hello e clique em Olá *geral* guia na parte superior de saudação do editor de saudação do projeto.
5. Em Olá *estruturas e bibliotecas vinculadas* seção, clique no botão Adicionar de saudação (+).
6. Na lista de saudação de bibliotecas já fornecido, procure `libxml2.2.tbd` e adicioná-lo tooyour projeto.

## <a name="import-hello-library"></a>Olá Importar biblioteca 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Se você estiver usando Swift, será necessário toocreate um cabeçalho de ponte e importar < AZSClient/AZSClient.h > existe:

1. Criar um arquivo de cabeçalho `Bridging-Header.h`e adicione Olá acima da declaração de importação.
2. Vá toohello *configurações da compilação* guia e procure *cabeçalho de ponte Objective-C*.
3. Clique duas vezes no campo de saudação do *cabeçalho de ponte Objective-C* e adicione o arquivo de cabeçalho de tooyour Olá caminho:`ProjectName/Bridging-Header.h`
4. Compilação Olá projeto (⌘ + B) tooverify que Olá cabeçalho ponte foi recebida pelo Xcode.
5. Começar a usar a biblioteca Olá diretamente em qualquer arquivo Swift, não é necessário para instruções de importação.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Operações assíncronas
> [!NOTE]
> Todos os métodos que realizam uma solicitação no serviço de saudação são operações assíncronas. Exemplos de código hello, você encontrará esses métodos têm um processador de conclusão. Código de manipulador de conclusão Olá executará **depois** Olá solicitação é concluída. Depois que o processador de conclusão Olá será executado de código **enquanto** Olá solicitação está sendo feita.
> 
> 

## <a name="create-a-container"></a>Criar um contêiner
Todos os blobs no Armazenamento do Azure devem residir em um contêiner. Olá exemplo a seguir mostra como toocreate um contêiner chamado *newcontainer*, em sua conta de armazenamento, se ainda não existir. Ao escolher um nome para o contêiner, estar atento a saudação mencionadas acima de regras de nomenclatura.

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

Você pode confirmar que isso funciona, observando Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verificar se *newcontainer* está na lista de saudação de contêineres para sua conta de armazenamento.

## <a name="set-container-permissions"></a>Definir permissões de contêiner
As permissões do contêiner são configuradas para acesso **privado** por padrão. No entanto, os contêineres fornecem algumas opções diferentes para acesso ao contêiner:

* **Privada**: dados de contêiner e blob podem ser lidos pelo proprietário da conta Olá somente.
* **Blob**: os dados do blob nesse contêiner podem ser lidos por meio de solicitação anônima, mas os dados do contêiner não estão disponíveis. Os clientes não podem enumerar blobs no contêiner Olá por solicitação anônima.
* **Contêiner**: os dados do contêiner e do blob podem ser lidos por solicitação anônima. Os clientes podem enumerar blobs dentro do contêiner de saudação por solicitação anônima, mas não é possível enumerar os contêineres na conta de armazenamento hello.

Olá exemplo a seguir mostra como toocreate um contêiner com **contêiner** acessar permissões, que permitem o acesso público, somente leitura para todos os usuários Olá Internet:

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

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
Conforme mencionado em Olá [conceitos do serviço de Blob](#blob-service-concepts) seção, o armazenamento de Blob oferece três tipos diferentes de blobs: blobs de blocos, blobs de acréscimo e blobs de página. biblioteca de iOS do armazenamento do Azure Olá dá suporte a todos os três tipos de blobs. Na maioria dos casos, o blob de blocos é hello recomendado toouse de tipo.

saudação de exemplo a seguir mostra como tooupload um bloco de blob de um NSString. Se um blob com o mesmo nome já existe neste recipiente de hello, conteúdo de saudação desse blob será substituído.

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

Você pode confirmar que isso funciona, observando Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com) e verificar o contêiner hello, *containerpublic*, contém o blob hello, *sampleblob*. Neste exemplo, usamos um contêiner público, então você também pode verificar se este aplicativo trabalhou vai toohello blobs URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Além disso toouploading um blob de bloco de um NSString, existem métodos semelhantes para NSData, NSInputStream ou um arquivo local.

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
Olá exemplo a seguir mostra como toolist todos os blobs em um contêiner. Ao executar esta operação, estar atento a saudação parâmetros a seguir:     

* **continuationToken** -Olá representa token de continuação onde começar Olá operação de listagem. Se nenhum token for fornecido, ele irá listar blobs desde o início de saudação. Qualquer número de blobs pode ser listado, de tooa definir máximo de zero. Mesmo se esse método retornar zero resultados, se `results.continuationToken` não for nulo, pode haver mais blobs no serviço de saudação que não foram listados.
* **prefixo** -você pode especificar Olá prefixo toouse listagem do blob. Somente os blobs que começarem com esse prefixo serão listados.
* **useFlatBlobListing** - conforme mencionado em Olá [nomeando e referenciando contêineres e blobs](#naming-and-referencing-containers-and-blobs) seção, embora Olá serviço Blob é um esquema de armazenamento simples, você pode criar uma hierarquia virtual nomeando blobs com caminho informações. No entanto, atualmente não há suporte para listagem não plana. Este recurso estará disponível em breve. Por enquanto, esse valor deve ser **YES**.
* **blobListingDetails** -você pode especificar quais itens tooinclude ao listar blobs
  * _AZSBlobListingDetailsNone_: lista apenas os blobs confirmados e não retorna os metadados dos blobs.
  * _AZSBlobListingDetailsSnapshots_: lista os blobs confirmados e os instantâneos dos blobs.
  * _AZSBlobListingDetailsMetadata_: recupera metadados de blob para cada blob retornado na listagem hello.
  * _AZSBlobListingDetailsUncommittedBlobs_: lista os blobs confirmados e não confirmados.
  * _AZSBlobListingDetailsCopy_: incluem copiar propriedades na listagem hello.
  * _AZSBlobListingDetailsAll_: lista todos os blobs confirmados disponíveis, os blobs não confirmados e os instantâneos e retorna todos os metadados e status de cópia dos blobs.
* **maxResults** -Olá número máximo de resultados tooreturn para esta operação. Use -1 toonot define um limite.
* **completionHandler** -bloco de saudação do código tooexecute com resultados Olá Olá operação de listagem.

Neste exemplo, um método auxiliar é usado toorecursively chamada hello lista blobs método toda vez que um token de continuação será retornado.

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

## <a name="download-a-blob"></a>Baixar um blob
Olá mostrado no exemplo a seguir como toodownload um objeto de NSString tooa blob.

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

## <a name="delete-a-blob"></a>Excluir um blob
Olá mostrado no exemplo a seguir como toodelete um blob.

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

## <a name="delete-a-blob-container"></a>Excluir um contêiner de blob
Olá mostrado no exemplo a seguir como toodelete um contêiner.

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

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como toouse armazenamento de Blob do iOS, siga essas toolearn links mais informações sobre a biblioteca de iOS hello e Olá o serviço de armazenamento.

* [Biblioteca de Cliente do Armazenamento do Azure para iOS](https://github.com/azure/azure-storage-ios)
* [Documentação de referência do iOS do Armazenamento do Azure](http://azure.github.io/azure-storage-ios/)
* [API REST de serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage)

Se você tiver dúvidas sobre essa biblioteca, sinta-se livre toopost tooour [Fórum do MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) ou [estouro de pilha](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Se você tiver sugestões de recursos de armazenamento do Azure, poste muito[comentários de armazenamento do Azure](https://feedback.azure.com/forums/217298-storage/).

