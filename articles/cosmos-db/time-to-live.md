---
title: dados de aaaExpire no banco de dados do Azure Cosmos com tempo toolive | Microsoft Docs
description: "Com TTL, o banco de dados do Microsoft Azure Cosmos fornece documentos de toohave de capacidade de saudação automaticamente excluídos do sistema Olá após um período de tempo."
services: cosmos-db
documentationcenter: 
keywords: tempo toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Expirar os dados em coleções do banco de dados do Azure Cosmos automaticamente com o tempo toolive
Os aplicativos podem gerar e armazenar grandes quantidades de dados. Alguns desses dados, como dados de evento, logs e informações da sessão do usuário gerados por computador, são úteis apenas por determinado período. Quando dados saudação se torna toohello excedente necessidades do aplicativo hello é seguro toopurge esses dados e reduz a necessidade de armazenamento de saudação de um aplicativo.

"Tempo toolive" ou TTL, o banco de dados do Microsoft Azure Cosmos fornece documentos de toohave de capacidade Olá limpos automaticamente do banco de dados de saudação após um período de tempo. tempo de padrão de saudação toolive pode ser definido no nível de coleção hello e substituído em uma base por documento. Depois de definir a TTL como um padrão de coleta ou em um nível de documento, o Cosmos DB removerá automaticamente os documentos existentes após esse período, em segundos, desde sua última modificação.

Tempo toolive no banco de dados do Cosmos usa um deslocamento em relação ao documento hello foi modificada pela última vez. toodo este TI utiliza Olá `_ts` campo que existe em todos os documentos. campo de TS Olá é estilo unix época timestamp representando Olá data e hora. Olá `_ts` campo é atualizado sempre que um documento é modificado. 

## <a name="ttl-behavior"></a>Comportamento de TTL
recurso TTL Olá é controlado pelas propriedades TTL em dois níveis - nível de documento hello e coleção de saudação. os valores Hello são definidos em segundos e são tratados como um delta de saudação `_ts` documento hello foi modificada pela última vez em.

1. DefaultTTL para coleção Olá
   
   * Se ausente (ou conjunto toonull), documentos não são excluídos automaticamente.
   * Se estiver presente e o valor de saudação é "-1" = infinito – documentos não expiram por padrão
   * Se estiver presente e o valor de saudação é um número ("n") – documentos expiram "n" segundos depois da última modificação
2. Tempo de vida para documentos de saudação: 
   
   * Propriedade é aplicável somente se DefaultTTL está presente para da coleção pai hello.
   * Substitui Olá DefaultTTL valor da coleção pai hello.

Assim que o documento de saudação expirou (`ttl`  +  `_ts` > = hora atual do servidor), Olá é marcada como "expirado". Nenhuma operação poderá ser nesses documentos depois desse período e elas serão excluídas dos resultados de saudação de todas as consultas executadas. documentos de saudação são fisicamente no sistema de saudação e são excluídos no plano de fundo de saudação oportunamente mais tarde. Isso não consumir qualquer [unidades de solicitação (RUs)](request-units.md) orçamento de coleção de saudação.

Olá acima lógica pode ser mostrado no Olá matriz a seguir:

|  | DefaultTTL ausente ou não definido na coleção de saudação | DefaultTTL = -1 na coleção | DefaultTTL = “n” na coleção |
| --- |:--- |:--- |:--- |
| TTL Ausente no documento |Nada toooverride no nível do documento como documento hello e coleção não tem nenhum conceito de TTL. |Nenhum documento nesta coleção expirará. |documentos de saudação nesta coleção expirará quando n intervalo expira. |
| TTL = -1 no documento |Nada toooverride no nível do documento hello desde que não define a coleção Olá Olá propriedade DefaultTTL que pode substituir um documento. Tempo de vida de um documento é não interpretado pelo sistema hello. |Nenhum documento nesta coleção expirará. |documento de saudação com TTL =-1 nesta coleção nunca expirará. Todos os outros documentos expirarão após o intervalo de “n”. |
| TTL = n no documento |Nada toooverride no nível do documento hello. TTL em um documento não interpretada pelo sistema hello. |documento de saudação com TTL = n expirará após n de intervalo, em segundos. Os outros documentos herdarão o intervalo de -1 e nunca expirarão. |documento de saudação com TTL = n expirará após n de intervalo, em segundos. Outros documentos herdará o intervalo de "n" da coleção de saudação. |

## <a name="configuring-ttl"></a>Configurando a TTL
Por padrão, o tempo toolive é desabilitado por padrão em todas as coleções de banco de dados do Cosmos e em todos os documentos.

## <a name="enabling-ttl"></a>Habilitando a TTL
tooenable TTL em uma coleção ou documentos hello dentro de uma coleção, você precisa de propriedade de DefaultTTL Olá tooset de uma coleção de tooeither -1 ou um número positivo diferente de zero. A configuração Olá DefaultTTL muito-1 significa que por padrão todos os documentos na coleção de saudação operará sempre mas Olá serviço Cosmos DB deve monitorar essa coleção para documentos que tenham substituído esse padrão.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Configurando a TTL padrão em uma coleção
Você está tooconfigure capaz de um tempo padrão toolive em um nível de coleção. Olá tooset TTL em uma coleção, você precisa tooprovide um número positivo diferente de zero que indica o período de hello, em segundos, tooexpire todos os documentos na coleção de saudação depois Olá modificado pela última vez timestamp do documento hello (`_ts`). Ou, você pode definir o saudação padrão muito-1, o que significa que todos os documentos inseridos na coleção toohello operará indefinidamente por padrão.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Configurando a TTL em um documento
Além disso toosetting um TTL padrão em uma coleção você pode definir o TTL específico em um nível de documento. Isso substituirá o padrão de saudação da coleção de saudação.

* Olá tooset TTL em um documento, você precisa tooprovide Olá a um número positivo diferente de zero, que indica o período, em segundos, o documento de saudação tooexpire depois Olá modificado pela última vez timestamp do documento hello (`_ts`).
* Se um documento não tem nenhum campo TTL, Olá, em seguida, o padrão de coleção de saudação será aplicada.
* Se o TTL for desabilitado no nível de coleção hello, campo TTL Olá no documento hello será ignorado até que o TTL seja habilitada novamente na coleção de saudação.

Aqui está um trecho de código mostrando como tooset Olá expiração do TTL em um documento:

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>Estendendo a TTL em um documento existente
Você pode redefinir Olá TTL em um documento, fazendo a qualquer operação de gravação no documento de saudação. Isso definirá Olá `_ts` toohello hora atual e Olá contagem regressiva toohello documento expiração, conforme definido pela Olá `ttl`, começará novamente. Se você quiser Olá toochange `ttl` de um documento, você pode atualizar o campo de saudação como você pode fazer com que qualquer outro campo configurável.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Removendo a TTL de um documento
Se um TTL tiver sido definido em um documento e você não deseja mais que tooexpire de documento, você pode recuperar documento hello, remover o campo TTL hello e substituir Olá documento no servidor de saudação. Quando o campo TTL Olá é removido do documento hello, Olá padrão da coleção de saudação será aplicado. toostop um documento de expiração e não herda da coleção hello, em seguida, você precisa tooset Olá TTL valor muito-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>Desabilitando a TTL
toodisable TTL inteiramente em uma coleção e o plano de fundo de saudação parar processo de procurar documentos expirados Olá DefaultTTL na coleção de saudação deve ser excluído. A exclusão desta propriedade é diferente da definição de muito-1. A configuração de muito-1 significa novos documentos adicionado toohello coleção operará para sempre, mas você pode substituí-lo em documentos específicos na coleção de saudação. Remover essa propriedade inteiramente de coleção de saudação significa que documentos não vai expirar, mesmo se houver documentos que tenham substituído explicitamente o padrão anterior.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>Perguntas frequentes
**Qual o preço da TTL?**

Não há nenhum custo adicional de toosetting TTL em um documento.

**Quanto tempo levará toodelete documento depois Olá TTL está ativo?**

documentos de saudação expirados imediatamente depois de saudação TTL está ativo e não poderão ser acessada por meio de CRUD ou APIs de consulta. 

**A TTL em um documento terá algum impacto sobre os encargos de RU?**

Não haverá nenhum impacto nos encargos de RU para as exclusões de documentos expirados por meio da TTL no Cosmos DB.

**Recurso TTL Olá apenas aplica tooentire documentos ou podem expirar valores de propriedade de documento individuais?**

TTL se aplica a todo o documento toohello. Se você gostaria que tooexpire apenas uma parte de um documento, ele é recomendável que você extrair parte de saudação do documento principal de saudação tooa documento separado de "vinculado" e, em seguida, use o TTL nesse documento extraída.

**Recurso TTL Olá tem os requisitos específicos de indexação?**

Sim. Olá coleção deve ter [conjunto de política de indexação](indexing-policies.md) tooeither consistente ou Lazy. Tentar tooset DefaultTTL em uma coleção com indexação conjunto tooNone resultará em um erro, assim como tooturn tentar desativar a indexação em uma coleção que tem um DefaultTTL já definido.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre Azure Cosmos DB, consulte serviço toohello [ *documentação* ](https://azure.microsoft.com/documentation/services/cosmos-db/) página.

