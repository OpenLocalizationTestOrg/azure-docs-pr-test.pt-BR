---
title: "aaaRequest unidades e taxa de transferência estimando - banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba mais sobre como toounderstand, especifique e estimar os requisitos de unidade de solicitação no banco de dados do Azure Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Unidades de Solicitação no Azure Cosmos DB
Agora disponível: [calculadora de unidades de solicitação](https://www.documentdb.com/capacityplanner) do Azure Cosmos DB. Saiba mais em [Estimativa das necessidades de produção](request-units.md#estimating-throughput-needs).

![Calculadora de produtividade][5]

## <a name="introduction"></a>Introdução
O [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) é o multimodelo de banco de dados distribuído globalmente da Microsoft. Com o banco de dados do Azure Cosmos, você não tem máquinas virtuais de toorent, implantar o software ou monitorar bancos de dados. Banco de dados do Azure Cosmos é operado e continuamente monitorado pelo Microsoft engenheiros superior toodeliver world classe disponibilidade, desempenho e proteção de dados. Você pode acessar seus dados usando as APIs de sua preferência, como [SQL do DocumentDB](documentdb-sql-query.md) (documento), MongoDB (documento), [Armazenamento de Tabelas do Azure](https://azure.microsoft.com/services/storage/tables/) (chave-valor) e [Gremlin](https://tinkerpop.apache.org/gremlin.html) (gráfico), todas com suporte nativo. moeda de saudação do banco de dados do Azure Cosmos é hello unidade de solicitação (RU). Com RUs, não é necessário tooreserve capacidades de leitura/gravação ou provisionar CPU, memória e IOPS.

Banco de dados do Azure Cosmos dá suporte a várias APIs com operações diferentes, variando de leituras simples e grava toocomplex consultas de gráfico. Como nem todas as solicitações são iguais, eles recebem uma quantidade normalizada de **unidades de solicitação** com base na quantidade de saudação da solicitação de saudação do computação tooserve necessária. número de saudação de unidades de solicitação para uma operação é determinístico, e você pode acompanhar o número de saudação de unidades de solicitação consumidos por qualquer operação no banco de dados do Azure Cosmos por meio de um cabeçalho de resposta. 

tooprovide um desempenho previsível, você precisa de taxa de transferência tooreserve em unidades de 100 RU/segundo. 

Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:  

* O que são unidades de solicitação e solicitações de encargos?
* Como especificar a capacidade da unidade de solicitação para uma coleção?
* Como estimar as necessidades de unidades de solicitação de meu aplicativo?
* O que acontecerá se eu exceder a capacidade da unidade de solicitação de uma coleção?

Como o banco de dados do Azure Cosmos é um banco de dados de vários modelo, é importante toonote que chamaremos tooa coleta/documento para um documento de API, um nó do gráfico/com a API do graph e uma tabela/entidade para a API de tabela. Taxa de transferência neste documento generalizaremos toohello conceitos de contêiner/item.

## <a name="request-units-and-request-charges"></a>Unidades de solicitação e solicitações de encargos
Banco de dados do Azure Cosmos oferece desempenho rápido e previsível por *reservar* toosatisfy recursos taxa de transferência do seu aplicativo precisa.  Porque o aplicativo de carga e acessar a mudança nos padrões ao longo do tempo, o banco de dados do Azure Cosmos permite tooeasily aumentar ou diminuir a quantidade de saudação do aplicativo de tooyour disponíveis de produtividade reservados.

Com o Azure Cosmos DB, a produtividade reservada é especificada em termos de processamento de unidades de solicitação por segundo. Você pode pensar unidades de solicitação como moeda da taxa de transferência, no qual você *reservar* garantia de uma quantidade de unidades de solicitação disponíveis tooyour aplicativo por segundo.  Cada operação do Azure Cosmos DB – gravar um documento, realizar uma consulta, atualizar um documento – consome CPU, memória e IOPS.  Ou seja, cada operação resulta em um *encargo de solicitação*, que é expressa em *unidades de solicitação*.  Noções básicas sobre fatores de saudação que afetam as cobranças de unidade de solicitação, juntamente com requisitos de taxa de transferência do seu aplicativo, permite que você toorun seu aplicativo como custo com eficiência possível. Pesquisador de objetos de consulta Olá também é um núcleo de saudação tootest ferramenta excelente de uma consulta.

É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde Aravind Ramachandran explica unidades de solicitação e um desempenho previsível com o banco de dados do Azure Cosmos.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Especificando a capacidade de unidades de solicitação no Azure Cosmos DB
Ao iniciar uma nova coleção, tabela ou gráfico, você especificar o número de saudação de unidades de solicitação por segundo (RU por segundo) que você deseja reservado. Com base na taxa de transferência fornecida hello, o banco de dados do Azure Cosmos aloca partições físicas toohost sua coleção e divisões/rebalances dados em partições à medida que cresce.

Banco de dados do Azure Cosmos requer que um toobe de chave de partição especificado quando uma coleção é provisionado com 2.500 unidades de solicitação ou superior. Uma chave de partição é tooscale necessário também taxa de transferência da coleção além 2.500 unidades de solicitação no hello futuras. Portanto, é altamente recomendável tooconfigure um [chave de partição](partition-data.md) ao criar um contêiner, independentemente da taxa de transferência inicial. Como os dados podem ter toobe divididos em várias partições, é necessário toopick uma chave de partição que tenha uma alta cardinalidade (100 toomillions de valores distintos), para que seu gráfico/de tabela de coleta e solicitações podem ser dimensionadas uniformemente por banco de dados do Azure Cosmos. 

> [!NOTE]
> Uma chave de partição é um limite lógico e não físico. Portanto, não é necessário toolimit número de saudação dos valores de chave de partição distintos. Na verdade é melhor toohave distinto particionar os valores de chave que menor, como o banco de dados do Azure Cosmos tem mais opções de balanceamento de carga.

Aqui está um trecho de código para criar uma coleção com 3.000 unidades por segundo usando Olá SDK .NET de solicitação:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

O Azure Cosmos DB opera em um modelo de reserva na produtividade. Ou seja, você será cobrado pela quantidade de saudação de taxa de transferência *reservado*, independentemente de quantos essa taxa de transferência é ativamente *usado*. Como uso, dados e carga padrões alteração seu aplicativo você pode facilmente aumentar e diminuir Olá quantidade de RUs reservados por meio de SDKs ou usando Olá [Portal do Azure](https://portal.azure.com).

Cada coleção/tabela/gráfico são mapeados tooan `Offer` recursos no Azure Cosmos DB, que tem metadados sobre a taxa de transferência fornecida hello. Você pode alterar o throughput Olá alocada pesquisando o recurso de oferta correspondente Olá para um contêiner, em seguida, atualizá-lo com o novo valor de taxa de transferência hello. Aqui está um trecho de código para alterar a taxa de transferência de saudação de uma coleção too5, 000 unidades de solicitação por segundo usando Olá .NET SDK:

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Não há toohello sem causar impacto na disponibilidade do seu contêiner quando você alterar a taxa de transferência de saudação. Normalmente reservado novos Olá de taxa de transferência é efetivo em segundos no aplicativo de taxa de transferência nova hello.

## <a name="request-unit-considerations"></a>Considerações sobre unidades de solicitação
Ao estimar o número de saudação do tooreserve de unidades de solicitação para o contêiner de banco de dados do Azure Cosmos, é importante tootake Olá variáveis a seguir em consideração:

* **Tamanho do item**. Olá unidades consumidas tooread aumenta o tamanho ou gravar dados de saudação também aumentará.
* **Contagem de propriedades do item**. Supondo que a indexação de padrão de todas as propriedades, Olá unidades consumidas toowrite um documento/nó/ntity aumentará o aumento do número de propriedade hello.
* **Consistência de dados**. Ao usar níveis de consistência de dados de alta segurança ou envelhecimento limitado, unidades adicionais será consumido tooread itens.
* **Propriedades indexadas**. Uma política de índice em cada contêiner determina quais propriedades são indexadas por padrão. Você pode reduzir o consumo de unidade de solicitação, limitando o número de saudação de propriedades indexadas ou habilitando o recurso de indexação lento.
* **Indexação de documentos**. Por padrão a que cada item é indexado automaticamente, consumirá menos unidades de solicitação se você escolher não tooindex alguns de seus itens.
* **Padrões de consulta**. complexidade de saudação de uma consulta afeta quantas unidades de solicitação são consumidas para uma operação. número de saudação de predicados, natureza dos predicados hello, projeções, número de UDFs e tamanho de saudação do conjunto de dados de origem Olá todos influenciam o custo de saudação de operações de consulta.
* **Uso de scripts**.  Assim como acontece com consultas, procedimentos armazenados e gatilhos consumam unidades de solicitação com base em complexidade Olá das operações de saudação que está sendo executada. À medida que desenvolve seu aplicativo, inspecionar a carga de solicitação Olá cabeçalho toobetter entender como cada operação está consumindo a capacidade da unidade de solicitação.

## <a name="estimating-throughput-needs"></a>Estimativa das necessidades de produção
Uma unidade de solicitação é uma medida normalizada de custo de processamento de solicitação. Uma unidade única solicitação representa Olá processamento capacidade necessária tooread (via autolink ou id) um único 1KB item consiste em 10 valores de propriedade unique (excluindo as propriedades do sistema). Uma solicitação toocreate (inserir), substituir ou excluir Olá mesmo item consumirá mais processamento do serviço de saudação e, portanto, mais unidades de solicitação.   

> [!NOTE]
> linha de base de saudação da unidade de solicitação de 1 para 1KB item corresponde tooa simple obter self link ou a id do item de saudação.
> 
> 

Por exemplo, aqui está uma tabela que mostra a solicitação de quantas unidades tooprovision em três tamanhos de item diferentes (1KB, 4KB e 64KB) e em dois níveis diferentes de desempenho (leituras de 500/segundo 100 gravações por segundo e 500 leituras/segundo + 500 gravações por segundo). consistência de dados Olá foi configurada na sessão e Olá política de indexação foi definido tooNone.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Tamanho do item</strong></p></td>
            <td valign="top"><p><strong>Leituras/segundo</strong></p></td>
            <td valign="top"><p><strong>Gravações/segundo</strong></p></td>
            <td valign="top"><p><strong>Unidades de solicitação</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1.000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3.000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1,3) + (100 * 7) = 1.350 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1,3) + (500 * 7) = 4.150 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9.800 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29.000 RU/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Use a Calculadora de unidade de solicitação Olá
problemas de clientes toohelp ajustar suas estimativas de taxa de transferência, não há um baseado na web [Calculadora de unidade de solicitação](https://www.documentdb.com/capacityplanner) toohelp estimar Olá solicitação unidade requisitos para operações comuns, incluindo:

* Criações de itens (gravações)
* Leituras de itens
* Exclusões de itens
* Atualizações de itens

ferramenta de saudação também inclui suporte para estimar as necessidades de armazenamento de dados com base nos itens do exemplo hello que você fornecer.

Usando a ferramenta de saudação é simple:

1. Carregue um ou mais itens representativos.
   
    ![Carregar o cálculo de unidade de solicitação de toohello itens][2]
2. requisitos de armazenamento de dados tooestimate, insira o número total de saudação de itens esperada toostore.
3. Inserir número Olá de itens a criar, ler, atualizar e excluir operações requer (em uma base por segundo). encargos de unidade de solicitação tooestimate Olá de operações de atualização de item, carregue uma cópia do item do exemplo hello da etapa 1 acima, o que inclui atualizações de campo típico.  Por exemplo, se as atualizações de item normalmente modificam duas propriedades chamadas lastLogin e userVisits, simplesmente copiar item do exemplo hello, atualizar Olá valores para essas duas propriedades e carregar item Olá copiado.
   
    ![Insira os requisitos de taxa de transferência no cálculo de unidade de solicitação Olá][3]
4. Clique em calcular e examine os resultados de saudação.
   
    ![Resultados da calculadora de unidade de solicitação][4]

> [!NOTE]
> Se você tiver tipos de item que serão muito diferente em termos de tamanho e hello número de propriedades indexadas, em seguida, carregue um exemplo de cada *tipo* de item típico toohello ferramenta e, em seguida, calcular os resultados de saudação.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Use o cabeçalho de resposta de custos do hello Azure Cosmos DB solicitação
Cada resposta do hello Azure Cosmos DB serviço inclui um cabeçalho personalizado (`x-ms-request-charge`) que contém unidades de solicitação Olá consumidas para solicitação de saudação. Esse cabeçalho também é acessível por meio de saudação do Azure Cosmos SDKs do banco de dados. Em Olá .NET SDK, RequestCharge é uma propriedade do objeto de ResourceResponse hello.  Para consultas, Olá Gerenciador de consulta de banco de dados do Azure Cosmos em Olá portal do Azure fornece informações de taxa de solicitação para consultas executadas.

![Examinando os encargos de RU no hello Pesquisador de objetos de consulta][1]

Com isso em mente, um método para calcular a quantidade de saudação de produtividade reservados exigida por seu aplicativo é associado à execução de operações típicas em relação a um representante item usado pelo seu aplicativo dos custos de unidade de solicitação toorecord hello e, em seguida, estimar Olá número de operações você antecipar executando a cada segundo.  Ser toomeasure se e incluem consultas típicas e uso de script de banco de dados do Azure Cosmos também.

> [!NOTE]
> Se você tiver tipos de item que serão muito diferente em termos de tamanho e hello número de propriedades indexadas, registre associada a cada carga de unidade Olá operação aplicável solicitação *tipo* de item típico.
> 
> 

Por exemplo:

1. Registre os custos de unidade de solicitação de saudação de criação (inserir) um item típico. 
2. Encargo de unidade de solicitação de registro Olá de leitura de um item típico.
3. Custos de unidade de solicitação de registro Olá de atualização de um item típico.
4. Encargo de unidade de solicitação Olá registro de consultas de item típico, comuns.
5. Olá registro solicitação unidade encargo de quaisquer scripts personalizados (procedimentos armazenados, disparadores, funções definidas pelo usuário) utilizado pelo aplicativo hello
6. Calcule a solicitação de necessária Olá que unidades especificadas Olá estimada o número de operações você antecipar toorun por segundo.

### <a id="GetLastRequestStatistics"></a>Usar o comando GetLastRequestStatistics da API para MongoDB
API para o MongoDB dá suporte a um comando personalizado, *getLastRequestStatistics*, para recuperar a taxa de solicitação de saudação para operações especificadas.

Por exemplo, em Olá Shell Mongo, execute operação de Olá que deseja tooverify Olá solicitação gratuitamente.
```
> db.sample.find()
```

Em seguida, execute o comando Olá *getLastRequestStatistics*.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

Com isso em mente, um método para calcular a quantidade de saudação de produtividade reservados exigida por seu aplicativo é associado à execução de operações típicas em relação a um representante item usado pelo seu aplicativo dos custos de unidade de solicitação toorecord hello e, em seguida, estimar Olá número de operações você antecipar executando a cada segundo.

> [!NOTE]
> Se você tiver tipos de item que serão muito diferente em termos de tamanho e hello número de propriedades indexadas, registre associada a cada carga de unidade Olá operação aplicável solicitação *tipo* de item típico.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>Usar as métricas de portal da API para MongoDB
Olá tooget de maneira mais simples uma boa estimativa da unidade de solicitação de encargos para a sua API para o banco de dados do MongoDB é toouse Olá [portal do Azure](https://portal.azure.com) métricas. Com hello *o número de solicitações* e *custos de solicitação* gráficos, você pode obter uma estimativa de quantas unidades de solicitação cada operação de consumo e quantas unidades de solicitação consomem relativo tooone outro.

![Métricas do portal da API para MongoDB][6]

## <a name="a-request-unit-estimation-example"></a>Um exemplo de estimativa de unidade de solicitação
Considere Olá aproximadamente 1KB documento a seguir:

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> Documentos são minimizados no banco de dados do Azure Cosmos, portanto calculado pelo sistema Olá tamanho do documento de saudação acima é um pouco menos de 1KB.
> 
> 

Hello tabela a seguir mostra a solicitação aproximada encargos de unidade para operações típicas neste item (encargos de unidade de solicitação aproximado Olá presume que o nível de consistência de conta Olá é definido muito "Sessão" e todos os itens são indexados automaticamente):

| Operação | Encargo de Unidade de Solicitação |
| --- | --- |
| Criar item |Cerca de 15 RUs |
| Ler item |Cerca de 1 RU |
| Consultar item por ID |Cerca de 2,5 RUs |

Além disso, esta tabela mostra solicitação aproximada encargos de unidade para consultas típicas usadas no aplicativo hello:

| Consultar | Encargo de Unidade de Solicitação | Nº de itens retornados |
| --- | --- | --- |
| Selecionar alimentos por id |Cerca de 2,5 RUs |1 |
| Selecionar alimentos por fabricante |Cerca de 7 RUs |7 |
| Selecionar por grupo de alimentos e solicitar por peso |Cerca de 70 RUs |100 |
| Selecionar os 10 alimentos principais em um grupo de alimentos |Cerca de 10 RUs |10 |

> [!NOTE]
> Encargos de RU variam com base no número de saudação de itens retornados.
> 
> 

Com essas informações, podemos estimar requisitos de RU saudação do número de saudação desse aplicativo considerando de operações e consultas que esperamos por segundo:

| Operação/consulta | Número estimado por segundo | RUs necessárias |
| --- | --- | --- |
| Criar item |10 |150 |
| Ler item |100 |100 |
| Selecionar alimentos por fabricante |25 |175 |
| Selecionar por grupo de alimentos |10 |700 |
| Selecionar os 10 principais |15 |Total de 150 |

Nesse caso, esperamos um requisito de taxa de transferência médio de 1.275 RUs/s.  Arredondamento toohello mais próximo de 100, seriam provisionar 1.300 RU/s para a coleção deste aplicativo.

## <a id="RequestRateTooLarge"></a> Excedendo os limites de produtividade reservada no Azure Cosmos DB
Lembre-se de que o consumo de unidade de solicitação é avaliado como uma taxa por segundo se orçamento hello está vazio. Para aplicativos que excedem Olá taxa de solicitação de provisionamento de unidade para um contêiner, solicitações toothat coleção será limitada até que a taxa de saudação cai abaixo de nível de saudação reservada. Quando ocorre uma limitação, o servidor de saudação preventivamente terminará solicitação Olá com RequestRateTooLargeException (código de status HTTP 429) e retorno Olá o cabeçalho x-ms-repetição-após-ms indicando de saudação período de tempo, em milissegundos, que Olá usuário deve aguardar antes de tentar novamente a solicitação de saudação.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

Se você estiver usando consultas de SDK de cliente .NET e LINQ hello e maior parte do tempo de saudação nunca tiver toodeal com esta exceção, como a versão atual de saudação do hello SDK de cliente .NET implicitamente captura essa resposta, aspectos Olá servidor especificado cabeçalho retry-after, e solicitação de saudação de repetições. A menos que sua conta está sendo acessada simultaneamente por vários clientes, a próxima repetição de saudação terá êxito.

Se você tiver mais de um cliente cumulativamente operando acima a taxa de solicitação hello, hello comportamento de repetição padrão pode não ser suficiente e cliente Olá lançará um DocumentClientException com o aplicativo de 429 toohello status código. Em casos como esse, você pode considerar o tratamento de comportamento de repetição e lógica de erro do aplicativo as rotinas de tratamento ou aumentando a taxa de transferência reservada para o contêiner de Olá Olá.

## <a id="RequestRateTooLargeAPIforMongoDB"></a> Exceder os limites de taxa de transferência reservada na API para MongoDB
Aplicativos que excedem a unidades de solicitação Olá provisionado para uma coleção serão limitados até que a taxa de saudação cai abaixo de nível de saudação reservada. Quando ocorre um acelerador, Olá back-end preventivamente terminará solicitação Olá com um *16500* código de erro - *muito muitas solicitações*. Por padrão, a API para o MongoDB automaticamente tentará too10 horas antes de retornar um *muito muitas solicitações* código de erro. Se você estiver recebendo muitas *muito muitas solicitações* códigos de erro, você pode considerar o comportamento de repetição de adição em rotinas de tratamento de erros do aplicativo ou [aumenta o processamento reservado para a coleção de saudaçãoOlá](set-throughput.md).

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre a taxa de transferência reservada com bancos de dados do banco de dados do Azure Cosmos explorar estes recursos:

* [Preços do Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Particionando dados no Azure Cosmos DB](partition-data.md)

toolearn mais sobre Azure Cosmos DB, consulte hello Azure Cosmos DB [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/). 

tooget iniciado com a escala e testes de desempenho com o Azure Cosmos DB, consulte [teste de desempenho e escala com o banco de dados do Azure Cosmos](performance-testing.md).

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
