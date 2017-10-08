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
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="46387-103">Unidades de solicitação por minuto no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="46387-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="46387-104">Banco de dados do Azure Cosmos é projetado toohelp atingir um desempenho rápido e previsível e a escala perfeitamente juntamente com o crescimento do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46387-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="46387-105">É possível provisionar a taxa de transferência em um contêiner do BD Cosmos com granularidades por segundo e por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="46387-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="46387-106">taxa de transferência fornecida por minuto granularidade Hello é usado toomanage inesperados picos na carga de trabalho de saudação que ocorrem em uma granularidade por segundo.</span><span class="sxs-lookup"><span data-stu-id="46387-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="46387-107">Este artigo fornece uma visão geral de como funciona a saudação de provisionamento de unidade de solicitação por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="46387-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="46387-108">meta de saudação em mente com provisionamento de RU/m é tooprovide um desempenho previsível em torno de necessidades imprevisíveis (especialmente se você precisa de análise de toorun sobre seus dados operacionais) e cargas de trabalho apresentar pico de uso.</span><span class="sxs-lookup"><span data-stu-id="46387-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="46387-109">Queremos toohave que nossos clientes consumam mais taxa de transferência Olá que ele provisiona para que eles podem ser dimensionados rapidamente com paz de espírito.</span><span class="sxs-lookup"><span data-stu-id="46387-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="46387-110">Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46387-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="46387-111">Como funciona uma Unidade de Solicitação por minuto?</span><span class="sxs-lookup"><span data-stu-id="46387-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="46387-112">Qual é a diferença de saudação entre unidade de solicitação por minuto e solicitações por segundo?</span><span class="sxs-lookup"><span data-stu-id="46387-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="46387-113">Como tooprovision RU/m?</span><span class="sxs-lookup"><span data-stu-id="46387-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="46387-114">Em que cenário eu devo considerar o provisionamento de Unidades de Solicitação por Minuto?</span><span class="sxs-lookup"><span data-stu-id="46387-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="46387-115">Como toouse Olá métricas portal toooptimize meu custo e desempenho?</span><span class="sxs-lookup"><span data-stu-id="46387-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="46387-116">Definir qual tipo de solicitação pode consumir seu orçamento para RU/m?</span><span class="sxs-lookup"><span data-stu-id="46387-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="46387-117">Provisionamento de unidades de solicitação por minuto (RU/m)</span><span class="sxs-lookup"><span data-stu-id="46387-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="46387-118">Ao provisionar o banco de dados do Azure Cosmos na granularidade de segundo hello (RU/s), você obtém garantia de saudação que sua solicitação tiver êxito em uma baixa latência se a taxa de transferência não excedeu a capacidade Olá provisionada nesse segundo.</span><span class="sxs-lookup"><span data-stu-id="46387-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="46387-119">Com RU/m, a granularidade de saudação está no minuto Olá com garantia de saudação que sua solicitação tiver êxito dentro desse minuto.</span><span class="sxs-lookup"><span data-stu-id="46387-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="46387-120">Em comparação com sistemas de toobursting, certifique-se de que você obtém de desempenho de Olá for previsível e você pode planejar isso.</span><span class="sxs-lookup"><span data-stu-id="46387-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="46387-121">forma de saudação por minuto provisionamento funciona é simples:</span><span class="sxs-lookup"><span data-stu-id="46387-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="46387-122">RU/m é cobrado por hora e em adição tooRU/s.</span><span class="sxs-lookup"><span data-stu-id="46387-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="46387-123">Para obter mais detalhes, visite a [página de preços](https://aka.ms/acdbpricing) do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="46387-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="46387-124">A RU/m pode ser habilitada no nível da coleção.</span><span class="sxs-lookup"><span data-stu-id="46387-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="46387-125">Isso pode ser feito por meio de saudação SDKs (Node. js, Java ou .net) ou por meio do portal hello (também incluem as cargas de trabalho do MongoDB API)</span><span class="sxs-lookup"><span data-stu-id="46387-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="46387-126">Quando RU/m está habilitado, para cada 100 RU/s provisionado, você também pode obter 1.000 RU/m provisionado (taxa de saudação é de 10 vezes)</span><span class="sxs-lookup"><span data-stu-id="46387-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="46387-127">Em um determinado segundo, uma unidade de solicitação consome o provisionamento de RU/m somente se você tiver ultrapassado seu provisionamento por segundo dentro desse segundo</span><span class="sxs-lookup"><span data-stu-id="46387-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="46387-128">Uma vez Olá termina o período de 60 segundos (UTC), Olá por minuto provisionamento é recarregado</span><span class="sxs-lookup"><span data-stu-id="46387-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="46387-129">A RU/m pode ser habilitada apenas para coleções com provisionamento máximo de 5.000 RU/s por partição.</span><span class="sxs-lookup"><span data-stu-id="46387-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="46387-130">Se dimensionar suas necessidades de taxa de transferência e tiver um alto nível de provisionamento por partição, você receberá uma mensagem de aviso</span><span class="sxs-lookup"><span data-stu-id="46387-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="46387-131">Abaixo, temos um exemplo concreto, em que um cliente pode provisionar 10kRU/s com 100kRU/m, economizando 73% dos custos em comparação com o provisionamento para o pico (com 50kRU/s) por um período de 90 segundos em uma coleção que tem 10.000 RU/s e 100.000 RU/m provisionadas:</span><span class="sxs-lookup"><span data-stu-id="46387-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="46387-132">segundo 1º: alocação do hello RU/m é definida como 100.000</span><span class="sxs-lookup"><span data-stu-id="46387-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="46387-133">segundo 3º: durante essa segunda Olá consumo de unidade de solicitação foi 11,010 RUs, 1,010 RUs acima Olá RU/s provisionamento.</span><span class="sxs-lookup"><span data-stu-id="46387-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="46387-134">Portanto, 1,010 RUs são deduzidos do orçamento do hello RU/m.</span><span class="sxs-lookup"><span data-stu-id="46387-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="46387-135">98,990 RUs estão disponíveis para Olá próximos segundos 57 RU/m de orçamento Olá</span><span class="sxs-lookup"><span data-stu-id="46387-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="46387-136">segundo 29: durante esse segundo, um grande aumento aconteceu (> 4 x maior do que o provisionamento por segundo) e o consumo de saudação da unidade de solicitação foi 46,920 RUs.</span><span class="sxs-lookup"><span data-stu-id="46387-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="46387-137">36,920 RUs são deduzidos do orçamento RU/m Olá descartado do 92,323 too55 de RUs (28 de segundo), 403 RUs (29 de segundo)</span><span class="sxs-lookup"><span data-stu-id="46387-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="46387-138">segundo 61st: orçamento RU/m é redefinido too100, RUs, 000.</span><span class="sxs-lookup"><span data-stu-id="46387-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Gráfico mostrando o consumo de saudação e provisionamento do banco de dados do Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="46387-140">Especificando a capacidade da unidade de solicitação com RU/m</span><span class="sxs-lookup"><span data-stu-id="46387-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="46387-141">Ao criar uma coleção de banco de dados do Azure Cosmos, você especificar o número de saudação de unidades de solicitação por segundo (RU por segundo) que você deseja reservado para a coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="46387-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="46387-142">Você também pode decidir se deseja RU tooadd por minuto.</span><span class="sxs-lookup"><span data-stu-id="46387-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="46387-143">Isso pode ser feito por meio de saudação Portal ou Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="46387-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="46387-144">Por meio do Portal de saudação</span><span class="sxs-lookup"><span data-stu-id="46387-144">Through hello Portal</span></span>

<span data-ttu-id="46387-145">Para habilitar ou desabilitar a RU por minuto, basta um clique ao provisionar uma coleção.</span><span class="sxs-lookup"><span data-stu-id="46387-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Captura de tela mostrando como tooset RU/m em Olá portal do Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="46387-147">Por meio de saudação SDK</span><span class="sxs-lookup"><span data-stu-id="46387-147">Through hello SDK</span></span>
<span data-ttu-id="46387-148">Primeiro, isso é importante toonote que RU/m só está disponível para Olá SDKs a seguir:</span><span class="sxs-lookup"><span data-stu-id="46387-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="46387-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="46387-149">.Net 1.14.0</span></span>
* <span data-ttu-id="46387-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="46387-150">Java 1.11.0</span></span>
* <span data-ttu-id="46387-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="46387-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="46387-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="46387-152">Python 2.2.0</span></span>

<span data-ttu-id="46387-153">Aqui está um trecho de código para criar uma coleção com 3.000 unidades de solicitação por unidades de solicitação de segundo e 30.000 por minuto usando Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="46387-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

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

<span data-ttu-id="46387-154">Aqui está um trecho de código para alterar a taxa de transferência de saudação de uma coleção too5, 000 unidades de solicitação por segundo sem provisionamento RU por minuto usando Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="46387-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

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

## <a name="good-fit-scenarios"></a><span data-ttu-id="46387-155">Cenários adequados</span><span class="sxs-lookup"><span data-stu-id="46387-155">Good fit scenarios</span></span>

<span data-ttu-id="46387-156">Nesta seção, fornecemos uma visão geral dos cenários em que é adequado habilitar as unidades de solicitação por minuto.</span><span class="sxs-lookup"><span data-stu-id="46387-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="46387-157">**Ambiente de desenvolvimento e teste:** adequado.</span><span class="sxs-lookup"><span data-stu-id="46387-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="46387-158">Durante a fase de desenvolvimento hello, se você estiver testando seu aplicativo com cargas de trabalho diferentes, RU/m pode fornecer flexibilidade Olá neste estágio.</span><span class="sxs-lookup"><span data-stu-id="46387-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="46387-159">Durante a saudação [emulador](local-emulator.md) é tootest uma excelente ferramenta gratuita do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="46387-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="46387-160">No entanto se você quiser toostart em um ambiente de nuvem, você terá uma grande flexibilidade com RU/m para suas necessidades de desempenho do ad hoc.</span><span class="sxs-lookup"><span data-stu-id="46387-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="46387-161">Você passará mais tempo desenvolvendo e menos tempo se preocupando com as necessidades de desempenho no início.</span><span class="sxs-lookup"><span data-stu-id="46387-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="46387-162">É recomendável começar com o provisionamento de saudação mínimo RU/s e habilitar RU/m.</span><span class="sxs-lookup"><span data-stu-id="46387-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="46387-163">**Necessidades imprevisíveis de granularidade por minuto, com picos de uso:** adequado – economia de 25 a 75%.</span><span class="sxs-lookup"><span data-stu-id="46387-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="46387-164">Já vimos uma grande melhoria com relação à RU/m e a maioria dos cenários de produção está nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="46387-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="46387-165">Se você tiver uma carga de trabalho IoT tem pico algumas vezes em um minuto, se você tiver consultas em execução quando o sistema faz inserção em massa no hello mesmo tempo, você precisará de capacidade extra para necessidades handeling apresentar pico de uso.</span><span class="sxs-lookup"><span data-stu-id="46387-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="46387-166">Recomendamos otimizar suas necessidades de recursos aplicando nossa abordagem passo a passo abaixo.</span><span class="sxs-lookup"><span data-stu-id="46387-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Gráfico mostrando o consumo de solicitação com granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="46387-168">*Figura – benchmark de consumo de RU*</span><span class="sxs-lookup"><span data-stu-id="46387-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="46387-169">**Tranquilidade:** adequado – economia de 10 a 20%.</span><span class="sxs-lookup"><span data-stu-id="46387-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="46387-170">Às vezes, você apenas deseja toohave paz de espírito e não se preocupar sobre possíveis picos e limitação.</span><span class="sxs-lookup"><span data-stu-id="46387-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="46387-171">Este recurso está à direita Olá um para você.</span><span class="sxs-lookup"><span data-stu-id="46387-171">This feature is hello right one for you.</span></span> <span data-ttu-id="46387-172">Nesse caso, recomendamos habilitar a RU/m e reduzir ligeiramente seu provisionamento por segundo.</span><span class="sxs-lookup"><span data-stu-id="46387-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="46387-173">Nesse caso é diferente da saudação acima como você não tentará toooptimize agressivamente o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="46387-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="46387-174">Trata-se de uma abordagem de "limitação zero" que você tem em mente.</span><span class="sxs-lookup"><span data-stu-id="46387-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="46387-175">As operações essenciais com necessidades de ad hoc: às vezes, é recomendável tooonly permitem operações críticas de acesso RU/m orçamento para alocação de saudação não obtenha consumir pelo ad hoc ou menos operações importantes.</span><span class="sxs-lookup"><span data-stu-id="46387-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="46387-176">Que podem ser definidas facilmente na seção de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="46387-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="46387-177">Usando Olá métricas portal toooptimize custo e desempenho</span><span class="sxs-lookup"><span data-stu-id="46387-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="46387-178">**Próximas semanas de hello, podemos desenvolverá mais conteúdo de saudação em torno de monitoramento RUs consumo minuto toooptimize que precisa de sua taxa de transferência.**</span><span class="sxs-lookup"><span data-stu-id="46387-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="46387-179">Por meio de métricas de portal hello, você pode ver a quantidade de segundos de RU regulares consumir versus RU minutos.</span><span class="sxs-lookup"><span data-stu-id="46387-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="46387-180">Monitorar essas métricas deve ajudá-lo a otimizar o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="46387-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="46387-181">É recomendável uma abordagem passo a passo sobre como toouse RU/m tooyour vantagem.</span><span class="sxs-lookup"><span data-stu-id="46387-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="46387-182">Para cada etapa, você deve ter uma visão geral do consumo de saudação RU representando um ciclo completo de sua carga de trabalho (pode ser horas, dias, ou até mesmo semanas) e obter informações sobre a utilização de saudação do qual você provisionar.</span><span class="sxs-lookup"><span data-stu-id="46387-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="46387-183">princípio de saudação por trás dessa abordagem é toomake o provisionamento de taxa de transferência como fechar como possíveis tooa provisão do ponto que corresponda aos critérios de desempenho abaixo.</span><span class="sxs-lookup"><span data-stu-id="46387-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![Gráfico mostrando o consumo de solicitação com granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="46387-185">toounderstand Olá ideal provisionamento ponto para sua carga de trabalho, você precisa toounderstand:</span><span class="sxs-lookup"><span data-stu-id="46387-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="46387-186">Padrões de consumo: nenhum pico, picos frequentes ou picos prolongados?</span><span class="sxs-lookup"><span data-stu-id="46387-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="46387-187">Picos pequenos (média de 2 vezes), medianos ou grandes (média de mais de 10 vezes)?</span><span class="sxs-lookup"><span data-stu-id="46387-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="46387-188">Porcentagem de solicitações limitadas: você se sente confortável se tiver um pouco de limitação?</span><span class="sxs-lookup"><span data-stu-id="46387-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="46387-189">Em caso afirmativo, quanto?</span><span class="sxs-lookup"><span data-stu-id="46387-189">If so, by how much?</span></span> 

<span data-ttu-id="46387-190">Depois de identificar quais são seus objetivos, você será capaz de tooget mais toohello ideal de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="46387-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="46387-191">tooassist, queremos tooprovide uma orientação geral sobre como toooptimize o provisionamento com base no seu consumo RU/m.</span><span class="sxs-lookup"><span data-stu-id="46387-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="46387-192">Este guia não se aplica a tooall tipo de cargas de trabalho, mas baseia-se no conhecimento de visualização privada de saudação.</span><span class="sxs-lookup"><span data-stu-id="46387-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="46387-193">Essas linhas de base poderão ser alteradas conforme aprendermos mais:</span><span class="sxs-lookup"><span data-stu-id="46387-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="46387-194">% de utilização da RU/m</span><span class="sxs-lookup"><span data-stu-id="46387-194">RU/m % utilization</span></span>|<span data-ttu-id="46387-195">Grau de utilização da RU/m</span><span class="sxs-lookup"><span data-stu-id="46387-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="46387-196">Ações recomendadas para provisionamento</span><span class="sxs-lookup"><span data-stu-id="46387-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="46387-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="46387-197">0-1%</span></span>|<span data-ttu-id="46387-198">Subutilização</span><span class="sxs-lookup"><span data-stu-id="46387-198">Under utilization</span></span>|<span data-ttu-id="46387-199">Reduzir tooconsume RU/s mais RU/m</span><span class="sxs-lookup"><span data-stu-id="46387-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="46387-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="46387-200">1-10%</span></span>|<span data-ttu-id="46387-201">Uso íntegro</span><span class="sxs-lookup"><span data-stu-id="46387-201">Healthy use</span></span>|<span data-ttu-id="46387-202">Lembre-Olá mesmo provisionamento nível</span><span class="sxs-lookup"><span data-stu-id="46387-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="46387-203">Acima de 10%</span><span class="sxs-lookup"><span data-stu-id="46387-203">Above 10%</span></span>|<span data-ttu-id="46387-204">Utilização excessiva</span><span class="sxs-lookup"><span data-stu-id="46387-204">Over utilization</span></span>|<span data-ttu-id="46387-205">Aumentar RU/s toorely menos em RU/m</span><span class="sxs-lookup"><span data-stu-id="46387-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="46387-206">Selecione quais operações podem consumir o orçamento de RU/m Olá</span><span class="sxs-lookup"><span data-stu-id="46387-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="46387-207">No nível de solicitação, você pode também habilitar/desabilitar solicitação de saudação do RU/m orçamento tooserve independentemente do tipo de operação.</span><span class="sxs-lookup"><span data-stu-id="46387-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="46387-208">Se regular orçamento RUs/s provisionado é consumido e solicitação de saudação não pode consumir o orçamento de RU/m Olá, essa solicitação será reduzida.</span><span class="sxs-lookup"><span data-stu-id="46387-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="46387-209">Por padrão, qualquer solicitação será atendida pelo orçamento de RU/m se o orçamento de RU/m para taxa de transferência estiver ativado.</span><span class="sxs-lookup"><span data-stu-id="46387-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="46387-210">Aqui está um trecho de código para desabilitar o orçamento RU/m usando Olá API DocumentDB para operações CRUD e consulta.</span><span class="sxs-lookup"><span data-stu-id="46387-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="46387-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46387-211">Next steps</span></span>

<span data-ttu-id="46387-212">Neste artigo, descrevemos como o particionamento funciona no BD Cosmos do Azure, como você pode criar coleções particionadas e como pode escolher uma boa chave de partição para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46387-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="46387-213">Executar testes de desempenho e escala com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="46387-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="46387-214">Consulte [Teste de desempenho e escala com o BD Cosmos do Azure](performance-testing.md) para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="46387-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="46387-215">Introdução a codificação com hello [SDKs](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="46387-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="46387-216">Saiba mais sobre a [taxa de transferência provisionada](request-units.md) no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="46387-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

