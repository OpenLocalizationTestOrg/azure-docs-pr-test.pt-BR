---
title: aaaHow toouse armazenamento de Blob do Node. js | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Como toouse armazenamento de Blob do Node. js
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Visão geral
Este artigo mostra como tooperform cenários comuns de usar o armazenamento de Blob. exemplos de saudação são gravados por meio de saudação API Node. js. cenários de saudação abordados incluem como tooupload, listar, baixar e excluir blobs.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Criar um aplicativo do Node.js
Para obter instruções sobre como toocreate um aplicativo Node. js, consulte [criar um aplicativo da web Node. js no serviço de aplicativo do Azure], [criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure] – usando o Windows PowerShell , ou [criar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix].

## <a name="configure-your-application-tooaccess-storage"></a>Configurar o armazenamento de tooaccess do aplicativo
toouse armazenamento do Azure, você precisa hello Azure Storage SDK para Node.js, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento Olá.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), toonavigate toohello pasta em que você criou seu exemplo aplicativo.
2. Tipo **npm instalar o armazenamento do azure** na janela de comando hello. A saída do comando de saudação é semelhante toohello exemplo de código a seguir.

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta, localize Olá **armazenamento do azure** pacote, que contém as bibliotecas de saudação que você precisa de armazenamento de tooaccess.

### <a name="import-hello-package"></a>Importar o pacote de saudação
Usando o bloco de notas ou outro editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello onde você pretende toouse armazenamento:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma conexão do Armazenamento do Azure
Olá módulo do Azure lerá variáveis de ambiente Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`, ou `AZURE_STORAGE_CONNECTION_STRING`, para obter informações necessárias tooconnect tooyour conta de armazenamento Azure. Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar **createBlobService**.

Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [portal do Azure](https://portal.azure.com) para um aplicativo web do Azure, consulte [usando o aplicativo web Node.js hello Azure serviço de tabela].

## <a name="create-a-container"></a>Criar um contêiner
Olá **BlobService** objeto permite que você trabalhe com contêineres e blobs. Olá código a seguir cria um **BlobService** objeto. Adicione a seguinte Olá superior de saudação do **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> Você pode acessar um blob anonimamente usando **createBlobServiceAnonymous** e fornecendo o endereço do host hello. Por exemplo, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

toocreate um novo contêiner, use **createContainerIfNotExists**. Olá, exemplo de código a seguir cria um novo contêiner denominado 'mycontainer':

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Se o contêiner de saudação for recém-criado, `result.created` é verdadeiro. Se já existir um contêiner hello, `result.created` é false. `response`contém informações sobre a operação de hello, incluindo informações de ETag Olá para o contêiner de saudação.

### <a name="container-security"></a>Segurança do contêiner
Por padrão, novos contêineres são privados e não podem ser acessados ​​anonimamente. contêiner de saudação toomake public para que você pode acessá-lo de forma anônima, você pode definir o nível de acesso do contêiner Olá muito**blob** ou **contêiner**.

* **blob** -permite acesso de leitura anônimo tooblob conteúdo e metadados nesse contêiner, mas não toocontainer metadados como listar todos os blobs dentro de um contêiner
* **contêiner** -permite acesso de leitura anônimo tooblob conteúdo e metadados, assim como metadados de contêiner

Olá exemplo de código a seguir demonstra o nível de acesso de saudação configuração muito**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

Como alternativa, você pode modificar o nível de acesso de saudação de um contêiner usando **setContainerAcl** toospecify nível de acesso de saudação. toocontainer nível de acesso para Olá exemplo alterações de código a seguir de saudação:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

Hello, resultado contém informações sobre a operação hello, incluindo Olá atual **ETag** para contêiner hello.

### <a name="filters"></a>Filtros
Você pode aplicar opcional filtragem operações toooperations executada usando **BlobService**. As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:

```nodejs
function handle (requestOptions, next)
```

Depois de fazer sua pré-processamento nas opções de solicitação hello, método hello precisa toocall "Avançar", passando um retorno de chamada com hello assinatura a seguir:

```nodejs
function (returnObject, finalCallback, next)
```

Esse retorno de chamada e após o processamento returnObject hello (resposta de saudação do servidor de toohello de solicitação de saudação), o retorno de chamada hello precisa tooeither invocar próximo se ela existe toocontinue outros filtros de processamento ou simplesmente invocar o serviço de saudação do finalCallback tooend invocação.

Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Olá seguir cria um **BlobService** objeto que usa Olá **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
Há três tipos de blobs: blob de blocos, blob de páginas e blob de anexo. Blobs de bloco permitem que você toomore com eficiência carregar dados grandes. Blobs de anexo otimizados para operações de acréscimo. Blobs de página são otimizados para operações de leitura/gravação. Para saber mais, confira [Noções básicas sobre Blobs de bloco, Blobs de acréscimo e Blobs de página](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>Blobs de bloco
blob de blocos de tooa de dados tooupload, Olá uso a seguir:

* **createBlockBlobFromLocalFile** - cria um novo blob de bloco e carrega o conteúdo de saudação de um arquivo
* **createBlockBlobFromStream** - cria um novo blob de bloco e carrega o conteúdo de saudação de um fluxo
* **createBlockBlobFromText** - cria um novo blob de bloco e carrega o conteúdo de saudação de uma cadeia de caracteres
* **createWriteStreamToBlockBlob** -fornece um blob de blocos de tooa de fluxo de gravação

Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **myblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Olá `result` retornado por esses métodos contém informações sobre a operação de saudação, como Olá **ETag** de blob de saudação.

### <a name="append-blobs"></a>Blobs de acréscimo
tooupload dados tooa novo blob de acréscimo, use o seguinte hello:

* **createAppendBlobFromLocalFile** - cria um novo blob de acréscimo e carrega o conteúdo de saudação de um arquivo
* **createAppendBlobFromStream** - cria um novo blob de acréscimo e carrega o conteúdo de saudação de um fluxo
* **createAppendBlobFromText** - cria um novo blob de acréscimo e carrega o conteúdo de saudação de uma cadeia de caracteres
* **createWriteStreamToNewAppendBlob** - cria um novo blob de acréscimo e, em seguida, fornece um tooit toowrite de fluxo

Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend um tooan de bloco existentes acrescentar blob, use Olá a seguir:

* **appendFromLocalFile** -Acrescente conteúdo de saudação do tooan arquivo existente acrescentar blob
* **appendFromStream** -Acrescente conteúdo de saudação do tooan fluxo existente acrescentar blob
* **appendFromText** -Acrescente conteúdo de saudação do tooan cadeia de caracteres existente acrescentar blob
* **appendBlockFromStream** -Acrescente conteúdo de saudação do tooan fluxo existente acrescentar blob
* **appendBlockFromText** -Acrescente conteúdo de saudação do tooan cadeia de caracteres existente acrescentar blob

> [!NOTE]
> appendFromXXX APIs fará algumas chamadas de servidor desnecessários validação do lado do cliente toofail tooavoid rápida. appendBlockFromXXX não fará isso.
>
>

Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Blobs de página
blob de páginas de tooa de dados tooupload, Olá uso a seguir:

* **createPageBlob** – cria um novo blob de páginas de um comprimento específico
* **createPageBlobFromLocalFile** - cria um novo blob de página e carrega o conteúdo de saudação de um arquivo
* **createPageBlobFromStream** - cria um novo blob de página e carrega o conteúdo de saudação de um fluxo
* **createWriteStreamToExistingPageBlob** -fornece um blob de página existente do gravação fluxo tooan
* **createWriteStreamToNewPageBlob** - cria um novo blob de página e, em seguida, fornece um tooit toowrite de fluxo

Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Blobs de página consistem em 'páginas’ de 512 bytes. Você receberá um erro ao carregar dados com um tamanho que não seja um múltiplo de 512.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
blobs de saudação toolist em um contêiner, use Olá **listBlobsSegmented** método. Se você desejar tooreturn blobs com um prefixo específico, use **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Olá `result` contém um `entries` coleção, que é uma matriz de objetos que descrevem cada blob. Se todos os blobs não podem ser retornados, Olá `result` também fornece um `continuationToken`, que pode ser usado como Olá segundo parâmetro tooretrieve entradas adicionais.

## <a name="download-blobs"></a>Baixar blobs
dados toodownload de um blob, use o seguinte Olá:

* **getBlobToLocalFile** -grava Olá toofile de conteúdo de blob
* **getBlobToStream** -grava o fluxo de tooa de conteúdo de blob Olá
* **getBlobToText** -grava o conteúdo de blob Olá tooa de cadeia de caracteres
* **createReadStream** -fornece um tooread de fluxo de blob Olá

Olá exemplo de código a seguir demonstra o uso de **getBlobToStream** conteúdo toodownload Olá Olá **myblob** blob e armazená-lo toohello **txt** arquivo usando um fluxo:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Olá `result` contém informações sobre Olá blob, incluindo **ETag** informações.

## <a name="delete-a-blob"></a>Excluir um blob
Finalmente, toodelete um blob, chame **deleteBlob**. Olá exclusões Olá blob denominado de exemplo de código a seguir **myblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Acesso simultâneo
blob de tooa toosupport acesso simultâneo de vários clientes ou várias instâncias do processo, você pode usar **ETags** ou **concessões**.

* **ETag** -fornece um toodetect de forma que Olá contêiner ou blob foi modificado por outro processo
* **Concessão** - fornece uma gravação de maneira tooobtain exclusivo, renovável, ou excluir o blob de tooa de acesso para um período de tempo

### <a name="etag"></a>ETag
Use ETags, se você precisar tooallow vários clientes ou instâncias toowrite toohello bloco Blob ou página Blob simultaneamente. Olá ETag permite toodetermine se hello contêiner ou blob tiver sido modificado desde que inicialmente ler ou criado, o que permite que você tooavoid substituindo as alterações confirmadas por outro processo ou cliente.

Você pode definir condições de ETag usando Olá opcional `options.accessConditions` parâmetro. Hello exemplo de código a seguir só carrega Olá **test.txt** arquivo se o blob Olá já existe e tem o valor de ETag Olá contido pelo `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Quando você estiver usando ETags, padrão geral de saudação é:

1. Obter Olá ETag como resultado de saudação de criar, lista ou operação de obtenção.
2. Executar uma ação, esse valor de ETag Olá a verificação não foi modificada.

Se o valor de saudação tiver sido modificado, isso indica que outro cliente ou instância modificada Olá blob ou contêiner desde que você obteve o valor de ETag Olá.

### <a name="lease"></a>Concessão
Você pode adquirir uma nova concessão usando Olá **acquireLease** método, especificando Olá contêiner ou blob que você deseja tooobtain uma concessão no. Por exemplo, a saudação de código a seguir adquire uma concessão em **myblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

As operações subsequentes na **myblob** deve fornecer Olá `options.leaseId` parâmetro. concessão Olá ID é retornado como `result.id` de **acquireLease**.

> [!NOTE]
> Por padrão, a duração da concessão Olá é infinita. Você pode especificar uma duração não infinita (entre 15 e 60 segundos), fornecendo Olá `options.leaseDuration` parâmetro.
>
>

use tooremove uma concessão, **releaseLease**. toobreak uma concessão, mas impede que outras pessoas obtenham uma nova concessão até que a duração de saudação original tiver expirado, use **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Trabalhar com assinaturas de acesso compartilhado
Assinaturas de acesso compartilhado (SAS) são uma tooblobs de acesso granular de tooprovide de maneira segura e contêineres sem fornecer o nome da conta de armazenamento ou chaves. Assinaturas de acesso compartilhado geralmente são usados tooprovide limitado acessar tooyour os dados, como permitir que um aplicativo móvel tooaccess blobs.

> [!NOTE]
> Enquanto você também pode permitir acesso anônimo tooblobs, assinaturas de acesso compartilhado permitem acesso tooprovide mais controlado, você deve gerar Olá SAS.
>
>

Um aplicativo confiável como um serviço baseado em nuvem gera assinaturas de acesso compartilhado usando Olá **generateSharedAccessSignature** de saudação **BlobService**e fornece-tooan não confiável ou aplicativo de confiança parcial, como um aplicativo móvel. Assinaturas geradas usando uma política, que descreve o início de saudação de acesso compartilhado e datas finais durante o qual Olá assinaturas de acesso compartilhado são válidas, bem como Olá acessar nível proprietário de assinaturas de acesso compartilhado toohello concedido.

Olá, exemplo de código a seguir gera uma nova política de acesso compartilhado que permite Olá compartilhado acesso assinaturas detentor tooperform operações de leitura no hello **myblob** blob e expira 100 minutos após o tempo de saudação é criado.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Observe que informações do host Olá devem ser fornecido, além disso, como é necessário quando proprietário de assinaturas de acesso compartilhado Olá tentativas de contêiner de saudação tooaccess.

Olá, em seguida, o aplicativo do cliente usa assinaturas de acesso compartilhado com **BlobServiceWithSAS** tooperform operações blob hello. Olá a seguir obtém informações sobre **myblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Desde que as assinaturas de acesso compartilhada de saudação foram geradas com acesso somente leitura, se uma tentativa de blob de saudação toomodify, um erro será retornado.

### <a name="access-control-lists"></a>Listas de controle de acesso
Você também pode usar uma política de acesso do acesso controle ACL (lista) tooset Olá SAS. Isso é útil se você quiser tooallow vários clientes tooaccess um contêiner, mas fornece as políticas de acesso diferentes para cada cliente.

Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política. saudação de exemplo de código a seguir define duas políticas, uma para 'user1' e outra para o 'Usuário2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Olá obtém de exemplo de código a seguir Olá ACL atual para **mycontainer**e, em seguida, adiciona novas políticas de saudação usando **setBlobAcl**. Essa abordagem permite:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Uma vez Olá que ACL é definida, você pode criar assinaturas de acesso compartilhado com base na ID de saudação de uma política. saudação de exemplo de código a seguir cria novas assinaturas de acesso compartilhado para o 'Usuário2':

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir.

* [Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference] (Referência do SDK do Armazenamento do Azure para API do Nó )
* [Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)
* Repositório [Microsoft Azure Storage SDK for Node.js][Azure Storage SDK for Node] (SDK do Armazenamento do Microsoft Azure para Node.js) no GitHub
* [Centro de Desenvolvedores do Node.js](https://azure.microsoft.com/develop/nodejs/)
* [Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[criar um aplicativo da web Node. js no serviço de aplicativo do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[usando o aplicativo web Node.js hello Azure serviço de tabela]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[criar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
