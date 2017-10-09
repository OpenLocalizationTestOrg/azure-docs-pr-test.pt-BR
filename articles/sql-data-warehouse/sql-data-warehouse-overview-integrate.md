---
title: "aaaBuild soluções integradas com o SQL Data Warehouse | Microsoft Docs"
description: "Ferramentas e parceiros com soluções que podem ser integradas ao SQL Data Warehouse "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="68b0e-103">Aproveitar outros serviços com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="68b0e-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="68b0e-104">Além disso tooits funcionalidade de núcleo, SQL Data Warehouse permite que os usuários tooleverage muitas Olá outros serviços no Azure junto com ele.</span><span class="sxs-lookup"><span data-stu-id="68b0e-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="68b0e-105">Especificamente, podemos atualmente tomaram medidas toodeeply integrar com o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="68b0e-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="68b0e-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="68b0e-106">Power BI</span></span>
* <span data-ttu-id="68b0e-107">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="68b0e-107">Azure Data Factory</span></span>
* <span data-ttu-id="68b0e-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="68b0e-108">Azure Machine Learning</span></span>
* <span data-ttu-id="68b0e-109">Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="68b0e-109">Azure Stream Analytics</span></span>

<span data-ttu-id="68b0e-110">Estamos trabalhando tooconnect com mais serviços em Olá ecossistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="68b0e-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="68b0e-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="68b0e-111">Power BI</span></span>
<span data-ttu-id="68b0e-112">Integração do Power BI permite que você tooleverage capacidade de computação de saudação do SQL Data Warehouse com o relatório dinâmico Olá e visualização do Power BI.</span><span class="sxs-lookup"><span data-stu-id="68b0e-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="68b0e-113">Atualmente, a integração do Power BI inclui:</span><span class="sxs-lookup"><span data-stu-id="68b0e-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="68b0e-114">**Conexão direta**: uma conexão mais avançada com a aplicação de lógica no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="68b0e-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="68b0e-115">Isso fornece uma análise mais rápida em uma escala maior.</span><span class="sxs-lookup"><span data-stu-id="68b0e-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="68b0e-116">**Abrir no Power BI**: botão 'Abrir no Power BI' hello passa informações de instância tooPower BI, permitindo uma conexão contínua.</span><span class="sxs-lookup"><span data-stu-id="68b0e-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="68b0e-117">Consulte [integrar com o Power BI](sql-data-warehouse-integrate-power-bi.md) ou hello [documentação do Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="68b0e-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="68b0e-118">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="68b0e-118">Azure Data Factory</span></span>
<span data-ttu-id="68b0e-119">A fábrica de dados do Azure oferece aos usuários um toocreate de plataforma gerenciado que complexas para extrair e carregar pipelines.</span><span class="sxs-lookup"><span data-stu-id="68b0e-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="68b0e-120">Integração do SQL Data Warehouse com o Azure Data Factory inclui o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="68b0e-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="68b0e-121">**Procedimentos armazenados**: coordenar a execução de saudação de procedimentos armazenados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="68b0e-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="68b0e-122">**Cópia**: dados de toomove ADF de uso no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="68b0e-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="68b0e-123">Essa operação pode usar o mecanismo de movimentação de dados padrão do ADF ou PolyBase em Olá abrange.</span><span class="sxs-lookup"><span data-stu-id="68b0e-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="68b0e-124">Consulte [integrar com o Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) ou hello [documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="68b0e-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="68b0e-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="68b0e-125">Azure Machine Learning</span></span>
<span data-ttu-id="68b0e-126">O aprendizado de máquina do Azure é um serviço de análise totalmente gerenciado que permite aos usuários toocreate modelos complexos utilizando um grande conjunto de ferramentas de previsão.</span><span class="sxs-lookup"><span data-stu-id="68b0e-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="68b0e-127">SQL Data Warehouse tem suporte como uma origem e de destino para esses modelos com hello funcionalidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="68b0e-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="68b0e-128">**Ler Dados:** encaminhe modelos em escala usando o T-SQL no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="68b0e-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="68b0e-129">**Dados de gravação:** confirmar alterações de qualquer modelo fazer tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="68b0e-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="68b0e-130">Consulte [integrar com o aprendizado de máquina do Azure](sql-data-warehouse-integrate-azure-machine-learning.md) ou hello [documentação de aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="68b0e-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="68b0e-131">Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="68b0e-131">Azure Stream Analytics</span></span>
<span data-ttu-id="68b0e-132">O Stream Analytics do Azure é uma infraestrutura complexa, totalmente gerenciada para processamento e consumo de dados de eventos gerados por meio do hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="68b0e-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="68b0e-133">Integração com o SQL Data Warehouse permite streaming toobe dados efetivamente processados e armazenados junto com dados relacionais, permitindo maior, mais análise avançada.</span><span class="sxs-lookup"><span data-stu-id="68b0e-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="68b0e-134">**Saída de trabalho:** enviar saída do Stream Analytics diretamente trabalhos tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="68b0e-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="68b0e-135">Consulte [integrar com o Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) ou hello [documentação do Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="68b0e-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
