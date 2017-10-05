---
title: "Compilar soluções integradas com o SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="aae84-103">Aproveitar outros serviços com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="aae84-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="aae84-104">Além de suas funcionalidades principais, o SQL Data Warehouse permite aos usuários aproveitar muitos dos outros serviços no Azure juntamente com ele.</span><span class="sxs-lookup"><span data-stu-id="aae84-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="aae84-105">Especificamente, atualmente tomamos medidas para maior integração com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aae84-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="aae84-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="aae84-106">Power BI</span></span>
* <span data-ttu-id="aae84-107">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="aae84-107">Azure Data Factory</span></span>
* <span data-ttu-id="aae84-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aae84-108">Azure Machine Learning</span></span>
* <span data-ttu-id="aae84-109">Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="aae84-109">Azure Stream Analytics</span></span>

<span data-ttu-id="aae84-110">Estamos trabalhando para nos conectar com mais serviços em todo o ecossistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="aae84-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="aae84-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="aae84-111">Power BI</span></span>
<span data-ttu-id="aae84-112">A integração do Power BI permite que você aproveite o poder de computação do SQL Data Warehouse com a e visualização e os relatórios dinâmicos do Power BI.</span><span class="sxs-lookup"><span data-stu-id="aae84-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="aae84-113">Atualmente, a integração do Power BI inclui:</span><span class="sxs-lookup"><span data-stu-id="aae84-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="aae84-114">**Conexão direta**: uma conexão mais avançada com a aplicação de lógica no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aae84-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="aae84-115">Isso fornece uma análise mais rápida em uma escala maior.</span><span class="sxs-lookup"><span data-stu-id="aae84-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="aae84-116">**Abrir no Power BI**: o botão 'Abrir no Power BI' passa informações de instância para Power BI, permitindo uma conexão contínua.</span><span class="sxs-lookup"><span data-stu-id="aae84-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="aae84-117">Consulte [Integrar com o Power BI](sql-data-warehouse-integrate-power-bi.md) ou [Documentação do Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="aae84-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="aae84-118">Fábrica de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="aae84-118">Azure Data Factory</span></span>
<span data-ttu-id="aae84-119">O Azure Data Factory oferece aos usuários uma plataforma gerenciada ao criar pipelines complexos de Extração-Carregamento.</span><span class="sxs-lookup"><span data-stu-id="aae84-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="aae84-120">A integração do SQL Data Warehouse com o Azure Data Factory inclui o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aae84-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="aae84-121">**Procedimentos Armazenados**: orquestre a execução de procedimentos armazenados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aae84-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="aae84-122">**Cópia**: use ADF para mover dados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aae84-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="aae84-123">Essa operação pode usar o mecanismo de movimentação de dados padrão do ADF ou PolyBase nos bastidores.</span><span class="sxs-lookup"><span data-stu-id="aae84-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="aae84-124">Confira [Integrar com o Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) ou a [Documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="aae84-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="aae84-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aae84-125">Azure Machine Learning</span></span>
<span data-ttu-id="aae84-126">O Azure Machine Learning é um serviço de análise totalmente gerenciado que permite aos usuários criar modelos complexos utilizando um grande conjunto de ferramentas de previsão.</span><span class="sxs-lookup"><span data-stu-id="aae84-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="aae84-127">O SQL Data Warehouse tem suporte como uma origem e um destino para esses modelos com a seguinte funcionalidade:</span><span class="sxs-lookup"><span data-stu-id="aae84-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="aae84-128">**Ler Dados:** encaminhe modelos em escala usando o T-SQL no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aae84-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="aae84-129">**Gravar Dados:** confirme as alterações de qualquer modelo de volta para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aae84-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="aae84-130">Confira [Integrar com o Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) ou a [Documentação do Aprendizado de Máquina do Azure](https://azure.microsoft.com/services/machine-learning/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="aae84-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="aae84-131">Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="aae84-131">Azure Stream Analytics</span></span>
<span data-ttu-id="aae84-132">O Stream Analytics do Azure é uma infraestrutura complexa, totalmente gerenciada para processamento e consumo de dados de eventos gerados por meio do hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="aae84-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="aae84-133">A integração com o SQL Data Warehouse permite transmitir dados para serem efetivamente processados e armazenados junto com dados relacionais, permitindo análise mais profunda e avançada.</span><span class="sxs-lookup"><span data-stu-id="aae84-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="aae84-134">**Saída de Trabalho:** envie a saída dos trabalhos do Stream Analytics diretamente para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aae84-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="aae84-135">Confira [Integrar com o Stream Analytics do Azure](sql-data-warehouse-integrate-azure-stream-analytics.md) ou a [documentação do Stream Analytics do Azure](https://azure.microsoft.com/documentation/services/stream-analytics/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="aae84-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
