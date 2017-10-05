---
title: "Amostra de dados em contêineres de blob do Azure, SQL Server e tabelas Hive | Microsoft Docs"
description: "Como explorar dados armazenados em vários ambientes do Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="c3226-103"><a name="heading"></a>Amostra de dados em contêineres de blob do Azure, SQL Server e tabelas Hive</span><span class="sxs-lookup"><span data-stu-id="c3226-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="c3226-104">Este documento leva a tópicos que abordam como obter amostras de dados armazenados em um dos três diferentes locais do Azure:</span><span class="sxs-lookup"><span data-stu-id="c3226-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="c3226-105">**dados no contêiner de blobs do Azure** é realizada baixando-os programaticamente e realizando a amostragem com um exemplo de código Python.</span><span class="sxs-lookup"><span data-stu-id="c3226-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="c3226-106">**dados do SQL Server** é realizada usando SQL e a linguagem de programação Python.</span><span class="sxs-lookup"><span data-stu-id="c3226-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="c3226-107">**dados da tabela do Hive** é realizada usando consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="c3226-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="c3226-108">O **menu** abaixo leva a tópicos que descrevem como obter dados de exemplo de cada um desses ambientes de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3226-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="c3226-109">Essa tarefa de amostragem é uma etapa do [TDSP (Processo de Ciência de Dados de Equipe)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="c3226-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="c3226-110">**Por que fazer a amostragem de dados?**</span><span class="sxs-lookup"><span data-stu-id="c3226-110">**Why sample data?**</span></span>

<span data-ttu-id="c3226-111">Se o conjunto de dados que você deseja analisar for grande, geralmente, é uma boa ideia reduzir os dados para um tamanho menor, mas representativo e mais gerenciável.</span><span class="sxs-lookup"><span data-stu-id="c3226-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="c3226-112">Isso facilita a compreensão de dados, exploração e engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="c3226-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="c3226-113">Sua função no Processo de Análise do Cortana é habilitar a rápida criação de protótipos de funções de processamento de dados e modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="c3226-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

