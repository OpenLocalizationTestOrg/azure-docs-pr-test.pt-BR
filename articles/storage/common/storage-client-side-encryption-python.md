---
title: Criptografia do lado do aaaClient com Python para o armazenamento do Microsoft Azure | Microsoft Docs
description: "Olá biblioteca de cliente de armazenamento do Azure para Python dá suporte à criptografia do lado do cliente para segurança máxima para seus aplicativos de armazenamento do Azure."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Criptografia do lado do cliente com Python para o Armazenamento do Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Visão geral
Olá [biblioteca de cliente de armazenamento do Azure para Python](https://pypi.python.org/pypi/azure-storage) dá suporte à criptografia de dados em aplicativos cliente antes de carregar tooAzure armazenamento e a descriptografia de dados durante o download toohello cliente.

> [!NOTE]
> biblioteca do Python de armazenamento do Azure Hello está em visualização.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Criptografia e descriptografia via técnica de envelope Olá
processos de saudação de criptografia e descriptografia siga técnica de envelope hello.

### <a name="encryption-via-hello-envelope-technique"></a>Criptografia via técnica de envelope Olá
A criptografia via técnica de envelope Olá funciona Olá maneira a seguir:

1. biblioteca de cliente de armazenamento do Azure Hello gera uma chave de criptografia do conteúdo (CEK), que é uma chave simétrica do uso de uma vez.
2. Os dados do usuário são criptografados usando esse CEK.
3. Olá CEK é fornecida (criptografada) usando a chave de criptografia de chave da saudação (KEK). Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica, que é gerenciada localmente.
   biblioteca de cliente de armazenamento Olá próprio nunca tem acesso tooKEK. biblioteca de saudação invoca chave saudação quebra automática de algoritmo que é fornecido pelo Olá KEK. Os usuários podem escolher toouse provedores personalizados para chave encapsulamento/desencapsulamento se desejado.
4. Olá os dados criptografados são, em seguida, carregar toohello serviço de armazenamento do Azure. saudação de chave encapsulada juntamente com alguns metadados adicionais de criptografia está armazenado como metadados (em um blob) ou interpolado com dados Olá criptografado (fila de mensagens e entidades de tabela).

### <a name="decryption-via-hello-envelope-technique"></a>Descriptografia via técnica de envelope Olá
Descriptografia via técnica de envelope Olá funciona Olá maneira a seguir:

1. biblioteca de saudação do cliente supõe que esse usuário hello está gerenciando (KEK) de chave de criptografia de chave Olá localmente. Olá usuário não precisa tooknow Olá chave específica que foi usada para criptografia. Em vez disso, um resolvedor de chave, que resolve tookeys diferentes identificadores de chave, pode ser configurado e usado.
2. biblioteca de saudação do cliente baixa dados Olá criptografado junto com qualquer material de criptografia que é armazenado no serviço de saudação.
3. chave de criptografia de conteúdo encapsulado de saudação (CEK) é então usando (descriptografado) desencapsulamento Olá a chave de criptografia de chave (KEK). Aqui novamente, biblioteca de saudação do cliente não tem acesso tooKEK. Ele simplesmente chama o algoritmo descodificar Olá provedor personalizado.
4. Olá conteúdo (CEK) de chave de criptografia, em seguida, é usado toodecrypt dados de usuário de saudação criptografado.

## <a name="encryption-mechanism"></a>Mecanismo de criptografia
biblioteca de cliente de armazenamento Olá usa [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) nos dados de usuário de tooencrypt de ordem. Especificamente, o modo [CBC (Encadeamento de Blocos de Criptografia)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) com AES. Cada serviço funciona ligeiramente diferente, portanto, discutiremos cada uma deles aqui.

### <a name="blobs"></a>Blobs
biblioteca de saudação do cliente atualmente oferece suporte à criptografia de somente blobs inteiras. Especificamente, a criptografia tem suporte quando os usuários usem Olá **criar*** métodos. Para downloads, os downloads completos e de intervalo têm suporte e a paralelização do download e do upload está disponível.

Durante a criptografia, biblioteca de saudação do cliente gerará um vetor de inicialização aleatória (IV) de 16 bytes, junto com uma chave de criptografia aleatória de conteúdo (CEK) de 32 bytes e executar a criptografia de envelope Olá de dados de blob usando essas informações. Olá encapsulado CEK e alguns metadados adicionais de criptografia são armazenadas como metadados junto com o blob criptografado de saudação no serviço de saudação do blob.

> [!WARNING]
> Se você estiver editando ou carregar seus próprios metadados de blob hello, será necessário tooensure que esses metadados são preservados. Se você carregar novos metadados sem esses metadados, Olá CEK encapsulado, IV e outros metadados serão perdidos e conteúdo do blob Olá nunca serão recuperável novamente.
> 
> 

Baixar um blob criptografado envolve recuperar conteúdo de saudação do blob de inteiro hello usando Olá **obter*** métodos de conveniência. Olá encapsulado CEK é aberto e usado em conjunto com hello IV (armazenados como metadados de blob nesse caso) tooreturn Olá descriptografado dados toohello usuários.

Baixar um intervalo arbitrário (**obter*** métodos com parâmetros de intervalo passado) em Olá blob criptografado envolve ajustar intervalo Olá fornecido por usuários em ordem tooget uma pequena quantidade de dados adicionais que podem ser usados saudação de descriptografar toosuccessfully intervalo solicitado.

Os blobs de blocos e os blobs de páginas podem ser criptografados/descriptografadas usando este esquema. No momento, não há suporte para a criptografia de blobs de acréscimo.

### <a name="queues"></a>Filas
Desde que a fila de mensagens pode ser de qualquer formato, a biblioteca de saudação do cliente define um formato personalizado que inclui hello vetor de inicialização (IV) e a chave de criptografia de conteúdo criptografada de saudação (CEK) no texto da mensagem de saudação.

Durante a criptografia, a biblioteca de saudação do cliente gera um IV aleatória de 16 bytes com uma CEK aleatória de 32 bytes e realiza a criptografia de envelope do texto da mensagem de saudação fila usando essas informações. Olá encapsulado CEK e alguns metadados adicionais de criptografia são adicionados toohello mensagem de fila criptografados. Essa mensagem modificada (mostrada abaixo) é armazenada no serviço de saudação.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

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
3. Olá encapsulado CEK e alguns metadados adicionais de criptografia, em seguida, são armazenados como duas propriedades adicionais de reservado. Olá reservados primeiro a propriedade (\_ClientEncryptionMetadata1) é uma propriedade de cadeia de caracteres que contém informações de saudação sobre IV, a versão e a chave encapsulado. Olá propriedade segundo reservada (\_ClientEncryptionMetadata2) é uma propriedade binária que contém informações de saudação sobre propriedades de saudação que são criptografados. Olá informação desta propriedade segundo (\_ClientEncryptionMetadata2) é criptografada.
4. Devido toothese reservado propriedades adicionais necessárias para a criptografia, os usuários agora podem ter somente 250 propriedades personalizadas em vez de 252. tamanho total de saudação da entidade Olá deve ser menor que 1MB.
   
   Observe que somente as propriedades de cadeia de caracteres podem ser criptografadas. Se outros tipos de propriedades são toobe criptografado, eles devem ser convertidos toostrings. cadeias de caracteres de saudação criptografada são armazenadas no serviço de saudação como propriedades binárias, e eles são convertidos toostrings back (brutas cadeias de caracteres, não EntityProperties com tipo EdmType.STRING) após a descriptografia.
   
   Para tabelas, além de toohello política de criptografia, usuários devem especificar Olá propriedades toobe criptografado. Isso pode ser feito por armazenar essas propriedades em objetos TableEntity com hello tipo conjunto tooEdmType.STRING e criptografar conjunto tootrue ou configuração Olá encryption_resolver_function no objeto de tableservice hello. Um resolvedor de criptografia é uma função que usa uma chave de partição, a chave de linha e o nome da propriedade e retorna um valor booliano que indica se essa propriedade deve ser criptografada. Durante a criptografia, biblioteca de saudação do cliente usará esse toodecide informações se uma propriedade deve ser criptografada durante a gravação toohello durante a transmissão. também fornece delegado Olá possibilidade de saudação da lógica em torno de como as propriedades são criptografadas. (Por exemplo, se X, então criptografar a propriedade A; caso contrário, criptografar as propriedades A e B.) Observe que ele é necessário não tooprovide essas informações durante a leitura ou consultar entidades.

### <a name="batch-operations"></a>Operações em lote
Uma política de criptografia se aplica a tooall linhas no lote de saudação. biblioteca de cliente Olá internamente irá gerar um novo IV aleatória e CEK aleatório por linha no lote de saudação. Os usuários também podem escolher tooencrypt propriedades diferentes para cada operação em lote Olá definindo esse comportamento no resolvedor de criptografia de saudação.
Se um lote é criado como um Gerenciador de contexto por meio do método de batch() tableservice hello, política de criptografia do hello tableservice serão automaticamente aplicadas toohello lote. Se um lote é criado, explicitamente, chamando o construtor hello, política de criptografia Olá deve ser passada como um parâmetro e à esquerda não modificado pelo tempo de vida de saudação do lote de saudação.
Observe que entidades foram criptografadas conforme são inseridos no lote hello usando a política de criptografia do lote da saudação (entidades não são criptografadas no tempo de saudação de confirmação de lote hello usando a política de criptografia do hello tableservice).

### <a name="queries"></a>Consultas
tooperform operações de consulta, você deve especificar um resolvedor de chave que é capaz de tooresolve todos Olá chaves no conjunto de resultados de saudação. Se uma entidade contida no resultado da consulta Olá não puder ser resolvido tooa provedor, a biblioteca de cliente Olá lançará um erro. Para qualquer consulta que executa projeções do lado de servidor, biblioteca de saudação do cliente irá adicionar propriedades de metadados de criptografia especial hello (\_ClientEncryptionMetadata1 e \_ClientEncryptionMetadata2) por padrão toohello colunas selecionadas .

> [!IMPORTANT]
> Lembre-se dos seguintes pontos importantes ao usar a criptografia no lado do cliente:
> 
> * Quando tooan do modo de leitura ou gravação criptografados blob, use comandos de carregamento de blob todo e comandos de download de blob de intervalo/inteiro. Evite escrever tooan blob criptografado usando operações de protocolo como colocar bloco, coloque a lista de bloqueios, gravar páginas ou limpar páginas; Caso contrário, você pode corromper o blob criptografado hello e torná-lo ilegível.
> * Para tabelas, existe uma restrição semelhante. Ser cuidadoso toonot atualização criptografada propriedades sem atualizar metadados de criptografia de saudação.
> * Se você definir metadados no blob criptografado hello, poderá substituir metadados relacionadas à criptografia de Olá exigido para descriptografia, como a definição de metadados não aditiva. Isso também ocorre em instantâneos. Evite especificar metadados ao criar um instantâneo de um blob criptografado. Se os metadados devem ser definidos, ser Olá-se de toocall **get_blob_metadata** tooget primeiro método hello metadados de criptografia atual e evitar gravações simultâneas ao conjunto de metadados.
> * Habilitar Olá **require_encryption** sinalizador no objeto de serviço Olá para usuários que devem trabalhar somente com os dados criptografados. Saiba mais logo abaixo.
> 
> 

biblioteca de cliente de armazenamento Olá espera Olá fornecido KEK e resolvedor chave Olá tooimplement interface a seguir. [Cofre de Chaves do Azure](https://azure.microsoft.com/services/key-vault/) ao gerenciamento de Python KEK está pendente e será integrado a essa biblioteca quando estiver concluído.

## <a name="client-api--interface"></a>API do cliente / Interface
Depois que um objeto de serviço de armazenamento (ou seja, blockblobservice) tiver sido criado, o usuário Olá pode atribuir valores toohello campos que constituem uma política de criptografia: key_encryption_key, key_resolver_function e require_encryption. Os usuários podem fornecer somente uma KEK, somente um resolvedor ou ambos. key_encryption_key é Olá básico tipo de chave que é identificado usando um identificador de chave e que fornece a lógica de saudação para encapsulamento/desencapsulamento. key_resolver_function é usado tooresolve uma chave durante o processo de descriptografia hello. Ele retorna uma KEK válida dado um identificador de chave. Isso fornece aos usuários Olá capacidade toochoose entre várias chaves que são gerenciados em vários locais.

Olá KEK deve implementar a seguir Olá métodos toosuccessfully criptografar dados:

* wrap_key(CEK): Olá encapsula especificado CEK (bytes) usando um algoritmo de saudação da escolha do usuário. Olá retorna encapsulado chave.
* get_key_wrap_algorithm(): algoritmo de saudação retorna usado toowrap chaves.
* get_kid(): retorna Olá cadeia de caracteres id de chave para essa KEK.
  Olá KEK deve implementar Olá toosuccessfully descriptografar dados de métodos a seguir:
* unwrap_key (cek, algoritmo): retorna Olá aberto formulário de saudação especificado CEK usando Olá algoritmo de cadeia de caracteres especificada.
* get_kid(): retorna uma ID da chave de cadeia de caracteres para essa KEK.

resolvedor de chave Olá pelo menos deve implementar um método que, recebe uma id de chave, retorna Olá KEK implementação Olá interface correspondente acima. Apenas este método é toobe toohello key_resolver_function propriedade no objeto de serviço Olá atribuída.

* Para criptografia, chave de saudação é usado sempre e ausência de saudação de uma chave resultará em erro.
* Para descriptografar:
  
  * resolvedor de chave Olá é invocado se especificado tooget chave de saudação. Se o resolvedor de saudação for especificado, mas não tem um mapeamento para o identificador de chave hello, um erro será gerado.
  * Se o resolvedor não for especificado, mas uma chave for especificada, chave Olá será usado se seu identificador corresponde ao identificador de chave Olá necessário. Se o identificador de saudação não corresponder, um erro será lançado.
    
    Olá exemplos de criptografia em azure.storage.samples <fix URL>demonstram um cenário de ponta a ponta mais detalhado para blobs, filas e tabelas.
      Exemplos de implementações de saudação KEK e resolvedor de chave são fornecidos nos arquivos de exemplo hello como KeyWrapper e KeyResolver respectivamente.

### <a name="requireencryption-mode"></a>Modo RequireEncryption
Os usuários podem habilitar opcionalmente um modo de operação no qual todos os downloads e uploads devem ser criptografados. Nesse modo, tentativas tooupload dados sem um criptografia política ou download de dados que não são criptografados no serviço Olá falhará no cliente de saudação. Olá **require_encryption** sinalizador em controles de objeto de serviço Olá esse comportamento.

### <a name="blob-service-encryption"></a>Criptografia do serviço Blob
Definir campos de política de criptografia Olá Olá blockblobservice objeto. Todo o resto será tratado pela biblioteca de cliente Olá internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Criptografia do serviço Fila
Definir campos de política de criptografia Olá Olá queueservice objeto. Todo o resto será tratado pela biblioteca de cliente Olá internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Criptografia do serviço Tabela
Além disso toocreating uma política de criptografia e configurá-la em Opções de solicitação, você deve especificar um **encryption_resolver_function** em Olá **tableservice**, ou conjunto hello criptografar o atributo Olá EntityProperty.

### <a name="using-hello-resolver"></a>Usando o resolvedor de saudação

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Usando atributos
Conforme mencionado acima, uma propriedade pode ser marcada para criptografia, armazenando-o em um objeto EntityProperty e configuração Olá criptografar o campo.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Criptografia e desempenho
Observe que criptografar seu armazenamento de dados resulta em uma sobrecarga adicional no desempenho. Olá conteúdo IV e chave devem ser gerada, próprio conteúdo Olá deve ser criptografado e metadados adicionais devem ser formatados e carregados. Essa sobrecarga irão variar dependendo da quantidade de saudação de dados que está sendo criptografadas. Recomendamos que os clientes sempre testem seus aplicativos a fim de verificar o desempenho durante o desenvolvimento.

## <a name="next-steps"></a>Próximas etapas
* Baixar Olá [biblioteca de cliente de armazenamento do Azure para Java PyPi pacote](https://pypi.python.org/pypi/azure-storage)
* Baixar Olá [biblioteca de cliente de armazenamento do Azure para Python código-fonte do GitHub](https://github.com/Azure/azure-storage-python)
