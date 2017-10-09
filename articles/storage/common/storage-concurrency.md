---
title: aaaManaging simultaneidade no armazenamento do Microsoft Azure
description: "Como a simultaneidade toomanage para Olá serviços Blob, fila, tabela e arquivo"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 5b8efbe0a9ebc881ded8f3abef5f138e0385f7c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Gerenciando a simultaneidade no Armazenamento do Microsoft Azure
## <a name="overview"></a>Visão geral
Os aplicativos baseados na Internet modernos consistem normalmente em vários usuários exibindo e atualizando dados de forma simultânea. Isso requer toothink de desenvolvedores do aplicativo cuidadosamente sobre como tooprovide um previsível enfrentar os usuários finais de tootheir, particularmente para cenários onde vários usuários podem atualizar Olá mesmo dados. Existem três estratégias de simultaneidade de dados principais que os desenvolvedores normalmente consideram:  

1. Simultaneidade otimista – um aplicativo executar uma atualização como parte de sua atualização verificará se os dados de saudação foi alterada desde o aplicativo hello lida pela última vez que os dados. Por exemplo, se dois usuários, exibir uma página wiki fazem uma atualização toohello mesmo página plataforma de wiki Olá deve garantir que essa atualização de segundo Olá não substitui a primeira atualização de hello – e que os dois usuários compreendem se a atualização foi bem-sucedida ou não. Essa estratégia é usada com mais frequência em aplicativos Web.
2. Simultaneidade pessimista – um aplicativo procurando tooperform uma atualização levará um bloqueio em um objeto impede que outros usuários atualizem dados saudação até Olá bloqueio seja liberado. Por exemplo, em um cenário de replicação de dados mestre/escravo onde único mestre Olá irá realizar atualizações mestre Olá normalmente conterá um bloqueio exclusivo para um longo período de tempo em Olá dados tooensure nenhuma outra pessoa pode atualizá-lo.
3. Último gravador ganha – uma abordagem que permite que qualquer tooproceed de operações de atualização sem verificar se qualquer outro aplicativo tem Olá dados atualizados desde que o aplicativo hello primeiro leia dados saudação. Essa estratégia (ou falta de uma estratégia formal) geralmente é usada onde os dados são particionados de forma que não há nenhum probabilidade de que vários usuários terão acesso Olá mesmos dados. Ela também pode ser útil em locais em que fluxos de dados de curta duração estão sendo processados.  

Este artigo fornece uma visão geral de como plataforma de armazenamento do Azure Olá simplifica o desenvolvimento, fornecendo suporte de primeira classe para todas as três dessas estratégias de simultaneidade.  

## <a name="azure-storage--simplifies-cloud-development"></a>Armazenamento do Azure: simplifica o desenvolvimento na nuvem
Olá serviço de armazenamento do Azure oferece suporte a todos os três estratégias, embora seja diferente na capacidade tooprovide total suporte a simultaneidade otimista e pessimista porque ele foi projetado tooembrace um modelo de consistência forte que garante que, quando Olá confirmações de serviço de armazenamento inserir ou todos os dados adicionais de toothat acessa verá hello mais recente de atualização de operação de atualização de dados. Plataformas de armazenamento que usam um modelo de consistência eventual têm um atraso entre quando uma gravação é executada por um usuário e quando Olá atualizado os dados podem ser vistos por outros usuários complicar, portanto, o desenvolvimento de aplicativos de cliente em inconsistências de tooprevent de ordem de afetar os usuários finais.  

Além disso tooselecting um desenvolvedores de estratégia de simultaneidade apropriada devem estar ciente de como uma plataforma de armazenamento isola alterações – particularmente toohello alterações em transações do mesmo objeto. saudação de serviço de armazenamento do Azure usa tooallow de isolamento de instantâneo ler toohappen operações simultaneamente com operações de gravação em uma única partição. Ao contrário de outros níveis de isolamento, o isolamento de instantâneo garante que todas as leituras vejam um instantâneo consistente dos dados saudação mesmo enquanto as atualizações estão ocorrendo – essencialmente, retornando valores de confirmada última Olá enquanto uma transação de atualização está sendo processada.  

## <a name="managing-concurrency-in-blob-storage"></a>Gerenciando Simultaneidade em Armazenamento de Blobs
Você pode optar por toouse em modelos de simultaneidade otimista ou pessimista toomanage acesso tooblobs e Olá de contêineres no serviço blob. Se você não especificar explicitamente uma estratégia de última grava wins é o padrão de saudação.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Simultaneidade otimista para blobs e contêineres
saudação de serviço de armazenamento atribui um objeto de tooevery identificador armazenado. Esse identificador é atualizado sempre que uma operação de atualização é realizada em um objeto. Identificador de saudação é retornado toohello cliente como parte de uma resposta HTTP GET usando Olá cabeçalho de ETag (marca de entidade) que é definido no protocolo de saudação HTTP. Um usuário que executa uma atualização em tal objeto pode enviar Olá ETag original junto com tooensure um cabeçalho condicional que uma atualização somente ocorrerá se uma determinada condição foi atendida – nesse caso, é um cabeçalho "If-Match", que exige Olá armazenamento condição Olá Serviço tooensure Olá valor Olá ETag especificado na solicitação de atualização de saudação é Olá mesmo que aquele armazenado no hello serviço de armazenamento.  

estrutura de tópicos Hello desse processo é o seguinte:  

1. Recuperar um blob do serviço de armazenamento hello, resposta Olá inclui um valor de cabeçalho ETag de HTTP que identifica a versão atual saudação do objeto Olá no serviço de armazenamento de saudação.
2. Quando você atualiza o blob hello, incluir o valor de ETag de saudação recebido na etapa 1 do hello **If-Match** condicional cabeçalho de solicitação de saudação enviar toohello serviço.
3. serviço Olá compara o valor de ETag de saudação na solicitação de saudação com valor de ETag atual Olá de blob de saudação.
4. Se o valor atual de ETag Olá de blob de saudação é uma versão diferente de Olá ETag no hello **If-Match** cabeçalho condicional na solicitação hello, serviço Olá retorna um 412 erro ao cliente toohello. Isso indica o cliente toohello que outro processo tem Olá blob atualizado desde que o cliente Olá recuperá-lo.
5. Se Olá atual ETag é o valor do blob Olá Olá mesma versão Olá ETag no hello **If-Match** executa cabeçalho condicional na solicitação hello, serviço Olá Olá solicitada de atualizações e operação Olá valor atual de ETag de blob de saudação tooshow que ele cria uma nova versão.  

Olá c# trecho a seguir (usando a biblioteca de cliente de armazenamento 4.2.0 de saudação) mostra um exemplo simples de como tooconstruct uma **If-Match AccessCondition** com base em Olá valor ETag que é acessado de propriedades de saudação de um blob que foi anteriormente ou recuperados ou inseridas. Ele então usa Olá **AccessCondition** quando ela atualiza o blob de saudação do objeto: Olá **AccessCondition** objeto adiciona Olá **If-Match** solicitação de toohello do cabeçalho. Se outro processo tiver atualizado o blob hello, o serviço de blob de saudação retornará uma mensagem de status HTTP 412 (Falha na Precondição). Você pode baixar o exemplo completo de saudação aqui: [simultaneidade gerenciar usando o armazenamento do Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

saudação de serviço de armazenamento também inclui suporte para cabeçalhos condicionais, como **If-Modified-Since**, **If-Unmodified-Since** e **If-None-Match** , bem como combinações dos mesmos. Para obter mais informações, consulte [Especificando cabeçalhos condicionais para operações de serviço Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx) no MSDN.  

Olá, tabela a seguir resume as operações de contêiner de saudação que aceitam cabeçalhos condicionais como **If-Match** na solicitação hello e que retornar um valor de ETag em resposta hello.  

| Operação | Retorna o valor de ETag do contêiner | Aceita cabeçalhos condicionais |
|:--- |:--- |:--- |
| Create Container |Sim |Não |
| Get Container Properties |Sim |Não |
| Get Container Metadata |Sim |Não |
| Set Container Metadata |Sim |Sim |
| Get Container ACL |Sim |Não |
| Set Container ACL |Sim |Sim (*) |
| Delete Container |Não |Sim |
| Lease Container |Sim |Sim |
| Listar Blobs |Não |Não |

permissões de saudação (*) definidas pelo SetContainerACL são armazenados em cache e atualizações toothese permissões levam 30 segundos toobe a garantia de toopropagate durante o período de atualizações não são consistentes.  

Olá, tabela a seguir resume as operações de blob de saudação que aceitam cabeçalhos condicionais, como **If-Match** na solicitação hello e que retornar um valor de ETag em resposta hello.

| Operação | Retorna o valor de ETag | Aceita cabeçalhos condicionais |
|:--- |:--- |:--- |
| Put Blob |Sim |Sim |
| Get Blob |Sim |Sim |
| Get Blob Properties |Sim |Sim |
| Set Blob Properties |Sim |Sim |
| Get Blob Metadata |Sim |Sim |
| Set Blob Metadata |Sim |Sim |
| Lease Blob (*) |Sim |Sim |
| Blob de instantâneo |Sim |Sim |
| Copiar blob |Sim |Sim (para o blob de origem e destino) |
| Anular copiar Blob |Não |Não |
| Delete Blob |Não |Sim |
| Put Block |Não |Não |
| Put Block List |Sim |Sim |
| Get Block List |Sim |Não |
| Put Page |Sim |Sim |
| Get Page Ranges |Sim |Sim |

(*) Blob de concessão não altera Olá ETag em um blob.  

### <a name="pessimistic-concurrency-for-blobs"></a>Simultaneidade pessimista para blobs
toolock um blob para uso exclusivo, você pode adquirir uma [concessão](http://msdn.microsoft.com/library/azure/ee691972.aspx) nele. Quando você adquire uma concessão, especifique por quanto tempo você precisa Olá concessão: isso pode ser para entre 15 too60 segundos ou infinita, quais valores de bloqueio exclusivo tooan. Você pode renovar um tooextend concessão finito-e você pode liberar qualquer concessão quando tiver terminado com ele. serviço de blob Olá automaticamente libera concessões Finitas quando eles expiram.  

Concessões de habilitar sincronização diferentes estratégias toobe com suporte, incluindo gravação exclusivo / compartilhado exclusiva, leitura gravação / exclusivo de leitura e compartilhados de gravação / leitura exclusivo. Quando existe uma concessão de serviço de armazenamento de saudação impõe exclusivo gravações (put, definir e operações de exclusão) no entanto, garantindo a exclusividade para operações de leitura requer Olá desenvolvedor tooensure que todos os aplicativos cliente usam uma ID de concessão e que somente um cliente de cada vez tem uma ID de concessão válida. As operações de leitura que não incluem uma ID de concessão resultam em leituras compartilhadas.  

Olá seguinte trecho de c# mostra um exemplo de adquirir uma concessão exclusiva em um blob de 30 segundos, atualizando o conteúdo de saudação do blob hello e, em seguida, a liberação de concessão de saudação. Se já houver uma concessão válida no blob hello quando você tentar tooacquire uma nova concessão, o serviço de blob de saudação retornará um resultado de status de "HTTP (409) conflito". Olá trecho a seguir usa uma **AccessCondition** tooencapsulate informações de concessão de saudação do objeto quando ele se um blob de saudação do tooupdate de solicitação no serviço de armazenamento de saudação.  Você pode baixar o exemplo completo de saudação aqui: [simultaneidade gerenciar usando o armazenamento do Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Se você tentar uma operação de gravação em um blob concedido sem passar a ID de concessão Olá, solicitação de saudação falhará com um erro 412. Observe que, se hello concessão expirar antes de chamar hello **UploadText** método mas ainda passe na ID de concessão hello, solicitação Olá também falhará com um **412** erro. Para obter mais informações sobre como gerenciar tempos de expiração da concessão e IDs de concessão, consulte Olá [Blob de concessão](http://msdn.microsoft.com/library/azure/ee691972.aspx) documentação REST.  

Olá seguintes operações de blob podem usar simultaneidade pessimista do concessões toomanage:  

* Put Blob
* Get Blob
* Get Blob Properties
* Set Blob Properties
* Get Blob Metadata
* Set Blob Metadata
* Delete Blob
* Put Block
* Put Block List
* Get Block List
* Put Page
* Get Page Ranges
* Snapshot Blob - ID de concessão opcional se existir uma concessão
* Copiar Blob - ID de concessão necessária a existência de uma concessão no blob de destino Olá
* Anular copiar Blob - necessário se existe uma concessão infinita no blob de destino de saudação do ID de concessão
* Lease Blob  

### <a name="pessimistic-concurrency-for-containers"></a>Simultaneidade pessimista para contêineres
Concessões em contêineres habilitar Olá mesmo toobe de estratégias de sincronização tem suporte em blobs (compartilhado Gravação exclusiva, leitura / gravação exclusivo / exclusivo de leitura e compartilhados de gravação / leitura exclusivo) no entanto Diferentemente de blobs de serviço de armazenamento de saudação apenas impõe exclusividade em operações de exclusão. toodelete um contêiner com uma concessão ativa, um cliente deve incluir a ID da concessão ativa Olá na solicitação de exclusão de saudação. Todas as outras operações de contêiner bem-sucedida em um contêiner concedido sem incluir a ID de concessão Olá caso em que eles são compartilhados operações. Se a exclusividade das operações de leitura ou atualização (colocação ou definição) for obrigatória, os desenvolvedores devem garantir que todos os clientes usem uma ID de concessão e que apenas um cliente de cada vez tenha uma ID de concessão válida.  

Olá seguintes operações de contêiner podem usar simultaneidade pessimista do concessões toomanage:  

* Delete Container
* Get Container Properties
* Get Container Metadata
* Set Container Metadata
* Get Container ACL
* Set Container ACL
* Lease Container  

Para obter mais informações, consulte:  

* [Especificando cabeçalhos condicionais para operações do serviço Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Lease Container](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Lease Blob ](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Gerenciar a simultaneidade no hello serviço tabela
Olá tabela usará a simultaneidade otimista como o comportamento padrão de hello quando você estiver trabalhando com entidades, ao contrário do serviço de blob Olá onde você deve escolher explicitamente tooperform verificações de simultaneidade otimista. Olá outra diferença entre os serviços blob e tabela Olá é que você só pode gerenciar o comportamento de simultaneidade de saudação de entidades, enquanto com o serviço blob hello, você pode gerenciar a simultaneidade de saudação de contêineres e blobs.  

simultaneidade otimista toouse e toocheck se outro processo modificado uma entidade porque foi recuperado do serviço de armazenamento de tabela hello, você pode usar o valor de ETag Olá que você recebe ao serviço de tabela Olá retorna uma entidade. estrutura de tópicos Hello desse processo é o seguinte:  

1. Recuperar uma entidade de serviço de armazenamento de tabela hello, resposta Olá inclui um valor de ETag que identifica o identificador atual de saudação associado a essa entidade no serviço de armazenamento de saudação.
2. Quando você atualizar entidade hello, incluir o valor de ETag de saudação recebido na etapa 1 do hello obrigatório **If-Match** cabeçalho de solicitação Olá enviar toohello serviço.
3. serviço Olá compara o valor de ETag de saudação na solicitação de saudação com valor de ETag atual Olá da entidade de saudação.
4. Se Olá atual ETag da entidade de saudação for diferente do hello ETag no hello obrigatório **If-Match** cabeçalho na solicitação hello, serviço Olá retorna um 412 erro ao cliente toohello. Isso indica o cliente toohello que outro processo atualizou entidade Olá desde que o cliente Olá recuperá-lo.
5. Se o valor atual de ETag Olá da entidade de saudação é Olá mesmo Olá ETag no hello obrigatório **If-Match** cabeçalho na solicitação de saudação ou hello **If-Match** cabeçalho contém um caractere curinga de saudação (*), o serviço de saudação executa Olá solicitada de atualizações e operação Olá ETag atual da saudação tooshow de entidade que foi atualizado.  

Observe que, ao contrário do serviço de blob hello, serviço de tabela Olá requer Olá cliente tooinclude um **If-Match** cabeçalho em solicitações de atualização. No entanto, é possível tooforce um incondicional (último gravador wins estratégia) de atualização e ignorar verificações de simultaneidade se cliente Olá define Olá **If-Match** cabeçalho toohello caractere curinga (*) solicitação hello.  

saudação de trecho de código c# a seguir mostra uma entidade customer que anteriormente foi criada ou recuperado com o seu endereço de email atualizado. Hello inicial inserir ou recuperar o valor de ETag de Olá operação lojas no objeto de saudação do cliente e como usa o exemplo hello hello mesma instância de objeto quando ele executa Olá operação de substituição, ele envia automaticamente o serviço de tabela toohello back do valor de ETag Olá, Habilitando o Olá serviço toocheck violações de concorrência. Se outro processo atualizou a entidade Olá no armazenamento de tabela, o serviço de saudação retornará uma mensagem de status HTTP 412 (Falha na Precondição).  Você pode baixar o exemplo completo de saudação aqui: [simultaneidade gerenciar usando o armazenamento do Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly Desabilitar verificação de simultaneidade hello, você deve definir Olá **ETag** propriedade Olá **funcionário** objeto muito "*" antes de executar a operação de substituição de saudação.  

```csharp
customer.ETag = "*";  
```

Olá tabela a seguir resume como as operações de entidade de tabela Olá usam valores de ETag:

| Operação | Retorna o valor de ETag | Requer o cabeçalho de solicitação If-Match |
|:--- |:--- |:--- |
| Query Entities |Sim |Não |
| Insert Entity |Sim |Não |
| Update Entity |Sim |Sim |
| Merge Entity |Sim |Sim |
| Delete Entity |Não |Sim |
| Insert or Replace Entity |Sim |Não |
| Insert or Merge Entity |Sim |Não |

Observe que Olá **inserir ou substituir entidade** e **inserir ou mesclar entidade** operações *não* executar verificações de simultaneidade, porque eles não enviam um toohello de valor de ETag serviço de tabela.  

Em geral, os desenvolvedores usando tabelas devem recorrer à simultaneidade otimista ao desenvolver aplicativos escalonáveis. Se pessimista é necessária, os desenvolvedores de uma abordagem podem levar ao acessar tabelas é tooassign um blob designado para cada tabela e tente tootake uma concessão no blob de saudação antes de operar em tabela hello. Essa abordagem exige Olá aplicativo tooensure acesso a dados todos os caminhos de obter Olá concessão anterior toooperating na tabela de saudação. Observe também que o tempo de concessão mínimo Olá é 15 segundos que requer consideração cuidadosa para escalabilidade.  

Para obter mais informações, consulte:  

* [Operações em entidades](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Gerenciar a simultaneidade no hello serviço fila
Um cenário que no qual simultaneidade é um problema no serviço de enfileiramento de saudação é onde vários clientes recuperar mensagens de uma fila. Quando uma mensagem é recuperada da fila de hello, resposta Olá inclui mensagem de saudação e um valor de recebimento pop, que é a mensagem de saudação toodelete necessária. mensagem de saudação não é excluída automaticamente da fila hello, mas depois que forem recuperado, não é visível tooother clientes Olá intervalo de tempo especificado pelo parâmetro de visibilitytimeout hello. cliente Olá que recupera a mensagem de saudação é mensagem de saudação toodelete esperado depois que foi processado, e antes de saudação tempo especificado por Olá TimeNextVisible elemento de saudação resposta, que é calculado com base no valor Olá Olá visibilitytimeout parâmetro. valor Olá visibilitytimeout é adicionado toohello tempo no qual Olá mensagem é recuperada valor Olá toodetermine TimeNextVisible.  

serviço de fila de saudação não tem suporte para simultaneidade otimista ou pessimista e para este mensagens recuperadas da fila de processamento de clientes de razão devem Verifique se as mensagens são processadas de forma idempotentes. A estratégia último a gravar vence é usada para operações de atualização, como SetQueueServiceProperties, SetQueueMetaData, SetQueueACL e UpdateMessage.  

Para obter mais informações, consulte:  

* [API REST do serviço Fila](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [Receber mensagens](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Gerenciar a simultaneidade no hello serviço de arquivos
serviço de arquivo Hello pode ser acessado usando dois protocolo diferentes pontos de extremidade – SMB e REST. Olá serviço REST não tem suporte para bloqueio otimista ou pessimista e todas as atualizações seguirão uma estratégia de wins último gravador. Os clientes SMB que montagem compartilhamentos de arquivos podem aproveitar o bloqueio mecanismos toomanage acesso tooshared arquivos do sistema – incluindo Olá capacidade tooperform pessimista. Quando um cliente SMB abre um arquivo, ele especifica o acesso ao arquivo hello e compartilhamento de modo. Definir uma opção de acesso de arquivo de "Gravação" ou "Leitura/gravação" junto com um modo de compartilhamento de arquivos de "None" resultará no arquivo hello está sendo bloqueado por um cliente SMB até que o arquivo hello está fechado. Se a operação REST é tentada em um arquivo em que um cliente SMB tem arquivo hello bloqueado Olá serviço REST retornará o código de status 409 (conflito) com código de erro sharingviolation, uma vez.  

Quando um cliente SMB abre um arquivo para exclusão, ele marca arquivo hello como exclusão pendente até que todos os outros clientes SMB identificadores abertos no arquivo estão fechados. Enquanto um arquivo estiver marcado como com exclusão pendente, todas as operações REST em tal arquivo retornarão o código de status 409 (Conflito) com o código de erro SMBDeletePending. Código de status 404 (não encontrado) não é retornado como é possível de saudação do hello SMB cliente tooremove arquivos de saudação exclusão sinalizador tooclosing anterior pendentes. Em outras palavras, o código de status 404 (não encontrado) só é esperado quando o arquivo hello foi removido. Observe que enquanto um arquivo está em um SMB de estado de exclusão pendente, ele não será incluído no hello que arquivos da lista de resultados. Além disso, observe que as operações de REST excluir arquivo e excluir o diretório de saudação são confirmadas atomicamente e não resultam em um estado de exclusão pendente.  

Para obter mais informações, consulte:  

* [Gerenciando bloqueios de arquivo](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Resumo e próximas etapas
Olá serviço de armazenamento do Microsoft Azure projetado toomeet necessidades de saudação de aplicativos online mais complexos de saudação sem fazer com que os desenvolvedores toocompromise ou Repense na chave suposições de design, como a consistência de dados e de simultaneidade que entram tootake para concedidas.  

Para Olá conclua o aplicativo de exemplo referenciado neste blog:  

* [Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Para obter mais informações sobre Armazenamento do Azure, consulte:  

* [Página inicial do Armazenamento do Microsoft Azure](https://azure.microsoft.com/services/storage/)
* [Introdução tooAzure armazenamento](storage-introduction.md)
* Introdução ao Armazenamento para [Blob](../blobs/storage-dotnet-how-to-use-blobs.md), [Tabela](../../cosmos-db/table-storage-how-to-use-dotnet.md), [Filas](../storage-dotnet-how-to-use-queues.md) e [Arquivos](../storage-dotnet-how-to-use-files.md)
* Arquitetura de Armazenamento – [Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx) (Armazenamento do Azure: um serviço de armazenamento em nuvem altamente disponível com coerência forte)

