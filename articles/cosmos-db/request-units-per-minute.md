---
title: "Azure CosmosDB: unidades de solicitação por minuto (RU/m) | Microsoft Docs"
description: "Saiba como reduzir custos utilizando unidades de solicitação por minuto."
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
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="8069c-103">Unidades de solicitação por minuto no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="8069c-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="8069c-104">O BD Cosmos do Azure foi criado para ajudá-lo a obter um desempenho rápido e previsível e a dimensionar continuamente conforme o crescimento de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8069c-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="8069c-105">É possível provisionar a taxa de transferência em um contêiner do BD Cosmos com granularidades por segundo e por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="8069c-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="8069c-106">A taxa de transferência provisionada com granularidade por minuto é usada para gerenciar picos inesperados na carga de trabalho que ocorrem com granularidade por segundo.</span><span class="sxs-lookup"><span data-stu-id="8069c-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="8069c-107">Este artigo fornece uma visão geral de como o provisionamento da Unidade de Solicitação por Minuto (RU/m) funciona.</span><span class="sxs-lookup"><span data-stu-id="8069c-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="8069c-108">A meta do provisionamento de RU/m é fornecer desempenho previsível diante de necessidades imprevisíveis (especialmente se você precisar executar análises de seus dados operacionais) e de cargas de trabalho que apresentam picos.</span><span class="sxs-lookup"><span data-stu-id="8069c-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="8069c-109">Queremos que nossos clientes consumam mais da taxa de transferência que eles provisionam para que possam dimensionar rapidamente com tranquilidade.</span><span class="sxs-lookup"><span data-stu-id="8069c-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="8069c-110">Depois de ler este artigo, você poderá responder as seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="8069c-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="8069c-111">Como funciona uma Unidade de Solicitação por minuto?</span><span class="sxs-lookup"><span data-stu-id="8069c-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="8069c-112">Qual é a diferença entre a Unidade de Solicitação por Minuto e a Unidade de Solicitação por Segundo?</span><span class="sxs-lookup"><span data-stu-id="8069c-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="8069c-113">Como provisionar RU/m?</span><span class="sxs-lookup"><span data-stu-id="8069c-113">How to provision RU/m?</span></span>
* <span data-ttu-id="8069c-114">Em que cenário eu devo considerar o provisionamento de Unidades de Solicitação por Minuto?</span><span class="sxs-lookup"><span data-stu-id="8069c-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="8069c-115">Como usar as métricas do portal para otimizar meu custo e meu desempenho?</span><span class="sxs-lookup"><span data-stu-id="8069c-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="8069c-116">Definir qual tipo de solicitação pode consumir seu orçamento para RU/m?</span><span class="sxs-lookup"><span data-stu-id="8069c-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="8069c-117">Provisionamento de unidades de solicitação por minuto (RU/m)</span><span class="sxs-lookup"><span data-stu-id="8069c-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="8069c-118">Quando provisiona o BD Cosmos do Azure com granularidade de segundo (RU/s), você tem a garantia de que a solicitação será bem-sucedida com baixa latência se a taxa de transferência não tiver ultrapassado a capacidade provisionada dentro desse segundo.</span><span class="sxs-lookup"><span data-stu-id="8069c-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="8069c-119">Com a RU/m, a granularidade é de minutos, com a garantia de que a solicitação terá êxito dentro desse minuto.</span><span class="sxs-lookup"><span data-stu-id="8069c-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="8069c-120">Em comparação com sistemas de intermitência, garantimos que o desempenho obtido será previsível e você poderá fazer planos com base nele.</span><span class="sxs-lookup"><span data-stu-id="8069c-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="8069c-121">A forma como o provisionamento por minuto funciona é simples:</span><span class="sxs-lookup"><span data-stu-id="8069c-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="8069c-122">A unidade RU/m é cobrada por hora, além da RU/s.</span><span class="sxs-lookup"><span data-stu-id="8069c-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="8069c-123">Para obter mais detalhes, visite a [página de preços](https://aka.ms/acdbpricing) do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8069c-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="8069c-124">A RU/m pode ser habilitada no nível da coleção.</span><span class="sxs-lookup"><span data-stu-id="8069c-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="8069c-125">Isso pode ser feito por meio dos SDKs (Node.js, Java ou .Net) ou por meio do portal (também inclui cargas de trabalho da API do MongoDB)</span><span class="sxs-lookup"><span data-stu-id="8069c-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="8069c-126">Quando a RU/m está habilitada, para cada 100 RU/s provisionadas, também são provisionadas 1.000 RU/m (a taxa é de 10 vezes)</span><span class="sxs-lookup"><span data-stu-id="8069c-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="8069c-127">Em um determinado segundo, uma unidade de solicitação consome o provisionamento de RU/m somente se você tiver ultrapassado seu provisionamento por segundo dentro desse segundo</span><span class="sxs-lookup"><span data-stu-id="8069c-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="8069c-128">Quando o período de 60 segundos (UTC) termina, o provisionamento por minuto é recarregado</span><span class="sxs-lookup"><span data-stu-id="8069c-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="8069c-129">A RU/m pode ser habilitada apenas para coleções com provisionamento máximo de 5.000 RU/s por partição.</span><span class="sxs-lookup"><span data-stu-id="8069c-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="8069c-130">Se dimensionar suas necessidades de taxa de transferência e tiver um alto nível de provisionamento por partição, você receberá uma mensagem de aviso</span><span class="sxs-lookup"><span data-stu-id="8069c-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="8069c-131">Abaixo, temos um exemplo concreto, em que um cliente pode provisionar 10kRU/s com 100kRU/m, economizando 73% dos custos em comparação com o provisionamento para o pico (com 50kRU/s) por um período de 90 segundos em uma coleção que tem 10.000 RU/s e 100.000 RU/m provisionadas:</span><span class="sxs-lookup"><span data-stu-id="8069c-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="8069c-132">1º segundo: o orçamento de RU/m está definido como 100.000</span><span class="sxs-lookup"><span data-stu-id="8069c-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="8069c-133">3º segundo: durante esse segundo, o consumo de unidades de solicitação foi de 11.010 RUs; 1.010 RUs acima do provisionamento de RU/s.</span><span class="sxs-lookup"><span data-stu-id="8069c-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="8069c-134">Portanto, 1.010 RUs são deduzidas do orçamento de RU/m.</span><span class="sxs-lookup"><span data-stu-id="8069c-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="8069c-135">98.990 RUs estão disponíveis para os próximos 57 segundos no orçamento de RU/m</span><span class="sxs-lookup"><span data-stu-id="8069c-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="8069c-136">29º segundo: durante esse segundo, um grande aumento aconteceu (mais de 4 vezes maior que o provisionamento por segundo) e o consumo de unidades de solicitação foi de 46.920 RUs.</span><span class="sxs-lookup"><span data-stu-id="8069c-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="8069c-137">36.920 RUs são deduzidas do orçamento de RU/m, que caiu de 92.323 RUs (28º segundo) para 55.403 RUs (29º segundo)</span><span class="sxs-lookup"><span data-stu-id="8069c-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="8069c-138">61º segundo: o orçamento de RU/m volta para 100.000 RUs.</span><span class="sxs-lookup"><span data-stu-id="8069c-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![Gráfico mostrando o consumo e o provisionamento do BD Cosmos do Azure](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="8069c-140">Especificando a capacidade da unidade de solicitação com RU/m</span><span class="sxs-lookup"><span data-stu-id="8069c-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="8069c-141">Ao criar uma coleção do BD Cosmos do Azure, você especifica o número de unidades de solicitação por segundo (RU por segundo) que deseja reservar para a coleção.</span><span class="sxs-lookup"><span data-stu-id="8069c-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="8069c-142">Você também pode decidir se deseja adicionar a RU por minuto.</span><span class="sxs-lookup"><span data-stu-id="8069c-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="8069c-143">Isso pode ser feito usando o Portal ou o SDK.</span><span class="sxs-lookup"><span data-stu-id="8069c-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="8069c-144">Usando o Portal</span><span class="sxs-lookup"><span data-stu-id="8069c-144">Through the Portal</span></span>

<span data-ttu-id="8069c-145">Para habilitar ou desabilitar a RU por minuto, basta um clique ao provisionar uma coleção.</span><span class="sxs-lookup"><span data-stu-id="8069c-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Captura de tela mostrando como definir a RU/m no Portal do Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="8069c-147">Usando o SDK</span><span class="sxs-lookup"><span data-stu-id="8069c-147">Through the SDK</span></span>
<span data-ttu-id="8069c-148">Primeiro, é importante observar que a RU/m só está disponível para os seguintes SDKs:</span><span class="sxs-lookup"><span data-stu-id="8069c-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="8069c-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="8069c-149">.Net 1.14.0</span></span>
* <span data-ttu-id="8069c-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="8069c-150">Java 1.11.0</span></span>
* <span data-ttu-id="8069c-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="8069c-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="8069c-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="8069c-152">Python 2.2.0</span></span>

<span data-ttu-id="8069c-153">Veja um trecho de código para criar uma coleção com 3.000 unidades de solicitação por segundo e 30.000 unidades de solicitação por minuto usando o SDK do .NET:</span><span class="sxs-lookup"><span data-stu-id="8069c-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="8069c-154">Veja um trecho de código para alterar a taxa de transferência de uma coleção para 5.000 unidades de solicitação por segundo sem provisionar a RU por minuto usando o SDK do .NET:</span><span class="sxs-lookup"><span data-stu-id="8069c-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="8069c-155">Cenários adequados</span><span class="sxs-lookup"><span data-stu-id="8069c-155">Good fit scenarios</span></span>

<span data-ttu-id="8069c-156">Nesta seção, fornecemos uma visão geral dos cenários em que é adequado habilitar as unidades de solicitação por minuto.</span><span class="sxs-lookup"><span data-stu-id="8069c-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="8069c-157">**Ambiente de desenvolvimento e teste:** adequado.</span><span class="sxs-lookup"><span data-stu-id="8069c-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="8069c-158">Durante a fase de desenvolvimento, se você estiver testando seu aplicativo com cargas de trabalho diferentes, a RU/m pode fornecer flexibilidade neste estágio.</span><span class="sxs-lookup"><span data-stu-id="8069c-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="8069c-159">Ao mesmo tempo, o [emulador](local-emulator.md) é uma ótima ferramenta gratuita para testar o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8069c-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="8069c-160">No entanto, se quiser começar em um ambiente de nuvem, você terá grande flexibilidade com a RU/m para suas necessidades de desempenho ad hoc.</span><span class="sxs-lookup"><span data-stu-id="8069c-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="8069c-161">Você passará mais tempo desenvolvendo e menos tempo se preocupando com as necessidades de desempenho no início.</span><span class="sxs-lookup"><span data-stu-id="8069c-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="8069c-162">É recomendável começar com o provisionamento mínimo de RU/s e habilitar a RU/m.</span><span class="sxs-lookup"><span data-stu-id="8069c-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="8069c-163">**Necessidades imprevisíveis de granularidade por minuto, com picos de uso:** adequado – economia de 25 a 75%.</span><span class="sxs-lookup"><span data-stu-id="8069c-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="8069c-164">Já vimos uma grande melhoria com relação à RU/m e a maioria dos cenários de produção está nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="8069c-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="8069c-165">Se tiver uma carga de trabalho de IoT que apresenta picos algumas vezes em um minuto e, se tiver consultas em execução quando o sistema faz uma inserção em massa ao mesmo tempo, você precisará de capacidade extra para lidar com esses picos.</span><span class="sxs-lookup"><span data-stu-id="8069c-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="8069c-166">Recomendamos otimizar suas necessidades de recursos aplicando nossa abordagem passo a passo abaixo.</span><span class="sxs-lookup"><span data-stu-id="8069c-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Gráfico mostrando o consumo de solicitação com granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="8069c-168">*Figura – benchmark de consumo de RU*</span><span class="sxs-lookup"><span data-stu-id="8069c-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="8069c-169">**Tranquilidade:** adequado – economia de 10 a 20%.</span><span class="sxs-lookup"><span data-stu-id="8069c-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="8069c-170">Às vezes, você só quer ter tranquilidade e não se preocupar com possíveis picos e limitações.</span><span class="sxs-lookup"><span data-stu-id="8069c-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="8069c-171">Este recurso é o ideal para você.</span><span class="sxs-lookup"><span data-stu-id="8069c-171">This feature is the right one for you.</span></span> <span data-ttu-id="8069c-172">Nesse caso, recomendamos habilitar a RU/m e reduzir ligeiramente seu provisionamento por segundo.</span><span class="sxs-lookup"><span data-stu-id="8069c-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="8069c-173">Este caso é diferente do acima, pois você não tentará otimizar agressivamente o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="8069c-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="8069c-174">Trata-se de uma abordagem de "limitação zero" que você tem em mente.</span><span class="sxs-lookup"><span data-stu-id="8069c-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="8069c-175">Operações críticas com necessidades ad hoc: às vezes, é recomendável permitir que apenas operações críticas tenham acesso ao orçamento de RU/m para que o orçamento não seja consumido por operações ad hoc ou operações menos importantes.</span><span class="sxs-lookup"><span data-stu-id="8069c-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="8069c-176">Isso pode ser definido com facilidade na seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="8069c-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="8069c-177">Usando as métricas do portal para otimizar o custo e o desempenho</span><span class="sxs-lookup"><span data-stu-id="8069c-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="8069c-178">**Nas próximas semanas, desenvolveremos mais o conteúdo sobre o monitoramento do consumo de RUs por minuto para otimizar suas necessidades de taxa de transferência.**</span><span class="sxs-lookup"><span data-stu-id="8069c-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="8069c-179">Por meio das métricas do portal, você pode quantos segundos de RU regulares são consumidos, em comparação com os minutos de RU.</span><span class="sxs-lookup"><span data-stu-id="8069c-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="8069c-180">Monitorar essas métricas deve ajudá-lo a otimizar o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="8069c-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="8069c-181">É recomendável uma abordagem passo a passo para usar a RU/m a seu favor.</span><span class="sxs-lookup"><span data-stu-id="8069c-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="8069c-182">Para cada etapa, você deve ter uma visão geral do consumo de RU que representa um ciclo completo de sua carga de trabalho (ele pode ser de horas, dias ou até mesmo semanas) e deve ter informações sobre a utilização daquilo que provisionar.</span><span class="sxs-lookup"><span data-stu-id="8069c-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="8069c-183">O princípio por trás dessa abordagem é fazer com que o provisionamento de taxa de transferência seja o mais próximo possível de um ponto de provisionamento que corresponda aos critérios de desempenho abaixo.</span><span class="sxs-lookup"><span data-stu-id="8069c-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![Gráfico mostrando o consumo de solicitação com granularidade de 5 minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="8069c-185">Para compreender o ponto de provisionamento ideal para sua carga de trabalho, você precisa compreender:</span><span class="sxs-lookup"><span data-stu-id="8069c-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="8069c-186">Padrões de consumo: nenhum pico, picos frequentes ou picos prolongados?</span><span class="sxs-lookup"><span data-stu-id="8069c-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="8069c-187">Picos pequenos (média de 2 vezes), medianos ou grandes (média de mais de 10 vezes)?</span><span class="sxs-lookup"><span data-stu-id="8069c-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="8069c-188">Porcentagem de solicitações limitadas: você se sente confortável se tiver um pouco de limitação?</span><span class="sxs-lookup"><span data-stu-id="8069c-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="8069c-189">Em caso afirmativo, quanto?</span><span class="sxs-lookup"><span data-stu-id="8069c-189">If so, by how much?</span></span> 

<span data-ttu-id="8069c-190">Depois de identificar quais são suas metas, você poderá se aproximar do provisionamento ideal.</span><span class="sxs-lookup"><span data-stu-id="8069c-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="8069c-191">Para ajudá-lo, queremos fornecer orientações gerais de como otimizar o provisionamento com base em seu consumo de RU/m.</span><span class="sxs-lookup"><span data-stu-id="8069c-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="8069c-192">Estas orientações não se aplicam a todos os tipos de cargas de trabalho, mas são baseadas em conhecimentos sobre o modo de versão prévia particular.</span><span class="sxs-lookup"><span data-stu-id="8069c-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="8069c-193">Essas linhas de base poderão ser alteradas conforme aprendermos mais:</span><span class="sxs-lookup"><span data-stu-id="8069c-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="8069c-194">% de utilização da RU/m</span><span class="sxs-lookup"><span data-stu-id="8069c-194">RU/m % utilization</span></span>|<span data-ttu-id="8069c-195">Grau de utilização da RU/m</span><span class="sxs-lookup"><span data-stu-id="8069c-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="8069c-196">Ações recomendadas para provisionamento</span><span class="sxs-lookup"><span data-stu-id="8069c-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="8069c-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="8069c-197">0-1%</span></span>|<span data-ttu-id="8069c-198">Subutilização</span><span class="sxs-lookup"><span data-stu-id="8069c-198">Under utilization</span></span>|<span data-ttu-id="8069c-199">Diminuir RU/s para consumir mais RU/m</span><span class="sxs-lookup"><span data-stu-id="8069c-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="8069c-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="8069c-200">1-10%</span></span>|<span data-ttu-id="8069c-201">Uso íntegro</span><span class="sxs-lookup"><span data-stu-id="8069c-201">Healthy use</span></span>|<span data-ttu-id="8069c-202">Manter o mesmo nível de provisionamento</span><span class="sxs-lookup"><span data-stu-id="8069c-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="8069c-203">Acima de 10%</span><span class="sxs-lookup"><span data-stu-id="8069c-203">Above 10%</span></span>|<span data-ttu-id="8069c-204">Utilização excessiva</span><span class="sxs-lookup"><span data-stu-id="8069c-204">Over utilization</span></span>|<span data-ttu-id="8069c-205">Aumentar RU/s para depender menos de RU/m</span><span class="sxs-lookup"><span data-stu-id="8069c-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="8069c-206">Selecionar quais operações podem consumir o orçamento de RU/m</span><span class="sxs-lookup"><span data-stu-id="8069c-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="8069c-207">No nível da solicitação, você pode também habilitar/desabilitar o orçamento de RU/m para atender à solicitação, independentemente do tipo de operação.</span><span class="sxs-lookup"><span data-stu-id="8069c-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="8069c-208">Se o orçamento de RUs/s regular provisionado for consumido e a solicitação não puder consumir o orçamento de RU/m, essa solicitação será limitada.</span><span class="sxs-lookup"><span data-stu-id="8069c-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="8069c-209">Por padrão, qualquer solicitação será atendida pelo orçamento de RU/m se o orçamento de RU/m para taxa de transferência estiver ativado.</span><span class="sxs-lookup"><span data-stu-id="8069c-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="8069c-210">Veja um trecho de código para desabilitar o orçamento de RU/m usando a API do DocumentDB para operações CRUD e de consulta.</span><span class="sxs-lookup"><span data-stu-id="8069c-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="8069c-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8069c-211">Next steps</span></span>

<span data-ttu-id="8069c-212">Neste artigo, descrevemos como o particionamento funciona no BD Cosmos do Azure, como você pode criar coleções particionadas e como pode escolher uma boa chave de partição para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8069c-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="8069c-213">Executar testes de desempenho e escala com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8069c-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="8069c-214">Consulte [Teste de desempenho e escala com o BD Cosmos do Azure](performance-testing.md) para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="8069c-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="8069c-215">Introdução à codificação com os [SDKs](documentdb-sdk-dotnet.md) ou a [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="8069c-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="8069c-216">Saiba mais sobre a [taxa de transferência provisionada](request-units.md) no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="8069c-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

