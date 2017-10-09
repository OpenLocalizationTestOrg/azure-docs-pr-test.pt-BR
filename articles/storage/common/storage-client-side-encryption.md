---
title: Criptografia do lado do aaaClient com o .NET para armazenamento do Microsoft Azure | Microsoft Docs
description: "Olá biblioteca de cliente de armazenamento do Azure para .NET oferece suporte a criptografia do lado do cliente e a integração com o Cofre de chaves do Azure para segurança máxima para seus aplicativos de armazenamento do Azure."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c09246f43801e17aff96ea453182d11ffbf5e420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a>Criptografia do lado do cliente e o Cofre da Chave do Azure para o Armazenamento do Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Visão geral
Olá [biblioteca de cliente de armazenamento do Azure para o pacote Nuget .NET](https://www.nuget.org/packages/WindowsAzure.Storage) dá suporte à criptografia de dados em aplicativos cliente antes de carregar tooAzure armazenamento e a descriptografia de dados durante o download toohello cliente. biblioteca de saudação também oferece suporte à integração com [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) para gerenciamento de chaves de conta de armazenamento.

Para obter um tutorial passo a passo que o Guie pelo processo de saudação de criptografar blobs usando a criptografia do lado do cliente e o Cofre de chaves do Azure, consulte [criptografar e descriptografar blobs no armazenamento do Microsoft Azure usando o Azure Key Vault](../blobs/storage-encrypt-decrypt-blobs-key-vault.md).

Para a criptografia do lado do cliente com Java, veja [Criptografia do lado do cliente com Java para o Armazenamento do Microsoft Azure](storage-client-side-encryption-java.md).

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Criptografia e descriptografia via técnica de envelope Olá
processos de saudação de criptografia e descriptografia siga técnica de envelope hello.

### <a name="encryption-via-hello-envelope-technique"></a>Criptografia via técnica de envelope Olá
A criptografia via técnica de envelope Olá funciona Olá maneira a seguir:

1. biblioteca de cliente de armazenamento do Azure Hello gera uma chave de criptografia do conteúdo (CEK), que é uma chave simétrica do uso de uma vez.
2. Os dados do usuário são criptografados usando esse CEK.
3. Olá CEK é fornecida (criptografada) usando a chave de criptografia de chave da saudação (KEK). Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e podem ser gerenciado localmente ou armazenado em cofres de chaves do Azure.
   
    biblioteca de cliente de armazenamento Olá próprio nunca tem acesso tooKEK. biblioteca de saudação invoca o algoritmo de chave encapsulamento Olá fornecida pelo Cofre de chaves. Os usuários podem escolher toouse provedores personalizados para chave encapsulamento/desencapsulamento se desejado.

4. Olá os dados criptografados são, em seguida, carregar toohello serviço de armazenamento do Azure. saudação de chave encapsulada juntamente com alguns metadados adicionais de criptografia está armazenado como metadados (em um blob) ou interpolado com dados Olá criptografado (fila de mensagens e entidades de tabela).

### <a name="decryption-via-hello-envelope-technique"></a>Descriptografia via técnica de envelope Olá
Descriptografia via técnica de envelope Olá funciona Olá maneira a seguir:

1. biblioteca de cliente de saudação pressupõe que o usuário hello está gerenciando (KEK) de chave de criptografia de chave Olá localmente ou em cofres de chaves do Azure. Olá usuário não precisa tooknow Olá chave específica que foi usada para criptografia. Em vez disso, um resolvedor de chave que resolve tookeys diferentes identificadores de chave pode ser configurado e usado.
2. biblioteca de saudação do cliente baixa dados Olá criptografado junto com qualquer material de criptografia que é armazenado no serviço de saudação.
3. chave de criptografia de conteúdo encapsulado de saudação (CEK) é então usando (descriptografado) desencapsulamento Olá a chave de criptografia de chave (KEK). Aqui novamente, biblioteca de saudação do cliente não tem acesso tooKEK. Ele simplesmente chama Olá personalizado ou algoritmo descodificar do provedor do Cofre de chaves.
4. Olá conteúdo (CEK) de chave de criptografia, em seguida, é usado toodecrypt dados de usuário de saudação criptografado.

## <a name="encryption-mechanism"></a>Mecanismo de criptografia
biblioteca de cliente de armazenamento Olá usa [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) nos dados de usuário de tooencrypt de ordem. Especificamente, o modo [CBC (Encadeamento de Blocos de Criptografia)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) com AES. Cada serviço funciona ligeiramente diferente, portanto, discutiremos cada uma deles aqui.

### <a name="blobs"></a>Blobs
biblioteca de saudação do cliente atualmente oferece suporte à criptografia de somente blobs inteiras. Especificamente, a criptografia tem suporte quando os usuários usem Olá **UploadFrom*** métodos ou hello **OpenWrite** método. Para downloads, tanto os downloads completos quanto os de intervalo têm suporte.

Durante a criptografia, biblioteca de saudação do cliente gerará um vetor de inicialização aleatória (IV) de 16 bytes, junto com uma chave de criptografia aleatória de conteúdo (CEK) de 32 bytes e executar a criptografia de envelope Olá de dados de blob usando essas informações. Olá encapsulado CEK e alguns metadados adicionais de criptografia são armazenadas como metadados junto com o blob criptografado de saudação no serviço de saudação do blob.

> [!WARNING]
> Se você estiver editando ou carregar seus próprios metadados de blob hello, será necessário tooensure que esses metadados são preservados. Se você carregar novos metadados sem esses metadados, hello CEK encapsulado, IV e outros metadados serão perdidos e conteúdo do blob Olá nunca será possível recuperá-la novamente.
> 
> 

Baixar um blob criptografado envolve recuperar conteúdo de saudação do blob de inteiro hello usando Olá **DownloadTo***/**BlobReadStream** conveniência métodos. Olá encapsulado CEK é aberto e usado em conjunto com hello IV (armazenados como metadados de blob nesse caso) tooreturn Olá descriptografado dados toohello usuários.

Baixar um intervalo arbitrário (**DownloadRange*** métodos) em Olá blob criptografado envolve ajustar o intervalo de saudação fornecido por usuários em ordem tooget uma pequena quantidade de dados adicionais que podem ser usado toosuccessfully descriptografar Olá intervalo solicitado.

Todos os tipos de blob (blobs de blocos, blobs de páginas e blobs de anexo) podem ser criptografados/descriptografados usando este esquema.

### <a name="queues"></a>Filas
Desde que a fila de mensagens pode ser de qualquer formato, a biblioteca de saudação do cliente define um formato personalizado que inclui hello vetor de inicialização (IV) e a chave de criptografia de conteúdo criptografada de saudação (CEK) no texto da mensagem de saudação.

Durante a criptografia, a biblioteca de saudação do cliente gera um IV aleatória de 16 bytes com uma CEK aleatória de 32 bytes e realiza a criptografia de envelope do texto da mensagem de saudação fila usando essas informações. Olá encapsulado CEK e alguns metadados adicionais de criptografia são adicionados toohello mensagem de fila criptografados. Essa mensagem modificada (mostrada abaixo) é armazenada no serviço de saudação.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

Durante a descriptografia, chave encapsulado Olá é extraído da mensagem da fila de saudação e aberto. Olá IV também é extraído da mensagem da fila de saudação e usado junto com dados de mensagem da fila do hello aberto toodecrypt chave hello. Observe que metadados de criptografia Olá são pequeno (em bytes) 500, enquanto ele contam para o limite de 64KB Olá para uma mensagem da fila, o impacto de saudação deve ser gerenciável.

### <a name="tables"></a>Tabelas
Olá biblioteca de cliente oferece suporte à criptografia de propriedades de entidade para inserir e substituir operações.

> [!NOTE]
> Atualmente não há suporte para a mesclagem. Como um subconjunto das propriedades pode ter sido criptografado anteriormente usando uma chave diferente, simplesmente mesclando novas propriedades de saudação e atualizar metadados Olá resultará em perda de dados. Mesclar o requer fazer serviço extra chama entidade pré-existente do tooread Olá do serviço hello, ou usando uma nova chave por propriedade, que não são adequados por motivos de desempenho.
> 
> 

Criptografia de dados de tabela funciona da seguinte maneira:  

1. Os usuários especificam Olá propriedades toobe criptografado.
2. biblioteca de saudação do cliente gera um vetor de inicialização aleatória (IV) de 16 bytes juntamente com uma chave de criptografia aleatória de conteúdo (CEK) de 32 bytes para cada entidade e executa criptografia de envelope em Olá propriedades individuais toobe criptografado derivando uma nova IV por propriedade. propriedade Olá criptografado é armazenada como dados binários.
3. Olá encapsulado CEK e alguns metadados adicionais de criptografia, em seguida, são armazenados como duas propriedades adicionais de reservado. propriedade reservada primeiro Hello (_ClientEncryptionMetadata1) é uma propriedade de cadeia de caracteres que contém informações de saudação sobre IV, a versão e a chave encapsulado. propriedade reservada segundo Hello (_ClientEncryptionMetadata2) é uma propriedade binária que contém informações de saudação sobre propriedades de saudação que são criptografados. informações de saudação nessa propriedade segundo (_ClientEncryptionMetadata2) são criptografada.
4. Devido toothese reservado propriedades adicionais necessárias para a criptografia, os usuários agora podem ter somente 250 propriedades personalizadas em vez de 252. tamanho total de saudação da entidade Olá deve ser menor que 1 MB.

Observe que somente as propriedades de cadeia de caracteres podem ser criptografadas. Se outros tipos de propriedades são toobe criptografado, eles devem ser convertidos toostrings. cadeias de caracteres de saudação criptografada são armazenadas no serviço de saudação como propriedades binárias, e eles são convertidos toostrings voltar depois da descriptografia.

Para tabelas, além de toohello política de criptografia, usuários devem especificar Olá propriedades toobe criptografado. Isso pode ser feito especificando o atributo [EncryptProperty] \(para entidades POCO que derivam de TableEntity) ou um resolvedor de criptografia nas opções de solicitação. Um resolvedor de criptografia é um delegado que usa uma chave de partição, a chave de linha e o nome da propriedade e retorna um valor booliano que indica se essa propriedade deve ser criptografada. Durante a criptografia, biblioteca de saudação do cliente usará esse toodecide informações se uma propriedade deve ser criptografada durante a gravação toohello durante a transmissão. também fornece delegado Olá possibilidade de saudação da lógica em torno de como as propriedades são criptografadas. (Por exemplo, se X, então criptografar a propriedade A; caso contrário, criptografar as propriedades A e B.) Observe que ele é necessário não tooprovide essas informações durante a leitura ou consultar entidades.

### <a name="batch-operations"></a>Operações em lote
Operações em lote, hello KEK mesmo será usado em todas as linhas de saudação da operação em lote porque a biblioteca de cliente Olá permite apenas um objeto de opções (e, portanto, uma política/KEK) por operação em lote. No entanto, biblioteca de cliente Olá internamente gerará um novo IV aleatória e CEK aleatório por linha em lote de saudação. Os usuários também podem escolher tooencrypt propriedades diferentes para cada operação em lote Olá definindo esse comportamento no resolvedor de criptografia de saudação.

### <a name="queries"></a>Consultas
tooperform operações de consulta, você deve especificar um resolvedor de chave que é capaz de tooresolve todos Olá chaves no conjunto de resultados de saudação. Se uma entidade contida no resultado da consulta Olá não puder ser resolvido tooa provedor, a biblioteca de cliente Olá lançará um erro. Para qualquer consulta que executa projeções do lado do servidor, biblioteca de saudação do cliente irá adicionar propriedades de metadados de criptografia especial hello (_ClientEncryptionMetadata1 e _ClientEncryptionMetadata2) por colunas de toohello selecionado padrão.

## <a name="azure-key-vault"></a>Cofre da Chave do Azure
O Cofre da Chave do Azure ajuda a proteger chaves criptográficas e segredos usados por aplicativos e serviços em nuvem. Usando o Cofre da Chave do Azure, os usuários podem criptografar chaves e segredos (como chaves de autenticação, chaves de conta de armazenamento, chaves de criptografia de dados, arquivos .PFX e senhas) usando chaves que são protegidas por HSMs (módulos de segurança de hardware). Para obter mais informações, veja [O que é o Cofre da Chave do Azure?](../../key-vault/key-vault-whatis.md).

biblioteca de cliente de armazenamento de saudação usa a biblioteca principal do hello Cofre de chaves em ordem tooprovide uma estrutura comum no Azure de gerenciamento de chaves. Os usuários também obter o benefício adicional de saudação do usando a biblioteca de extensões do Cofre de chaves de saudação. biblioteca de extensões de saudação fornece uma funcionalidade útil simple e contínuo simétrica/RSA local e provedores principais de nuvem, bem como com o cache e a agregação.

### <a name="interface-and-dependencies"></a>Interface e dependências
Há três pacotes do Cofre da Chave:

* Microsoft.Azure.KeyVault.Core contém hello IKey e IKeyResolver. Este é um pequeno pacote sem dependências. biblioteca de cliente de armazenamento Olá para .NET define como uma dependência.
* Microsoft.Azure.KeyVault contém cliente de REST do Cofre de chave hello.
* Microsoft.Azure.KeyVault.Extensions contém o código de extensão que inclui implementações de algoritmos criptográficos e um RSAKey e SymmetricKey. Ele depende de namespaces do núcleo e KeyVault hello e fornece funcionalidade toodefine um resolvedor de agregação (quando os usuários desejam toouse vários provedores de chave) e um resolvedor de chave de cache. Embora a biblioteca de cliente de armazenamento Olá não depende diretamente esse pacote, se os usuários deseja toouse Azure Key Vault toostore suas chaves ou toouse Olá Olá de tooconsume de extensões de Cofre de chaves local e na nuvem de provedores criptográficos, eles precisarão deste pacote.

O Cofre da Chave foi criado para chaves mestras de alto valor e os limites por Cofre da Chave são criados com tal prioridade em mente. Ao executar a criptografia do lado do cliente com o Cofre de chaves, modelo preferido Olá é toouse simétrica mestra chaves armazenadas como segredos no cofre de chaves e armazenados em cache localmente. Os usuários devem fazer seguinte hello:

1. Criar um segredo off-line e carregá-lo tooKey cofre.
2. Use o identificador de base do segredo hello como um parâmetro tooresolve Olá a versão atual do segredo Olá para criptografia e armazenar essas informações localmente em cache. Use CachingKeyResolver para armazenamento em cache; os usuários é tooimplement não esperado seu próprios cache lógica.
3. Use o resolvedor de cache Olá como uma entrada ao criar a política de criptografia de saudação.

Para obter mais informações sobre o uso de Cofre de chaves podem ser encontradas no hello [exemplos de código de criptografia](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).

## <a name="best-practices"></a>Práticas recomendadas
Suporte a criptografia está disponível somente na biblioteca de cliente de armazenamento de saudação para .NET. Atualmente, o Windows Phone e o Tempo de Execução do Windows não dão suporte à criptografia.

> [!IMPORTANT]
> Lembre-se dos seguintes pontos importantes ao usar a criptografia no lado do cliente:
> 
> * Quando tooan do modo de leitura ou gravação criptografados blob, use comandos de carregamento de blob todo e comandos de download de blob de intervalo/inteiro. Evite escrever tooan blob criptografado usando operações de protocolo como colocar bloco, coloque a lista de bloqueios, gravar páginas, páginas limpar ou acrescentar bloco; Caso contrário, você pode corromper o blob criptografado hello e torná-lo ilegível.
> * Para tabelas, existe uma restrição semelhante. Ser cuidadoso toonot atualização criptografada propriedades sem atualizar metadados de criptografia de saudação.
> * Se você definir metadados no blob criptografado hello, poderá substituir metadados relacionadas à criptografia de Olá exigido para descriptografia, como a definição de metadados não aditiva. Isso também ocorre em instantâneos. Evite especificar metadados ao criar um instantâneo de um blob criptografado. Se os metadados devem ser definidos, ser Olá-se de toocall **FetchAttributes** tooget primeiro método hello metadados de criptografia atual e evitar gravações simultâneas ao conjunto de metadados.
> * Habilitar Olá **RequireEncryption** propriedade nas opções de solicitação saudação padrão para usuários que devem trabalhar somente com os dados criptografados. Saiba mais logo abaixo.
> 
> 

## <a name="client-api--interface"></a>API do cliente / Interface
Ao criar um objeto EncryptionPolicy, os usuários podem fornecer somente uma chave (Implementando IKey), somente um resolvedor (Implementando IKeyResolver) ou ambos. IKey é Olá básico tipo de chave que é identificado usando um identificador de chave e que fornece a lógica de saudação para encapsulamento/desencapsulamento. IKeyResolver é usado tooresolve uma chave durante o processo de descriptografia hello. Ele define um método ResolveKey que retorna um IKey dado um certo identificador de chave. Isso fornece aos usuários Olá capacidade toochoose entre várias chaves que são gerenciados em vários locais.

* Para criptografia, chave de saudação é usado sempre e ausência de saudação de uma chave resultará em erro.
* Para descriptografar:
  * resolvedor de chave Olá é invocado se especificado tooget chave de saudação. Se o resolvedor de saudação for especificado, mas não tem um mapeamento para o identificador de chave hello, um erro será gerado.
  * Se o resolvedor não for especificado, mas uma chave for especificada, chave Olá será usado se seu identificador corresponde ao identificador de chave Olá necessário. Se o identificador de saudação não corresponder, um erro será lançado.

Olá [exemplos de criptografia](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) demonstram um cenário de ponta a ponta mais detalhado para blobs, filas e tabelas, juntamente com a integração do Cofre de chaves.

### <a name="requireencryption-mode"></a>Modo RequireEncryption
Os usuários podem habilitar opcionalmente um modo de operação no qual todos os downloads e uploads devem ser criptografados. Nesse modo, tentativas tooupload dados sem um criptografia política ou download de dados que não são criptografados no serviço Olá falhará no cliente de saudação. Olá **RequireEncryption** propriedade do objeto de opções de solicitação Olá controla esse comportamento. Se seu aplicativo irá criptografar todos os objetos armazenados no armazenamento do Azure, você pode definir Olá **RequireEncryption** propriedade nas opções de solicitação padrão Olá Olá objeto de serviço cliente. Por exemplo, definir **CloudBlobClient.DefaultRequestOptions.RequireEncryption** muito**true** toorequire criptografia para todas as operações de blob executadas por meio do objeto cliente.

### <a name="blob-service-encryption"></a>Criptografia do serviço Blob
Criar um **BlobEncryptionPolicy** do objeto e defina-o nas opções de solicitação hello (ou por API em um nível de cliente usando **DefaultRequestOptions**). Todo o resto será tratado pela biblioteca de cliente Olá internamente.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Criptografia do serviço Fila
Criar um **QueueEncryptionPolicy** do objeto e defina-o nas opções de solicitação hello (ou por API em um nível de cliente usando **DefaultRequestOptions**). Todo o resto será tratado pela biblioteca de cliente Olá internamente.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a>Criptografia do serviço Tabela
Além disso toocreating uma política de criptografia e configurá-la em Opções de solicitação, você deve especificar um **EncryptionResolver** na **TableRequestOptions**, ou defina o atributo Olá [EncryptProperty] em entidade de saudação.

#### <a name="using-hello-resolver"></a>Usando o resolvedor de saudação

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a>Usando atributos
Conforme mencionado acima, se a entidade Olá implementa TableEntity, em seguida, propriedades de saudação podem ser decoradas com atributo Olá [EncryptProperty] em vez de especificar Olá **EncryptionResolver**.

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a>Criptografia e desempenho
Observe que criptografar seu armazenamento de dados resulta em uma sobrecarga adicional no desempenho. Olá conteúdo IV e chave devem ser gerada, próprio conteúdo Olá deve ser criptografado e metadados adicionais devem ser formatados e carregados. Essa sobrecarga irão variar dependendo da quantidade de saudação de dados que está sendo criptografadas. Recomendamos que os clientes sempre testem seus aplicativos a fim de verificar o desempenho durante o desenvolvimento.

## <a name="next-steps"></a>Próximas etapas
* [Tutorial: criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Cofre da Chave do Azure](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)
* Baixar Olá [biblioteca de cliente de armazenamento do Azure para o pacote NuGet .NET](https://www.nuget.org/packages/WindowsAzure.Storage)
* Baixar hello Azure Key Vault NuGet [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [cliente](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), e [extensões](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) pacotes  
* Visite Olá [documentação do Cofre de chave do Azure](../../key-vault/key-vault-whatis.md)
