---
title: "Carregar dados em ambientes de armazenamento do Azure para análise | Microsoft Docs"
description: Mover dados de e para o Armazenamento de Blobs do Azure
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
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="97ea0-103">Carregar dados em ambientes de armazenamento para análise</span><span class="sxs-lookup"><span data-stu-id="97ea0-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="97ea0-104">O Processo de Ciência de Dados de Equipe exige que os dados sejam incluídos ou carregados em uma variedade de ambientes de armazenamento diferentes para serem processados ou analisados da maneira mais apropriada em cada estágio do processo.</span><span class="sxs-lookup"><span data-stu-id="97ea0-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="97ea0-105">Os destinos de dados geralmente usados para processamento incluem Armazenamento de Blobs do Azure, bancos de dados do SQL Azure, SQL Server na VM do Azure, HDInsight (Hadoop) e Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="97ea0-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="97ea0-106">Esse **menu** liga os tópicos que descrevem como ingerir dados em ambientes de destino nos quais os dados podem ser armazenados e processados.</span><span class="sxs-lookup"><span data-stu-id="97ea0-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="97ea0-107">Necessidades comerciais e técnicos, bem como o local inicial, formato e tamanho de seus dados que determinarão os ambientes de destino no qual os dados precisam ser incluídos para atingir as metas de sua análise.</span><span class="sxs-lookup"><span data-stu-id="97ea0-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="97ea0-108">Não é incomum para um cenário exigir dados a serem movidos entre vários ambientes para atingir a variedade de tarefas necessárias para construir um modelo de previsão.</span><span class="sxs-lookup"><span data-stu-id="97ea0-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="97ea0-109">Essa sequência de tarefas pode incluir, por exemplo, a exploração de dados, pré-processamento, limpar, redução da resolução e treinamento de modelo.</span><span class="sxs-lookup"><span data-stu-id="97ea0-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

