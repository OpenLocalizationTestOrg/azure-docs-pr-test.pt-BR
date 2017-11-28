---
title: "Plataformas de análise: tooStream de comparação do Apache Storm análise | Microsoft Docs"
description: "Obtenha orientação escolhendo uma plataforma de análise de nuvem usando uma comparação de Apache Storm tooStream análise. Compreender os recursos e diferenças."
keywords: "plataforma de análise, plataformas de análise, plataforma de análise de nuvem, comparação com o storm"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="2425e-105">Escolher uma plataforma de análise de streaming: comparação do Apache Storm com o Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="2425e-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="2425e-106">O Azure fornece várias soluções para analisar dados de streaming: [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) e [Apache Storm no Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="2425e-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="2425e-107">Ambas as plataformas de análise fornecem vantagens de saudação de uma solução de PaaS.</span><span class="sxs-lookup"><span data-stu-id="2425e-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="2425e-108">Mas plataformas Olá têm algumas diferenças significativas em seus recursos, bem como em como configurar e gerenciá-los.</span><span class="sxs-lookup"><span data-stu-id="2425e-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="2425e-109">Este artigo fornece uma comparação lado a lado de toohelp de recursos, que você pode escolher entre Apache Storm e análise de fluxo do Azure como uma plataforma de análise de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2425e-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="2425e-110">Recursos gerais</span><span class="sxs-lookup"><span data-stu-id="2425e-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="2425e-112">
                    <strong>Stream Analytics do Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="2425e-113">
                    <strong>Apache Storm no HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-114">
                    <strong>Software livre?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-115">Não.</span><span class="sxs-lookup"><span data-stu-id="2425e-115">No.</span></span> <span data-ttu-id="2425e-116">O Stream Analytics do Azure é uma oferta de propriedade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2425e-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-117">Sim.</span><span class="sxs-lookup"><span data-stu-id="2425e-117">Yes.</span></span> <span data-ttu-id="2425e-118">O Apache Storm é uma tecnologia licenciada pela Apache.</span><span class="sxs-lookup"><span data-stu-id="2425e-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-119">
                    <strong>Suporte da Microsoft?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-120">Sim</span><span class="sxs-lookup"><span data-stu-id="2425e-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-121">Sim</span><span class="sxs-lookup"><span data-stu-id="2425e-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-122">
                    <strong>Requisitos de hardware</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-123">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="2425e-123">None.</span></span> <span data-ttu-id="2425e-124">Azure Stream Analytics é um serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="2425e-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-125">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="2425e-125">None.</span></span> <span data-ttu-id="2425e-126">Apache tempestade é um serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="2425e-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-127">
                    <strong>Unidade de nível superior</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-128">Os usuários implantam e monitoram trabalhos de streaming.</span><span class="sxs-lookup"><span data-stu-id="2425e-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-129">O usuários implantam e monitoram um cluster inteiro, que pode hospedar vários trabalhos do Storm, bem como outras cargas de trabalho (inclusive lote).</span><span class="sxs-lookup"><span data-stu-id="2425e-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-130">
                    <strong>Preço</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-131">Preço por volume de dados processados e Olá número de unidades de streaming por hora que Olá trabalho está em execução.</span><span class="sxs-lookup"><span data-stu-id="2425e-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="2425e-132">Para obter mais informações, consulte <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Preços do Stream Analytics</a>.</span><span class="sxs-lookup"><span data-stu-id="2425e-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-133">unidade de saudação de compra é baseado em cluster e é cobrada com base na hora de Olá Olá cluster está em execução, independentemente dos trabalhos implantados.</span><span class="sxs-lookup"><span data-stu-id="2425e-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="2425e-134">Para obter mais informações, consulte <a href="http://azure.microsoft.com/pricing/details/hdinsight/">Preços do HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="2425e-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="2425e-135">Criação</span><span class="sxs-lookup"><span data-stu-id="2425e-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="2425e-137">
                    <strong>Stream Analytics do Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="2425e-138">
                    <strong>Apache Storm no HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-139">
                    <strong>Recursos: SQL DSL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-140">Sim.</span><span class="sxs-lookup"><span data-stu-id="2425e-140">Yes.</span></span> <span data-ttu-id="2425e-141">O Stream Analytics fornece uma linguagem SQL para criar transformações.</span><span class="sxs-lookup"><span data-stu-id="2425e-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-142">Não.</span><span class="sxs-lookup"><span data-stu-id="2425e-142">No.</span></span> <span data-ttu-id="2425e-143">Os usuários devem escrever código em Java ou C# ou então usar APIs do Trident.</span><span class="sxs-lookup"><span data-stu-id="2425e-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-144">
                    <strong>Recursos: operadores temporais?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-145">Agregações em janelas e junções temporais têm suporte por padrão.</span><span class="sxs-lookup"><span data-stu-id="2425e-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-146">Operadores temporais devem ser implementadas por usuário hello.</span><span class="sxs-lookup"><span data-stu-id="2425e-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-147">
                    <strong>Experiência de desenvolvimento</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-148">Os usuários podem criar, depurar e monitorar trabalhos através do hello portal do Azure, usando dados de exemplo derivados de um fluxo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="2425e-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-149">Usuários que usam o .NET podem desenvolver, depurar e monitorar por meio do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2425e-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="2425e-150">Usuários usando o Java ou outras linguagens podem usar Olá IDE de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="2425e-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-151">
                    <strong>Suporte para depuração</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-152">Logs de status e as operações de trabalho básico são depuração toohelp disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2425e-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="2425e-153">Análise de fluxo no momento não permitem aos usuários especificar o conteúdo ou a quantidade de conteúdo está incluído nos logs de hello (ou seja, modo detalhado).</span><span class="sxs-lookup"><span data-stu-id="2425e-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-154">Os logs detalhados estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2425e-154">Detailed logs are available.</span></span> <span data-ttu-id="2425e-155">Os usuários podem acessar os logs no Visual Studio ou fazendo logon no cluster toohello e acessar logs de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="2425e-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-156">
                    <strong>Extensibilidade usando código personalizado?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-157">Suporte parcial com UDFs de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2425e-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="2425e-158">Para obter mais informações, consulte <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Integração do JavaScript UDF</a>.</span><span class="sxs-lookup"><span data-stu-id="2425e-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-159">Sim.</span><span class="sxs-lookup"><span data-stu-id="2425e-159">Yes.</span></span> <span data-ttu-id="2425e-160">Os usuários podem gravar código personalizado em C#, Java ou qualquer outra linguagem com suporte no Storm.</span><span class="sxs-lookup"><span data-stu-id="2425e-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="2425e-161">Fontes de dados (entradas) e saídas</span><span class="sxs-lookup"><span data-stu-id="2425e-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="2425e-163">
                    <strong>Stream Analytics do Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="2425e-164">
                    <strong>Apache Storm no HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-165">
                 <strong>Fontes de dados de entrada</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="2425e-166">Hubs de Eventos do Azure e Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2425e-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-167">Os Conectores estão disponíveis para os Hubs de Eventos do Azure, o Barramento de Serviço do Microsoft Azure, o Kafka e muito mais.</span><span class="sxs-lookup"><span data-stu-id="2425e-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="2425e-168">Os usuários podem criar conectores adicionais usando código personalizado.</span><span class="sxs-lookup"><span data-stu-id="2425e-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-169">
                    <strong>Formatos de dados de entrada</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-170">Avro, JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="2425e-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-171">Os usuários podem implementar qualquer formato usando código personalizado.</span><span class="sxs-lookup"><span data-stu-id="2425e-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-172">
                    <strong>Saídas</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-173">Um trabalho de streaming pode ter várias saídas.</span><span class="sxs-lookup"><span data-stu-id="2425e-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="2425e-174">As saídas com suporte são Hubs de Eventos do Azure, Armazenamento de Blobs do Azure, Armazenamento de Tabelas do Azure, BD SQL do Azure e Power BI.</span><span class="sxs-lookup"><span data-stu-id="2425e-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-175">O Storm dá suporte a várias saídas em uma topologia e cada saída pode ter uma lógica personalizada para processamento downstream.</span><span class="sxs-lookup"><span data-stu-id="2425e-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="2425e-176">O Storm inclui conectores para o Power BI, Hubs de Eventos do Azure, Armazenamento de Blobs do Azure, Azure Cosmos DB, SQL e HBase.</span><span class="sxs-lookup"><span data-stu-id="2425e-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="2425e-177">Os usuários podem criar conectores adicionais usando código personalizado.</span><span class="sxs-lookup"><span data-stu-id="2425e-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-178">
                    <strong>Formatos de codificação de dados</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-179">Os dados devem ser formatados usando UTF-8.</span><span class="sxs-lookup"><span data-stu-id="2425e-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-180">Os usuários podem implementar qualquer formato de codificação de dados usando código personalizado.</span><span class="sxs-lookup"><span data-stu-id="2425e-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="2425e-181">Gerenciamento e operações</span><span class="sxs-lookup"><span data-stu-id="2425e-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="2425e-183">
                    <strong>Stream Analytics do Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="2425e-184">
                    <strong>Apache Storm no HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-185">
                    <strong>Modelo de implantação de trabalho</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-186">Portal do Azure, PowerShell e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="2425e-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-187">Portal do Azure PowerShell, o Visual Studio e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="2425e-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-188">
                    <strong>Monitoramento (estatísticas, contadores, etc.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-189">O monitoramento é implementado usando o Portal do Azure e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="2425e-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="2425e-190">Usuários também podem configurar alertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="2425e-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-191">Monitoramento é implementado usando APIs REST e Olá profusão de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="2425e-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-192">
                    <strong>Escalabilidade</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-193">Escalabilidade é determinada pelo número de saudação de unidades de Streaming (SUs) para cada trabalho.</span><span class="sxs-lookup"><span data-stu-id="2425e-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="2425e-194">Cada unidade de Streaming processa o too1 MB/segundo, com um máximo de 50 unidades.</span><span class="sxs-lookup"><span data-stu-id="2425e-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="2425e-195">Para obter mais informações, consulte <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">taxa de transferência escala tooincrease</a>.</span><span class="sxs-lookup"><span data-stu-id="2425e-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-196">Escalabilidade é determinada pelo número de saudação de nós no cluster HDInsight profusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2425e-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="2425e-197">limite superior Olá número de saudação de nós é definido pela cota do Azure do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="2425e-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-198">
                    <strong>Limites de processamento de dados</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-199">Os usuários podem aumentar o processamento de dados ou otimizar os custos aumentando ou diminuindo o número de saudação de unidades de Streaming, com um limite de 1 GB/segundo.</span><span class="sxs-lookup"><span data-stu-id="2425e-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-200">Os usuários podem escalar ou reduzir verticalmente o tamanho do cluster.</span><span class="sxs-lookup"><span data-stu-id="2425e-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-201">
                    <strong>Parar/Retomar</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-202">Interromper e retomar no último lugar interrompido.</span><span class="sxs-lookup"><span data-stu-id="2425e-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-203">Interromper e retomar no último local parado com base em uma marca-d'água.</span><span class="sxs-lookup"><span data-stu-id="2425e-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-204">
                    <strong>Atualização de serviço e estrutura</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-205">Aplicação de patch automáticas sem tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="2425e-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-206">Aplicação de patch automáticas sem tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="2425e-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-207">
                    <strong>Continuidade de negócios por meio de um serviço altamente disponível com SLAs garantidos</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="2425e-208">SLA de 99,9% de tempo de atividade</span><span class="sxs-lookup"><span data-stu-id="2425e-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="2425e-209">Recuperação automática de falhas</span><span class="sxs-lookup"><span data-stu-id="2425e-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="2425e-210">Recuperação interna de operadores temporais com monitoração de estado</span><span class="sxs-lookup"><span data-stu-id="2425e-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-211">SLA de 99,9% de tempo de atividade do cluster Storm de saudação.</span><span class="sxs-lookup"><span data-stu-id="2425e-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="2425e-212">O Apache Storm é uma plataforma de streaming tolerante a falhas.</span><span class="sxs-lookup"><span data-stu-id="2425e-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="2425e-213">No entanto, é tooensure de responsabilidade do usuário Olá que streaming trabalhos são executados sem interrupção.</span><span class="sxs-lookup"><span data-stu-id="2425e-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="2425e-214">Recursos avançados</span><span class="sxs-lookup"><span data-stu-id="2425e-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="2425e-216">
                    <strong>Stream Analytics do Azure</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="2425e-217">
                    <strong>Apache Storm no HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-218">
                    <strong>Chegada tardia e manipulação de eventos fora de ordem</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-219">Políticas internas configuráveis podem reordenar eventos, soltá-los ou ajustar a hora do evento.</span><span class="sxs-lookup"><span data-stu-id="2425e-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-220">Os usuários devem implementar lógica toohandle neste cenário.</span><span class="sxs-lookup"><span data-stu-id="2425e-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-221">
                    <strong>Dados de referência</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-222">Dados de referência estão disponíveis no Armazenamento de Blobs do Azure com um máximo de 100 MB de cache na memória.</span><span class="sxs-lookup"><span data-stu-id="2425e-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="2425e-223">Dados de referência são atualizados pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="2425e-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-224">Sem limites de tamanho dos dados.</span><span class="sxs-lookup"><span data-stu-id="2425e-224">No limits on data size.</span></span> <span data-ttu-id="2425e-225">Os conectores estão disponíveis para HBase, Azure Cosmos DB, SQL Server e Azure.</span><span class="sxs-lookup"><span data-stu-id="2425e-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="2425e-226">Os usuários podem criar conectores adicionais usando código personalizado.</span><span class="sxs-lookup"><span data-stu-id="2425e-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="2425e-227">Os dados de referência devem ser atualizados usando código personalizado.</span><span class="sxs-lookup"><span data-stu-id="2425e-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="2425e-228">
                    <strong>Integração ao Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="2425e-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="2425e-229">Modelos de Machine Learning do Azure publicados podem ser configurados como funções durante a criação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="2425e-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="2425e-230">Para saber mais, confira <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Escalar para funções de Machine Learning</a>.</span><span class="sxs-lookup"><span data-stu-id="2425e-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="2425e-231">Disponível por meio de bolts do Storm.</span><span class="sxs-lookup"><span data-stu-id="2425e-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
