---
title: "Integridade preditiva do veículo e hábitos de condução - Azure | Microsoft Docs"
description: "Use os recursos do Cortana Intelligence para obter informações preditivas em tempo real sobre a integridade do veículo e hábitos de condução."
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
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="43f63-103">Manual da solução de análise de telemetria do veículo</span><span class="sxs-lookup"><span data-stu-id="43f63-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="43f63-104">Este **menu** fornece links para os capítulos deste manual.</span><span class="sxs-lookup"><span data-stu-id="43f63-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="43f63-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="43f63-105">Overview</span></span>
<span data-ttu-id="43f63-106">Os supercomputadores foram retirados do laboratório e agora estão estacionados em nossa garagem!</span><span class="sxs-lookup"><span data-stu-id="43f63-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="43f63-107">Esses automóveis de ponta contêm uma infinidade de sensores, dando-lhes a capacidade de acompanhar e monitorar milhões de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="43f63-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="43f63-108">Esperamos que até 2020, a maioria desses carros esteja conectada à Internet.</span><span class="sxs-lookup"><span data-stu-id="43f63-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="43f63-109">Imagine-se explorando essa riqueza de dados para fornecer maior segurança, confiabilidade e uma experiência melhor de condução!</span><span class="sxs-lookup"><span data-stu-id="43f63-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="43f63-110">A Microsoft tornou esse sonho uma realidade por meio do Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="43f63-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="43f63-111">O Cortana Intelligence da Microsoft é um pacote de análise avançada e de Big Data totalmente gerenciado que o habilita a transformar seus dados em ação inteligente.</span><span class="sxs-lookup"><span data-stu-id="43f63-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="43f63-112">Gostaríamos de apresentar o Modelo de Solução de Análise de Telemetria do Veículo do Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="43f63-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="43f63-113">Esta solução demonstra como concessionárias, fabricantes de automóveis e seguradoras podem usar os recursos do Cortana Intelligence para obter informações preditivas em tempo real sobre a integridade do veículo e hábitos de condução.</span><span class="sxs-lookup"><span data-stu-id="43f63-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="43f63-114">A solução é implementada como um [padrão de arquitetura lambda](https://en.wikipedia.org/wiki/Lambda_architecture) , mostrando o potencial completo da plataforma do Cortana Intelligence para processamento em tempo real e em lote.</span><span class="sxs-lookup"><span data-stu-id="43f63-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="43f63-115">A solução:</span><span class="sxs-lookup"><span data-stu-id="43f63-115">The solution:</span></span> 

* <span data-ttu-id="43f63-116">fornece um simulador de Telemática do Veículo</span><span class="sxs-lookup"><span data-stu-id="43f63-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="43f63-117">aproveita os Hubs De eventos para a ingestão de milhões de eventos de telemetria simulados do veículo no Azure</span><span class="sxs-lookup"><span data-stu-id="43f63-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="43f63-118">usa o Stream Analytics para obter informações em tempo real sobre a integridade do veículo</span><span class="sxs-lookup"><span data-stu-id="43f63-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="43f63-119">mantém os dados em um armazenamento de longo prazo para análise em e lote mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="43f63-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="43f63-120">aproveita o Machine Learning para a detecção de anomalias em tempo real e o processamento em lote para obter informações preditivas.</span><span class="sxs-lookup"><span data-stu-id="43f63-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="43f63-121">aproveita o HDInsight para transformar dados em escala e o Data Factory para lidar com a orquestração, agendamento, gerenciamento de recursos e monitoramento do pipeline de processamento em lote</span><span class="sxs-lookup"><span data-stu-id="43f63-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="43f63-122">fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva usando Power BI</span><span class="sxs-lookup"><span data-stu-id="43f63-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="43f63-123">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="43f63-123">Architecture</span></span>
<span data-ttu-id="43f63-124">![Diagrama de arquitetura da solução](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1 – Arquitetura da Solução de Análise da Telemetria do Veículo*</span><span class="sxs-lookup"><span data-stu-id="43f63-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="43f63-125">Essa solução inclui os seguintes **componentes do Cortana Intelligence** e apresenta sua integração de ponta a ponta:</span><span class="sxs-lookup"><span data-stu-id="43f63-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="43f63-126">**Hubs de Eventos** para a ingestão de milhões de eventos de telemetria do veículo no Azure.</span><span class="sxs-lookup"><span data-stu-id="43f63-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="43f63-127">**Stream Analytics** para obter informações em tempo real sobre a integridade do veículo e persistir esses dados no armazenamento de longo prazo para uma análise de lote mais avançada.</span><span class="sxs-lookup"><span data-stu-id="43f63-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="43f63-128">
            **Machine Learning** para detecção de anomalias em tempo real e processamento em lote para obter previsões.</span><span class="sxs-lookup"><span data-stu-id="43f63-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="43f63-129">**HDInsight** é utilizado para transformar dados em escala</span><span class="sxs-lookup"><span data-stu-id="43f63-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="43f63-130">**Data Factory** lida com a orquestração, o agendamento, o gerenciamento de recursos e o monitoramento do pipeline de processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="43f63-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="43f63-131">**PowerBI** fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="43f63-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="43f63-132">Essa solução acessa duas **fontes de dados**diferentes:</span><span class="sxs-lookup"><span data-stu-id="43f63-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="43f63-133">**Sinais de veículo e diagnóstico simulados**: um simulador de telemática do veículo emite informações de diagnóstico e sinais que correspondem ao estado do veículo e ao padrão de condução em um determinado momento.</span><span class="sxs-lookup"><span data-stu-id="43f63-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="43f63-134">**Catálogo do veículo**: um conjunto de dados de referência que contém um VIN para o mapeamento do modelo.</span><span class="sxs-lookup"><span data-stu-id="43f63-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>

