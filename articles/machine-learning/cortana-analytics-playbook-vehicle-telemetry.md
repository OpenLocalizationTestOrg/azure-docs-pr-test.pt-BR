---
title: "integridade de veículo aaaPredict e orientar hábitos - Azure | Microsoft Docs"
description: "Usar recursos de saudação do insights de previsão e em tempo real de inteligência Cortana toogain na integridade do veículo e orientar hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="34e97-103">Manual da solução de análise de telemetria do veículo</span><span class="sxs-lookup"><span data-stu-id="34e97-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="34e97-104">Isso **menu** toohello capítulos neste guia estratégico de links.</span><span class="sxs-lookup"><span data-stu-id="34e97-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="34e97-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="34e97-105">Overview</span></span>
<span data-ttu-id="34e97-106">Computadores superusuários tem sido movido do laboratório hello e agora são estacionadas em nosso garagem!</span><span class="sxs-lookup"><span data-stu-id="34e97-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="34e97-107">Esses automóveis ponta contêm uma grande variedade de sensores, dando-lhes Olá capacidade tootrack e monitoram milhões de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="34e97-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="34e97-108">Esperamos que por 2020, a maioria desses carros será foram toohello conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="34e97-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="34e97-109">Imagine tocar nessa riqueza de segurança dos dados tooprovide maior, confiabilidade e uma experiência melhor uma!</span><span class="sxs-lookup"><span data-stu-id="34e97-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="34e97-110">A Microsoft tornou esse sonho uma realidade por meio do Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="34e97-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="34e97-111">Inteligência de Cortana da Microsoft é uma grande de dados totalmente gerenciados e análise conjunto avançado que permite que você tootransform seus dados em ação inteligente.</span><span class="sxs-lookup"><span data-stu-id="34e97-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="34e97-112">Queremos toointroduce toohello Cortana Intelligence veículo telemetria análise de solução de modelo.</span><span class="sxs-lookup"><span data-stu-id="34e97-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="34e97-113">Esta solução demonstra como revendedores de carro, automóveis fabricantes e companhias podem usar recursos de saudação do Cortana Intelligence toogain em tempo real e hábitos de previsão ideias sobre a integridade de veículo e referências.</span><span class="sxs-lookup"><span data-stu-id="34e97-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="34e97-114">solução de saudação é implementada como um [padrão de arquitetura de lambda](https://en.wikipedia.org/wiki/Lambda_architecture) mostrando todo o potencial da plataforma de inteligência Cortana Olá para hello em tempo real e processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="34e97-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="34e97-115">solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="34e97-115">hello solution:</span></span> 

* <span data-ttu-id="34e97-116">fornece um simulador de Telemática do Veículo</span><span class="sxs-lookup"><span data-stu-id="34e97-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="34e97-117">aproveita os Hubs De eventos para a ingestão de milhões de eventos de telemetria simulados do veículo no Azure</span><span class="sxs-lookup"><span data-stu-id="34e97-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="34e97-118">usa as informações em tempo real do Stream Analytics toogain na integridade do veículo</span><span class="sxs-lookup"><span data-stu-id="34e97-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="34e97-119">persistir dados saudação no armazenamento de longo prazo para análises mais ricas de lote.</span><span class="sxs-lookup"><span data-stu-id="34e97-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="34e97-120">tira proveito de aprendizado de máquina para detecção de anomalias em tempo real e processamento toogain previsão insights do lote.</span><span class="sxs-lookup"><span data-stu-id="34e97-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="34e97-121">aproveita o HDInsight tootransform dados em escala e coordenação de toohandle da fábrica de dados, agendamento, gerenciamento de recursos e monitoramento do pipeline de processamento de lote Olá</span><span class="sxs-lookup"><span data-stu-id="34e97-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="34e97-122">fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva usando Power BI</span><span class="sxs-lookup"><span data-stu-id="34e97-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="34e97-123">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="34e97-123">Architecture</span></span>
<span data-ttu-id="34e97-124">![Diagrama de arquitetura da solução](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1 – Arquitetura da Solução de Análise da Telemetria do Veículo*</span><span class="sxs-lookup"><span data-stu-id="34e97-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="34e97-125">Essa solução inclui o seguinte Olá **componentes Intelligence Cortana** e apresenta sua integração de tooend final:</span><span class="sxs-lookup"><span data-stu-id="34e97-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="34e97-126">**Hubs de Eventos** para a ingestão de milhões de eventos de telemetria do veículo no Azure.</span><span class="sxs-lookup"><span data-stu-id="34e97-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="34e97-127">**Stream Analytics** para obter informações em tempo real sobre a integridade do veículo e persistir esses dados no armazenamento de longo prazo para uma análise de lote mais avançada.</span><span class="sxs-lookup"><span data-stu-id="34e97-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="34e97-128">**Aprendizado de máquina** para detecção de anomalias em tempo real e insights previsão toogain de processamento em lotes.</span><span class="sxs-lookup"><span data-stu-id="34e97-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="34e97-129">**HDInsight** tootransform utilizou dados em grande escala</span><span class="sxs-lookup"><span data-stu-id="34e97-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="34e97-130">**Fábrica de dados** manipula orquestração, agendamento, gerenciamento de recursos e o monitoramento do pipeline de processamento de lote hello.</span><span class="sxs-lookup"><span data-stu-id="34e97-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="34e97-131">**PowerBI** fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="34e97-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="34e97-132">Essa solução acessa duas **fontes de dados**diferentes:</span><span class="sxs-lookup"><span data-stu-id="34e97-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="34e97-133">**Simulados veículo sinais e diagnóstico**: um simulador de telematics veículo emite sinais que correspondem a toohello estado de veículo hello e hello direcionando padrão em um determinado ponto no tempo e informações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="34e97-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="34e97-134">**Catálogo de veículo**: um conjunto de dados de referência que contém um mapeamento de toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="34e97-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

