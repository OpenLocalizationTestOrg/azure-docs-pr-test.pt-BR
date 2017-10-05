---
title: "Visão geral da Captura de Hubs de Eventos do Azure | Microsoft Docs"
description: "Capturar dados telemétricos com a Captura de Hubs de Eventos"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 9ae6aa57200b99f382c6e60565db9cfc69f1d3c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="9f02a-103">Captura de Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="9f02a-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="9f02a-104">A Captura de Hubs de Eventos do Azure permite que você forneça automaticamente os dados de streaming em seus Hubs de Eventos para a conta de [Armazenamento de Blobs do Azure](https://azure.microsoft.com/services/storage/blobs/) ou [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) de sua escolha, com maior flexibilidade para especificar uma hora ou um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="9f02a-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="9f02a-105">A configuração da Captura é rápida, não há custos administrativos para executá-la e ela é dimensionada automaticamente com as [unidades de produtividade](event-hubs-features.md#capacity) dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="9f02a-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="9f02a-106">A Captura de Hubs de Eventos é a maneira mais fácil de carregar dados de streaming no Azure e permite que você se concentre no processamento de dados em vez de se concentrar na captura de dados.</span><span class="sxs-lookup"><span data-stu-id="9f02a-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="9f02a-107">A Captura de Hubs de Eventos permite processar pipelines em tempo real e baseados em lote no mesmo fluxo.</span><span class="sxs-lookup"><span data-stu-id="9f02a-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="9f02a-108">Isso significa que você pode criar soluções que crescem com suas necessidades ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="9f02a-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="9f02a-109">Se você estiver criando sistemas baseados em lote com o objetivo de processá-los em tempo real no futuro ou para adicionar um caminho frio eficiente para uma solução em tempo real, a Captura de Hubs de Eventos facilita o trabalho de transmissão de dados.</span><span class="sxs-lookup"><span data-stu-id="9f02a-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="9f02a-110">Como a Captura de Hubs de Eventos funciona</span><span class="sxs-lookup"><span data-stu-id="9f02a-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="9f02a-111">Os Hubs de Eventos são um buffer de tempo de retenção durável para a entrada de telemetria, semelhante a um log distribuído.</span><span class="sxs-lookup"><span data-stu-id="9f02a-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="9f02a-112">A chave para reduzir os Hubs de Eventos é o [modelo de consumidor particionado](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="9f02a-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="9f02a-113">Cada partição é um segmento independente de dados e é consumido de forma independente.</span><span class="sxs-lookup"><span data-stu-id="9f02a-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="9f02a-114">Ao longo do tempo, esses dados expiram com base no período de retenção configurável.</span><span class="sxs-lookup"><span data-stu-id="9f02a-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="9f02a-115">Assim, um Hub de Eventos específico nunca fica “cheio demais”.</span><span class="sxs-lookup"><span data-stu-id="9f02a-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="9f02a-116">A Captura de Hubs de Eventos permite que você especifique sua própria conta de Armazenamento de Blobs do Azure e o contêiner, ou conta do Azure Data Lake Store, que será usado para armazenar os dados capturados.</span><span class="sxs-lookup"><span data-stu-id="9f02a-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="9f02a-117">Essa conta pode estar na mesma região que o hub de eventos ou em outra região, concedendo flexibilidade ao recurso de Captura de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="9f02a-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="9f02a-118">Os dados capturados são gravados no formato [Apache Avro][Apache Avro]: um formato compacto, rápido e binário que fornece estruturas de dados avançados com esquema embutido.</span><span class="sxs-lookup"><span data-stu-id="9f02a-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="9f02a-119">Esse formato é amplamente usado no ecossistema do Hadoop, pelo Stream Analytics e pelo Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9f02a-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="9f02a-120">Mais informações sobre como trabalhar com Avro estão disponíveis neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9f02a-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="9f02a-121">Janelas da Captura</span><span class="sxs-lookup"><span data-stu-id="9f02a-121">Capture windowing</span></span>

<span data-ttu-id="9f02a-122">A Captura de Hubs de Eventos permite que você configure uma janela para controlar a captura.</span><span class="sxs-lookup"><span data-stu-id="9f02a-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="9f02a-123">Essa janela tem configuração mínima de tamanho e tempo com uma “política de ganha quem vem primeiro”, o que significa que o primeiro gatilho encontrado causa uma operação de captura.</span><span class="sxs-lookup"><span data-stu-id="9f02a-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="9f02a-124">Se você tiver uma janela de captura de quinze minutos/100 MB e enviar 1 MB por segundo, a janela de tamanho será disparada antes da janela de tempo.</span><span class="sxs-lookup"><span data-stu-id="9f02a-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="9f02a-125">Cada partição captura de forma independente e grava um blob de blocos completo durante o tempo de captura, nomeado com a hora em que o intervalo de captura foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="9f02a-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="9f02a-126">A convenção de nomenclatura de armazenamento é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="9f02a-126">The storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="9f02a-127">Dimensionamento de unidades de produtividade</span><span class="sxs-lookup"><span data-stu-id="9f02a-127">Scaling to throughput units</span></span>

<span data-ttu-id="9f02a-128">O tráfego dos Hubs de Eventos é controlado por [unidades de produtividade](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="9f02a-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="9f02a-129">Uma única unidade de produtividade permite o ingresso de 1 MB por segundo ou 1.000 eventos por segundo e duas vezes essa quantidade de saída.</span><span class="sxs-lookup"><span data-stu-id="9f02a-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="9f02a-130">Os Hubs de Evento Standard podem ser configurados com 1 a 20 unidades de produtividade e outras podem ser adquiridas por meio de uma [solicitação de suporte][support request] para aumento de cota.</span><span class="sxs-lookup"><span data-stu-id="9f02a-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="9f02a-131">O uso além das unidades de produtividade adquiridas é restringido.</span><span class="sxs-lookup"><span data-stu-id="9f02a-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="9f02a-132">A Captura de Hubs de Eventos copia os dados diretamente do armazenamento interno dos Hubs de Eventos, ignorando as cotas de saída das unidades de produtividade e salvando a saída de outros leitores de processamento, como o Stream Analytics ou o Spark.</span><span class="sxs-lookup"><span data-stu-id="9f02a-132">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="9f02a-133">Uma vez configurado, a Captura de Hubs de Eventos é executada automaticamente quando você envia o primeiro evento e continua em execução.</span><span class="sxs-lookup"><span data-stu-id="9f02a-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="9f02a-134">Para que o seu processamento downstream saiba mais facilmente que o processo está funcionando, os Hubs de Eventos gravam arquivos vazios quando não há nenhum dado.</span><span class="sxs-lookup"><span data-stu-id="9f02a-134">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="9f02a-135">Esse processo fornece cadência e marcador previsíveis que podem alimentar os processadores em lotes.</span><span class="sxs-lookup"><span data-stu-id="9f02a-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="9f02a-136">Configurando a Captura de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="9f02a-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="9f02a-137">Você pode configurar a Captura na hora da criação do hub de eventos usando o [Portal do Azure](https://portal.azure.com) ou usando modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9f02a-137">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="9f02a-138">Para obter mais informações, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="9f02a-138">For more information, see the following articles:</span></span>

- [<span data-ttu-id="9f02a-139">Habilitar a Captura de Hubs de Evento usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f02a-139">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="9f02a-140">Criar um namespace de Hubs de Eventos com o hub de eventos e habilitar a Captura usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9f02a-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="9f02a-141">Explorar os arquivos capturados e trabalhar com o Avro</span><span class="sxs-lookup"><span data-stu-id="9f02a-141">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="9f02a-142">A Captura de Hubs de Eventos cria arquivos no formato Avro, conforme especificado na janela de tempo configurada.</span><span class="sxs-lookup"><span data-stu-id="9f02a-142">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="9f02a-143">Você pode exibir esses arquivos em qualquer ferramenta, como o [Gerenciador de Armazenamento do Azure][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="9f02a-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="9f02a-144">Você pode baixar os arquivos localmente para trabalhar com eles.</span><span class="sxs-lookup"><span data-stu-id="9f02a-144">You can download the files locally to work on them.</span></span>

<span data-ttu-id="9f02a-145">Os arquivos produzidos pela Captura de Hubs de Eventos têm o seguinte esquema Avro:</span><span class="sxs-lookup"><span data-stu-id="9f02a-145">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="9f02a-146">Uma maneira fácil de explorar arquivos do Avro é usando o jar [Ferramentas Avro][Avro Tools] do Apache.</span><span class="sxs-lookup"><span data-stu-id="9f02a-146">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="9f02a-147">Depois de baixar o jar, você pode ver o esquema de um arquivo específico do Avro executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9f02a-147">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="9f02a-148">Esse comando retorna</span><span class="sxs-lookup"><span data-stu-id="9f02a-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="9f02a-149">Você também pode usar as Ferramentas Avro para converter o arquivo em formato JSON e executar outros tipos de processamento.</span><span class="sxs-lookup"><span data-stu-id="9f02a-149">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="9f02a-150">Para executar um processamento mais avançado, baixe e instale o Avro na plataforma escolhida.</span><span class="sxs-lookup"><span data-stu-id="9f02a-150">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="9f02a-151">No momento da redação deste artigo, há implementações disponíveis para C, C++, C\#, Java, NodeJS, Perl, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="9f02a-151">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="9f02a-152">O Apache Avro tem guias de Introdução completos para [Java][Java] e [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="9f02a-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="9f02a-153">Você também pode ler o artigo [Introdução à Captura de Hubs de Eventos](event-hubs-capture-python.md).</span><span class="sxs-lookup"><span data-stu-id="9f02a-153">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="9f02a-154">Como a Captura de Hubs de Eventos é cobrada</span><span class="sxs-lookup"><span data-stu-id="9f02a-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="9f02a-155">A Captura de Hubs de Eventos é medida da mesma forma que as unidades de produtividade, com uma taxa por hora.</span><span class="sxs-lookup"><span data-stu-id="9f02a-155">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="9f02a-156">A cobrança é diretamente proporcional ao número de unidades de produtividade adquiridas para o namespace.</span><span class="sxs-lookup"><span data-stu-id="9f02a-156">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="9f02a-157">Conforme as unidades de produtividade são aumentadas ou diminuídas, a Captura de Hubs de Eventos aumenta e diminui para ter o desempenho correspondente.</span><span class="sxs-lookup"><span data-stu-id="9f02a-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="9f02a-158">Os medidores ocorrem em tandem.</span><span class="sxs-lookup"><span data-stu-id="9f02a-158">The meters occur in tandem.</span></span> <span data-ttu-id="9f02a-159">Para detalhes de preços, consulte [Preços dos Hubs de Eventos](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="9f02a-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9f02a-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f02a-160">Next steps</span></span>

<span data-ttu-id="9f02a-161">A Captura de Hubs de Eventos é a forma mais fácil de obter dados para o Azure.</span><span class="sxs-lookup"><span data-stu-id="9f02a-161">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="9f02a-162">Usando o Azure Data Lake, o Azure Data Factory e o Azure HDInsight, você pode executar processamento em lotes e outras análises usando ferramentas familiares e plataformas de sua escolha, na escala que precisar.</span><span class="sxs-lookup"><span data-stu-id="9f02a-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="9f02a-163">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="9f02a-163">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="9f02a-164">Começar a enviar e receber eventos</span><span class="sxs-lookup"><span data-stu-id="9f02a-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="9f02a-165">Um [aplicativo de exemplo completo que usa os Hubs de Eventos][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="9f02a-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="9f02a-166">[Visão Geral dos Hubs de Eventos][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="9f02a-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
