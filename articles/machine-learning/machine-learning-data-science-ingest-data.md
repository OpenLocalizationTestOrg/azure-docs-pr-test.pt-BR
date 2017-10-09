---
title: "dados aaaLoad em ambientes de armazenamento do Azure para análise | Microsoft Docs"
description: Mover dados tooand do armazenamento de BLOBs do Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="f4b51-103">Carregar dados em ambientes de armazenamento para análise</span><span class="sxs-lookup"><span data-stu-id="f4b51-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="f4b51-104">Olá, equipe de processo de ciência de dados exige que dados ser incluídos ou carregados em uma variedade de armazenamento diferentes ambientes toobe processado ou analisados de forma mais apropriada do hello em cada estágio do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f4b51-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="f4b51-105">Os destinos de dados geralmente usados para processamento incluem Armazenamento de Blobs do Azure, bancos de dados do SQL Azure, SQL Server na VM do Azure, HDInsight (Hadoop) e Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f4b51-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="f4b51-106">Isso **menu** links tootopics que descrevem como dados tooingest nesses ambientes onde os dados de saudação são armazenados e processados de destino.</span><span class="sxs-lookup"><span data-stu-id="f4b51-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="f4b51-107">Técnico e necessidades de negócios, bem como o local inicial do hello, formatar e tamanho dos dados determinará os ambientes de destino Olá em qual Olá dados precisam toobe incluído tooachieve Olá objetivos de sua análise.</span><span class="sxs-lookup"><span data-stu-id="f4b51-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="f4b51-108">Não é incomum um toobe de dados do cenário toorequire movido entre vários ambientes tooachieve Olá diversas tarefas necessárias tooconstruct um modelo de previsão.</span><span class="sxs-lookup"><span data-stu-id="f4b51-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="f4b51-109">Essa sequência de tarefas pode incluir, por exemplo, a exploração de dados, pré-processamento, limpar, redução da resolução e treinamento de modelo.</span><span class="sxs-lookup"><span data-stu-id="f4b51-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

