---
title: "Azure CosmosDB: unidades de solicitação por minuto (RU/m) | Microsoft Docs"
description: "Saiba como o custo de tooreduce utilizando unidades por minuto de solicitação."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Unidades de solicitação por minuto no BD Cosmos do Azure

Banco de dados do Azure Cosmos é projetado toohelp atingir um desempenho rápido e previsível e a escala perfeitamente juntamente com o crescimento do seu aplicativo. É possível provisionar a taxa de transferência em um contêiner do BD Cosmos com granularidades por segundo e por minuto (RU/m). taxa de transferência fornecida por minuto granularidade Hello é usado toomanage inesperados picos na carga de trabalho de saudação que ocorrem em uma granularidade por segundo. 

Este artigo fornece uma visão geral de como funciona a saudação de provisionamento de unidade de solicitação por minuto (RU/m). meta de saudação em mente com provisionamento de RU/m é tooprovide um desempenho previsível em torno de necessidades imprevisíveis (especialmente se você precisa de análise de toorun sobre seus dados operacionais) e cargas de trabalho apresentar pico de uso. Queremos toohave que nossos clientes consumam mais taxa de transferência Olá que ele provisiona para que eles podem ser dimensionados rapidamente com paz de espírito.

Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:

* Como funciona uma Unidade de Solicitação por minuto?
* Qual é a diferença de saudação entre unidade de solicitação por minuto e solicitações por segundo?
* Como tooprovision RU/m?
* Em que cenário eu devo considerar o provisionamento de Unidades de Solicitação por Minuto?
* Como toouse Olá métricas portal toooptimize meu custo e desempenho?
* Definir qual tipo de solicitação pode consumir seu orçamento para RU/m?

## <a name="provisioning-request-units-per-minute-rum"></a>Provisionamento de unidades de solicitação por minuto (RU/m)

Ao provisionar o banco de dados do Azure Cosmos na granularidade de segundo hello (RU/s), você obtém garantia de saudação que sua solicitação tiver êxito em uma baixa latência se a taxa de transferência não excedeu a capacidade Olá provisionada nesse segundo. Com RU/m, a granularidade de saudação está no minuto Olá com garantia de saudação que sua solicitação tiver êxito dentro desse minuto. Em comparação com sistemas de toobursting, certifique-se de que você obtém de desempenho de Olá for previsível e você pode planejar isso.

forma de saudação por minuto provisionamento funciona é simples:

* RU/m é cobrado por hora e em adição tooRU/s. Para obter mais detalhes, visite a [página de preços](https://aka.ms/acdbpricing) do BD Cosmos do Azure.
* A RU/m pode ser habilitada no nível da coleção. Isso pode ser feito por meio de saudação SDKs (Node. js, Java ou .net) ou por meio do portal hello (também incluem as cargas de trabalho do MongoDB API)
* Quando RU/m está habilitado, para cada 100 RU/s provisionado, você também pode obter 1.000 RU/m provisionado (taxa de saudação é de 10 vezes)
* Em um determinado segundo, uma unidade de solicitação consome o provisionamento de RU/m somente se você tiver ultrapassado seu provisionamento por segundo dentro desse segundo
* Uma vez Olá termina o período de 60 segundos (UTC), Olá por minuto provisionamento é recarregado
* A RU/m pode ser habilitada apenas para coleções com provisionamento máximo de 5.000 RU/s por partição. Se dimensionar suas necessidades de taxa de transferência e tiver um alto nível de provisionamento por partição, você receberá uma mensagem de aviso

Abaixo, temos um exemplo concreto, em que um cliente pode provisionar 10kRU/s com 100kRU/m, economizando 73% dos custos em comparação com o provisionamento para o pico (com 50kRU/s) por um período de 90 segundos em uma coleção que tem 10.000 RU/s e 100.000 RU/m provisionadas:

* segundo 1º: alocação do hello RU/m é definida como 100.000
* segundo 3º: durante essa segunda Olá consumo de unidade de solicitação foi 11,010 RUs, 1,010 RUs acima Olá RU/s provisionamento. Portanto, 1,010 RUs são deduzidos do orçamento do hello RU/m. 98,990 RUs estão disponíveis para Olá próximos segundos 57 RU/m de orçamento Olá
* segundo 29: durante esse segundo, um grande aumento aconteceu (> 4 x maior do que o provisionamento por segundo) e o consumo de saudação da unidade de solicitação foi 46,920 RUs. 36,920 RUs são deduzidos do orçamento RU/m Olá descartado do 92,323 too55 de RUs (28 de segundo), 403 RUs (29 de segundo)
* segundo 61st: orçamento RU/m é redefinido too100, RUs, 000.
 
![Gráfico mostrando o consumo de saudação e provisionamento do banco de dados do Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Especificando a capacidade da unidade de solicitação com RU/m

Ao criar uma coleção de banco de dados do Azure Cosmos, você especificar o número de saudação de unidades de solicitação por segundo (RU por segundo) que você deseja reservado para a coleção de saudação. Você também pode decidir se deseja RU tooadd por minuto. Isso pode ser feito por meio de saudação Portal ou Olá SDK. 

### <a name="through-hello-portal"></a>Por meio do Portal de saudação

Para habilitar ou desabilitar a RU por minuto, basta um clique ao provisionar uma coleção. 

 ![Captura de tela mostrando como tooset RU/m em Olá portal do Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Por meio de saudação SDK
Primeiro, isso é importante toonote que RU/m só está disponível para Olá SDKs a seguir:

* .Net 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Aqui está um trecho de código para criar uma coleção com 3.000 unidades de solicitação por unidades de solicitação de segundo e 30.000 por minuto usando Olá .NET SDK:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Aqui está um trecho de código para alterar a taxa de transferência de saudação de uma coleção too5, 000 unidades de solicitação por segundo sem provisionamento RU por minuto usando Olá .NET SDK:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>Cenários adequados

Nesta seção, fornecemos uma visão geral dos cenários em que é adequado habilitar as unidades de solicitação por minuto.

**Ambiente de desenvolvimento e teste:** adequado. Durante a fase de desenvolvimento hello, se você estiver testando seu aplicativo com cargas de trabalho diferentes, RU/m pode fornecer flexibilidade Olá neste estágio. Durante a saudação [emulador](local-emulator.md) é tootest uma excelente ferramenta gratuita do Azure Cosmos DB. No entanto se você quiser toostart em um ambiente de nuvem, você terá uma grande flexibilidade com RU/m para suas necessidades de desempenho do ad hoc. Você passará mais tempo desenvolvendo e menos tempo se preocupando com as necessidades de desempenho no início. É recomendável começar com o provisionamento de saudação mínimo RU/s e habilitar RU/m.

**Necessidades imprevisíveis de granularidade por minuto, com picos de uso:** adequado – economia de 25 a 75%. Já vimos uma grande melhoria com relação à RU/m e a maioria dos cenários de produção está nesse grupo. Se você tiver uma carga de trabalho IoT tem pico algumas vezes em um minuto, se você tiver consultas em execução quando o sistema faz inserção em massa no hello mesmo tempo, você precisará de capacidade extra para necessidades handeling apresentar pico de uso. Recomendamos otimizar suas necessidades de recursos aplicando nossa abordagem passo a passo abaixo.

 ![Gráfico mostrando o consumo de solicitação com granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Figura – benchmark de consumo de RU*

**Tranquilidade:** adequado – economia de 10 a 20%. Às vezes, você apenas deseja toohave paz de espírito e não se preocupar sobre possíveis picos e limitação. Este recurso está à direita Olá um para você. Nesse caso, recomendamos habilitar a RU/m e reduzir ligeiramente seu provisionamento por segundo. Nesse caso é diferente da saudação acima como você não tentará toooptimize agressivamente o provisionamento. Trata-se de uma abordagem de "limitação zero" que você tem em mente.

As operações essenciais com necessidades de ad hoc: às vezes, é recomendável tooonly permitem operações críticas de acesso RU/m orçamento para alocação de saudação não obtenha consumir pelo ad hoc ou menos operações importantes. Que podem ser definidas facilmente na seção de saudação abaixo.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Usando Olá métricas portal toooptimize custo e desempenho

**Próximas semanas de hello, podemos desenvolverá mais conteúdo de saudação em torno de monitoramento RUs consumo minuto toooptimize que precisa de sua taxa de transferência.**

Por meio de métricas de portal hello, você pode ver a quantidade de segundos de RU regulares consumir versus RU minutos. Monitorar essas métricas deve ajudá-lo a otimizar o provisionamento. 

É recomendável uma abordagem passo a passo sobre como toouse RU/m tooyour vantagem. Para cada etapa, você deve ter uma visão geral do consumo de saudação RU representando um ciclo completo de sua carga de trabalho (pode ser horas, dias, ou até mesmo semanas) e obter informações sobre a utilização de saudação do qual você provisionar.

princípio de saudação por trás dessa abordagem é toomake o provisionamento de taxa de transferência como fechar como possíveis tooa provisão do ponto que corresponda aos critérios de desempenho abaixo. 

![Gráfico mostrando o consumo de solicitação com granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand Olá ideal provisionamento ponto para sua carga de trabalho, você precisa toounderstand:

* Padrões de consumo: nenhum pico, picos frequentes ou picos prolongados? Picos pequenos (média de 2 vezes), medianos ou grandes (média de mais de 10 vezes)?
* Porcentagem de solicitações limitadas: você se sente confortável se tiver um pouco de limitação? Em caso afirmativo, quanto? 

Depois de identificar quais são seus objetivos, você será capaz de tooget mais toohello ideal de provisionamento.

tooassist, queremos tooprovide uma orientação geral sobre como toooptimize o provisionamento com base no seu consumo RU/m. Este guia não se aplica a tooall tipo de cargas de trabalho, mas baseia-se no conhecimento de visualização privada de saudação. Essas linhas de base poderão ser alteradas conforme aprendermos mais:

|% de utilização da RU/m|Grau de utilização da RU/m|Ações recomendadas para provisionamento|
|---|---|---|
|0-1%|Subutilização|Reduzir tooconsume RU/s mais RU/m|
|1-10%|Uso íntegro|Lembre-Olá mesmo provisionamento nível|
|Acima de 10%|Utilização excessiva|Aumentar RU/s toorely menos em RU/m|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Selecione quais operações podem consumir o orçamento de RU/m Olá

No nível de solicitação, você pode também habilitar/desabilitar solicitação de saudação do RU/m orçamento tooserve independentemente do tipo de operação. Se regular orçamento RUs/s provisionado é consumido e solicitação de saudação não pode consumir o orçamento de RU/m Olá, essa solicitação será reduzida. Por padrão, qualquer solicitação será atendida pelo orçamento de RU/m se o orçamento de RU/m para taxa de transferência estiver ativado. 

Aqui está um trecho de código para desabilitar o orçamento RU/m usando Olá API DocumentDB para operações CRUD e consulta.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Próximas etapas

Neste artigo, descrevemos como o particionamento funciona no BD Cosmos do Azure, como você pode criar coleções particionadas e como pode escolher uma boa chave de partição para seu aplicativo.

* Executar testes de desempenho e escala com o BD Cosmos do Azure. Consulte [Teste de desempenho e escala com o BD Cosmos do Azure](performance-testing.md) para obter um exemplo.
* Introdução a codificação com hello [SDKs](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).
* Saiba mais sobre a [taxa de transferência provisionada](request-units.md) no BD Cosmos do Azure 

