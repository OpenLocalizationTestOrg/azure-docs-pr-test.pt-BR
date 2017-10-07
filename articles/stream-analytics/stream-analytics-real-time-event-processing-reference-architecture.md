---
title: "processamento com o processamento de eventos de análise de fluxo de eventos de tempo aaaReal | Microsoft Docs"
description: "Saiba como um conjunto de serviços do Azure pode interoperar para habilitar a análise e o processamento de eventos em tempo real."
keywords: "processamento em tempo real, processamento de eventos, arquitetura de referência"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="3628f-104">Arquitetura de referência: processamento de eventos em tempo real com o Stream Analytics do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3628f-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="3628f-105">arquitetura de referência de saudação para processamento com o Azure Stream Analytics de eventos em tempo real é pretendida tooprovide um projeto de genérico para a implantação de uma plataforma em tempo real como uma solução de processamento de fluxo de serviço (PaaS) com o Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3628f-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="3628f-106">Resumo</span><span class="sxs-lookup"><span data-stu-id="3628f-106">Summary</span></span>
<span data-ttu-id="3628f-107">Tradicionalmente, as soluções de análise baseadas em recursos, como ETL (extrair, transformar, carregar) e o data warehouse, onde os dados são armazenados tooanalysis anterior.</span><span class="sxs-lookup"><span data-stu-id="3628f-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="3628f-108">Requisitos de alteração, incluindo mais dados tardios rapidamente, sendo transferida para esse limite de toohello modelo existente.</span><span class="sxs-lookup"><span data-stu-id="3628f-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="3628f-109">dados de tooanalyze capacidade Hello dentro de movimentação toostorage anterior de fluxos são uma solução e, embora não seja um novo recurso, abordagem de saudação não foi amplamente adotada em todos os mercados verticais.</span><span class="sxs-lookup"><span data-stu-id="3628f-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="3628f-110">O Microsoft Azure oferece um catálogo abrangente de tecnologias de análise que são capazes de dar suporte a uma matriz de diferentes requisitos e cenários de solução.</span><span class="sxs-lookup"><span data-stu-id="3628f-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="3628f-111">Selecionar quais toodeploy os serviços do Azure para uma solução de ponta a ponta pode ser um desafio dado a gama de ofertas hello.</span><span class="sxs-lookup"><span data-stu-id="3628f-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="3628f-112">Este documento é projetado toodescribe Olá recursos e interoperação de Olá vários serviços do Azure que oferecem suporte a uma solução de fluxo de eventos.</span><span class="sxs-lookup"><span data-stu-id="3628f-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="3628f-113">Ele também explica alguns dos cenários de saudação em que os clientes podem aproveitar esse tipo de abordagem.</span><span class="sxs-lookup"><span data-stu-id="3628f-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="3628f-114">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="3628f-114">Contents</span></span>
* <span data-ttu-id="3628f-115">Resumo executivo</span><span class="sxs-lookup"><span data-stu-id="3628f-115">Executive Summary</span></span>
* <span data-ttu-id="3628f-116">Análise de tempo de tooReal de Introdução</span><span class="sxs-lookup"><span data-stu-id="3628f-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="3628f-117">Proposta de valor de dados em tempo real no Azure</span><span class="sxs-lookup"><span data-stu-id="3628f-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="3628f-118">Cenários comuns de análise em tempo real</span><span class="sxs-lookup"><span data-stu-id="3628f-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="3628f-119">Arquitetura e componentes</span><span class="sxs-lookup"><span data-stu-id="3628f-119">Architecture and Components</span></span>
  * <span data-ttu-id="3628f-120">Fontes de dados</span><span class="sxs-lookup"><span data-stu-id="3628f-120">Data Sources</span></span>
  * <span data-ttu-id="3628f-121">Camada de integração de dados</span><span class="sxs-lookup"><span data-stu-id="3628f-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="3628f-122">Camada de análise em tempo real</span><span class="sxs-lookup"><span data-stu-id="3628f-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="3628f-123">Camada de armazenamento de dados</span><span class="sxs-lookup"><span data-stu-id="3628f-123">Data Storage Layer</span></span>
  * <span data-ttu-id="3628f-124">Camada de apresentação/consumo</span><span class="sxs-lookup"><span data-stu-id="3628f-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="3628f-125">Conclusão</span><span class="sxs-lookup"><span data-stu-id="3628f-125">Conclusion</span></span>

<span data-ttu-id="3628f-126">**Autor:** Charles Feddersen, arquiteto de soluções, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="3628f-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="3628f-127">**Publicação:** janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="3628f-127">**Published:** January 2015</span></span>

<span data-ttu-id="3628f-128">**Revisão:** 1.0</span><span class="sxs-lookup"><span data-stu-id="3628f-128">**Revision:** 1.0</span></span>

<span data-ttu-id="3628f-129">**Download:** [Processamento de eventos em tempo real com o Stream Analytics do Microsoft Azure](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="3628f-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="3628f-130">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="3628f-130">Get help</span></span>
<span data-ttu-id="3628f-131">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3628f-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3628f-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3628f-132">Next steps</span></span>
* [<span data-ttu-id="3628f-133">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3628f-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3628f-134">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3628f-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3628f-135">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3628f-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3628f-136">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3628f-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3628f-137">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3628f-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

